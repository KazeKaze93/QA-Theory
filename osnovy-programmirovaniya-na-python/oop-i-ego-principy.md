# ООП и его принципы

**Объектно-ориентированное программирование** — это подход, при котором программа строится из объектов, взаимодействующих между собой.\
Объекты создаются на основе **классов** и имеют **состояние** (данные) и **поведение** (методы).

***

### **4 ключевых принципа ООП**

| Принцип             | Кратко                                                                        | Пример в Python                                                                     | Зачем нужен                                                  |
| ------------------- | ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| **1. Инкапсуляция** | Объединение данных и методов в одном объекте, сокрытие внутренней реализации. | Приватные атрибуты (`_balance`, `__password`) и методы.                             | Позволяет защищать данные от прямого вмешательства и ошибок. |
| **2. Наследование** | Класс может наследовать атрибуты и методы другого класса.                     | class ElectricCar(Car): pass                                                        | Повторное использование кода, создание иерархий.             |
| **3. Полиморфизм**  | Один интерфейс — разная реализация.                                           | Метод `run()` в `Car` и `TestRunner` — разные реализации, но одинаковое имя.        | Упрощает работу с разными объектами, не заботясь об их типе. |
| **4. Абстракция**   | Выделение значимой информации, сокрытие деталей реализации.                   | Класс `Database` с методом `connect()`, внутри которого сложная логика подключения. | Сокрытие ненужных деталей, упрощение интерфейса.             |

***

### **В автоматизации тестирования**

* **Инкапсуляция** — скрытие деталей взаимодействия с веб-элементами в Page Object.
* **Наследование** — базовый класс для страниц или тестов (напр., `BasePage`, `BaseTest`).
* **Полиморфизм** — разные страницы могут иметь метод `open()`, но реализация будет своя.
* **Абстракция** — работа с API через обёртку, а не напрямую через `requests`.

***

### **3. Пример кода: `models.py`**

```python
from abc import ABC, abstractmethod

# Абстрактный класс (абстракция)
class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

# Родительский класс
class Rectangle(Shape):
    def __init__(self, width, height):
        # Инкапсуляция
        self._width = width
        self._height = height

    # Геттеры и сеттеры
    @property
    def width(self):
        return self._width

    @width.setter
    def width(self, value):
        if value > 0:
            self._width = value
        else:
            raise ValueError("Width must be positive")

    @property
    def height(self):
        return self._height

    @height.setter
    def height(self, value):
        if value > 0:
            self._height = value
        else:
            raise ValueError("Height must be positive")

    # Полиморфизм — метод area будет реализован по-разному
    def area(self):
        return self._width * self._height

# Наследование
class Square(Rectangle):
    def __init__(self, side):
        super().__init__(side, side)

    # Полиморфизм — переопределяем area (не обязательно, но можно)
    def area(self):
        return self._width ** 2
```

***

### **4. Пример автотеста: `tests/test_models.py`**

```python
import pytest
from oop_demo.models import Rectangle, Square

def test_rectangle_area():
    rect = Rectangle(3, 4)
    assert rect.area() == 12
    rect.width = 5
    assert rect.area() == 20

def test_square_area():
    sq = Square(4)
    assert sq.area() == 16
    sq.width = 5
    assert sq.area() == 25
```
