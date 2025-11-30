---
description: ределить невозможно, выбросите исключение.
---

# Напишите программу, которая принимает имя файла и выводит его расширение. Если расширение у файла оп

```python
def get_file_extension(file_name):
    try:
        # Разделяем имя файла и расширение
        file_parts = file_name.split(".")
        
        # Проверяем, есть ли у файла расширение
        if len(file_parts) > 1:
            # Если есть, возвращаем последнюю часть
            return file_parts[-1]
        else:
            # Если расширение отсутствует, выбрасываем исключение
            raise ValueError("Файл не имеет расширения.")
    except Exception as e:
        # Ловим исключение и выводим сообщение об ошибке
        print(f"Ошибка: {e}")

# Пример использования
file_name = input("Введите имя файла: ")
extension = get_file_extension(file_name)

if extension:
    print(f"Расширение файла: {extension}")
```

```python
def get_file_extension(file_name):
    file_parts = file_name.split(".")
    return file_parts[-1] if len(file_parts) > 1 else ""

# Пример использования
file_name = input("Введите имя файла: ")
extension = get_file_extension(file_name)

if extension:
    print(f"Расширение файла: {extension}")

```

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Введите имя файла: ");
        String fileName = scanner.nextLine();

        try {
            String extension = getFileExtension(fileName);
            System.out.println("Расширение файла: " + extension);
        } catch (IllegalArgumentException e) {
            System.out.println("Невозможно определить расширение файла: " + e.getMessage());
        }
    }

    public static String getFileExtension(String fileName) {
        int dotIndex = fileName.lastIndexOf('.');
        if (dotIndex == -1 || dotIndex == fileName.length() - 1) {
            throw new IllegalArgumentException("Отсутствует или некорректное расширение файла");
        }
        return fileName.substring(dotIndex + 1);
    }
}

```
