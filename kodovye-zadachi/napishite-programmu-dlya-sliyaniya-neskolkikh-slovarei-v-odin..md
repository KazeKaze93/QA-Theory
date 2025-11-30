# Напишите программу для слияния нескольких словарей в один.

```python
def merge_dicts(*dicts):
    merged_dict = {}
    for d in dicts:
        merged_dict.update(d)
    return merged_dict

# Пример использования
dict1 = {'one': 1, 'two': 2}
dict2 = {'three': 3, 'four': 4}
dict3 = {'five': 5, 'six': 6}

merged_dict = merge_dicts(dict1, dict2, dict3)

# Вывод результата
print("Исходные словари:")
print("dict1:", dict1)
print("dict2:", dict2)
print("dict3:", dict3)
print("\nОбъединенный словарь:")
print("merged_dict:", merged_dict)
```

Этот код создает функцию `merge_dicts`, которая принимает произвольное количество словарей и объединяет их в один, используя метод `update()`. Результат будет:

```
Исходные словари:
dict1: {'one': 1, 'two': 2}
dict2: {'three': 3, 'four': 4}
dict3: {'five': 5, 'six': 6}

Объединенный словарь:
merged_dict: {'one': 1, 'two': 2, 'three': 3, 'four': 4, 'five': 5, 'six': 6}
```

```java
import java.util.*;

public class Solution {
    public static void main(String[] args) {
        Map<Integer, String> dictionary1 = new HashMap<>();
        dictionary1.put(1, "one");
        dictionary1.put(2, "two");
        
        Map<Integer, String> dictionary2 = new HashMap<>();
        dictionary2.put(3, "three");
        dictionary2.put(4, "four");
        
        Map<Integer, String> mergedDictionary = mergeDictionaries(dictionary1, dictionary2);
        System.out.println("Объединенный словарь:");
        System.out.println(mergedDictionary);
    }
    
    public static <K, V> Map<K, V> mergeDictionaries(Map<K, V>... dictionaries) {
        Map<K, V> mergedDictionary = new HashMap<>();
        for (Map<K, V> dictionary : dictionaries) {
            mergedDictionary.putAll(dictionary);
        }
        return mergedDictionary;
    }
}

```
