# Что такое рекурсия?

### **1. Что такое рекурсия**

* **Рекурсия** — это когда функция **вызывает сама себя** для решения задачи.
* Обычно задача делится на **более простые подзадачи**, пока не достигнем **базового случая** (условие выхода).

***

### **2. Структура рекурсивной функции**

1. **Базовый случай** — условие, при котором функция перестаёт вызывать сама себя.
2. **Рекурсивный случай** — часть задачи, где функция вызывает саму себя с “упрощёнными” данными.

```python
def factorial(n):
    if n == 0:        # базовый случай
        return 1
    return n * factorial(n-1)  # рекурсивный случай

print(factorial(5))  # 120
```

***

### **3. Пример с деревом/структурой данных**

Рекурсия часто используется для обхода вложенных структур:

```python
def print_nested_list(lst):
    for item in lst:
        if isinstance(item, list):
            print_nested_list(item)  # рекурсивный вызов
        else:
            print(item)

nested = [1, [2, 3], [4, [5, 6]]]
print_nested_list(nested)
```

**Вывод:**

```
1
2
3
4
5
6
```

***

### **4. Применение рекурсии в автоматизации тестирования**

* **Обход DOM-дерева**: поиск элементов в сложных вложенных структурах.
* **Обход вложенных JSON-ответов**: поиск ключей/значений.
* **Рекурсивные генераторы данных**: например, создание вложенных тестовых структур.

```python
def find_key(data, target):
    if isinstance(data, dict):
        for k, v in data.items():
            if k == target:
                return v
            result = find_key(v, target)
            if result:
                return result
    elif isinstance(data, list):
        for item in data:
            result = find_key(item, target)
            if result:
                return result
    return None

response = {"user": {"id": 1, "details": {"name": "Alice"}}}
print(find_key(response, "name"))  # Alice
```

***

### **5. Важные моменты**

* Всегда нужен **базовый случай**, иначе будет **бесконечная рекурсия → RecursionError**.
* В Python есть ограничение на глубину рекурсии (`sys.getrecursionlimit()`, обычно 1000).
