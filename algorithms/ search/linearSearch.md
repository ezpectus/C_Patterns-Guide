# 🔍 Linear Search / Линейный поиск
```🇷🇺 Описание задачи
Дан массив целых чисел arr[] и целевое значение target.
Нужно найти индекс элемента, равного target, используя линейный поиск. Если элемент не найден — вернуть -1.

🇬🇧 Problem Statement
Given an array of integers arr[] and a target value target,
implement linear search to return the index of the target. If not found, return -1.
```

## 📐 Входные данные / Input

- arr[] — массив длины n (не обязательно отсортированный)
- target — целое число, которое нужно найти

## 🎯 Выход / Output
- Индекс элемента target в массиве arr[], если найден

- -1, если target отсутствует

## 🧠 Алгоритм / Algorithm

- Линейный поиск работает за O(n):
- Проходим по всем элементам массива:
- Если arr[i] == target → возвращаем i
- Если не нашли — возвращаем -1

## 🧪 Тестовые данные / Test Cases
```txt
Input: arr = [4, 2, 7, 1, 9], target = 7
Output: 2

Input: arr = [5, 3, 8, 6], target = 10
Output: -1

Input: arr = [0, 0, 0, 0], target = 0
Output: 0

Input: arr = [1, 2, 3, 4, 5], target = 5
Output: 4
```

## 💻 Код на C / C Code
```c
#include <stdio.h>

int linear_search(int *arr, int n, int target) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == target)
            return i;
    }
    return -1;
}

void run_tests() {
    int a1[] = {4, 2, 7, 1, 9};
    int a2[] = {5, 3, 8, 6};
    int a3[] = {0, 0, 0, 0};
    int a4[] = {1, 2, 3, 4, 5};

    printf("Test 1: %d\n", linear_search(a1, 5, 7));   // Output: 2
    printf("Test 2: %d\n", linear_search(a2, 4, 10));  // Output: -1
    printf("Test 3: %d\n", linear_search(a3, 4, 0));   // Output: 0
    printf("Test 4: %d\n", linear_search(a4, 5, 5));   // Output: 4
}

int main() {
    run_tests();
    return 0;
}
```

## Skeleton of Linear Search on C
```c
// 🔧 Базовая реализация линейного поиска
int linear_search(int *arr, int size, int target) {
    for (int i = 0; i < size; i++) {
        if (arr[i] == target)
            return i; // Найден элемент — возвращаем индекс
    }
    return -1; // Элемент не найден
}
```
## 🧱 Архитектурные сигналы

- ✅ Модуль linear_search() — минималистичная логика, без побочных эффектов
- ✅ Подходит для неотсортированных массивов
- ✅ run_tests() — легко масштабировать на edge cases
- ✅ main() — точка входа, запускает тесты

## 📦 Повторное использование

Этот шаблон можно адаптировать для:

- Поиска по строкам, структурам, условиям
- Поиска первого/последнего вхождения
- Фильтрации по предикату (например, arr[i] > 10)

## 🧩 Расширения
- 🔄 Поиск всех индексов target (массив результатов)

- 🧮 Подсчёт количества вхождений

- 🧠 Поиск по сложному условию (например, target % arr[i] == 0)

## 🧘 Заключение
Линейный поиск — простейший, но универсальный алгоритм.
Он должен быть в инженерном репозитории как базовый строительный блок.
Особенно полезен в ситуациях, где массив не отсортирован или содержит сложные структуры.




---
