# Тип String – строки и текст

В Java тип `String` представляет собой последовательность символов Unicode и используется для хранения строковых данных, таких как текст и символьные данные. `String` является ссылочным типом данных, что означает, что он представляет объект в памяти, а не примитивный тип данных.

1. **Инициализация**: Строки могут быть инициализированы с использованием двойных кавычек (`" "`). Например:

```java
String message = "Hello, world!";
```

2. **Неизменяемость**: Строки в Java являются неизменяемыми, что означает, что после создания строки вы не можете изменить её содержимое. Любая операция, которая кажется изменением строки, фактически создаёт новую строку. Например:

```java
String str = "Hello";
str = str + " World"; // Создается новая строка "Hello World", а старая строка "Hello" остается без изменений
```

3. **Конкатенация**: Конкатенация строк (объединение строк) выполняется с использованием оператора `+`. Например:

```java
String firstName = "John";
String lastName = "Doe";
String fullName = firstName + " " + lastName; // fullName будет равен "John Doe"
```

4. **Методы класса String**: Класс `String` предоставляет множество методов для работы со строками, таких как `length()`, `charAt()`, `substring()`, `toUpperCase()`, `toLowerCase()`, `equals()`, `startsWith()`, `endsWith()` и многие другие. Эти методы позволяют выполнять различные операции со строками, такие как получение длины строки, извлечение подстроки, сравнение строк и т. д.

```java
String str = "Hello, World!";
int length = str.length(); // Получить длину строки
char firstChar = str.charAt(0); // Получить первый символ строки
String substring = str.substring(7); // Получить подстроку начиная с индекса 7
boolean isEqual = str.equals("Hello, World!"); // Сравнить строки
```

5. **Форматирование строк**: Для форматирования строк в Java можно использовать методы `String.format()` или классы `StringBuilder` и `StringBuffer`.

```java
String formattedString = String.format("Имя: %s, Возраст: %d", name, age);
```



1. **length()**: Возвращает длину строки.

```java
String str = "Hello";
int length = str.length(); // length будет равен 5
```

2. **charAt(int index)**: Возвращает символ по указанному индексу строки.

```java
String str = "Java";
char ch = str.charAt(2); // ch будет равен 'v'
```

3. **substring(int beginIndex)**: Возвращает подстроку начиная с указанного индекса до конца строки.

```java
String str = "Hello, world!";
String subStr = str.substring(7); // subStr будет равен "world!"
```

4. **substring(int beginIndex, int endIndex)**: Возвращает подстроку, начиная с указанного индекса и заканчивая индексом переданным вторым параметром.

```java
String str = "Hello, world!";
String subStr = str.substring(7, 12); // subStr будет равен "world"
```

5. **toUpperCase()** и **toLowerCase()**: Преобразует все символы строки в верхний или нижний регистр соответственно.

```java
String str = "Java";
String upperCaseStr = str.toUpperCase(); // upperCaseStr будет равен "JAVA"
String lowerCaseStr = str.toLowerCase(); // lowerCaseStr будет равен "java"
```

6. **equals(Object obj)**: Сравнивает две строки на равенство.

```java
String str1 = "Hello";
String str2 = "Hello";
boolean isEqual = str1.equals(str2); // isEqual будет равен true
```

7. **startsWith(String prefix)** и **endsWith(String suffix)**: Проверяет, начинается ли или заканчивается ли строка соответственно с заданным префиксом или суффиксом.

```java
String str = "Hello, world!";
boolean startsWithHello = str.startsWith("Hello"); // startsWithHello будет равен true
boolean endsWithWorld = str.endsWith("World"); // endsWithWorld будет равен false
```

8. split(String regex): используется для разделения строки на подстроки на основе заданного разделителя и возвращает массив подстрок.

```java
String str = "Hello World Java";
String[] words = str.split("\\s+");
for (String word : words) {
    System.out.println(word);
}

```
