---
description: >-
  Необходимо вывести из этого словаря число с наибольшей суммой цифр, а также
  сумму этого значения
---

# Дан словарь натуральных чисел и его длина.



```python
dct = {0: 242, 1: 4424, 2: 542424, 3: 64242, 4: 94242, 5: 14242, 6: 204, 7: 9004, 8: 400}

def func(dct):
    index, value = max(dct.items(), key=lambda x: sum(int(numb) for numb in str(x[1])))
    value_sum = sum(int(numb) for numb in str(value))
    return index, value, value_sum

index, value, value_sum = func(dct)
print(f"Индекс: {index}, Значение: {value}, Сумма цифр: {value_sum}")


```

```java
import java.util.HashMap;
import java.util.Map;

public class Solution {
    public void findNumberWithMaxDigitSum(Map<Integer, Integer> dictionary) {
        int maxSum = Integer.MIN_VALUE; // Начальное значение максимальной суммы
        int maxNumber = -1; // Начальное значение числа с наибольшей суммой

        for (Map.Entry<Integer, Integer> entry : dictionary.entrySet()) {
            int number = entry.getKey();
            int sum = 0;
            while (number > 0) {
                sum += number % 10;
                number /= 10;
            }
            if (sum > maxSum || (sum == maxSum && number > maxNumber)) {
                maxSum = sum;
                maxNumber = entry.getKey();
            }
        }

        System.out.println("Число с наибольшей суммой цифр: " + maxNumber);
        System.out.println("Сумма этого числа: " + maxSum);
    }
}

```
