# SOLID

> "SOLID — это набор принципов для написания поддерживаемого и масштабируемого кода. S — одна ответственность, O — расширяемость без изменения кода, L — корректная подстановка наследников, I — разделение интерфейсов, D — зависимость от абстракций, а не от конкретных реализаций."

***

#### **S — Single Responsibility Principle (Принцип единственной ответственности)**

**Идея:** Класс или модуль должен иметь только одну причину для изменения.\
**Зачем:** Уменьшает связанность, упрощает поддержку.\
**Пример:**

```python
# Плохо — класс делает и валидацию, и сохранение
class User:
    def save(self):
        pass
    def validate(self):
        pass

# Хорошо — разделили ответственность
class User:
    pass

class UserValidator:
    def validate(self, user):
        pass

class UserRepository:
    def save(self, user):
        pass
```

***

#### **O — Open/Closed Principle (Принцип открытости/закрытости)**

**Идея:** Код должен быть открыт для расширения, но закрыт для изменения.\
**Зачем:** Добавляем новое поведение без переписывания старого кода.\
**Пример:**

```python
# Плохо — для нового типа фигуры меняем код метода
class AreaCalculator:
    def calc(self, shape):
        if isinstance(shape, Circle):
            return 3.14 * shape.r ** 2
        elif isinstance(shape, Square):
            return shape.a ** 2

# Хорошо — полиморфизм
class Shape:
    def area(self):
        pass

class Circle(Shape):
    def area(self):
        return 3.14 * self.r ** 2

class Square(Shape):
    def area(self):
        return self.a ** 2
```

***

#### **L — Liskov Substitution Principle (Принцип подстановки Барбары Лисков)**

**Идея:** Объекты подклассов должны заменять объекты базовых классов без изменения поведения.\
**Зачем:** Предотвращает неожиданное поведение при полиморфизме.\
**Пример:**

```python
# Плохо — подкласс меняет контракт базового класса
class Bird:
    def fly(self):
        pass

class Penguin(Bird):
    def fly(self):  # Нарушение: пингвин не летает
        raise NotImplementedError
```

***

#### **I — Interface Segregation Principle (Принцип разделения интерфейсов)**

**Идея:** Не заставляй клиента реализовывать интерфейс, который он не использует.\
**Зачем:** Избегаем "толстых" интерфейсов.\
**Пример:**

```python
# Плохо — лишние методы
class Worker:
    def work(self):
        pass
    def eat(self):
        pass

# Хорошо — разделили интерфейсы
class Workable:
    def work(self):
        pass

class Eatable:
    def eat(self):
        pass
```

***

#### **D — Dependency Inversion Principle (Принцип инверсии зависимостей)**

**Идея:** Модули верхнего уровня не должны зависеть от модулей нижнего уровня, оба должны зависеть от абстракций.\
**Зачем:** Облегчает тестирование и замену реализаций.\
**Пример:**

```python
# Плохо — прямое создание зависимости
class Service:
    def send(self):
        pass

class Controller:
    def __init__(self):
        self.service = Service()  # Жёсткая зависимость

# Хорошо — внедрение зависимости через абстракцию
class ServiceInterface:
    def send(self):
        pass

class Controller:
    def __init__(self, service: ServiceInterface):
        self.service = service
```
