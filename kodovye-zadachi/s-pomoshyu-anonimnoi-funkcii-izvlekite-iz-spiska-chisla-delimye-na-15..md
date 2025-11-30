# С помощью анонимной функции извлеките из списка числа, делимые на 15.

```python
my_list = [15, 30, 45, 60, 75, 90, 105]

# Используем анонимную функцию для фильтрации чисел, делимых на 15
result = list(filter(lambda x: x % 15 == 0, my_list))

print("Числа, делимые на 15:", result)
```

```java
import java.util.*;
import java.util.function.*;

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(15, 30, 45, 10, 20, 25);

        // Используем анонимное лямбда-выражение для фильтрации чисел, делимых на 15
        List<Integer> divisibleBy15 = filterNumbers(numbers, new Predicate<Integer>() {
            @Override
            public boolean test(Integer number) {
                return number % 15 == 0;
            }
        });

        System.out.println("Числа, делимые на 15: " + divisibleBy15);
    }

    public static List<Integer> filterNumbers(List<Integer> numbers, Predicate<Integer> predicate) {
        List<Integer> result = new ArrayList<>();
        for (Integer number : numbers) {
            if (predicate.test(number)) {
                result.add(number);
            }
        }
        return result;
    }
}

```
