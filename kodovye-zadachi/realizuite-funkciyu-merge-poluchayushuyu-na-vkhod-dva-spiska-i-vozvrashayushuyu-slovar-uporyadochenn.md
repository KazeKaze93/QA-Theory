---
description: >-
  ключам(ключ из первого списка, значение из второго). Длина списка не
  обязательно равна длине другого
---

# Реализуйте функцию merge(), получающую на вход два списка и возвращающую словарь, упорядоченный по

```python
def merge(keys, values):
    # Используем функцию zip для объединения списков в кортежи
    # Затем сортируем по ключам и создаем словарь
    return dict(sorted(zip(keys, values)))


# Пример использования
keys_list = ['b', 'a', 'c']
values_list = [2, 1, 3]

result_dict = merge(keys_list, values_list)
print(result_dict)

```

В этом примере используется функция `zip()`, чтобы создать кортежи из соответствующих элементов двух списков. Затем эти кортежи преобразуются в словарь с помощью `dict()`. Важно отметить, что если списки разной длины, то создаваемый словарь будет содержать ключи и значения только до минимальной длины списка.

```java
import java.util.*;

public class Solution {
    public static void main(String[] args) {
        List<String> keys = Arrays.asList("a", "b", "c");
        List<Integer> values = Arrays.asList(1, 2, 3, 4);
        Map<String, Integer> mergedMap = merge(keys, values);
        System.out.println("Словарь, упорядоченный по ключам:");
        System.out.println(mergedMap);
    }
    
    public static <K, V> Map<K, V> merge(List<K> keys, List<V> values) {
        Map<K, V> mergedMap = new LinkedHashMap<>();
        Iterator<K> keyIterator = keys.iterator();
        Iterator<V> valueIterator = values.iterator();
        while (keyIterator.hasNext() && valueIterator.hasNext()) {
            K key = keyIterator.next();
            V value = valueIterator.next();
            mergedMap.put(key, value);
        }
        return mergedMap;
    }
}

```
