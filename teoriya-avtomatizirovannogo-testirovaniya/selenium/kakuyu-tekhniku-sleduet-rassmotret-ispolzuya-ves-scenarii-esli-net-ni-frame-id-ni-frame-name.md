# Какую технику следует рассмотреть, используя весь сценарий, если «нет ни frame id, ни frame name»?

Когда в **Selenium (Python)** нужно работать с `iframe`, обычно используют

```python
driver.switch_to.frame("frame_id")
driver.switch_to.frame("frame_name")
```

Но если **нет `id` и `name`**, то применяют **поиск по WebElement**.

***

### 🔹 Техника: переключение по WebElement

```python
from selenium import webdriver

driver = webdriver.Chrome()
driver.get("https://example.com")

# Находим iframe как элемент (например, по XPath или CSS)
iframe = driver.find_element("xpath", "//iframe[contains(@src, 'frame_content')]")

# Переключаемся внутрь
driver.switch_to.frame(iframe)

# Теперь можно работать с элементами внутри iframe
text = driver.find_element("tag name", "body").text
print(text)

# Возврат в основной контент
driver.switch_to.default_content()
```

***

### 🔹 Если iframe вложенные

Иногда бывают `iframe` внутри `iframe`. Тогда нужно переключаться по шагам:

```python
# Внешний iframe
outer = driver.find_element("xpath", "//iframe[@class='outer']")
driver.switch_to.frame(outer)

# Внутренний iframe
inner = driver.find_element("xpath", "//iframe[@class='inner']")
driver.switch_to.frame(inner)

# Работаем внутри
element = driver.find_element("id", "some_id").text
print(element)

# Возврат в корень
driver.switch_to.default_content()
```

***

📌 Итого:\
Если **нет `id` и `name`**, используем технику **`driver.switch_to.frame(WebElement)`** → это самый универсальный способ.
