---
description: е длинное.
---

# Напишите программу, которая принимает текст и выводит два слова: наиболее часто встречающееся и само

```python
from collections import Counter

def analyze_text(text):
    # Разбиваем текст на слова
    words = text.split()

    # Находим наиболее часто встречающееся слово
    most_common_word = Counter(words).most_common(1)[0][0]

    # Находим самое длинное слово
    longest_word = max(words, key=len)

    return most_common_word, longest_word

# Пример использования
input_text = input("Введите текст: ")

most_common, longest = analyze_text(input_text)
print(f"Наиболее часто встречающееся слово: {most_common}")
print(f"Самое длинное слово: {longest}")
```

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        String text = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis ut magna eget velit viverra venenatis.";

        // Разбиваем текст на слова и подсчитываем количество вхождений каждого слова
        Map<String, Integer> wordCounts = new HashMap<>();
        String[] words = text.split("\\s+");
        for (String word : words) {
            wordCounts.put(word, wordCounts.getOrDefault(word, 0) + 1);
        }

        // Находим наиболее часто встречающееся слово
        String mostFrequentWord = Collections.max(wordCounts.entrySet(), Map.Entry.comparingByValue()).getKey();

        // Находим самое длинное слово
        String longestWord = Arrays.stream(words)
                                    .max(Comparator.comparing(String::length))
                                    .orElse("");

        System.out.println("Наиболее часто встречающееся слово: " + mostFrequentWord);
        System.out.println("Самое длинное слово: " + longestWord);
    }
}

```
