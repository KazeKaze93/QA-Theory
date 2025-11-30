# Как вычитать данные из динамической веб-таблицы?

***

### 🔹 Общая стратегия:

1. Найти **таблицу** (по `id`, `class`, `xpath` и т.д.).
2. Внутри неё найти **строки** (`<tr>`).
3. В каждой строке найти **ячейки** (`<td>` или `<th>`).
4. Пройтись циклом и вытащить текст.

***

### 🔹 Пример кода

Предположим, у нас таблица:

```html
<table id="users">
  <thead>
    <tr><th>ID</th><th>Name</th><th>Email</th></tr>
  </thead>
  <tbody>
    <tr><td>1</td><td>Alice</td><td>alice@test.com</td></tr>
    <tr><td>2</td><td>Bob</td><td>bob@test.com</td></tr>
  </tbody>
</table>
```

#### 📌 Python + Selenium

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()
driver.get("https://example.com")

# Находим таблицу
table = driver.find_element(By.ID, "users")

# Находим все строки tbody
rows = table.find_elements(By.TAG_NAME, "tr")

# Перебираем строки
for row in rows:
    # Находим все ячейки в строке
    cells = row.find_elements(By.TAG_NAME, "td")
    data = [cell.text for cell in cells]
    print(data)
```

👉 Вывод:

```
['1', 'Alice', 'alice@test.com']
['2', 'Bob', 'bob@test.com']
```

***

### 🔹 Если таблица динамическая (подгружается AJAX-ом)

Тогда надо подождать, пока она появится:

```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

# Ждём, пока появятся строки
rows = WebDriverWait(driver, 10).until(
    EC.presence_of_all_elements_located((By.XPATH, "//table[@id='users']/tbody/tr"))
)
```

***

### 🔹 Дополнительно

*   Можно получить количество строк:

    ```python
    len(rows)
    ```
*   Можно получить количество колонок в первой строке:

    ```python
    len(rows[0].find_elements(By.TAG_NAME, "td"))
    ```
*   Можно вытащить конкретную ячейку (например, 2-я строка, 3-й столбец):

    ```python
    cell = rows[1].find_elements(By.TAG_NAME, "td")[2]
    print(cell.text)
    ```

