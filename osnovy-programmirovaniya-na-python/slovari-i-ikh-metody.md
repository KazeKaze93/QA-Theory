# Словари и их методы

### **1. Что такое словарь**

* Словарь — это **неупорядоченная коллекция пар «ключ: значение»**.
* Ключи должны быть **уникальными и неизменяемыми** (например, строки, числа, кортежи).
* Значения могут быть **любого типа**.

```python
user = {"username": "alice", "password": "123"}
print(user["username"])  # alice
```

***

### **2. Основные методы словарей**

| Метод                           | Описание                                                           |
| ------------------------------- | ------------------------------------------------------------------ |
| `dict.get(key, default)`        | Возвращает значение по ключу, если нет ключа — `default`           |
| `dict.keys()`                   | Возвращает объект с ключами словаря                                |
| `dict.values()`                 | Возвращает объект со значениями словаря                            |
| `dict.items()`                  | Возвращает объект с парами `(ключ, значение)`                      |
| `dict.update(other_dict)`       | Обновляет словарь значениями из другого словаря                    |
| `dict.pop(key, default)`        | Удаляет ключ и возвращает значение, если ключа нет — `default`     |
| `dict.popitem()`                | Удаляет и возвращает пару `(ключ, значение)`                       |
| `dict.clear()`                  | Очищает словарь                                                    |
| `dict.setdefault(key, default)` | Возвращает значение по ключу, если ключа нет — добавляет `default` |
| `dict.copy()`                   | Создаёт поверхностную копию словаря                                |

***

### **3. Примеры использования**

```python
user = {"username": "alice", "password": "123"}

# Получение значений
print(user.get("username"))       # alice
print(user.get("email", "none")) # none

# Добавление и обновление
user["email"] = "alice@example.com"
user.update({"password": "456"})

# Удаление
user.pop("email")
last_item = user.popitem()  # удаляет последнюю добавленную пару

# Просмотр
print(user.keys())    # dict_keys(['username', 'password'])
print(user.values())  # dict_values(['alice', '456'])
print(user.items())   # dict_items([('username', 'alice'), ('password', '456')])
```

***

### **4. Применение в автотестах**

* **Обработка JSON/API ответов**

```python
response = {"status": "ok", "data": {"id": 1, "name": "Alice"}}
assert response.get("status") == "ok"
```

* **Генерация тестовых данных**

```python
test_user = {}
test_user.setdefault("username", "testuser")
test_user.setdefault("password", "123")
```

* **Фильтрация данных**

```python
users = [{"name": "Alice", "active": True}, {"name": "Bob", "active": False}]
active_users = [u for u in users if u.get("active")]
```
