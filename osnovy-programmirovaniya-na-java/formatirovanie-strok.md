# Форматирование строк

В Java для форматирования строк можно использовать несколько методов и классов. Одним из наиболее часто используемых методов является метод `String.format()`, а также классы `Formatter` и `StringBuilder`.&#x20;

1. **Метод `String.format()`**: Этот метод создает отформатированную строку с использованием указанного формата и аргументов.

```java
String name = "John";
int age = 30;
String formattedString = String.format("Имя: %s, Возраст: %d", name, age);
System.out.println(formattedString); // Вывод: Имя: John, Возраст: 30
```

2. **Класс `Formatter`**: Этот класс представляет собой форматированный вывод и позволяет форматировать строки с использованием спецификаторов формата.

```java
import java.util.Formatter;

Formatter formatter = new Formatter();
formatter.format("Имя: %s, Возраст: %d", name, age);
String formattedString = formatter.toString();
formatter.close();
System.out.println(formattedString); // Вывод: Имя: John, Возраст: 30
```

3. **Класс `StringBuilder`**: `StringBuilder` позволяет создавать и изменять строки, и его метод `append()` может использоваться для форматирования строк.

```java
StringBuilder sb = new StringBuilder();
sb.append("Имя: ").append(name).append(", Возраст: ").append(age);
String formattedString = sb.toString();
System.out.println(formattedString); // Вывод: Имя: John, Возраст: 30
```

4. **Форматирование с использованием спецификаторов**: Вы можете использовать спецификаторы формата для определения формата вывода, таких как `%s` для строк, `%d` для целых чисел и `%f` для чисел с плавающей точкой.

```java
String name = "John";
int age = 30;
double salary = 1000.50;
String formattedString = String.format("Имя: %s, Возраст: %d, Зарплата: %.2f", name, age, salary);
System.out.println(formattedString); // Вывод: Имя: John, Возраст: 30, Зарплата: 1000.50
```

