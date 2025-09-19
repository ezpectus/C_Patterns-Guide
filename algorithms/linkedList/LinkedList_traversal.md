# 🔍 Linked List Analysis with Reverse Traversal and Key Statistics

## 📘 Назначение лабораторной задачи

> Реализовать односвязный список из `n` элементов, где каждый элемент содержит целочисленный ключ.  
> Выполнить:
- Вывод списка в прямом порядке  
- Вывод списка в обратном порядке  
- Вычисление среднего значения ключей  
- Подсчёт количества элементов с ключами меньше и больше среднего

Цель — освоить базовые операции над связанными структурами, научиться строить, обходить и анализировать списки.

---

## 💻 Полный код на C с тестами
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
    int key;
    struct Node *next;
} Node;

// 🔧 Создание списка из массива
Node* createList(int *data, int n) {
    Node *head = NULL, *tail = NULL;
    for (int i = 0; i < n; i++) {
        Node *newNode = malloc(sizeof(Node));
        newNode->key = data[i];
        newNode->next = NULL;
        if (!head)
            head = tail = newNode;
        else {
            tail->next = newNode;
            tail = newNode;
        }
    }
    return head;
}

// 🔧 Прямой вывод
void printList(Node *head) {
    printf("List (forward): ");
    while (head) {
        printf("%d ", head->key);
        head = head->next;
    }
    printf("\n");
}

// 🔧 Обратный вывод (рекурсивно)
void printReverse(Node *head) {
    if (!head) return;
    printReverse(head->next);
    printf("%d ", head->key);
}

// 🔧 Среднее значение
double average(Node *head) {
    int sum = 0, count = 0;
    while (head) {
        sum += head->key;
        count++;
        head = head->next;
    }
    return count ? (double)sum / count : 0;
}

// 🔧 Подсчёт меньше/больше среднего
void countRelativeToAverage(Node *head, double avg, int *less, int *greater) {
    *less = *greater = 0;
    while (head) {
        if (head->key < avg) (*less)++;
        if (head->key > avg) (*greater)++;
        head = head->next;
    }
}

// 🔧 Освобождение памяти
void freeList(Node *head) {
    while (head) {
        Node *tmp = head;
        head = head->next;
        free(tmp);
    }
}

// 🔧 Тесты
void run_tests() {
    int data1[] = {1, 2, 3, 4, 5};     // avg = 3.0
    int data2[] = {10, 20, 30};        // avg = 20.0
    int data3[] = {5, 5, 5, 5};        // avg = 5.0

    int *datasets[] = {data1, data2, data3};
    int sizes[] = {5, 3, 4};

    for (int t = 0; t < 3; t++) {
        printf("Test %d:\n", t + 1);
        Node *list = createList(datasets[t], sizes[t]);

        printList(list);
        printf("List (reverse): ");
        printReverse(list);
        printf("\n");

        double avg = average(list);
        printf("Average: %.2f\n", avg);

        int less, greater;
        countRelativeToAverage(list, avg, &less, &greater);
        printf("Keys < avg: %d\n", less);
        printf("Keys > avg: %d\n", greater);

        freeList(list);
        printf("\n");
    }
}

int main() {
    run_tests();
    return 0;
}
```
---

## 🧠 Архитектурная логика (расширенная)

### 📐 Модель

- Структура `Node` содержит:
  - `int key` — информационный элемент
  - `Node *next` — указатель на следующий узел
- Список создаётся через `createList()` из массива входных данных
- Вывод:
  - Прямой — итеративно через `printList()`
  - Обратный — рекурсивно через `printReverse()`
- Среднее значение — через сумму и счёт элементов
- Подсчёт — через сравнение каждого ключа с `avg`

### 📊 Сложность

- **Время**: `O(n)` — один проход на каждую операцию
- **Память**: `O(n)` — `n` узлов + стек при обратном выводе
- **Выделение памяти**: через `malloc`, освобождение — вручную через `freeList()`

### ⚠️ Ограничения

- Нет произвольного доступа по индексу — только последовательный обход
- Обратный вывод требует рекурсии — стек может переполниться при больших `n`
- Среднее значение — `double`, может потребовать округления при выводе

---

## 🧪 Тестовые данные

| Тест | Вход           | Среднее | < avg | > avg |
|------|----------------|---------|-------|-------|
| 1    | 1 2 3 4 5      | 3.0     | 2     | 2     |
| 2    | 10 20 30       | 20.0    | 1     | 1     |
| 3    | 5 5 5 5        | 5.0     | 0     | 0     |

---

## 📦 Повторное использование

Модуль можно адаптировать для:

- Двусвязных списков (`prev` указатель)
- Сортировки списка по ключу
- Удаления узлов по значению
- Хранения структур с метаданными (`timestamp`, `label`, `flags`)
- Интеграции с файлами (сериализация/десериализация)
- Потоковой обработки данных (например, из stdin или сетевого сокета)

---

## 🧘 Заключение

Модуль — фундамент для лабораторок по связанным структурам. Он показывает:

- Как строить и анализировать списки
- Как использовать рекурсию для обратного обхода
- Как вычислять статистику по ключам
- Как освобождать память корректно
- Как масштабировать архитектуру под реальные задачи



---
