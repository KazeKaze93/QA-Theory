# Класс StringBuilder

Класс `StringBuilder` в Java представляет собой изменяемую последовательность символов, которая используется для создания и изменения строк. Он отличается от класса `String`, который является неизменяемым, что означает, что каждая операция над строкой создает новый объект, в то время как `StringBuilder` позволяет изменять строку без создания нового объекта каждый раз.

1. **Создание объекта StringBuilder**: Вы можете создать объект `StringBuilder` с помощью конструктора или метода `append()`.

```java
StringBuilder sb = new StringBuilder(); // Создание пустого объекта StringBuilder
StringBuilder sb = new StringBuilder("Hello"); // Создание объекта StringBuilder с начальным содержимым "Hello"
```

2. **Методы для добавления содержимого**: Методы `append()` используются для добавления содержимого к объекту `StringBuilder`.

```java
StringBuilder sb = new StringBuilder();
sb.append("Hello"); // Добавление строки "Hello"
sb.append(" ").append("world"); // Добавление строки " world"
```

3. **Методы для вставки содержимого**: Методы `insert()` используются для вставки содержимого в определенное место в объекте `StringBuilder`.

```java
StringBuilder sb = new StringBuilder("world");
sb.insert(0, "Hello, "); // Вставка строки "Hello, " в начало
```

4. **Методы для удаления содержимого**: Методы `delete()` и `deleteCharAt()` используются для удаления содержимого из объекта `StringBuilder`.

```java
StringBuilder sb = new StringBuilder("Hello, world");
sb.delete(5, 13); // Удаление подстроки с позиции 5 до 13 (не включительно)
sb.deleteCharAt(0); // Удаление символа на позиции 0
```

5. **Методы для изменения содержимого**: Методы `replace()` и `setCharAt()` используются для замены или изменения символов в объекте `StringBuilder`.

```java
StringBuilder sb = new StringBuilder("Hello, world");
sb.replace(0, 5, "Hi"); // Замена подстроки с позиции 0 до 5 (не включительно) на "Hi"
sb.setCharAt(7, 'W'); // Изменение символа на позиции 7 на 'W'
```

6. **Методы для получения содержимого**: Методы `toString()` и `charAt()` используются для получения содержимого или символа из объекта `StringBuilder`.

```java
StringBuilder sb = new StringBuilder("Hello, world");
String str = sb.toString(); // Получение содержимого как строки
char ch = sb.charAt(7); // Получение символа на позиции 7
```
