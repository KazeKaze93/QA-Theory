---
description: ом.
---

# Напишите программу, которая принимает два списка и выводит все элементы первого, которых нет во втор

```python
def find_unique_elements(list1, list2):
    unique_elements = [element for element in list1 if element not in list2]
    return unique_elements
```

or

```python
def find_unique_elements(list1, list2):
    set1 = set(list1)
    set2 = set(list2)
    unique_elements = set1 - set2
    return list(unique_elements)
```

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<Integer> list1 = Arrays.asList(1, 2, 3, 4, 5);
        List<Integer> list2 = Arrays.asList(3, 4, 5, 6, 7);
        
        List<Integer> uniqueElements = findUniqueElements(list1, list2);
        
        System.out.println("Элементы первого списка, которых нет во втором: " + uniqueElements);
    }

    public static <T> List<T> findUniqueElements(List<T> list1, List<T> list2) {
        Set<T> set2 = new HashSet<>(list2);
        List<T> uniqueElements = new ArrayList<>();
        for (T element : list1) {
            if (!set2.contains(element)) {
                uniqueElements.add(element);
            }
        }
        return uniqueElements;
    }
}

```
