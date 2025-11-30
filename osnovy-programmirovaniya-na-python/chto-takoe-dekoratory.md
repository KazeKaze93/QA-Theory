# Что такое декораторы?

### **1. Что такое декоратор**

* **Декоратор** — это функция, которая **принимает другую функцию и возвращает её (или изменённую версию)**.
* Используется для **добавления функционала к функции или методу без изменения её исходного кода**.

***

### **2. Синтаксис**

```python
@decorator_name
def my_function():
    pass
```

* Это **аналогично**:

```python
def my_function():
    pass

my_function = decorator_name(my_function)
```

***

### **3. Пример простого декоратора**

```python
def my_decorator(func):
    def wrapper():
        print("До выполнения функции")
        func()
        print("После выполнения функции")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
```

**Вывод:**

```
До выполнения функции
Hello!
После выполнения функции
```

***

### **4. Декоратор с аргументами функции**

```python
def decorator(func):
    def wrapper(a, b):
        print(f"Суммируем {a} и {b}")
        return func(a, b)
    return wrapper

@decorator
def add(x, y):
    return x + y

result = add(5, 3)
print(result)  # 8
```

***

### **5. Декораторы в автоматизации тестирования**

* **Логирование выполнения тестов**:

```python
def log(func):
    def wrapper(*args, **kwargs):
        print(f"Запуск {func.__name__}")
        result = func(*args, **kwargs)
        print(f"Завершение {func.__name__}")
        return result
    return wrapper

@log
def test_login():
    assert login("user", "pass") == True
```

* **Повтор попыток (retry) при падении теста**:

```python
def retry(times):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(times):
                try:
                    return func(*args, **kwargs)
                except AssertionError:
                    print("Попытка неудачна")
        return wrapper
    return decorator

@retry(3)
def flaky_test():
    assert random.choice([True, False])
```

* **Измерение времени выполнения теста**:

```python
import time

def timer(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} заняла {end-start:.4f} секунд")
        return result
    return wrapper
```

***

💡 **Вывод:**

* Декораторы = способ **добавить функционал к функции/методу без изменения исходного кода**.
* Часто используются в **логировании, retry, тайминге, проверках pre/post условий в автотестах**.
