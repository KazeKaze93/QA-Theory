# Работа с регистрами

В Python **работа с регистрами** обычно относится к **обработке строк** — переводу текста в верхний, нижний регистр или проверке регистра символов.&#x20;

***

### **1. Основные методы работы с регистром строк**

| Метод           | Что делает                                        | Пример                                         |
| --------------- | ------------------------------------------------- | ---------------------------------------------- |
| `.lower()`      | Переводит все символы в **строчные**              | `"Hello".lower()` → `"hello"`                  |
| `.upper()`      | Переводит все символы в **прописные**             | `"Hello".upper()` → `"HELLO"`                  |
| `.title()`      | Каждое слово начинается с заглавной               | `"hello world".title()` → `"Hello World"`      |
| `.capitalize()` | Первая буква строки заглавная, остальное строчные | `"hello world".capitalize()` → `"Hello world"` |
| `.swapcase()`   | Меняет регистр на противоположный                 | `"Hello World".swapcase()` → `"hELLO wORLD"`   |
| `.isupper()`    | Проверяет, все ли символы заглавные               | `"HELLO".isupper()` → `True`                   |
| `.islower()`    | Проверяет, все ли символы строчные                | `"hello".islower()` → `True`                   |

***

### **2. Примеры использования**

```python
text = "Hello, World!"

print(text.lower())       # "hello, world!"
print(text.upper())       # "HELLO, WORLD!"
print(text.title())       # "Hello, World!"
print(text.capitalize())  # "Hello, world!"
print(text.swapcase())    # "hELLO, wORLD!"
print(text.isupper())     # False
print(text.islower())     # False
```

***

### **3. Работа с регистрами в автоматизации тестов**

* **Сравнение строк из UI или API** без учета регистра:

```python
expected = "Success"
actual = "success"
assert expected.lower() == actual.lower()
```

* **Приведение данных к единому регистру** перед записью в базу или лог.
* **Фильтрация элементов списка** по тексту, игнорируя регистр:

```python
items = ["apple", "Banana", "Cherry"]
filtered = [x for x in items if x.lower().startswith("b")]
print(filtered)  # ['Banana']
```
