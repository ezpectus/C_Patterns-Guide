# 1.4 Algorithms for transforming one-dimensional arrays
## 📘 Призначення лабораторної роботи
Лабораторна №1.4 — «Алгоритми перетворення одновимірних масивів (векторів)». Мета: відсортувати масив за зростанням модулів, виконати перетворення масиву, 
згенерувати новий масив у зворотному порядку, і сформувати новий масив з позитивними елементами спочатку.

## 🧠 Пояснення задач
Вхід: натуральне число n, масив цілих чисел A[1..4n] у межах [-50, 50].

Завдання:

Відсортувати A за зростанням модулів:
```
∣𝑎1∣≤∣𝑎2∣≤⋯≤∣𝑎𝑛∣
```
#### Перетворити масив A у новий масив B згідно з варіантом 16:

- Ч1 (1..n) → прямий порядок
- Ч2 (n+1..2n) ← зворотний порядок
- Ч3 (2n+1..3n) ← зворотний порядок
- Ч4 (3n+1..4n) ← зворотний порядок

- Створити новий масив B, що є реверсом A.
- Створити новий масив B: спочатку всі додатні елементи A, потім усі інші.

  
## 💻 Програма 1: з проміжним масивом B (чисто, швидко)
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

static int cmp_abs_asc(const void *pa, const void *pb) {
    int a = *(const int*)pa, b = *(const int*)pb;
    int aa = (a < 0 ? -a : a), bb = (b < 0 ? -b : b);
    if (aa != bb) return aa - bb;
    return a - b;
}

// 1) Сортування за модулем
void sort_by_abs_with_temp(const int *A, int *B, int n) {
    memcpy(B, A, n * sizeof(int));
    qsort(B, n, sizeof(int), cmp_abs_asc);
}

// 2) Перетворення за схемою варіанта 16
void transform_variant16(const int *A, int *B, int n) {
    int k = 0;
    for (int i = 0; i < n; i++) B[k++] = A[i];             // Ч1 →
    for (int i = 2*n - 1; i >= n; i--) B[k++] = A[i];      // Ч2 ←
    for (int i = 3*n - 1; i >= 2*n; i--) B[k++] = A[i];    // Ч3 ←
    for (int i = 4*n - 1; i >= 3*n; i--) B[k++] = A[i];    // Ч4 ←
}

// 3) Реверс
void reverse_into_new(const int *A, int *B, int n) {
    for (int i = 0; i < n; i++) B[i] = A[n - 1 - i];
}

// 4) Позитивні спочатку
void positives_then_others(const int *A, int *B, int n) {
    int k = 0;
    for (int i = 0; i < n; i++) if (A[i] > 0) B[k++] = A[i];
    for (int i = 0; i < n; i++) if (A[i] <= 0) B[k++] = A[i];
}

static void print_array(const char *label, const int *X, int n) {
    printf("%s: ", label);
    for (int i = 0; i < n; i++) printf("%d ", X[i]);
    printf("\n");
}

void run_tests_prog1() {
    int A[16] = {1,2,3,4, 5,6,7,8, 9,10,11,12, 13,14,15,16};
    int B[16];
    int n = 16;

    print_array("A", A, n);

    sort_by_abs_with_temp(A, B, n);
    print_array("B sort |A| asc", B, n);

    transform_variant16(A, B, 4);
    print_array("B variant16", B, 16);

    reverse_into_new(A, B, n);
    print_array("B reverse", B, n);

    positives_then_others(A, B, n);
    print_array("B pos→others", B, n);
}

int main() {
    run_tests_prog1();
    return 0;
}

```
---

## 💻 Програма 2: in-place, лише одна допоміжна змінна
```c
#include <stdio.h>
#include <stdlib.h>

static int iabs(int x) { return x < 0 ? -x : x; }

// 1) In-place сортування за модулем
void sort_by_abs_in_place(int *A, int n) {
    for (int i = 0; i < n - 1; i++) {
        int minIdx = i;
        for (int j = i + 1; j < n; j++) {
            if (iabs(A[j]) < iabs(A[minIdx]) ||
               (iabs(A[j]) == iabs(A[minIdx]) && A[j] < A[minIdx])) {
                minIdx = j;
            }
        }
        if (minIdx != i) {
            int tmp = A[i];
            A[i] = A[minIdx];
            A[minIdx] = tmp;
        }
    }
}

// 2) In-place перестановка за схемою варіанта 16
void transform_variant16_in_place(int *A, int n) {
    int B[4*n], k = 0;
    for (int i = 0; i < n; i++) B[k++] = A[i];
    for (int i = 2*n - 1; i >= n; i--) B[k++] = A[i];
    for (int i = 3*n - 1; i >= 2*n; i--) B[k++] = A[i];
    for (int i = 4*n - 1; i >= 3*n; i--) B[k++] = A[i];
    for (int i = 0; i < 4*n; i++) A[i] = B[i];
}

// 3) Реверс in-place
void reverse_in_place(int *A, int n) {
    for (int i = 0, j = n - 1; i < j; i++, j--) {
        int tmp = A[i];
        A[i] = A[j];
        A[j] = tmp;
    }
}

// 4) Позитивні спочатку in-place
void positives_then_others_in_place(int *A, int n) {
    int write = 0;
    for (int read = 0; read < n; read++) {
        if (A[read] > 0) {
            int tmp = A[write];
            A[write] = A[read];
            A[read] = tmp;
            write++;
        }
    }
}

static void print_array(const char *label, const int *X, int n) {
    printf("%s: ", label);
    for (int i = 0; i < n; i++) printf("%d ", X[i]);
    printf("\n");
}

void run_tests_prog2() {
    int A[16] = {1,2,3,4, 5,6,7,8, 9,10,11,12, 13,14,15,16};
    int n = 16;

    print_array("A", A, n);

    sort_by_abs_in_place(A, n);
    print_array("A sort |A| asc", A, n);

    transform_variant16_in_place(A, 4);
    print_array("A variant16", A, 16);

    reverse_in_place(A, n);
    print_array("A reverse", A, n);

    positives_then_others_in_place(A, n);
    print_array("A pos→others", A, n);
}

int main() {
    run_tests_prog2();
    return 0;
}

```
## 📊 Складність

Сортування за модулем:

- З проміжним масивом: O(n log n) (qsort), пам’ять O(n).
- In-place (selection): O(n^2), пам’ять O(1).
- Реверс: час O(n), пам’ять O(1) або O(n) для нової копії.

Позитивні спочатку:

- З новим масивом: O(n), пам’ять O(n).
- In-place: O(n), пам’ять O(1).
- Зсув елемента: O(n), пам’ять O(1) або O(n) для копії.


---
