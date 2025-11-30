# Как обрабатывать браузерные сообщения (alerts)?

\
В веб-приложениях нередко появляются **браузерные диалоговые окна**:

* `alert()` – простое сообщение
* `confirm()` – сообщение с кнопками **OK / Cancel**
* `prompt()` – сообщение с полем ввода

В **Selenium** они обрабатываются через `switch_to.alert`.

***

#### 🔹 Работа с `alert`

```python
from selenium import webdriver
import time

driver = webdriver.Chrome()
driver.get("https://example.com")

# Ждём, пока появится alert
time.sleep(2)

# Переключаемся на alert
alert = driver.switch_to.alert

print(alert.text)  # Получаем текст alert
alert.accept()     # Нажимаем "OK"
```

***

#### 🔹 Работа с `confirm`

```python
alert = driver.switch_to.alert

print(alert.text)
alert.accept()   # Нажимаем "OK"
# alert.dismiss()  # Нажимаем "Cancel"
```

***

#### 🔹 Работа с `prompt`

```python
alert = driver.switch_to.alert

print(alert.text)
alert.send_keys("Test input")  # Вводим текст
alert.accept()                 # Подтверждаем
```

***

#### 🔹 Особенности

1. **Если alert открыт, пока вы кликаете другой элемент — Selenium выдаст `UnhandledAlertException`.**\
   Поэтому всегда сначала обрабатываем alert.
2. Для ожидания появления alert лучше использовать **Explicit Wait**:

```python
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

WebDriverWait(driver, 10).until(EC.alert_is_present())

alert = driver.switch_to.alert
print(alert.text)
alert.accept()
```

***

✅ Таким образом, через `switch_to.alert` можно полностью контролировать браузерные сообщения.
