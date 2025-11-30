# Коллекторы

Коллекторы (Collectors) в Java Stream API предоставляют удобный способ собирать элементы потока в различные коллекции или другие структуры данных. Они позволяют выполнить конечную операцию на потоке данных, собрав результаты в желаемый контейнер или агрегируя данные в другом формате.

1.  **toList**: Собирает элементы потока в список.

    ```java
    List<T> list = stream.collect(Collectors.toList());
    ```
2.  **toSet**: Собирает элементы потока в множество.

    ```java
    Set<T> set = stream.collect(Collectors.toSet());
    ```
3.  **toMap**: Собирает элементы потока в карту, используя ключи и значения, вычисленные из элементов потока.

    ```java
    Map<K, V> map = stream.collect(Collectors.toMap(keyMapper, valueMapper));
    ```
4.  **joining**: Собирает элементы потока в одну строку, объединяя их с разделителем.

    ```java
    String result = stream.collect(Collectors.joining(delimiter));
    ```
5.  **groupingBy**: Группирует элементы потока по заданному критерию.

    ```java
    Map<K, List<T>> groups = stream.collect(Collectors.groupingBy(classifier));
    ```
6.  **partitioningBy**: Разделяет элементы потока на две группы на основе заданного предиката.

    ```java
    Map<Boolean, List<T>> partitions = stream.collect(Collectors.partitioningBy(predicate));
    ```
7.  **counting**: Подсчитывает количество элементов в потоке.

    ```java
    long count = stream.collect(Collectors.counting());
    ```
8.  **summarizingInt/Long/Double**: Предоставляет сводную статистику для числовых элементов потока (сумма, среднее значение, максимальное, минимальное значение и количество элементов).

    ```java
    IntSummaryStatistics stats = stream.collect(Collectors.summarizingInt());
    ```
9.  **reducing**: Применяет функцию сведения (reduction) ко всем элементам потока.

    ```java
    Optional<T> result = stream.collect(Collectors.reducing(reductionFunction));
    ```
10. **mapping**: Применяет функцию к элементам потока и собирает результаты в коллекцию.

    ```java
    List<U> result = stream.collect(Collectors.mapping(mapper, downstreamCollector));
    ```
