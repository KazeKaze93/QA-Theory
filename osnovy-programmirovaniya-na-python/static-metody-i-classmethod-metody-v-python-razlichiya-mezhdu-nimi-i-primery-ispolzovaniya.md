# static методы и classmethod методы в python, различия между ними и примеры использования

В Python есть два типа методов в классах, которые не требуют создания экземпляра для вызова — это **`@staticmethod`** и **`@classmethod`**.

***

### 1. `@staticmethod`

* Метод, который не получает автоматически ни ссылку на объект (`self`), ни на класс (`cls`).
* Это обычная функция, которая логически связана с классом, но не зависит от состояния объекта или класса.
* Вызывается через класс или экземпляр.

#### Пример

```python
class MathUtils:
    @staticmethod
    def add(a, b):
        return a + b

print(MathUtils.add(5, 3))  # 8

obj = MathUtils()
print(obj.add(10, 7))       # 17
```

***

### 2. `@classmethod`

* Метод, который автоматически получает ссылку на класс (`cls`) в качестве первого аргумента, а не на объект.
* Может использоваться для работы с классом, например, для изменения состояния класса или создания альтернативных конструкторов.
* Вызывается через класс или экземпляр.

#### Пример

```python
class Person:
    species = "Homo sapiens"

    def __init__(self, name):
        self.name = name

    @classmethod
    def create_anonymous(cls):
        return cls("Anonymous")

    @classmethod
    def get_species(cls):
        return cls.species

p = Person.create_anonymous()
print(p.name)             # Anonymous
print(Person.get_species())  # Homo sapiens
```

***

### Ключевые различия

| Особенность                | `@staticmethod`                                                          | `@classmethod`                                                            |
| -------------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------- |
| Первый параметр            | Нет (`self` и `cls` не передаются)                                       | Класс (`cls`) передаётся автоматически                                    |
| Доступ к состоянию класса  | Нет                                                                      | Есть                                                                      |
| Доступ к состоянию объекта | Нет                                                                      | Нет                                                                       |
| Использование              | Функции, связанные с классом логически, без доступа к объекту или классу | Методы, которые работают с классом, например, альтернативные конструкторы |
| Вызов                      | Через класс или экземпляр                                                | Через класс или экземпляр                                                 |

***

### Когда использовать?

* **`@staticmethod`** — когда нужна утилитарная функция, не зависящая от состояния класса или объекта.
* **`@classmethod`** — когда нужно работать с классом, например, создавать объекты разными способами или менять поведение для подклассов.

***

#### Пример с `@classmethod` — альтернативный конструктор для тестовых данных

```python
class TestUser:
    def __init__(self, username, password):
        self.username = username
        self.password = password

    @classmethod
    def create_default_user(cls):
        # Создаёт объект с дефолтными тестовыми данными
        return cls("test_user", "password123")

# Использование
default_user = TestUser.create_default_user()
print(default_user.username)  # test_user
```

Такой метод удобно использовать, чтобы быстро создавать типовые объекты для тестов.

***

#### Пример с `@staticmethod` — вспомогательная функция для валидации

```python
class Validator:
    @staticmethod
    def is_email_valid(email):
        return "@" in email and "." in email

# Использование
print(Validator.is_email_valid("user@example.com"))  # True
print(Validator.is_email_valid("userexample.com"))   # False
```

Это удобно для утилитарных функций, которые не зависят от данных объекта или класса, но логически связаны с ним.

####
