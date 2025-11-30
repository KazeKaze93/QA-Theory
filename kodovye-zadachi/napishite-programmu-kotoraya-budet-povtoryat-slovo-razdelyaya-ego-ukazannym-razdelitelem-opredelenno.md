---
description: количество раз.
---

# Напишите программу, которая будет повторять слово, разделяя его указанным разделителем, определенное

```python
def repeat_word(word, separator, count):
    # Повторяем слово count раз и объединяем с разделителем
    return separator.join([word] * count)

# Входные параметры
word = "Тест"
separator = "И"
count = 3

# Вызов функции и вывод результата
output = repeat_word(word, separator, count)
print(output)  # Выведет: ТестИТестИТест

```

```java
public class WordRepeater {
    public static void main(String[] args) {
        String word = "hello"; // Слово для повторения
        String delimiter = ", "; // Разделитель
        int repeatCount = 5; // Количество повторений
        repeatWord(word, delimiter, repeatCount);
    }

    public static void repeatWord(String word, String delimiter, int repeatCount) {
        StringBuilder result = new StringBuilder(word);
        for (int i = 1; i < repeatCount; i++) {
            result.append(delimiter).append(word);
        }
        System.out.println(result);
    }
}

```
