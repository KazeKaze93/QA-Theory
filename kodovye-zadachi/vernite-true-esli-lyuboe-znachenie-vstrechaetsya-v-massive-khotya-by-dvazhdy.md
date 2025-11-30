---
description: >-
  Если задан целочисленный массив nums, верните true, если любое значение
  встречается в массиве хотя бы дважды, и верните false, если каждый элемент
  отличается от другого.
---

# Верните true, если любое значение встречается в массиве хотя бы дважды

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        seen = set()
        for num in nums:
            if num in seen:
                return True
            seen.add(num)
        return False

solution = Solution()
nums = [1, 2, 3, 1]
print(solution.containsDuplicate(nums))  # Вывод: True
```

Вернуть значение дубликатов:

```python
def find_duplicates(arr):
    seen = set()
    duplicates = set()

    for element in arr:
        if element in seen:
            duplicates.add(element)
        else:
            seen.add(element)

    return list(duplicates)

# Пример использования:
my_array = [1, 2, 3, 4, 5, 2, 3, 4]
result = find_duplicates(my_array)

if result:
    print("Элементы, встречающиеся хотя бы дважды:", result)
else:
    print("Нет дубликатов в массиве.")

```

```java
import java.util.HashSet;
import java.util.Set;

public class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for (int num : nums) {
            if (set.contains(num)) {
                return true;
            }
            set.add(num);
        }
        return false;
    }
}

```

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        int[] nums = {1, 2, 3, 4, 5}; // Пример массива
        System.out.println(containsDuplicate(nums));
    }

    public static boolean containsDuplicate(int[] nums) {
        return nums.length != Arrays.stream(nums).distinct().count();
    }
}

```
