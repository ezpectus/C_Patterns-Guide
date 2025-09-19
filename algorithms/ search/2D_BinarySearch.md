# 🔍 Binary Search in 2D Matrix (C version)

## 🇷🇺 Описание задачи  
Дана матрица `m × n`, в которой:
- Каждая строка отсортирована по возрастанию  
- Последний элемент строки ≤ первого элемента следующей строки

Нужно найти элемент `target` с помощью бинарного поиска.

---

## 📐 Входные данные / Input  
- `matrix[m][n]` — отсортированная матрица  
- `target` — целое число, которое нужно найти

## 🎯 Выход / Output  
- `true`, если элемент найден  
- `false`, если отсутствует

---

## 💻 Код на C / C Code

```c
#include <stdio.h>
#include <stdbool.h>

bool searchMatrix(int matrix[][100], int rows, int cols, int target) {
    int left = 0;
    int right = rows * cols - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;
        int row = mid / cols;
        int col = mid % cols;
        int value = matrix[row][col];

        if (value == target)
            return true;
        else if (value < target)
            left = mid + 1;
        else
            right = mid - 1;
    }

    return false;
}

void run_tests() {
    int matrix[3][100] = {
        {1, 3, 5},
        {7, 9, 11},
        {13, 15, 17}
    };

    printf("Test 1: %s\n", searchMatrix(matrix, 3, 3, 9) ? "Found" : "Not found");   // ✅ Found
    printf("Test 2: %s\n", searchMatrix(matrix, 3, 3, 4) ? "Found" : "Not found");   // ❌ Not found
    printf("Test 3: %s\n", searchMatrix(matrix, 3, 3, 1) ? "Found" : "Not found");   // ✅ Found
    printf("Test 4: %s\n", searchMatrix(matrix, 3, 3, 17) ? "Found" : "Not found");  // ✅ Found
    printf("Test 5: %s\n", searchMatrix(matrix, 3, 3, 20) ? "Found" : "Not found");  // ❌ Not found
}

int main() {
    run_tests();
    return 0;
}
```



## 🧠 Отличия от дефолтной версии бинарного поиска

| Характеристика              | Обычный Binary Search (`arr[]`) | Binary Search в 2D матрице (`matrix[][]`) |
|----------------------------|----------------------------------|-------------------------------------------|
| Структура данных           | Одномерный массив               | Двумерная матрица                         |
| Индексация                 | `arr[mid]`                      | `matrix[mid / cols][mid % cols]`          |
| Размер поиска              | `n`                             | `rows × cols`                             |
| Условие отсортированности  | Массив отсортирован             | Матрица отсортирована построчно и глобально |
| Выход                      | Индекс или `-1`                 | `true` / `false`                          |
| Преобразование индекса     | Не требуется                    | Требуется: `row = mid / cols`, `col = mid % cols` |

---

## 🧱 Архитектурные сигналы

✅ Модуль `searchMatrix()` — чистая логика, без I/O  
✅ `run_tests()` — изолированные тесты, легко расширять  
✅ `main()` — точка входа, запускает тесты  
✅ Используется безопасный mid: `left + (right - left) / 2`  
✅ Преобразование индекса — минимальное, без лишних структур

---

## 📦 Повторное использование

Модуль можно адаптировать для:

- Поиска в C++, Java, C#
- Поиска в матрицах с другими условиями сортировки
- Расширения на lower/upper bound
- Интервального поиска в 2D

---

## 🧘 Заключение

Бинарный поиск в матрице — это расширение классического паттерна, где ты работаешь с двумерной структурой как с линейной.  
Этот модуль — основа для задач LeetCode, олимпиад и инженерных репозиториев.



---
