# Как протестировать билд на Android?

## 1. Подготовка

1. Убедиться в рабочем артефакте: `app.apk` или `app.aab`.
2. Подпись: release-подпись присутствует или включён Play App Signing.
3. Собрать debug и release сборки:
   * Gradle: `./gradlew assembleDebug` / `./gradlew assembleRelease`
   * Для AAB: `./gradlew bundleRelease` → получаем `app-release.aab`.

## 2. Установка билда на устройство (ручная проверка)

* Установка APK:

```bash
adb devices
adb install -r path/to/app.apk    # -r — перезаписать
adb uninstall com.example.app
```

* Установка AAB (универсальный .apk через bundletool):

```bash
# Скачать bundletool.jar
java -jar bundletool.jar build-apks --bundle=app.aab --output=app.apks --mode=universal
unzip app.apks -d out
adb install -r out/universal.apk
```

* Очистка данных и перезапуск:

```bash
adb shell pm clear com.example.app
adb shell am start -n com.example.app/.MainActivity
```

## 3. Сбор логов и багрепортов

* Логи в реальном времени:

```bash
adb logcat -c
adb logcat > device_logcat.txt
```

* Багрепорт:

```bash
adb bugreport bugreport.zip
```

* Снять стек трейс при крэше: `logcat` + `tombstones` (`adb shell ls /data/tombstones`).

## 4. Быстрая ручная проверка (smoke)

Проверить на одном реальном устройстве минимум:

* Установка/удаление, первый запуск.
* Авторизация/логин.
* Основной пользовательский путь (critical flow).
* Отправка/приём данных (offline/online).
* Работа уведомлений, deep links, интенты.
* Разрешения (permissions) — запросы и поведение при отказе.
* Пауза/возобновление (background/foreground).\
  Записывать шаги + скриншоты (`adb exec-out screencap -p > sc.png`).

## 5. Тестирование на множестве устройств (фрагментация)

* Эмуляторы: разные API (minSdk → targetSdk), разные экраны, плотности.
* Реальные устройства: как минимум 3–5 популярных моделей/версий у вашей аудитории.
* Облачные сервисы: Firebase Test Lab, BrowserStack, Sauce Labs — для широкого охвата устройств.

## 6. Автоматизация тестов

* Unit tests: `./gradlew test` (JVM).
* Instrumentation / UI tests: Espresso / UIAutomator: `./gradlew connectedAndroidTest`.
* Пример запуска определённого теста:

```bash
adb shell am instrument -w -r -e class com.example.MyTest com.example.test/androidx.test.runner.AndroidJUnitRunner
```

* E2E через Appium (если нужно кроссплатформенно).
* CI: запускать тесты в пайплайне (GitHub Actions, GitLab CI, Bitrise) и/или отправлять сборки в Firebase Test Lab.

## 7. Типы тестирования и конкретные проверки

* Регрессия — ключевые пользовательские пути.
* Функциональное — фичи по спецификации.
* UI/UX — корректность верстки на разных экранах и локалях.
* Производительность: холодный/тёплый запуск, время отклика, кадры/сек (ANR и jank).
* Память/утечки: профилирование в Android Studio / LeakCanary.
* Энергопотребление: батарея / wakelocks.
* Сеть: тесты при слабом соединении/потере соединения/переходе 3G↔4G↔Wi-Fi (use Charles/CLI tools или встроенные эмуляции).
* Безопасность: хранение ключей, TLS, Intent-exposure, WebView.
* Хранилище: backup/restore, миграции БД.
* Параллельные сессии/мультиоконность (если релевантно).
* Локализация и форматы дат/валют.

## 8. Инструменты для нагрузочного / автоматического тестирования

* Firebase Test Lab — набора тестов на множестве устройств.
* Android Profiler, Systrace — для производительности.
* Monkey/MonkeyRunner — стресс-тесты (генерация случайных событий).
* Gatling/Locust (для бэкенда) + эмуляция мобильного трафика.
* LeakCanary — обнаружение утечек памяти.

## 9. Работа с Flaky tests / нестабильностью

* Использовать IdlingResource (Espresso) для синхронизации.
* Убрать жесткие таймауты, заменить sleep на ожидания условий.
* Локальные mocking/stubbing сервисов (MockWebServer / WireMock).
* Повторный запуск упавших тестов в CI с контролем процента флейков — если > threshold — лечить, не игнорировать.

## 10. Play Console — предрелизные опции и релиз-гейт

* Internal/Closed/Open testing tracks: быстро раздаёт билд тестерам.
* Pre-launch report (Test Lab) — автоматическая проверка на наборах устройств (UI, краши).
* Release checklist в Play Console: review, rollout % (степенчатый релиз), crash & ANR monitoring, vitals.
* Поддержка App Bundles: Play генерирует оптимизированные APK для устройств — проверить signing & targeting.

## 11. Критерии готовности к релизу (пример)

* Smoke tests OK на реальных устройствах.
* Unit + Instrumentation тесты проходят в CI.
* Нивелированы критические баги (P0/P1).
* Crash rate и ANR < допустимых значений в метриках.
* Производительность в пределах SLA (cold start, memory).
* Rollout plan: поэтапный — 5% → 25% → 100%.

## 12. Полезные команды и проверки (сводка)

```bash
# установить apk
adb install -r app.apk

# удалить
adb uninstall com.example.app

# запустить активити
adb shell am start -n com.example.app/.MainActivity

# очистить данные
adb shell pm clear com.example.app

# запустить instrumentation тесты
adb shell am instrument -w com.example.test/androidx.test.runner.AndroidJUnitRunner

# логи
adb logcat

# скриншот
adb exec-out screencap -p > screen.png

# снять багрепорт
adb bugreport bugreport.zip
```

## 13. Дополнительные практические советы (коротко, без рассуждений)

* Всегда иметь reproducible steps и минимальный repro-apk для багов.
* Использовать feature flags / remote config для безопасного выключения фич в проде.
* Хранить релизную конфигурацию и ключи в защищённом месте, не коммитить подпись в публичный репозиторий.
* Вести матрицу устройств и покрытие тестами.
* Оценивайте метрики после релиза (crashlytics, Play Console vitals) и откатывайте при необходимости.
