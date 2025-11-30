---
description: ... n"
---

# Реализуйте функцию convert(), принимающую числовое значение n и возвращающую строку вида "123456 ...

Для реализации функции `convert()`, которая принимает числовое значение `n` и возвращает строку вида "123456...n", вы можете воспользоваться циклом, чтобы построить строку, включающую все числа от 1 до `n`. Вот пример на Python:

```python
def convert(n):
    if n < 1:
        return "Invalid input. Please provide a positive integer greater than or equal to 1."

    result = ''.join(str(i) for i in range(1, n + 1))
    return result

# Примеры использования:
print(convert(5))  # Выведет: "12345"
print(convert(10))  # Выведет: "12345678910"
print(convert(0))  # Выведет: "Invalid input. Please provide a positive integer greater than or equal to 1."
```

Эта функция создает строку, объединяя числа от 1 до `n` при помощи генератора списка и метода `join()`. В случае, если `n` меньше 1, функция вернет сообщение об ошибке.

Или:<br>

```python
def convert(n):
    return ''.join(map(str, range(1, n + 1)))

print(convert(12))

```

```java
public class Solution {
    public static void main(String[] args) {
        int n = 5;
        String result = convert(n);
        System.out.println(result);
    }
    
    public static String convert(int n) {
        StringBuilder sb = new StringBuilder();
        for (int i = 1; i <= n; i++) {
            sb.append(i);
        }
        return sb.toString();
    }
}

```
