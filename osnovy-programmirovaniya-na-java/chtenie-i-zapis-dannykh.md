# Чтение и запись данных

1. **Чтение данных**:
   * Для чтения данных из различных источников, таких как файлы, сетевые соединения или стандартный ввод (клавиатура), используйте классы `InputStream`, `Reader`, `BufferedReader`, `Scanner` и другие.
   * Вызовите методы чтения соответствующего класса, такие как `read()`, `readLine()`, `nextLine()`, чтобы получить данные из потока.
   * Обработайте данные, как требуется в вашей программе.

Пример чтения данных из файла с использованием `BufferedReader`:

```java
import java.io.*;

public class Main {
    public static void main(String[] args) {
        try {
            BufferedReader reader = new BufferedReader(new FileReader("input.txt"));
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
            reader.close(); // Закрываем поток чтения
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

2. **Запись данных**:
   * Для записи данных в различные места назначения, такие как файлы, сетевые соединения или стандартный вывод (консоль), используйте классы `OutputStream`, `Writer`, `BufferedWriter`, `PrintWriter` и другие.
   * Вызовите методы записи соответствующего класса, такие как `write()`, `println()`, чтобы записать данные в поток.
   * Убедитесь, что вы закрываете поток записи после завершения операции записи.

Пример записи данных в файл с использованием `BufferedWriter`:

```java
import java.io.*;

public class Main {
    public static void main(String[] args) {
        try {
            BufferedWriter writer = new BufferedWriter(new FileWriter("output.txt"));
            writer.write("Hello, World!");
            writer.newLine(); // Добавляем новую строку
            writer.write("This is a new line.");
            writer.close(); // Закрываем поток записи
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

Помните о важности закрытия потоков чтения и записи после их использования, чтобы освободить ресурсы и избежать утечек памяти или блокировок. Используйте блок `try-with-resources`, если ваша программа работает на Java 7 или выше, для автоматического закрытия потоков при выходе из блока.
