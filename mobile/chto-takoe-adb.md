# Что такое ADB?

**ADB (Android Debug Bridge)** — это инструмент командной строки для взаимодействия с Android-устройствами или эмуляторами. Он входит в **Android SDK** и используется для разработки, тестирования и отладки приложений.

***

#### Основные функции ADB

1. **Подключение к устройству**

* Позволяет работать с физическим Android-устройством или эмулятором через USB или TCP/IP.
* Пример команды для проверки подключённых устройств:

```bash
adb devices
```

2. **Управление приложениями**

* Установка APK:

```bash
adb install app.apk
```

* Удаление приложения:

```bash
adb uninstall com.example.app
```

* Запуск Activity:

```bash
adb shell am start -n com.example.app/.MainActivity
```

3. **Снятие логов**

* Просмотр логов приложения и системы:

```bash
adb logcat
```

* Фильтрация по тегу или уровню логирования:

```bash
adb logcat MyAppTag:D *:S
```

4. **Доступ к файловой системе**

* Копирование файлов на устройство:

```bash
adb push localfile /sdcard/
```

* Копирование с устройства:

```bash
adb pull /sdcard/file.txt ./file.txt
```

* Работа с shell:

```bash
adb shell
```

5. **Отладка и тестирование**

* Снятие скриншотов и видео:

```bash
adb shell screencap /sdcard/screen.png
adb pull /sdcard/screen.png
```

```bash
adb shell screenrecord /sdcard/video.mp4
```

* Симуляция ввода (тапы, свайпы, текст):

```bash
adb shell input tap x y
adb shell input text "Hello"
```

6. **Системная информация**

* Просмотр процессов:

```bash
adb shell ps
```

* Проверка состояния батареи:

```bash
adb shell dumpsys battery
```

* Информация о сети:

```bash
adb shell dumpsys connectivity
```

***

#### Применение в QA

* Автоматизация тестов и скриптов через команды ADB.
* Снятие логов, багрепортов и crash reports.
* Тестирование UI без Appium (например, через `adb shell input`).
* Контроль состояния устройства и приложений во время регрессионного тестирования.

***

Иными словами, **ADB — это мост между компьютером и Android-устройством**, который позволяет управлять приложением и системой, собирать данные для тестирования и отладки.
