# Что такое case function?

`CASE` в SQL — это конструкция, которая работает как условный оператор (**аналог if-else**). Она позволяет возвращать разные значения в зависимости от условия.

***

### Виды `CASE`

#### 1️⃣ **Простой CASE**

Сравнивает выражение с набором значений.

```sql
SELECT name,
       CASE department_id
            WHEN 1 THEN 'HR'
            WHEN 2 THEN 'Finance'
            WHEN 3 THEN 'IT'
            ELSE 'Other'
       END AS department_name
FROM employees;
```

Здесь `department_id` проверяется на равенство 1, 2, 3.

***

#### 2️⃣ **Поисковый CASE**

Позволяет задавать произвольные логические условия (`WHEN ... THEN`).

```sql
SELECT name, salary,
       CASE
            WHEN salary < 3000 THEN 'Low'
            WHEN salary BETWEEN 3000 AND 7000 THEN 'Medium'
            ELSE 'High'
       END AS salary_level
FROM employees;
```

Здесь сравнение идёт по диапазонам.

***

### Особенности

* `CASE` всегда возвращает **одно значение**.
* Можно использовать в `SELECT`, `WHERE`, `ORDER BY`, `GROUP BY`.
* Работает до первого совпавшего условия (`WHEN`).
* Если ни одно условие не выполнено и нет `ELSE`, результат будет `NULL`.

***

### Пример для QA-задач

Хочешь проверить корректность бизнес-логики:

```sql
SELECT order_id,
       CASE 
           WHEN status = 'P' THEN 'Pending'
           WHEN status = 'C' THEN 'Completed'
           WHEN status = 'X' THEN 'Cancelled'
           ELSE 'Unknown'
       END AS status_text
FROM orders;
```
