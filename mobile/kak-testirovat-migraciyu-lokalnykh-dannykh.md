# Как тестировать миграцию локальных данных?

Тестирование миграции локальных данных в Android — это проверка того, что при обновлении приложения данные, сохранённые в старой версии (SharedPreferences, SQLite/Room, файлы), корректно переносятся в новую структуру без потерь и ошибок.

***

#### 1. **Определяем тип хранилища**

* **SharedPreferences** — ключ-значение.
* **SQLite/Room** — реляционная БД.
* **Файловое хранилище** — JSON, XML, бинарные файлы.

Каждое требует отдельного подхода к миграции.

***

#### 2. **Подготовка тестового сценария**

1. Создать **демо-данные**, которые будут существовать в старой версии приложения.
2. Сымитировать установку старой версии приложения или использовать старый schema version в БД.
3. Выполнить миграцию до новой версии с обновлённой схемой.

Для Room, например, это может быть:

```kotlin
val oldDb = Room.databaseBuilder(context, AppDatabase::class.java, "test.db")
    .addMigrations() // старые миграции
    .build()
```

***

#### 3. **Unit-тесты миграций (для Room)**

Room поддерживает встроенные тесты:

```kotlin
@get:Rule
val helper: MigrationTestHelper = MigrationTestHelper(
    InstrumentationRegistry.getInstrumentation(),
    AppDatabase::class.java.canonicalName,
    FrameworkSQLiteOpenHelperFactory()
)

@Test
fun migrate1To2() {
    val dbName = "test.db"
    helper.createDatabase(dbName, 1).apply {
        execSQL("INSERT INTO user (id, name) VALUES (1, 'OldName')")
        close()
    }

    val db = helper.runMigrationsAndValidate(dbName, 2, true, MIGRATION_1_2)
    val cursor = db.query("SELECT * FROM user")
    assertTrue(cursor.moveToFirst())
    assertEquals("OldName", cursor.getString(cursor.getColumnIndex("name")))
    cursor.close()
    db.close()
}
```

* **`MigrationTestHelper`** — создаёт базу старой версии, выполняет миграцию и проверяет schema integrity.
* **`runMigrationsAndValidate`** — проверяет, что таблицы и колонки соответствуют новой версии.

***

#### 4. **Инструментальные тесты на устройстве**

* Установить старую версию APK на эмулятор/устройство.
* Заполнить реальные данные (через UI или прямой insert).
* Обновить приложение новым APK.
* Проверить:
  * все данные на месте (ключи SharedPreferences, таблицы Room/SQLite, файлы).
  * новые колонки/фичи работают корректно.
  * ошибки при чтении отсутствуют (`SQLiteException`, `NullPointerException`).

***

#### 5. **Тестирование разных сценариев**

1. **Пустая база** — при отсутствии данных приложение обновляется без ошибок.
2. **Частично заполненная база** — часть данных устарела, часть актуальна.
3. **Максимальный объём данных** — проверка производительности и корректного переноса.
4. **Нестандартные данные** — null, пустые строки, специальные символы, крайние значения.
5. **Многократные обновления** — миграция через несколько версий подряд (v1→v2→v3).

***

#### 6. **Проверка корректности после миграции**

* **UI-проверка:** данные отображаются в списках, формах, графиках.
* **Логика приложения:** редактирование, удаление и фильтрация данных.
* **Integrity check:** row counts, foreign keys, non-null constraints.
* **SharedPreferences:** проверка новых ключей и сохранённых значений.

***

#### 7. **Инструменты**

* **Room MigrationTestHelper** — unit-тесты миграции БД.
* **Espresso / UIAutomator** — проверка визуальных данных после миграции.
* **adb shell / SQLite CLI** — прямой контроль за содержимым базы:

```bash
adb shell
sqlite3 /data/data/com.example.app/databases/app.db
SELECT * FROM user;
```

* **JUnit + Robolectric** — быстрые unit-тесты без эмулятора для SharedPreferences и файлов.

***

#### 8. **Рекомендации**

* Всегда тестировать миграцию на **копии production-базы**, если возможно.
* Добавлять **fallback / backup**: если миграция не удалась, откатывать или восстанавливать старую базу.
* Автоматизировать тесты миграции в CI, чтобы ошибки выявлялись на ранних стадиях.
* Документировать изменения схемы и порядок миграций.

***

При таком подходе можно гарантировать, что данные пользователей не потеряются, а приложение корректно обработает любую версию базы.
