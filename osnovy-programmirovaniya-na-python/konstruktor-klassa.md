# Конструктор класса

Конструктор класса в Python — это специальный метод, который автоматически вызывается при создании экземпляра класса и отвечает за инициализацию объекта.

***

#### В Python конструктор — это метод `__init__`

* Его задача — задать начальные значения атрибутов объекта.
* Обязательно должен принимать как минимум один аргумент — `self` (ссылка на создаваемый объект).
* Можно принимать любые дополнительные параметры, чтобы передавать данные при создании объекта.

***

#### Синтаксис

```python
class MyClass:
    def __init__(self, arg1, arg2):
        self.arg1 = arg1
        self.arg2 = arg2
```

***

#### Пример

```python
class Person:
    def __init__(self, name, age):
        self.name = name    # присваиваем имя объекту
        self.age = age      # присваиваем возраст

    def greet(self):
        print(f"Привет, меня зовут {self.name}, мне {self.age} лет.")

# Создаём объект
p = Person("Иван", 30)
p.greet()  # Привет, меня зовут Иван, мне 30 лет.
```

***

#### Особенности

* `__init__` — не создает объект, а лишь инициализирует уже созданный (создание происходит через `__new__`, но обычно это не нужно трогать).
* Можно создавать конструктор с параметрами по умолчанию, чтобы можно было создавать объекты с разным набором данных.
* Внутри конструктора можно вызывать другие методы и выполнять любую логику инициализации.

***

#### Пример: Конструктор в классе страницы для Selenium WebDriver

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

class LoginPage:
    def __init__(self, driver):
        self.driver = driver  # Инициализируем драйвер, чтобы использовать его в методах

        # Определяем локаторы элементов
        self.username_input = (By.ID, "username")
        self.password_input = (By.ID, "password")
        self.login_button = (By.ID, "loginBtn")

    def enter_username(self, username):
        self.driver.find_element(*self.username_input).send_keys(username)

    def enter_password(self, password):
        self.driver.find_element(*self.password_input).send_keys(password)

    def click_login(self):
        self.driver.find_element(*self.login_button).click()
```

***

#### Как использовать:

```python
driver = webdriver.Chrome()
driver.get("https://example.com/login")

login_page = LoginPage(driver)  # Конструктор инициализирует драйвер и локаторы
login_page.enter_username("my_user")
login_page.enter_password("my_password")
login_page.click_login()
```

***

#### Почему конструктор важен здесь?

* Передаём **driver** в конструктор — чтобы иметь доступ к веб-драйверу в методах класса.
* В конструкторе задаём локаторы и другие начальные данные.
* Это упрощает повторное использование кода и делает тесты более читаемыми и поддерживаемыми.
