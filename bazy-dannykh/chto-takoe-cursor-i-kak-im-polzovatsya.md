# Что такое cursor и как им пользоваться?

**Cursor (курсор)** в SQL — это объект базы данных, который позволяет поочерёдно проходить по строкам результата запроса и работать с ними построчно.

***

### Зачем нужен

* Когда нужно обрабатывать результат **не сразу целиком**, а **пошагово**.
* Удобен для сложных процедур, где на каждую строку надо выполнить дополнительную логику (например, вычисления, вставки в другие таблицы).
* Используется в хранимых процедурах и триггерах.

***

### Как работает

1. **Объявление курсора** (cursor) для SQL-запроса.
2. **Открытие** курсора (open).
3. **Чтение строк** по одной (fetch).
4. **Закрытие** курсора (close).
5. **Освобождение ресурсов** (deallocate).

***

### Пример (SQL Server / PostgreSQL синтаксис немного разный)

#### SQL Server:

```sql
DECLARE cur CURSOR FOR
    SELECT name FROM employees;

OPEN cur;

DECLARE @name NVARCHAR(50);

FETCH NEXT FROM cur INTO @name;

WHILE @@FETCH_STATUS = 0
BEGIN
    PRINT 'Сотрудник: ' + @name;
    FETCH NEXT FROM cur INTO @name;
END

CLOSE cur;
DEALLOCATE cur;
```

***

#### PostgreSQL (через PL/pgSQL):

```sql
DO $$
DECLARE
    emp_name text;
    cur CURSOR FOR SELECT name FROM employees;
BEGIN
    OPEN cur;
    LOOP
        FETCH cur INTO emp_name;
        EXIT WHEN NOT FOUND;
        RAISE NOTICE 'Сотрудник: %', emp_name;
    END LOOP;
    CLOSE cur;
END$$;
```

***

### Важный момент

* Курсоры **тяжёлые и медленные** по сравнению с обычными SQL-операциями.
* Их стараются избегать, заменяя на **JOIN, агрегаты, оконные функции**.
* Но бывают задачи, где построчная обработка необходима.
