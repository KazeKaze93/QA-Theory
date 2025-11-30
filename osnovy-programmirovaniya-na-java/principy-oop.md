# Принципы ООП

1.  **Наследование**:

    Наследование позволяет создавать новые классы на основе уже существующих классов. Подкласс (или производный класс) наследует свойства и методы родительского класса. Это позволяет повторно использовать код и создавать иерархии классов.



    ```java
    // Родительский класс
    class Animal {
        void eat() {
            System.out.println("Животное ест");
        }
    }

    // Подкласс, наследующий родительский класс
    class Dog extends Animal {
        void bark() {
            System.out.println("Собака лает");
        }
    }

    public class Main {
        public static void main(String[] args) {
            Dog dog = new Dog();
            dog.eat(); // Метод eat() унаследован от класса Animal
            dog.bark(); // Метод bark() из класса Dog
        }
    }
    ```
2.  **Инкапсуляция**:

    Инкапсуляция означает скрытие деталей реализации объекта от внешнего мира и предоставление доступа к ним только через публичные методы. Это позволяет обеспечить безопасность и контроль над данными.



    ```java
    class Person {
        private String name;

        // Методы доступа к полю name (геттер и сеттер)
        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }
    }

    public class Main {
        public static void main(String[] args) {
            Person person = new Person();
            person.setName("John");
            System.out.println("Имя: " + person.getName());
        }
    }
    ```
3.  **Полиморфизм**:

    Полиморфизм позволяет объектам одного типа обрабатываться как объекты другого типа. Это достигается через наследование и переопределение методов в подклассах.



    ```java
    // Родительский класс
    class Animal {
        void makeSound() {
            System.out.println("Животное издает звук");
        }
    }

    // Подкласс, переопределяющий метод родительского класса
    class Dog extends Animal {
        void makeSound() {
            System.out.println("Собака лает");
        }
    }

    public class Main {
        public static void main(String[] args) {
            Animal animal = new Dog(); // Полиморфизм
            animal.makeSound(); // Вывод: "Собака лает"
        }
    }
    ```
4.  **Абстракция**:

    Абстракция позволяет скрывать детали реализации и предоставлять простой интерфейс для взаимодействия с объектами. Это достигается через абстрактные классы и интерфейсы.



    ```java
    // Абстрактный класс
    abstract class Shape {
        abstract void draw(); // Абстрактный метод
    }

    // Подкласс, реализующий абстрактный метод
    class Circle extends Shape {
        void draw() {
            System.out.println("Рисуем круг");
        }
    }

    public class Main {
        public static void main(String[] args) {
            Shape shape = new Circle(); // Используем абстракцию
            shape.draw(); // Вывод: "Рисуем круг"
        }
    }
    ```
