---
description: >-
  который содержит в себе два значения: model - строковое обозначение модели
  авто, RW - читать и изменять, speed - скорость, RO - только читать
---

# описать класс Car

```python
class Car:
    def __init__(self, model, speed):
        self.model = model
        self._speed = speed  # Используем _speed для инкапсуляции, чтобы сделать его доступным только для чтения

    @property
    def speed(self):
        return self._speed

# Пример использования
car1 = Car("Toyota Camry", 120)
print(f"Модель: {car1.model}, Скорость: {car1.speed} км/ч")

# Изменение модели
car1.model = "Honda Accord"
print(f"Новая модель: {car1.model}, Скорость: {car1.speed} км/ч")

# Попытка изменения скорости (вызовет AttributeError)
# car1.speed = 130
```

```java
public class Car {
    // Строковое обозначение модели авто (читать и изменять)
    private String model;
    
    // Скорость автомобиля (только для чтения)
    private final int speed;
    
    // Конструктор класса Car
    public Car(String model, int speed) {
        this.model = model;
        this.speed = speed;
    }
    
    // Метод для получения модели автомобиля
    public String getModel() {
        return model;
    }
    
    // Метод для изменения модели автомобиля
    public void setModel(String model) {
        this.model = model;
    }
    
    // Метод для чтения скорости автомобиля
    public int getSpeed() {
        return speed;
    }
}

```
