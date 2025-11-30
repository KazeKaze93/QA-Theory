# Нужно вернуть список, который состоит из элементов, общих для этих двух списков.

`a = [1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]`;

`b = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13]`.



```python
def common_elements(list1, list2):
    return list(set(list1) & set(list2))

# пример
a = [1, 2, 3, 4, 5]
b = [3, 4, 5, 6, 7]

print(common_elements(a, b))  # [3, 4, 5]

```

```python
a = [1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
b = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13]


common_elements = [element for element in a if element in b]

print(list(set(common_elements)))
```
