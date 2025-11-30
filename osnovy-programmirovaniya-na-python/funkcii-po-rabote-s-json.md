# Функции по работе с json

В Python для работы с JSON основная библиотека — **`json`** (встроенная, устанавливать не нужно).

***

### **1. Основные функции модуля `json`**

| Функция                    | Назначение                                                       | Пример                         |
| -------------------------- | ---------------------------------------------------------------- | ------------------------------ |
| `json.load(file_obj)`      | Читает JSON из **открытого файла** и преобразует в Python-объект | `data = json.load(f)`          |
| `json.loads(str)`          | Читает JSON **из строки**                                        | `data = json.loads('{"a":1}')` |
| `json.dump(obj, file_obj)` | Записывает Python-объект в файл в формате JSON                   | `json.dump(data, f)`           |
| `json.dumps(obj)`          | Преобразует Python-объект в строку JSON                          | `s = json.dumps(data)`         |

***

### **2. Примеры**

#### 📄 Чтение JSON из файла

```python
import json

with open("data.json", "r", encoding="utf-8") as f:
    data = json.load(f)

print(data)  # {'name': 'Kakha', 'age': 30}
```

***

#### 📜 Чтение JSON из строки

```python
import json

json_str = '{"name": "Kakha", "age": 30}'
data = json.loads(json_str)

print(data["name"])  # Kakha
```

***

#### 💾 Запись JSON в файл

```python
import json

data = {"name": "Kakha", "age": 30}

with open("output.json", "w", encoding="utf-8") as f:
    json.dump(data, f, indent=4, ensure_ascii=False)
```

* `indent=4` — красивое форматирование.
* `ensure_ascii=False` — чтобы сохранить кириллицу как есть, а не `\u041a`.

***

#### 🔄 Преобразование Python → JSON-строка

```python
import json

data = {"name": "Каха", "age": 30}
json_str = json.dumps(data, indent=2, ensure_ascii=False)

print(json_str)
```

***

### **3. Особенности**

* Python `dict` ↔ JSON `object`
* Python `list` ↔ JSON `array`
* Python `str` ↔ JSON `string`
* Python `int/float` ↔ JSON `number`
* Python `True/False` ↔ JSON `true/false`
* Python `None` ↔ JSON `null`

***

💡 **В автотестах JSON часто используют**:

* для парсинга API-ответов (`response.json()` в `requests`)
* для хранения тестовых данных
* для сравнения ожидаемого и фактического результата

***

### **1. Чтение тестовых данных из JSON**

```python
import json
import pytest

@pytest.fixture
def test_data():
    with open("tests/data/user.json", encoding="utf-8") as f:
        return json.load(f)

def test_user_data(test_data):
    assert test_data["role"] == "admin"
```

💡 _Так тесты остаются независимыми от кода — данные хранятся в отдельных файлах._

***

### **2. Работа с API и парсинг JSON**

```python
import requests

def test_api_get_user():
    response = requests.get("https://reqres.in/api/users/2")
    assert response.status_code == 200

    data = response.json()
    assert data["data"]["id"] == 2
    assert "email" in data["data"]
```

💡 _`response.json()` — сразу отдаёт dict, без ручного `json.loads()`._

***

### **3. Сравнение с эталонным JSON**

```python
import json

def test_api_response_matches_expected():
    # Загружаем эталонный ответ
    with open("tests/data/expected_user.json", encoding="utf-8") as f:
        expected = json.load(f)

    # Получаем фактический
    actual = {
        "name": "Kakha",
        "age": 30
    }

    assert actual == expected
```

💡 _Удобно, если JSON маленький и не содержит динамических полей._

***

### **4. Игнор динамических полей при сравнении**

```python
def remove_dynamic_fields(data: dict, fields_to_remove: list):
    return {k: v for k, v in data.items() if k not in fields_to_remove}

def test_api_ignore_timestamps():
    actual = {"id": 1, "createdAt": "2025-08-13T12:00:00Z"}
    expected = {"id": 1, "createdAt": "<ignore>"}

    assert remove_dynamic_fields(actual, ["createdAt"]) == \
           remove_dynamic_fields(expected, ["createdAt"])
```

💡 _Используется, когда API возвращает время, токены и другие переменные значения._

***

### **5. Валидация JSON-схемы**

```python
from jsonschema import validate

schema = {
    "type": "object",
    "properties": {
        "id": {"type": "integer"},
        "email": {"type": "string", "format": "email"}
    },
    "required": ["id", "email"]
}

def test_validate_json_schema():
    data = {"id": 2, "email": "test@example.com"}
    validate(instance=data, schema=schema)
```

💡 _Это особенно любят спрашивать на собесах: как проверить, что API отдаёт данные правильного формата._

***

### **6. Преобразование JSON в строку для логов**

```python
import json
import logging

logging.basicConfig(level=logging.INFO)

def test_log_json():
    data = {"status": "ok", "result": [1, 2, 3]}
    logging.info(json.dumps(data, indent=2, ensure_ascii=False))
```

💡 _Красивый лог помогает отлаживать тесты и понимать, что вернул API._

