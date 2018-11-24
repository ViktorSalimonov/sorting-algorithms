# Алгоритмы сортировки на Python

## Сортировка вставками (Insertion Sort)
Основаня идея — рассматривать последовательность как две части: первая включает отсортированные элменты, вторая — неотсортированные. Алгоритм сортировки вставками последовательно помещает каждый элемент из неотсортированной части на правильную позицию отсортированной части.

```python
def insertion_sort(arr):
    n = len(arr)
    for i in range(1, n):
        current_value = arr[i]
        j = i - 1
        while j >= 0:
            if current_value < arr[j]:
                arr[j+1] = arr[j]
                arr[j] = current_value
                j = j - 1
            else:
                break
    return arr
```

Оценка сложности:
- В худшем случае **O(N²)**
- В среднем случае **O(N²)**
- В лучшем случае **O(N²)**

## Быстрая сортировка  (Quick Sort)
Рекурсивный алгоритм, который работает по следующему принципу:
1. Выбрать опорный элемент из массива. Это можно сделать разными способами, в данной реализации этой будет случайный элемент.
2. Сравнить все элементы с опорным и распределить их в подмассивы. Первый подмассив будет состоять из элементов, которые меньше опорного; второй — больше опорного или равные.
3. Рекурсивно выполнить шаги 1 и 2, пока в подмассиве есть хотя бы 2 элемента.

```python
import random

def quick_sort(arr):
    n = len(arr)
    if n <= 1:
        return arr
    else:
        pivot = random.choice(arr)
        less = [x for x in arr if x < pivot]
        greater_or_equal = [x for x in arr if x >= pivot]
        return quick_sort(less) + quick_sort(greater_or_equal)
```

Оценка сложности:
- В худшем случае **O(n²)**
- В среднем случае **O(n * log n)**
- В лучшем случае **O(n * log n)**

## Сортировка слиянием (Merge Sort)
Рекурсивный алгоритм, который работает по следующему принципу:
1. Разделить массив на две равные части
2. Отсортировать каждую половину
3. Из двух отсортированных массивов получить один (операция слияния)

```python
def merge_sort(arr):
    n = len(arr)
    if n <= 1:
        return arr
    else:
        middle = int(len(arr) / 2)
        left = merge_sort(arr[:middle])
        right = merge_sort(arr[middle:])
        return merge(left, right)

def merge(left, right):
    result = []
    while len(left) > 0 and len(right) > 0:
        if left[0] <= right[0]:
            result.append(left[0])
            left = left[1:]
        else:
            result.append(right[0])
            right = right[1:]
    if len(left) > 0:
        result += left
    if len(right) > 0:
        result += right
    return result
```

Оценка сложности:
- В худшем случае **O(n * log n)**
- В среднем случае **O(n * log n)**
- В лучшем случае **O(n * log n)**
