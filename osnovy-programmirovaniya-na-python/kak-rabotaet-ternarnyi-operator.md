# Как работает тернарный оператор

В Python **тернарный оператор** — это способ **сократить условный оператор `if-else`** в одну строку.

***

### **1. Синтаксис**

```python
value_if_true if condition else value_if_false
```

* **condition** — условие, которое проверяется.
* **value\_if\_true** — значение, которое вернётся, если условие истинно.
* **value\_if\_false** — значение, которое вернётся, если условие ложно.

***

### **2. Примеры**

#### **2.1 Простое присваивание**

```python
x = 10
result = "Even" if x % 2 == 0 else "Odd"
print(result)  # "Even"
```

#### **2.2 Вызов функции**

```python
def greet():
    return "Hello"

def bye():
    return "Goodbye"

is_morning = True
message = greet() if is_morning else bye()
print(message)  # "Hello"
```

#### **2.3 В списках/генераторах**

```python
numbers = [1, 2, 3, 4]
labels = ["Even" if n % 2 == 0 else "Odd" for n in numbers]
print(labels)  # ['Odd', 'Even', 'Odd', 'Even']
```

***

### **3. Отличие от обычного `if-else`**

```python
# обычный if-else
if x % 2 == 0:
    result = "Even"
else:
    result = "Odd"

# тернарный оператор
result = "Even" if x % 2 == 0 else "Odd"
```

* Тернарный оператор — **короткая, компактная запись**.
* Можно использовать в **присваиваниях, возврате функции, генераторах списков**.

***

### **4. Применение в автоматизации тестирования**

* Быстро выбрать **значение параметра для теста**:

```python
status_code = 200
message = "OK" if status_code == 200 else "Error"
```

* Использовать в **генерации данных или фильтрации**:

```python
results = [res if res != None else "N/A" for res in api_responses]
```
