# Параметризированные типы в Java – Generics

Параметризированные типы, или обобщения (Generics) в Java, представляют собой механизм, который позволяет создавать классы, интерфейсы и методы, которые могут работать с различными типами данных, обеспечивая при этом типовую безопасность во время компиляции. Это означает, что вы можете создать обобщенный класс или метод, который будет принимать или возвращать значения определенного типа, но без указания конкретного типа данных.&#x20;

```java
public class Box<T> {
    private T value;

    public void setValue(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }

    public static void main(String[] args) {
        Box<Integer> integerBox = new Box<>();
        integerBox.setValue(10);
        System.out.println("Значение integerBox: " + integerBox.getValue());

        Box<String> stringBox = new Box<>();
        stringBox.setValue("Привет, мир!");
        System.out.println("Значение stringBox: " + stringBox.getValue());
    }
}
```

В этом примере `Box` - это обобщенный класс с параметром типа `T`. При создании экземпляра `Box` мы указываем тип данных в угловых скобках (например, `Box<Integer>` или `Box<String>`). После этого мы можем использовать этот класс с конкретным типом данных, который мы определили.
