# Контекстный менеджер

### **1. Что такое контекстный менеджер**

* Контекстный менеджер управляет ресурсами, обеспечивая **правильное открытие и закрытие**.
* Используется через конструкцию `with`.
* Основная идея: **гарантированное выполнение кода при входе и выходе из контекста**, даже если возникла ошибка.

***

### **2. Синтаксис**

```python
with <context_manager> as <variable>:
    # код внутри контекста
```

***

### **3. Пример с файлом**

```python
with open("test.txt", "w") as f:
    f.write("Hello, world!")
# Файл автоматически закрыт после выхода из блока
```

✅ Не нужно вызывать `f.close()` вручную.

***

### **4. Пример с блокировками (threading.Lock)**

```python
import threading

lock = threading.Lock()

with lock:
    # критическая секция
    print("Работаем с ресурсом безопасно")
```

* Контекстный менеджер гарантирует, что блокировка освободится даже при ошибке.

***

### **5. Создание собственного контекстного менеджера**

#### Вариант 1: через методы `__enter__` и `__exit__`

```python
class MyResource:
    def __enter__(self):
        print("Ресурс открыт")
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        print("Ресурс закрыт")

with MyResource() as r:
    print("Используем ресурс")
```

**Вывод:**

```
Ресурс открыт
Используем ресурс
Ресурс закрыт
```

#### Вариант 2: через декоратор `contextlib.contextmanager`

```python
from contextlib import contextmanager

@contextmanager
def my_resource():
    print("Открываю ресурс")
    yield "ресурс"
    print("Закрываю ресурс")

with my_resource() as r:
    print(f"Работаем с {r}")
```

***

### **6. Применение в автоматизации тестирования**

* **Файлы**: чтение/запись тестовых данных.
* **WebDriver**: запуск браузера и автоматическое закрытие.

```python
from selenium import webdriver

with webdriver.Chrome() as driver:
    driver.get("https://example.com")
    print(driver.title)
# Браузер закрыт автоматически
```

* **Сессии API**: `requests.Session()` через `with` для корректного закрытия соединения.
