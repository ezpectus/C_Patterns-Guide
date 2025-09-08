# 🔍 DFS (Обход в глубину) — дерево

## 💡 Идея алгоритма
DFS — это рекурсивный или стековый обход, который уходит "вглубь" структуры, прежде чем вернуться назад.  
Для бинарного дерева есть три основных варианта:

- **Preorder (NLR)** — сначала узел, потом левый, потом правый  
- **Inorder (LNR)** — сначала левый, потом узел, потом правый  
- **Postorder (LRN)** — сначала левый, потом правый, потом узел  

## 📦 Применение
| Тип обхода | Где используется | Что даёт |
|------------|------------------|----------|
| Preorder   | Построение дерева, сериализация | Узлы в порядке создания |
| Inorder    | BST (Binary Search Tree) | Отсортированный вывод |
| Postorder  | Удаление дерева, вычисление выражений | Сначала дети, потом родитель |

## 🧠 Подход
- Рекурсивная функция `void dfs(TreeNode* node)`  
- Условие выхода: `if (node == NULL) return;`  
- Порядок вызовов зависит от типа обхода  
- Можно заменить стеком, но рекурсия чище для дерева

## 🧪 Пример кода (C)

```c
typedef struct TreeNode {
    int val;
    struct TreeNode* left;
    struct TreeNode* right;
} TreeNode;

void preorder(TreeNode* node) {
    if (node == NULL) return;
    printf("%d ", node->val);
    preorder(node->left);
    preorder(node->right);
}

void inorder(TreeNode* node) {
    if (node == NULL) return;
    inorder(node->left);
    printf("%d ", node->val);
    inorder(node->right);
}

void postorder(TreeNode* node) {
    if (node == NULL) return;
    postorder(node->left);
    postorder(node->right);
    printf("%d ", node->val);
}
```
## 🔁 Сравнение трёх обходов

| Тип       | Порядок вызовов           | Где используется                     |
|-----------|----------------------------|--------------------------------------|
| Preorder  | `visit → left → right`     | Построение, сериализация             |
| Inorder   | `left → visit → right`     | BST, отсортированный вывод           |
| Postorder | `left → right → visit`     | Удаление, выражения, освобождение    |

---

# 🌲 DFS — Полный пример на C

## 📘 Структура + тестовые данные + обход

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct TreeNode {
    int val;
    struct TreeNode* left;
    struct TreeNode* right;
} TreeNode;

// Создание узла
TreeNode* newNode(int val) {
    TreeNode* node = (TreeNode*)malloc(sizeof(TreeNode));
    node->val = val;
    node->left = node->right = NULL;
    return node;
}

// DFS — Preorder обход
void dfs(TreeNode* root) {
    if (root == NULL) return;
    printf("%d ", root->val);       // Посещение узла
    dfs(root->left);                // Левое поддерево
    dfs(root->right);               // Правое поддерево
}

int main() {
    /*
        Пример дерева:
              1
             / \
            2   3
           / \
          4   5
    */

    TreeNode* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);

    printf("DFS Preorder: ");
    dfs(root);  // Ожидаемый вывод: 1 2 4 5 3
    printf("\n");

    return 0;
}
```
## 🧩 Архитектура DFS — сигнальные точки

- `if (root == NULL) return;` — базовый стоп  
- `visit` (действие над узлом) вставляется:
  - Preorder → до рекурсий
  - Inorder → между рекурсий
  - Postorder → после рекурсий
- Один шаблон → три обхода
- Можно заменить рекурсию на стек

## 🧠 Что показывает

- Рекурсивный обход дерева
- Пример дерева с 5 узлами
- Вывод в порядке Preorder: сначала узел, потом левый, потом правый


## 🧱 Шаблон DFS — без реализации

## 📘 Чистый каркас для объяснения архитектуры
```c
typedef struct TreeNode {
    int val;
    struct TreeNode* left;
    struct TreeNode* right;
} TreeNode;

// DFS обход дерева
void dfs(TreeNode* root) {
    // TODO: реализовать обход
}
```
## 🌐 DFS на графе (через список смежности)

```c
#define MAX 100
int visited[MAX];
vector<int> adj[MAX];

void dfs(int node) {
    if (visited[node]) return;
    visited[node] = 1;
    printf("%d ", node);
    for (int i = 0; i < adj[node].size(); i++) {
        dfs(adj[node][i]);
    }
}
```

## 🧾 Вывод

DFS — это фундаментальный шаблон обхода, который адаптируется под любую структуру: дерево, граф, выражение, сериализацию.  
Три варианта (Preorder, Inorder, Postorder) — это просто разные точки действия внутри одного рекурсивного каркаса.  
Понимание порядка вызовов и сигнальных точек позволяет строить универсальные модули, пригодные для экзамена, репо и реальных задач.  
Рекурсия даёт чистоту, стек — контроль, граф — масштаб. Всё остальное — просто детали реализации.



---



