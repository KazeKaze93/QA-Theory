# Логические операции

Логические операции в Java позволяют комбинировать и проверять логические выражения.&#x20;

1. **Логическое И (&&)**:
   * Оператор `&&` возвращает `true`, если оба операнда равны `true`, и `false` в противном случае.
   * Если первый операнд в выражении `&&` равен `false`, второй операнд не вычисляется (происходит короткое замыкание).

Пример:

```java
boolean isSunny = true;
boolean isWarm = true;

if (isSunny && isWarm) {
    System.out.println("It's sunny and warm today!");
}
```

2. **Логическое ИЛИ (||)**:
   * Оператор `||` возвращает `true`, если хотя бы один из операндов равен `true`, и `false` в противном случае.
   * Если первый операнд в выражении `||` равен `true`, второй операнд не вычисляется (происходит короткое замыкание).

Пример:

```java
boolean isSunny = true;
boolean isRaining = false;

if (isSunny || isRaining) {
    System.out.println("It's either sunny or raining today!");
}
```

3. **Логическое отрицание (!)**:
   * Оператор `!` (логическое отрицание) инвертирует значение своего операнда. Если операнд равен `true`, `!` вернет `false`, и наоборот.

Пример:

```java
boolean isSunny = true;

if (!isSunny) {
    System.out.println("It's not sunny today!");
}
```
