# Как Пропустить Тестовый Метод в TestNG?

В TestNG для пропуска тестового метода можно использовать аннотацию `@Test` с параметром `enabled`. Если значение параметра `enabled` установлено в `false`, то тестовый метод будет пропущен при выполнении тестового сценария.

Пример:

```java
import org.testng.annotations.Test;

public class MyTest {

    @Test(enabled = false)
    public void skippedTestMethod() {
        // Этот метод будет пропущен при выполнении тестового сценария
        System.out.println("Этот метод будет пропущен");
    }

    @Test
    public void activeTestMethod() {
        // Этот метод будет выполнен при выполнении тестового сценария
        System.out.println("Этот метод будет выполнен");
    }
}
```

В приведенном примере метод `skippedTestMethod` будет пропущен, так как у него установлен параметр `enabled = false`. Метод `activeTestMethod` будет выполнен, так как параметр `enabled` не указан (по умолчанию считается `true`).
