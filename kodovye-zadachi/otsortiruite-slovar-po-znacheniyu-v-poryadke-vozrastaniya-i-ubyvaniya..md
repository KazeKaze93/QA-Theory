# Отсортируйте словарь по значению в порядке возрастания и убывания.

Для сортировки словаря по значениям в порядке возрастания и убывания, вы можете использовать функцию `sorted` с параметром `key`, который указывает на функцию, возвращающую значение, по которому нужно сортировать. Вот пример кода на Python:

```python
# Исходный словарь
my_dict = {'one': 1, 'four': 4, 'three': 3, 'five': 5, 'two': 2}

# Сортировка по значению в порядке возрастания
ascending_sorted_dict = dict(sorted(my_dict.items(), key=lambda item: item[1]))

# Сортировка по значению в порядке убывания
descending_sorted_dict = dict(sorted(my_dict.items(), key=lambda item: item[1], reverse=True))

# Вывод результатов
print("Сортировка по значению в порядке возрастания:", ascending_sorted_dict)
print("Сортировка по значению в порядке убывания:", descending_sorted_dict)
```

Этот код создает два новых словаря, один с сортировкой по значениям в порядке возрастания, а другой в порядке убывания. Результат будет следующим:

```
Сортировка по значению в порядке возрастания: {'one': 1, 'two': 2, 'three': 3, 'four': 4, 'five': 5}
Сортировка по значению в порядке убывания: {'five': 5, 'four': 4, 'three': 3, 'two': 2, 'one': 1}
```



Для сортировки по возрастанию:

```java
import java.util.*;

public class Solution {
    public static void main(String[] args) {
        Map<Integer, Integer> dictionary = new HashMap<>();
        dictionary.put(1, 10);
        dictionary.put(2, 5);
        dictionary.put(3, 8);
        
        System.out.println("Сортировка по возрастанию:");
        dictionary.entrySet().stream()
            .sorted(Map.Entry.comparingByValue())
            .forEach(entry -> System.out.println(entry.getKey() + ": " + entry.getValue()));
    }
}
```

Для сортировки по убыванию:

```java
import java.util.*;

public class Solution {
    public static void main(String[] args) {
        Map<Integer, Integer> dictionary = new HashMap<>();
        dictionary.put(1, 10);
        dictionary.put(2, 5);
        dictionary.put(3, 8);
        
        System.out.println("Сортировка по убыванию:");
        dictionary.entrySet().stream()
            .sorted(Collections.reverseOrder(Map.Entry.comparingByValue()))
            .forEach(entry -> System.out.println(entry.getKey() + ": " + entry.getValue()));
    }
}
```
