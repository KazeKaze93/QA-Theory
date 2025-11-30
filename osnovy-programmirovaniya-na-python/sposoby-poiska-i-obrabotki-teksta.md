# Способы поиска и обработки текста

### 1. Встроенные методы строк (str)

* **`str.find(substring)`** — возвращает индекс первого вхождения подстроки или -1, если не найдено.
* **`str.index(substring)`** — то же, но вызывает ошибку, если подстрока не найдена.
* **`str.count(substring)`** — считает количество вхождений подстроки.
* **`str.startswith(prefix)`** и **`str.endswith(suffix)`** — проверяют начало и конец строки.
* **`str.replace(old, new)`** — замена подстроки.
* **`str.split(sep)`** — разбивает строку по разделителю.
* **`str.strip()`** — удаляет пробелы и спецсимволы по краям.

Пример:

```python
text = "Hello, world! Hello!"
print(text.find("world"))  # 7
print(text.count("Hello"))  # 2
print(text.startswith("Hell"))  # True
```

***

### 2. Регулярные выражения (модуль `re`)

Самый мощный и гибкий способ поиска и обработки сложных шаблонов текста.

Основные функции:

* **`re.search(pattern, string)`** — ищет первое совпадение.
* **`re.findall(pattern, string)`** — возвращает список всех совпадений.
* **`re.match(pattern, string)`** — проверяет совпадение только в начале строки.
* **`re.sub(pattern, repl, string)`** — замена по шаблону.

Пример:

```python
import re

text = "User: alice, ID: 1234"

# Найти ID
match = re.search(r'ID:\s*(\d+)', text)
if match:
    print(match.group(1))  # 1234

# Найти все слова, начинающиеся с буквы 'a'
print(re.findall(r'\ba\w*', text))  # ['alice']
```

***

### 3. Методы обработки текста с помощью библиотеки `string`

* `string` содержит полезные константы и функции, например `string.ascii_letters`, `string.punctuation` для фильтрации и проверки символов.

***

### 4. Использование `in` для проверки вхождения подстроки

```python
if "error" in log_line.lower():
    print("Обнаружена ошибка")
```

***

### 5. Пример сложной обработки

Парсинг лога с помощью регулярных выражений, фильтрация строк, подсчёт ошибок и замена:

```python
import re

log = """
ERROR: file not found
WARNING: low disk space
ERROR: access denied
"""

errors = re.findall(r'ERROR: (.+)', log)
print(errors)  # ['file not found', 'access denied']

cleaned_log = re.sub(r'WARNING: .+', '', log)
print(cleaned_log)
```

***

### Где применяется на практике?

* Проверка содержимого ответов API в тестах.
* Валидация логов и поиск ошибок.
* Обработка и фильтрация текстовых данных в тестовых данных и отчетах.
