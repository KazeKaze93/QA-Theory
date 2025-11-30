---
description: инственный элемент.
---

# В непустом массиве целых чисел nums каждый элемент встречается дважды, кроме одного. Найдите этот ед



```python
from typing import List

class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        unique_nums = set()
        for num in nums:
            if num in unique_nums:
                unique_nums.remove(num)
            else:
                unique_nums.add(num)
        return unique_nums.pop()

```

```python
from typing import List

class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        result = 0
        for num in nums:
            result ^= num
        return result

```

```java
import java.util.HashMap;
import java.util.Map;

public class Solution {
    public int singleNumber(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        // Подсчет количества вхождений каждого элемента
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        // Поиск элемента, который встречается только один раз
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            if (entry.getValue() == 1) {
                return entry.getKey();
            }
        }
        return -1; // Если такого элемента не найдено
    }
}

```

```java
public class Solution {
    public int singleNumber(int[] nums) {
        int result = 0;
        for (int num : nums) {
            result ^= num;
        }
        return result;
    }
}

```
