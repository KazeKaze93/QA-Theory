# Какие exceptions может бросить Selenium? Что они означают и как их обрабатывать?

### 🔹 Основные исключения Selenium

| Exception                                                                                    | Когда возникает                                                                         | Как обрабатывать                                               |
| -------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| **`NoSuchElementException`**                                                                 | Элемент не найден на странице                                                           | Проверять локатор, использовать `WebDriverWait`                |
| **`TimeoutException`**                                                                       | Явное ожидание (`WebDriverWait`) не дождалось элемента/условия                          | Увеличить таймаут, проверить условие                           |
| **`NoSuchWindowException`**                                                                  | Окно/вкладка не существует или уже закрыта                                              | Проверять доступные окна `driver.window_handles`               |
| **`NoSuchFrameException`**                                                                   | `iframe` не найден                                                                      | Проверить наличие фрейма перед `switch_to.frame()`             |
| **`ElementNotVisibleException`** (устаревший, теперь чаще `ElementNotInteractableException`) | Элемент есть, но не виден                                                               | Использовать `WebDriverWait` с `visibility_of_element_located` |
| **`ElementNotInteractableException`**                                                        | Элемент найден, но с ним нельзя взаимодействовать (например, скрыт)                     | Ждать, пока элемент станет кликабельным                        |
| **`StaleElementReferenceException`**                                                         | Элемент найден ранее, но DOM обновился (например, после перезагрузки)                   | Находить элемент заново перед действием                        |
| **`InvalidSelectorException`**                                                               | XPath или CSS некорректный                                                              | Исправить локатор                                              |
| **`WebDriverException`**                                                                     | Общая ошибка работы WebDriver (например, нет соединения с драйвером)                    | Проверить драйвер/браузер                                      |
| **`JavascriptException`**                                                                    | Ошибка при выполнении `execute_script`                                                  | Проверить JS-код                                               |
| **`MoveTargetOutOfBoundsException`**                                                         | Попытка переместить курсор за пределы страницы                                          | Проверить координаты                                           |
| **`NoAlertPresentException`**                                                                | Попытка переключиться на alert, которого нет                                            | Проверять `WebDriverWait(alert_is_present())`                  |
| **`SessionNotCreatedException`**                                                             | Драйвер не может создать сессию (часто из-за несовпадения версий ChromeDriver/браузера) | Обновить драйвер/браузер                                       |
| **`ElementClickInterceptedException`**                                                       | При клике другой элемент перекрывает нужный                                             | Ждать, пока элемент не освободится                             |

***

### 🔹 Примеры обработки исключений в Python

#### 1. Простая обработка

```python
from selenium.common.exceptions import NoSuchElementException

try:
    element = driver.find_element("id", "login")
except NoSuchElementException:
    print("Элемент не найден!")
```

***

#### 2. С явным ожиданием

```python
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.common.exceptions import TimeoutException

try:
    element = WebDriverWait(driver, 5).until(
        EC.presence_of_element_located((By.ID, "login"))
    )
except TimeoutException:
    print("Элемент не появился в течение 5 секунд")
```

***

#### 3. Отлов нескольких исключений

```python
from selenium.common.exceptions import (
    NoSuchElementException,
    StaleElementReferenceException,
)

try:
    element = driver.find_element("id", "login")
    element.click()
except (NoSuchElementException, StaleElementReferenceException) as e:
    print(f"Ошибка при работе с элементом: {e}")
```

***

📌 **Итог**:\
Selenium кидает **десятки разных исключений**, но на практике самые частые — это `NoSuchElementException`, `TimeoutException`, `StaleElementReferenceException` и `ElementNotInteractableException`.\
Обрабатывать их лучше через `try/except` и **явные ожидания (WebDriverWait)**.

