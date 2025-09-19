## 🔍 Название алгоритма

- In-Place Selection Sort for 2D Matrix (🇺🇦 Сортування безпосереднім вибором у двовимірному масиві)

## 🧠 Архитектурная логика 

**Модель хранения**  
Матрица `A[m][n]` интерпретируется как линейный массив длины `m × n`, что позволяет применять классические одномерные алгоритмы сортировки без преобразования структуры.

**Алгоритм сортировки**  
Используется метод **прямого выбора (selection sort)** — на каждой итерации выбирается минимальный элемент из неотсортированной части и меняется местами с текущим.

**Индексация**  
Для доступа к элементу по линейному индексу `i` используется преобразование:  


\[
\text{row} = i / n,\quad \text{col} = i \% n
\]

  
Это позволяет работать с матрицей как с одномерным массивом, сохраняя структуру и не выделяя дополнительную память.
  ---
```c

#include <stdio.h>

#define ROWS 3
#define COLS 4

void sortMatrix(int matrix[ROWS][COLS]) {
    int total = ROWS * COLS;

    for (int i = 0; i < total - 1; i++) {
        int minIndex = i;
        int minRow = minIndex / COLS;
        int minCol = minIndex % COLS;

        for (int j = i + 1; j < total; j++) {
            int row = j / COLS;
            int col = j % COLS;

            if (matrix[row][col] < matrix[minRow][minCol]) {
                minIndex = j;
                minRow = row;
                minCol = col;
            }
        }

        // Swap current i-th element with minIndex element
        int iRow = i / COLS;
        int iCol = i % COLS;

        int temp = matrix[iRow][iCol];
        matrix[iRow][iCol] = matrix[minRow][minCol];
        matrix[minRow][minCol] = temp;
    }
}

void printMatrix(int matrix[ROWS][COLS]) {
    for (int i = 0; i < ROWS; i++) {
        for (int j = 0; j < COLS; j++) {
            printf("%d\t", matrix[i][j]);
        }
        printf("\n");
    }
}

int main() {
    int matrix[ROWS][COLS] = {
        {12, 5, 9, 1},
        {8, 3, 7, 4},
        {11, 6, 2, 10}
    };

    printf("Before sorting:\n");
    printMatrix(matrix);

    sortMatrix(matrix);

    printf("\nAfter sorting:\n");
    printMatrix(matrix);

    return 0;
}
```
---


**In-place**  
Все операции происходят **внутри исходной матрицы**, без создания временных копий или буферов. Используются только переменные `i`, `j`, `minIndex`, и временная переменная `temp` для обмена.

**Сложность**
- Время: `O((m × n)^2)` — как у обычного selection sort  
- Память: `O(1)` — только счётчики и временные переменные

**Поведение на частичных массивах**  
Алгоритм можно адаптировать для сортировки **только части матрицы** — например, одной строки, одного столбца или подматрицы, если задать границы `start` и `end` в линейной форме.

**Применимость**  
Подходит для лабораторных работ, где требуется:
- Реализация базовых алгоритмов без библиотек  
- Демонстрация понимания индексации и работы с памятью  
- Сортировка без использования `malloc`, `new`, `vector`, `List` и других структур



---
