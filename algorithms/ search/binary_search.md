# 🔍 Binary Search / Бинарный поиск

## 🇷🇺 Описание задачи

Дан отсортированный массив целых чисел `arr[]` и целевое значение `target`.  
Нужно найти индекс элемента, равного `target`, используя **бинарный поиск**.  
Если элемент не найден — вернуть `-1`.

---

## 🇬🇧 Problem Statement

Given a sorted array of integers `arr[]` and a target value `target`,  
implement **binary search** to return the index of the target.  
If not found, return `-1`.

---

## 📐 Входные данные / Input

- `arr[]` — отсортированный массив длины `n`
- `target` — целое число, которое нужно найти

---

## 🎯 Выход / Output

- Индекс элемента `target` в массиве `arr[]`, если найден
- `-1`, если `target` отсутствует

---

## 🧠 Алгоритм / Algorithm

Бинарный поиск работает за `O(log n)`:

1. Инициализируем `left = 0`, `right = n - 1`
2. Пока `left <= right`:
   - Вычисляем `mid = (left + right) / 2`
   - Если `arr[mid] == target` → возвращаем `mid`
   - Если `arr[mid] < target` → ищем справа: `left = mid + 1`
   - Иначе → ищем слева: `right = mid - 1`
3. Если не нашли — возвращаем `-1`

---

## 🧪 Тестовые данные / Test Cases

```txt
Input: arr = [1, 3, 5, 7, 9], target = 5
Output: 2

Input: arr = [2, 4, 6, 8, 10], target = 7
Output: -1

Input: arr = [0, 1, 2, 3, 4, 5], target = 0
Output: 0

Input: arr = [10, 20, 30, 40, 50], target = 50
Output: 4
```

## 💻 Код на C / C Code
```c
#include <stdio.h>

int binary_search(int *arr, int n, int target) {
    int left = 0, right = n - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target)
            return mid;
        else if (arr[mid] < target)
            left = mid + 1;
        else
            right = mid - 1;
    }
    return -1;
}

void run_tests() {
    int a1[] = {1, 3, 5, 7, 9};
    int a2[] = {2, 4, 6, 8, 10};
    int a3[] = {0, 1, 2, 3, 4, 5};
    int a4[] = {10, 20, 30, 40, 50};

    printf("Test 1: %d\n", binary_search(a1, 5, 5));   // Output: 2
    printf("Test 2: %d\n", binary_search(a2, 5, 7));   // Output: -1
    printf("Test 3: %d\n", binary_search(a3, 6, 0));   // Output: 0
    printf("Test 4: %d\n", binary_search(a4, 5, 50));  // Output: 4
}

int main() {
    run_tests();
    return 0;
}
```

# Skeleton of Binary Search on C
```c
// 🔧 Базовая реализация бинарного поиска в отсортированном массиве
int binary_search(int *arr, int size, int target) {
    int left = 0;               // Левая граница поиска
    int right = size - 1;       // Правая граница поиска

    while (left <= right) {
        int mid = left + (right - left) / 2; // Центр, безопасный от переполнения

        if (arr[mid] == target)
            return mid;         // Найден элемент — возвращаем индекс

        if (arr[mid] < target)
            left = mid + 1;     // Ищем справа от mid
        else
            right = mid - 1;    // Ищем слева от mid
    }

    return -1; // Элемент не найден
}
```


## 🧱 Архитектурные сигналы

- ✅ Модуль binary_search() — чистая логика, без I/O
- ✅ run_tests() — изолированные тесты, легко расширять
- ✅ main() — точка входа, запускает тесты
- ✅ Используется mid = left + (right - left) / 2 — безопасно от переполнения

## 📦 Повторное использование

Этот шаблон можно адаптировать для:

- Поиска в строках, вещественных числах, структурах
- Модифицированного бинарного поиска (первое/последнее вхождение)
- Интервального поиска, lower/upper bound

## 🧩 Расширения
- 🔄 Рекурсивная реализация

- 📈 Поиск в неотсортированном массиве (через сортировку)

- 🧮 Поиск ближайшего элемента, если target не найден

## 🧘 Заключение
- Бинарный поиск — фундаментальный алгоритм, который должен быть в каждом инженерном репозитории. 
- Этот модуль — основа для более сложных паттернов: поиск в матрицах, деревьях, функциях, и даже в архитектурных сигналах.

