# При заданном целом числе n посчитайте n + nn + nnn.

```python
def calculate_expression(n):
    # Преобразуем число в строку и выполняем вычисление
    n_str = str(n)
    nn = int(n_str * 2)
    nnn = int(n_str * 3)
    
    result = n + nn + nnn
    return result

# Пример использования
try:
    # Вводим целое число
    n = int(input("Введите целое число n: "))
    
    # Вычисляем и выводим результат
    result = calculate_expression(n)
    print(f"Результат выражения {n} + {n * 11} + {n * 111} равен {result}")
except ValueError:
    print("Ошибка: Введите корректное целое число.")
```

```python
def calculate_expression(n):
    return n + int(str(n) * 2) + int(str(n) * 3)

# Пример использования
try:
    # Вводим целое число
    n = int(input("Введите целое число n: "))
    
    # Вычисляем и выводим результат
    result = calculate_expression(n)
    print(f"Результат выражения {n} + {n * 11} + {n * 111} равен {result}")
except ValueError:
    print("Ошибка: Введите корректное целое число.")

```

```java
public class Main {
    public static void main(String[] args) {
        int n = 5;
        int result = calculateExpression(n);
        System.out.println("Результат выражения: " + result);
    }

    public static int calculateExpression(int n) {
        // Создаем строки для n, nn и nnn
        String nStr = String.valueOf(n);
        String nnStr = nStr + nStr;
        String nnnStr = nnStr + nStr;

        // Преобразуем строки в целые числа и складываем
        int nnInt = Integer.parseInt(nnStr);
        int nnnInt = Integer.parseInt(nnnStr);
        return n + nnInt + nnnInt;
    }
}

```
