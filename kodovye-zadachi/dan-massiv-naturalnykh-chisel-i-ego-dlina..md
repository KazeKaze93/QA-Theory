---
description: Необходимо вывести из этого массива число с наибольшей суммой цифр
---

# Дан массив натуральных чисел и его длина.

```python
arr = [120000, 135, 17, 8, 267, 9, 1500]

def func(lst):
    index, value = max(enumerate(lst), key=lambda x: sum(int(digit) for digit in str(x[1])))
    return index, value

result_index, result_value = func(arr)
print(f"Индекс числа с наибольшей суммой цифр: {result_index}")
print(f"Значение числа: {result_value}")

```

Или

```python
arr = [120000, 135, 17, 8, 267, 9, 1500]


def max_sum_of_digits(numbers):
    max_index = None
    max_digit_sum = 0

    for i, number in enumerate(numbers):
        current_digit_sum = sum(int(digit) for digit in str(number))
        if current_digit_sum > max_digit_sum:
            max_digit_sum = current_digit_sum
            max_index = i

    return max_index, numbers[max_index]


result_index, result_value = max_sum_of_digits(arr)
print(f"Индекс числа с наибольшей суммой цифр: {result_index}")
print(f"Значение числа: {result_value}")


```

```java
public class Solution {
    public int findNumberWithMaxDigitSum(int[] nums) {
        int maxSum = Integer.MIN_VALUE; // Начальное значение максимальной суммы
        int number = -1; // Начальное значение числа с наибольшей суммой

        for (int num : nums) {
            int sum = 0;
            while (num > 0) {
                sum += num % 10;
                num /= 10;
            }
            if (sum > maxSum || (sum == maxSum && num > number)) {
                maxSum = sum;
                number = num;
            }
        }

        return number;
    }
}


```
