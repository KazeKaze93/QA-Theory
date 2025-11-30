---
description: >-
  Палиндром — это слово или фраза, которые одинаково читаются слева направо и
  справа налево.
---

# Напишите проверку на то, является ли строка палиндромом.

```python
def is_palindrome(s):
    # Удаляем пробелы и приводим строку к нижнему регистру
    s = s.replace(" ", "").lower()
    
    # Сравниваем строку с её обратным порядком
    return s == s[::-1]

# Пример использования
string_to_check = "A man a plan a canal Panama"
result = is_palindrome(string_to_check)

if result:
    print(f'Строка "{string_to_check}" является палиндромом.')
else:
    print(f'Строка "{string_to_check}" не является палиндромом.')
```

Этот код удаляет пробелы из строки, приводит её к нижнему регистру и затем сравнивает её с обратным порядком. Если строки равны, то строка является палиндромом. В данном примере вывод будет:

```
Строка "A man a plan a canal Panama" является палиндромом.
```

или

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        # Удаляем пробелы и приводим строку к нижнему регистру
        s = ''.join(char.lower() for char in s if char.isalnum())

        # Сравниваем строку с её обратным порядком
        return s == s[::-1]
```

```java
public class Solution {
    public static void main(String[] args) {
        String str = "radar";
        boolean isPalindrome = isPalindrome(str);
        if (isPalindrome) {
            System.out.println("Строка \"" + str + "\" является палиндромом.");
        } else {
            System.out.println("Строка \"" + str + "\" не является палиндромом.");
        }
    }
    
    public static boolean isPalindrome(String str) {
        int left = 0;
        int right = str.length() - 1;
        while (left < right) {
            if (str.charAt(left) != str.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
}

```
