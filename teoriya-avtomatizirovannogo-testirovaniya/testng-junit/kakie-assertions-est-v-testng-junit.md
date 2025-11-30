# Какие assertions есть в TestNG/JUnit?

#### Проверки в TestNG:

1.  **`assertEquals`**:

    ```java
    Assert.assertEquals(фактическое, ожидаемое);
    ```
2.  **`assertNotEquals`**:

    ```java
    Assert.assertNotEquals(фактическое, ожидаемое);
    ```
3.  **`assertTrue`**:

    ```java
    Assert.assertTrue(условие);
    ```
4.  **`assertFalse`**:

    ```java
    Assert.assertFalse(условие);
    ```
5.  **`assertNull`**:

    ```java
    Assert.assertNull(объект);
    ```
6.  **`assertNotNull`**:

    ```java
    Assert.assertNotNull(объект);
    ```
7.  **`assertSame`** (проверяет, указывают ли две ссылки на один и тот же объект):

    ```java
    Assert.assertSame(фактическое, ожидаемое);
    ```
8.  **`assertNotSame`** (проверяет, указывают ли две ссылки на разные объекты):

    ```java
    Assert.assertNotSame(фактическое, ожидаемое);
    ```
9.  **`fail`** (помечает тест как неудачный):

    ```java
    Assert.fail("Тест провален намеренно");
    ```
10. **`assertThrows`** (доступно в TestNG 7 и выше, проверяет, вызывается ли исключение):

    ```java
    Assert.assertThrows(Exception.class, () -> {
        // Код, который должен вызывать исключение
    });
    ```

#### Проверки в JUnit:

1.  **`assertEquals`**:

    ```java
    assertEquals(ожидаемое, фактическое);
    ```
2.  **`assertNotEquals`**:

    ```java
    assertNotEquals(ожидаемое, фактическое);
    ```
3.  **`assertTrue`**:

    ```java
    assertTrue(условие);
    ```
4.  **`assertFalse`**:

    ```java
    assertFalse(условие);
    ```
5.  **`assertNull`**:

    ```java
    assertNull(объект);
    ```
6.  **`assertNotNull`**:

    ```java
    assertNotNull(объект);
    ```
7.  **`assertSame`** (проверяет, указывают ли две ссылки на один и тот же объект):

    ```java
    assertSame(ожидаемое, фактическое);
    ```
8.  **`assertNotSame`** (проверяет, указывают ли две ссылки на разные объекты):

    ```java
    assertNotSame(ожидаемое, фактическое);
    ```
9.  **`fail`** (помечает тест как неудачный):

    ```java
    fail("Тест провален намеренно");
    ```
10. **`assertThrows`** (JUnit 5, проверяет, вызывается ли исключение):

    ```java
    assertThrows(Exception.class, () -> {
        // Код, который должен вызывать исключение
    });
    ```
