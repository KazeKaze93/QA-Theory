# Как выполнять тесты параллельно TestNG/JUnit?

#### Параллельное выполнение тестов в TestNG:

TestNG предоставляет встроенную поддержку для параллельного выполнения тестов. Вот несколько способов настроить параллельное выполнение:

1.  **Аннотация `@Test` с параметром `parallel`:**

    ```java
    @Test(threadPoolSize = 3, invocationCount = 10,  timeOut = 10000)
    public void testMethod() {
        // Тело тестового метода
    }
    ```

    Это означает, что метод будет запущен в 3 потоках с общим количеством выполнений 10.
2.  **XML-конфигурация:**

    Создайте XML-файл для конфигурации, указывающий, какие классы или методы должны выполняться параллельно. Пример:

    ```xml
    <!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
    <suite name="Suite1" parallel="classes" thread-count="5">
      <test name="Test1">
        <classes>
          <class name="com.example.TestClass1"/>
          <class name="com.example.TestClass2"/>
        </classes>
      </test>
    </suite>
    ```

    Затем запустите тесты с использованием созданного XML-файла.

#### Параллельное выполнение тестов в JUnit:

JUnit не предоставляет встроенных аннотаций для параллельного выполнения, но можно использовать внешние инструменты или библиотеки. Например, вы можете использовать библиотеку [JUnit 5 Parallel Test Execution](https://github.com/junit-team/junit5/pull/2607) для JUnit 5.

Пример использования библиотеки для JUnit 5:

```java
@Execution(ExecutionMode.CONCURRENT)
public class MyParallelTest {
    @Test
    public void test1() {
        // Тело тестового метода
    }

    @Test
    public void test2() {
        // Тело тестового метода
    }
}
```
