# Как взаимодействовать с запросами, отправляемыми из браузера?

\
В Selenium классическом **нет встроенной поддержки перехвата/управления сетевыми запросами** (HTTP/HTTPS), потому что он работает только с DOM. Но в автоматизации есть несколько способов:

***

### 🔹 Подходы к работе с запросами из браузера

#### 1. **Selenium + BrowserMob Proxy / MITM Proxy**

* Используется внешний прокси-сервер, который «вклинивается» между браузером и сервером.
* Можно перехватывать, проверять и модифицировать запросы/ответы.

Пример с **BrowserMob Proxy**:

```python
from browsermobproxy import Server
from selenium import webdriver

server = Server("path/to/browsermob-proxy")
server.start()
proxy = server.create_proxy()

chrome_options = webdriver.ChromeOptions()
chrome_options.add_argument(f"--proxy-server={proxy.proxy}")

driver = webdriver.Chrome(options=chrome_options)

proxy.new_har("test", options={"captureHeaders": True, "captureContent": True})
driver.get("https://example.com")

# Получаем все запросы
for entry in proxy.har['log']['entries']:
    url = entry['request']['url']
    status = entry['response']['status']
    print(f"{url} -> {status}")
```

📌 Минус: настройка не всегда тривиальная, нужны сторонние утилиты.

***

#### 2. **Selenium Wire**

Очень удобное расширение Selenium, позволяющее перехватывать HTTP(S) запросы напрямую.

```python
from seleniumwire import webdriver  # pip install selenium-wire

options = {}
driver = webdriver.Chrome(seleniumwire_options=options)

driver.get("https://example.com")

# Перехватить все запросы
for request in driver.requests:
    if request.response:
        print(request.url, request.response.status_code)
```

Можно даже **подменять заголовки и ответы**:

```python
driver.scopes = ['.*example.*']  # фильтр по URL

for request in driver.requests:
    if "api" in request.url:
        print(request.headers)
```

***

#### 3. **Playwright или Cypress (альтернатива Selenium)**

* **Playwright** (Python, JS, Java) умеет нативно работать с сетью:

```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch()
    page = browser.new_page()

    def log_request(route, request):
        print(f"Request: {request.url}")
        route.continue_()

    page.route("**/*", log_request)
    page.goto("https://example.com")
    browser.close()
```

* Тут можно **мокать API**, перехватывать и менять ответы.
* Для тестов API + UI — это гораздо удобнее, чем Selenium.

***

#### 4. **DevTools Protocol (CDP) в Selenium 4+**

В ChromeDriver/Selenium 4 появился доступ к Chrome DevTools Protocol, что позволяет слушать сетевые события.

```python
from selenium import webdriver

driver = webdriver.Chrome()

# Включаем мониторинг сетевых событий
driver.execute_cdp_cmd("Network.enable", {})

# Делаем запрос
driver.get("https://example.com")

# Перехватываем ответы
logs = driver.get_log("performance")
for log in logs:
    print(log)
```

📌 Но тут много «сырого» JSON, приходится разбирать руками.

***

### 🔹 Итог

* Для **Selenium классического** лучше использовать **Selenium Wire** (проще всего).
* Для **гибкой работы с API/UI** — перейти на **Playwright** (он поддерживает перехват, моки, подмену ответов из коробки).
* Проксирование (BrowserMob Proxy, MITMProxy) — более старый вариант, но всё ещё рабочий.

