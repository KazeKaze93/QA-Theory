# Нужно проверить, все ли числа в последовательности уникальны.

```python
def are_all_unique(sequence):
    # Преобразуем последовательность во множество и сравниваем длины
    return len(sequence) == len(set(sequence))
```

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<Integer> sequence1 = Arrays.asList(1, 2, 3, 4, 5);
        List<Integer> sequence2 = Arrays.asList(1, 2, 3, 4, 5, 1);

        System.out.println("Последовательность 1 уникальна: " + areAllUnique(sequence1));
        System.out.println("Последовательность 2 уникальна: " + areAllUnique(sequence2));
    }

    public static boolean areAllUnique(List<Integer> sequence) {
        Set<Integer> uniqueNumbers = new HashSet<>();
        for (Integer number : sequence) {
            if (uniqueNumbers.contains(number)) {
                return false; // Найдено повторяющееся число, последовательность не уникальна
            }
            uniqueNumbers.add(number);
        }
        return true; // Все числа уникальны
    }
}

```
