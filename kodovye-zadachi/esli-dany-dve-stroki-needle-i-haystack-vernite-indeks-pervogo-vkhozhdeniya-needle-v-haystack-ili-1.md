---
description: если needle не является частью haystack.
---

# Если даны две строки needle и haystack, верните индекс первого вхождения needle в haystack или -1,



```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if not needle:
            return 0
        if needle in haystack:
            return haystack.index(needle)
        else:
            return -1


haystack = "sadbutsad"
needle = "sad"
solution = Solution()
print(solution.strStr(haystack, needle))  # Вывод: True

```

```java
public class Solution {
    public int strStr(String haystack, String needle) {
        int index = haystack.indexOf(needle);
        return index != -1 ? index : -1;
    }
}
```
