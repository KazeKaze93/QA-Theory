# Как взаимодействовать с cookies, LocalStorage и SessionStorage?

### 🔹 Работа с **Cookies** в Selenium

Selenium имеет встроенные методы для работы с cookies браузера:

```python
from selenium import webdriver

driver = webdriver.Chrome()
driver.get("https://example.com")

# Получить все cookies
print(driver.get_cookies())

# Получить cookie по имени
print(driver.get_cookie("session_id"))

# Добавить cookie
driver.add_cookie({"name": "test_cookie", "value": "12345"})

# Удалить cookie по имени
driver.delete_cookie("test_cookie")

# Удалить все cookies
driver.delete_all_cookies()
```

📌 Используется, например, для **автоматического входа** без логина/пароля (подставляем `session_id` в cookies).

***

### 🔹 Работа с **LocalStorage** и **SessionStorage**

Selenium напрямую не имеет API для LocalStorage/SessionStorage, но можно использовать **JavaScript** через `execute_script()`.

#### ✅ LocalStorage

```python
# Установить значение
driver.execute_script("window.localStorage.setItem('key', 'value');")

# Получить значение
value = driver.execute_script("return window.localStorage.getItem('key');")
print(value)

# Удалить элемент
driver.execute_script("window.localStorage.removeItem('key');")

# Очистить LocalStorage
driver.execute_script("window.localStorage.clear();")
```

#### ✅ SessionStorage

```python
# Установить значение
driver.execute_script("window.sessionStorage.setItem('key', 'value');")

# Получить значение
value = driver.execute_script("return window.sessionStorage.getItem('key');")
print(value)

# Удалить элемент
driver.execute_script("window.sessionStorage.removeItem('key');")

# Очистить SessionStorage
driver.execute_script("window.sessionStorage.clear();")
```

***

### 🔹 Различия

* **Cookies** – хранятся на сервере и клиенте, отправляются с каждым HTTP-запросом. Используются для сессий и авторизации.
* **LocalStorage** – хранит данные в браузере **постоянно**, пока не будет очищен (даже после перезапуска).
* **SessionStorage** – хранит данные **только в рамках одной вкладки**, очищается при её закрытии.

***

✅ Итог:

* Для **авторизации** → чаще используют **cookies**.
* Для **тестовых данных/флагов UI** → LocalStorage.
* Для **временных данных в одной вкладке** → SessionStorage.

