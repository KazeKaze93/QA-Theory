# Напишите функцию, которая переворачивает строку. Входная строка задана в виде массива символов s.

```python
from typing import List

class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        left, right = 0, len(s) - 1
        while left < right:
            # Swap characters at left and right pointers
            s[left], s[right] = s[right], s[left]
            # Move pointers towards the center
            left += 1
            right -= 1
            
solution = Solution()
s = ["h", "e", "l", "l", "o"]
solution.reverseString(s)
print(s)  # Output: ["o", "l", "l", "e", "h"]

```

```python
def func(lst):
    lst.reverse()
    return lst
```

```python
def func(lst):
    return lst[::-1]
```

```python
def func(lst):
    return list(reversed(lst))
```

```java
public class Solution {
    public void reverseString(char[] s) {
        int left = 0;
        int right = s.length - 1;
        
        while (left < right) {
            char temp = s[left];
            s[left] = s[right];
            s[right] = temp;
            left++;
            right--;
        }
    }
}

```

```java
public class Solution {
    public void reverseString(char[] s) {
        StringBuilder sb = new StringBuilder();
        sb.append(s);
        sb.reverse();
        sb.getChars(0, sb.length(), s, 0);
    }
}

```
