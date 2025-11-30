# Сложите цифры целого числа.

```python
def sum_of_digits(number):
    # Преобразуем число в строку, затем каждую цифру в число и суммируем их
    return sum(int(digit) for digit in str(abs(number)))

# Пример использования
try:
    # Вводим целое число
    num = int(input("Введите целое число: "))

    # Вычисляем и выводим сумму цифр
    result = sum_of_digits(num)
    print(f"Сумма цифр числа {num} равна {result}")
except ValueError:
    print("Ошибка: Введите корректное целое число.")
```

```python
def sum_of_digits(number):
    # Определяем знак числа
    sign = -1 if number < 0 else 1
    
    # Суммируем цифры, учитывая знак числа
    return sign * sum(int(digit) for digit in str(abs(number)))

# Пример использования
result = sum_of_digits(-12345)
print(result)  # Вывод: -15

```

```java
public class Main {
    public static void main(String[] args) {
        int number = 12345;
        int sum = sumDigits(number);
        System.out.println("Сумма цифр числа " + number + ": " + sum);
    }

    public static int sumDigits(int number) {
        int sum = 0;
        while (number != 0) {
            sum += number % 10; // Добавляем к сумме последнюю цифру числа
            number /= 10; // Убираем последнюю цифру числа
        }
        return sum;
    }
}

```
