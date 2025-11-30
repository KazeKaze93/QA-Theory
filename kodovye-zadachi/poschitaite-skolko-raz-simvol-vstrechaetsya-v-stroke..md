# Посчитайте, сколько раз символ встречается в строке.

```python
def count_occurrences(input_string, target_char):
    # Используем метод count() для подсчета вхождений символа
    occurrences = input_string.count(target_char)
    return occurrences

# Пример использования
input_str = input("Введите строку: ")
char_to_count = input("Введите символ для подсчета: ")

result = count_occurrences(input_str, char_to_count)
print(f"Символ '{char_to_count}' встречается в строке {result} раз(а).")
```

```java
public class Main {
    public static void main(String[] args) {
        String str = "hello world";
        char ch = 'o';
        int count = countOccurrences(str, ch);
        System.out.println("Символ '" + ch + "' встречается в строке '" + str + "' " + count + " раз(а).");
    }

    public static int countOccurrences(String str, char ch) {
        int count = 0;
        for (int i = 0; i < str.length(); i++) {
            if (str.charAt(i) == ch) {
                count++;
            }
        }
        return count;
    }
}

```
