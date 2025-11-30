# Модуль collections

Модуль **`collections`** в Python — это стандартная библиотека, которая предоставляет специализированные контейнеры данных с дополнительной функциональностью по сравнению с базовыми типами данных (список, словарь, множество и т.д.). Он часто используется в автоматизации для удобной работы с коллекциями данных.

Основные структуры данных из `collections`:

1.  **`namedtuple`**\
    — Создаёт кортеж с именованными полями. Удобен, когда нужно иметь кортеж с доступом к элементам по имени, а не только по индексу.

    ```python
    from collections import namedtuple
    Point = namedtuple('Point', ['x', 'y'])
    p = Point(10, 20)
    print(p.x)  # 10
    ```
2.  **`deque`**\
    — Двунаправленная очередь с быстрыми операциями добавления и удаления с обоих концов (очень эффективна для очередей и стэков).

    ```python
    from collections import deque
    d = deque([1, 2, 3])
    d.appendleft(0)
    d.pop()
    ```
3.  **`Counter`**\
    — Счётчик элементов в итерируемом объекте, удобно для подсчёта повторений.

    ```python
    from collections import Counter
    c = Counter(['a', 'b', 'a', 'c', 'b', 'a'])
    print(c)  # Counter({'a': 3, 'b': 2, 'c': 1})
    ```
4.  **`OrderedDict`** (до Python 3.7 имел смысл, с 3.7 обычный dict уже сохраняет порядок вставки)\
    — Словарь, который сохраняет порядок добавления элементов. Полезен, если важен порядок.

    ```python
    from collections import OrderedDict
    od = OrderedDict()
    od['one'] = 1
    od['two'] = 2
    ```
5.  **`defaultdict`**\
    — Словарь с значениями по умолчанию. При обращении к несуществующему ключу автоматически создаёт значение по заданной функции.

    ```python
    from collections import defaultdict
    dd = defaultdict(int)  # по умолчанию 0
    dd['a'] += 1
    print(dd['a'])  # 1
    ```

***

#### Когда полезен в автоматизации?

* `Counter` для подсчёта, например, количества успешных/неуспешных тестов.
* `defaultdict` — удобен при агрегации данных по ключам (например, группировка логов по типу).
* `deque` — для реализации очередей заданий, если нужна эффективная вставка/удаление.
* `namedtuple` — для структурирования данных с именованными полями (например, результаты тестов).

***

#### Пример 1. Использование `Counter` для подсчёта результатов тестов

Представим, что у нас есть список результатов запуска тестов, и мы хотим посчитать, сколько было успешных и неуспешных тестов.

```python
from collections import Counter

def test_results_summary():
    # Имитируем результаты тестов
    test_results = ['passed', 'failed', 'passed', 'skipped', 'failed', 'passed']

    counter = Counter(test_results)

    assert counter['passed'] == 3
    assert counter['failed'] == 2
    assert counter['skipped'] == 1
```

***

#### Пример 2. Использование `defaultdict` для группировки логов по уровню

```python
from collections import defaultdict

def test_group_logs_by_level():
    logs = [
        ('ERROR', 'Null pointer exception'),
        ('INFO', 'Started process'),
        ('ERROR', 'Index out of range'),
        ('DEBUG', 'Variable x = 10'),
        ('INFO', 'Process finished'),
    ]

    grouped_logs = defaultdict(list)

    for level, message in logs:
        grouped_logs[level].append(message)

    assert len(grouped_logs['ERROR']) == 2
    assert len(grouped_logs['INFO']) == 2
    assert len(grouped_logs['DEBUG']) == 1
```

***

#### Пример 3. Использование `namedtuple` для структурирования данных теста

```python
from collections import namedtuple

TestCase = namedtuple('TestCase', ['name', 'input_data', 'expected_result'])

def test_using_namedtuple():
    test_case = TestCase(name='Check addition', input_data=(2, 3), expected_result=5)

    result = sum(test_case.input_data)

    assert result == test_case.expected_result
```

***

#### Пример 4. Использование `deque` для очереди задач в тесте

```python
from collections import deque

def test_task_queue():
    tasks = deque(['test_login', 'test_logout', 'test_payment'])

    # Выполняем первый тест
    current_task = tasks.popleft()
    assert current_task == 'test_login'

    # Добавим новый тест в очередь
    tasks.append('test_profile')

    assert list(tasks) == ['test_logout', 'test_payment', 'test_profile']
```
