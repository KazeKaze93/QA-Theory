# Для чего используют browser capabilities, arguments и options?

В автоматизации тестирования (Selenium, Appium, Playwright и др.) **browser capabilities, arguments и options** используются для **конфигурации браузера перед запуском теста**. Они позволяют контролировать поведение браузера, среду тестирования и функции, которые будут доступны во время теста.

***

#### 1. **Capabilities (возможности)**

* **Что это:** набор ключ-значение, описывающий свойства браузера и среды.
* **Применение:**
  * Указать **тип браузера и его версию** (`browserName`, `version`).
  * Настроить **платформу или устройство** (`platformName`, `deviceName`).
  * В Appium: указать, какое приложение запускать (`app`), режим автоматизации (`automationName`).
* **Пример (Selenium, Python):**

```python
from selenium import webdriver
caps = {
    "browserName": "chrome",
    "platformName": "Windows 10",
    "version": "116.0"
}
driver = webdriver.Remote(command_executor='http://localhost:4444/wd/hub', desired_capabilities=caps)
```

***

#### 2. **Arguments (аргументы)**

* **Что это:** дополнительные параметры командной строки, с которыми запускается браузер.
* **Применение:**
  * Отключение UI: `--headless`
  * Игнорирование сертификатов: `--ignore-certificate-errors`
  * Отключение расширений: `--disable-extensions`
  * Установка размера окна: `--window-size=1920,1080`
* **Пример (ChromeOptions, Python):**

```python
from selenium.webdriver.chrome.options import Options
options = Options()
options.add_argument("--headless")
options.add_argument("--window-size=1920,1080")
driver = webdriver.Chrome(options=options)
```

***

#### 3. **Options (настройки/конфигурация)**

* **Что это:** объект, который объединяет capabilities и arguments, а также дополнительные настройки браузера.
* **Применение:**
  * Установка **user-agent**
  * Настройка **загрузки файлов**, папки для профиля
  * Включение/отключение **cookies, уведомлений, geolocation**
* **Пример (ChromeOptions):**

```python
options = webdriver.ChromeOptions()
options.add_argument("--disable-notifications")
options.add_experimental_option("prefs", {"download.default_directory": "/tmp"})
driver = webdriver.Chrome(options=options)
```

***

#### **Итог**

* **Capabilities:** задают “что за браузер и где он запускается”.
* **Arguments:** передают команды/флаги для запуска браузера.
* **Options:** объект, который объединяет arguments и capabilities, плюс дополнительные настройки для управления поведением браузера.

Это позволяет QA **точно контролировать среду тестирования**, эмулировать разные условия и устранять нестабильность тестов из-за окружения.
