# Как работают dict comprehension, list comprehension и set comprehension?

В Python **comprehension** — это короткий и читаемый способ создавать новые коллекции (списки, словари, множества) на основе уже имеющихся данных, часто с фильтрацией и преобразованием элементов.

Они позволяют заменить многострочный цикл одной компактной конструкцией.

***

### 1. **List comprehension** — создание списка

📌 Синтаксис:

```python
[выражение for элемент in итерируемый_объект if условие]
```

Пример:

```python
numbers = [1, 2, 3, 4, 5]
squares = [n ** 2 for n in numbers]
print(squares)  # [1, 4, 9, 16, 25]
```

С фильтром:

```python
even_squares = [n ** 2 for n in numbers if n % 2 == 0]
print(even_squares)  # [4, 16]
```

***

### 2. **Set comprehension** — создание множества

📌 Почти как list comprehension, но в фигурных скобках:

```python
numbers = [1, 2, 2, 3, 4, 4]
unique_squares = {n ** 2 for n in numbers}
print(unique_squares)  # {16, 1, 4, 9}
```

📌 Особенность: автоматически удаляет дубликаты.

***

### 3. **Dict comprehension** — создание словаря

📌 Используется, когда нужно создать словарь из итерируемого объекта:

```python
words = ["apple", "banana", "cherry"]
word_lengths = {word: len(word) for word in words}
print(word_lengths)  # {'apple': 5, 'banana': 6, 'cherry': 6}
```

С фильтром:

```python
short_words = {w: len(w) for w in words if len(w) <= 5}
print(short_words)  # {'apple': 5}
```

***

### 4. Вложенные comprehension

Можно вкладывать, например, для матриц:

```python
matrix = [[1, 2], [3, 4], [5, 6]]
flat = [num for row in matrix for num in row]
print(flat)  # [1, 2, 3, 4, 5, 6]
```

***

### 5. Пример в автотестах (QA Automation)

📌 Получить список **только упавших тестов**:

```python
test_results = {"test_1": "passed", "test_2": "failed", "test_3": "failed"}
failed_tests = [name for name, result in test_results.items() if result == "failed"]
print(failed_tests)  # ['test_2', 'test_3']
```

📌 Преобразовать результаты тестов в словарь:

```python
status_map = {name: (result == "passed") for name, result in test_results.items()}
print(status_map)  # {'test_1': True, 'test_2': False, 'test_3': False}
```
