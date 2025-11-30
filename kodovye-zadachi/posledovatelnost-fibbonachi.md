# Последовательность Фиббоначи

Итеративный подход:

```python
def fibonacci(n):
    fib_sequence = [0, 1]
    while len(fib_sequence) < n:
        fib_sequence.append(sum(fib_sequence[-2:]))
    return fib_sequence[:n]

# Пример использования
n = int(input("Введите количество чисел Фибоначчи: "))
fibonacci_sequence = fibonacci(n)
print(f"Последовательность чисел Фибоначчи для n={n}:")
print(fibonacci_sequence)

```

```python
def fibonacci(n):
    fib_sequence = [0, 1]  # Начальные элементы последовательности
    
    # Для n=0 или n=1 возвращаем соответствующее значение
    if n == 0:
        return [0]
    elif n == 1:
        return [0, 1]
    
    # Добавляем новые элементы в последовательность до достижения длины n
    while len(fib_sequence) < n:
        next_number = fib_sequence[-1] + fib_sequence[-2]  # Следующее число - сумма двух предыдущих
        fib_sequence.append(next_number)
    
    return fib_sequence

# Пример использования
n = int(input("Введите количество чисел Фибоначчи: "))
fibonacci_sequence = fibonacci(n)
print(f"Последовательность чисел Фибоначчи для n={n}:")
print(fibonacci_sequence)

```

Рекурсивный подход:

```python
def fibonacci(n):
    if n <= 1:
        return n
    else:
        return fibonacci(n-1) + fibonacci(n-2)

# Пример использования функции:
num = 10  # Задаем номер числа Фибоначчи, которое хотим вычислить
result = fibonacci(num)
print(f"Число Фибоначчи под номером {num} равно {result}")

```

```java
public class FibonacciSequence {
    public static void main(String[] args) {
        int n = 10; // Количество чисел в последовательности
        printFibonacciSequence(n);
    }

    public static void printFibonacciSequence(int n) {
        int a = 0;
        int b = 1;
        System.out.println("Последовательность Фибоначчи:");
        System.out.print(a + " " + b + " ");
        for (int i = 2; i < n; i++) {
            int next = a + b;
            System.out.print(next + " ");
            a = b;
            b = next;
        }
    }
}

```
