# Что такое Electron-based applications? Как использовать Selenium и Appium для их тестирования?

**Electron-based applications** — это десктопные приложения, которые построены на **веб-технологиях** (HTML, CSS, JavaScript) и запускаются внутри Chromium + Node.js. Примеры: **Slack, VS Code, Discord, WhatsApp Desktop**.

Основная идея: приложение работает как веб-страница, но имеет доступ к файловой системе и возможностям ОС через Node.js.

***

### **Особенности тестирования Electron-приложений**

1. **Внутренний веб-контент**

* UI в Electron — это фактически веб-страница.
* Можно использовать **веб-тестовые инструменты** для взаимодействия с DOM.

2. **Доступ к Node.js API**

* Позволяет тестировать **файловые операции, системные вызовы**, которые в обычном вебе недоступны.

***

### **Использование Selenium**

Selenium можно использовать для **тестирования интерфейса**, потому что Electron основан на Chromium:

1. **Подключение через ChromeDriver**

* Electron-приложения поставляются с **chromedriver**, совместимым с версией Chromium внутри приложения.
* Нужно указать путь к исполняемому файлу Electron.

**Пример (Python, Selenium):**

```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.chrome.options import Options

options = Options()
options.binary_location = "/path/to/electron/app"  # путь к .exe или .app
driver = webdriver.Chrome(service=Service("/path/to/chromedriver"), options=options)

driver.get("http://localhost")  # тестируем Electron UI как веб
```

2. **Взаимодействие с DOM**

* Можно использовать обычные **locators** (`id`, `class`, `xpath`) для кнопок, полей, списков.

***

### **Использование Appium**

Appium позволяет **тестировать Electron-приложения как десктопные приложения**, через специальный драйвер `appium-electron-driver`.

1. **Настройка capabilities:**

```json
{
  "platformName": "electron",
  "app": "/path/to/electron/app",
  "automationName": "electron"
}
```

2. **Возможности Appium для Electron**

* Запуск и управление приложением (open, close, restart).
* Взаимодействие с **UI через селекторы DOM**.
* Можно писать тесты на любом поддерживаемом языке (Python, Java, JS).

3. **Особенности**

* Тесты работают **как с веб-страницей**, но в десктопном окружении.
* Можно автоматизировать не только UI, но и системные взаимодействия через Node.js API (через тестовый код приложения).

***

#### **Итог**

* **Electron apps** — это десктопные приложения на базе Chromium и Node.js.
* **Selenium** подходит для тестирования UI, потому что UI — это веб-страница.
* **Appium** через `appium-electron-driver` позволяет автоматизировать Electron-приложения как десктопные приложения с доступом к DOM и системным функциям.

Это сочетание позволяет QA проверять **как интерфейс, так и взаимодействие с системой**, используя привычные инструменты для веб и мобильной автоматизации.
