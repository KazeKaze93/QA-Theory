---
description: 'my_dict = {''a'':500, ''b'':5874, ''c'': 560,''d'':400, ''e'':5874, ''f'': 20}.'
---

# Найдите три ключа с самыми высокими значениями в словаре



```python
my_dict = {'a': 500, 'b': 5874, 'c': 560, 'd': 400, 'e': 5874, 'f': 20}

# Находим три ключа с самыми высокими значениями
top_keys = sorted(my_dict.items(), key=lambda x: x[1], reverse=True)[:3]

print(dict(top_keys))
```

```java
import java.util.*;

public class Solution {
    public static void main(String[] args) {
        Map<String, Integer> my_dict = new HashMap<>();
        my_dict.put("a", 500);
        my_dict.put("b", 5874);
        my_dict.put("c", 560);
        my_dict.put("d", 400);
        my_dict.put("e", 5874);
        my_dict.put("f", 20);

        List<Map.Entry<String, Integer>> sortedEntries = new ArrayList<>(my_dict.entrySet());
        Collections.sort(sortedEntries, (a, b) -> b.getValue().compareTo(a.getValue()));

        System.out.println("Три ключа с самыми высокими значениями:");
        for (int i = 0; i < 3 && i < sortedEntries.size(); i++) {
            Map.Entry<String, Integer> entry = sortedEntries.get(i);
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
    }
}

```
