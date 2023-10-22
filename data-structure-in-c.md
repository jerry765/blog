---
title: 数据结构笔记
date: 2023-09-27 18:07:21
mdate: 2023-10-09 14:44:35
categories: GEE
tags: 
- C
- data structure
---

> 参考书籍：数据结构与算法分析（C语言描述） 原书第二版

<!-- more -->

## 第 1 章 引论

递归的四条基本法则
- **基准情形**：不用递归就能求解
- **不断推进**：递归调用必须能够朝着产生基本情形的方向推进
- **设计法则**：假设所有的递归调用都能运行
- **合成效益法则**（compound interest rule）：在求解一个问题的同一实例时，切勿在不同的递归调用中做重复性的工作

## 第 2 章 算法分析

> 计算任何事情不要超过一次

### 最大子序列和

#### 算法1

``` C
int MaxSubsequenceSum(const int A[], int N) {
    int ThisSum, MaxSum, i, j, k;
    
    MaxSum = 0;
    for (i = 0; i < N; i++) {
        for (j = i; j < N; j++) {
            ThisSum = 0;
            
            for (k = i; k <= j; k++){
                ThisSum += A[k];    /* 过分耗时 */
            }
            
            if(ThisSum > MaxSum) {
                MaxSum = ThisSum;
            }
        }
    }
    return MaxSum;
}
```
复杂度为`O(N*3)`

#### 算法2

``` C
int MaxSubSequenceSum(const int A[], int N) {
    int ThisSum, MaxSum, i, j;

    MaxSum = 0;
    for(i = 0; i < N; i++) {
        ThisSum = 0;

        for(j = i; j < N; j++) {
            ThisSum += A[j];

            if(ThisSum > MaxSum) {
                MaxSum = ThisSum;
            }
        }
    }

    return MaxSum;
}
```
复杂度为`O(N*2)`

#### 算法3

分析知最大子序列和可能在三处出现，或者整个出现在输入数据的左半部，或者整个出现在右半部，或者跨越输入数据的中部从而占据左右两半部分。前两种情况可以递归求解，第三种情况的最大和可以通过求出前半部分的最大和（包括前半部分的最后一个元素）以及后半部分的最大和（包括后半部分的第一个元素）而得到。

**递归调用的一般形式是通过传递输入的数组以及左（Left）边界和右（Right）边界，它们界定了数组待处理的部分。单行驱动程序通过传递数组以及边界 0 和 N-1 以启动该过程。**

``` C
static int MaxSubSum(const int A[], int Left, int Right) {
    int MaxLeftSum, MaxRightSum;
    int MaxLeftBorderSum, MaxRightBorderSum;
    int LeftBorderSum, RightBorderSum;
    int Center, i;

    // Base Case
    if(Left == Right) {
        if(A[Left] > 0) {
            return A[Left];
        } else {
            return 0
        }
    }

    Center = (Left + Right)/2;  // assume N is even
    MaxLeftSum = MaxSubSum(A, Left, Center);
    MaxRightSum = MaxSubSum(A, Center + 1; right);

    MaxLeftBorderSum = 0; LeftBorderSum = 0;
    for(i = Center; i >= Left; i--) {
        LeftBorderSum += A[i];
        if(LeftBorderSum > MaxLeftBorderSum) {
            MaxLeftBorderSum = LeftBorderSum;
        }
    }

    MaxRightBorderSum = 0; RightBorderSum = 0;
    for(i = Center + 1; i <= Right; i++) {
        RightBorderSum += A[i];
        if(RightBorderSum > MaxRightBorderSum) {
            MaxRightBorderSum = RightBorderSum;
        }
    }

    return Max3(MaxLeftSum, MaxRightSum, MaxLeftBorderSum, MaxRightBorderSum);
}

int MaxSubsequenceSum(const int A[], int N) {
    return MaxSubSum(A, 0, N - 1);
}
```
复杂度为`O(N)`

#### 算法4

``` C
int MaxSubsequenceSum(const int A[], int N) {
    int ThisSum, MaxSum, j;

    ThisSum = MaxSum = 0;
    for(j = 0; j < N; j++) {
        ThisSum += A[j];

        if(ThisSum > MaxSum) {
            MaxSum = ThisSum;
        } else if (ThisSum < 0) {
            ThisSum = 0;    // clear ThisSum when negative
        }
    }

    return MaxSum;
}
```

在任意时刻，算法都能对它已经读入的数据给出子序列问题的正确答案，具有这种特性的算法叫做**联机算法**（on-line algorithm）。仅需要常量空间并以线性时间运行的联机算法几乎是完美的算法。

## 第 3 章 表、栈和队列

### 表

``` C
#ifndef _List_H

struct Node;
typedef struct Node *PtrToNode;
typedef PtrToNode List;
typedef PtrToNode Position;

typedef int ElementType;

List MakeEmpty(List L);
int IsEmpty(List L);
int IsLast(Position P, List L);
Position Find(ElementType X, List L);
void Delete(ElementType X, List L);
Position FindPrevious(ElementType X, List L);
void Insert(ElementType X, List L, Position P);
void DeleteList(List L);
Position Header(List L);
Position First(List L);
Position Advance(Position P);
ElementType Retrieve(Position P);

#endif  /* _List_H */

// Place in the implementation file
struct Node
{
    ElementType Element;
    Position Next;
};

// Return true if L is empty
int IsEmpty(List L) {
    return L->Next == NULL;
}

// Return true if P is the last position in list L
// Parameter L is unused in this implementation
int IsLast(Position P, List L) {
    return P->Next == NULL;
}

// Return Position of X in L; NULL if not found
Position Find(ElementType X, List L) {
    Position P;

    P = L->Next;
    while(P != NULL && P->Element != X) {
        P = P->Next;
    }

    return P;
}

// Delete first occurrence of X from a list
// Assume use of a header node
void Delete(ElementType X, List L) {
    Position P, TempCell;

    P = FindPrevious(X, L);

    if(!IsLast(P, L)) {
        // Assumption of header use
        // X is found, delete it
        TempCell = P->Next;
        P->Next = TempCell->Next; // Bypass deleted cell
        free(TempCell);
    }
}

// If X is not found, then next field of returned
// Position is NULL
// Assumes a header
Position FindPrevious(ElementType X, List L) {
    Position P;

    P = L;
    while(P->Next != NULL && P->Next->Element != X) {
        P = P->Next;
    }
    
    return P;
}

// Insert (after legal position P)
// Header implementation assumed
// Parameter L is unused in this implementation
void Insert(ElementType X, List L, Position P) {
    Position TmpCell;

    TmpCell = malloc(sizeof(struct Node));
    if(TmpCell == NULL) {
        FatalError("Out of space!!!");
    }

    TmpCell->Element = X;
    TmpCell->Next = P->Next;
    P->Next = TmpCell;
}

void DeleteList(List L) {
    Position P, Tmp;

    P = L->Next;    // Header assumed
    L->Next = NULL;
    while (P != NULL) {
        Tmp = P->Next;
        free(P);
        P = Tmp;
    }
}
```

## 第 4 章 树

### 二叉树

二叉树的一个性质是**平均二叉树的深度要比 N 小的多**，这个平均深度为**O(根号 N)**；对于二叉查找树（binary search tree），深度的平均值为**O(log N)**。

#### 平均情形分析

假设所有树出现的机会均等，则树的所有节点的平均深度为**O(log N)**。

- 平衡条件：任何节点的深度均不得过深
- 放弃平衡条件，允许树有任意的深度，但是在每次操作之后要使用一个规则进行调整，使得后面的操作效率更高。**自调查（self-adjusting）类结构**。

### AVL 树

一颗 AVL 树是其每个节点的左子树和右子树的高度最多差 1 的二叉查找树。（空树的高度定义为-1。）在高度为 h 的 AVL 树中，最少节点数 S(h) 由 S(h)=S(h-1)+S(h-2)+1 给出。

插入一个节点可能破坏 AVL 树的特性，通过旋转进行修正。高度不平衡时，必须重新平衡的节点的两棵子树的高度差 2 。

#### 旋转

把树形象地看成柔软灵活的，重力作用。
除旋转引起的局部变化外，树的其余部分必须知晓该变化。

#### 代码

递归地将 X 插入到了 T 的相应的子树中。如果子树的高度不变，那么插入完成。否则，如果 T 中出现了高度不平衡，那么我们根据 X 以及 T 和子树中的关键字做适当的单旋转或双旋转，更新这些高度（并解决好与树的其余部分的连接），从而完成插入。

<!-- TODO：寻找满意的旋转图 -->

``` C
# ifdef _AVLTree_H

struct AvlNode;
typedef struct AvlNode *Position;
typedef struct AvlNode *AvlTree;    // AVL树

AvlTree MakeEmpty(AvlTree T);
Position Find(ElementType X, AvlTree T);
Position FindMin(AvlTree T);
Position FindMax(AvlTree T);
AvlTree Insert(ElementType X, AvlTree T);
AvlTree Delete(ElementType X, AvlTree T);
ElementType Retrieve(Position P);

# endif /* _AVLTree_H */

// Place in the implementation file
struct AvlNode
{
    ElementType Element;
    AvlTree Left;
    AvlTree Right;
    int Height;
};

static int Height(Position P)
{
    if (P == NULL)
        return -1;
    else
        return P->Height;
}

AvlTree Insert(ElementType X, AvlTree T)
{
    if (T == NULL)
    {
        // Create and return a one-node tree
        T = malloc(sizeof(struct AvlNode));
        if (T == NULL)
            FatalError("Out of space!!!");
        else
        {
            T->Element = X;
            T->Height = 0;
            T->Left = T->Right = NULL;
        }
    }
    else if (X < T->Element)
    {
        T->Left = Insert(X, T->Left);
        if (Height(T->Left) - Height(T->Right) == 2)
            if (X < T->Left->Element)
                T = SingleRotateWithLeft(T);
            else
                T = DoubleRotateWithLeft(T);
    }
    else if (X > T->Element)
    {
        T->Right = Insert(X, T->Right);
        if (Height(T->Right) - Height(T->Left) == 2)
            if (X > T->Right->Element)
                T = SingleRotateWithRight(T);
            else
                T = DoubleRotateWithRight(T);
    }
    // Else X is in the tree already; we'll do nothing

    T->Height = Max(Height(T->Left), Height(T->Right)) + 1;
    return T;
}

static Position SingleRotateWithLeft(Position K2)
{
    Position K1;

    K1 = K2->Left;
    K2->Left = K1->Right;
    K1->Right = K2;

    K2->Height = Max(Height(K2->Left), Height(K2->Right)) + 1;
    K1->Height = Max(Height(K1->Left), K2->Height) + 1;

    return K1;  // New root
}

static Position SingleRotateWithRight(Position K1)
{
    Position K2;

    K2 = K1->Right;
    K1->Right = K2->Left;
    K2->Left = K1;

    K1->Height = Max(Height(K1->Left), Height(K1->Right)) + 1;
    K2->Height = Max(Height(K2->Right), K1->Height) + 1;

    return K2;  // New root
}

static Position DoubleRotateWithLeft(Position K3)
{
    // Rotate between K1 and K2
    K3->Left = SingleRotateWithRight(K3->Left);

    // Rotate between K3 and K2
    return SingleRotateWithLeft(K3);
}

static Position DoubleRotateWithRight(Position K1)
{
    // Rotate between K3 and K2
    K1->Right = SingleRotateWithLeft(K1->Right);

    // Rotate between K1 and K2
    return SingleRotateWithRight(K1);
}
```

### 伸展树

伸展树（splay tree）保证从空树开始连续 M 次对树的操作最多花费`O(M log N)`时间，并不保证任意一次操作花费 O（N） 时间的可能。*不存在坏的输入序列*。
*当 M 次操作的序列总的最坏情形运行时间为 O(MF(N)) 时，我们就说它的摊还（amortized）运行时间为 O(F(N))。*一颗伸展树每次操作的摊还代价为 `O(log N)`。
伸展树是基于这样的事实：对于二叉查找树来说，每次操作最坏情形时间 O(N) 并不坏，只要它相对不常发生就行。累积的运行时间很重要。
*只要有一个节点被访问，它就必须被移动。当一个节点被访问后，它就要经过一系列的 AVL 树的旋转后放到根上。*

伸展树不要求保留高度或平衡信息，因此它在某种程度上节省空间并简化代码。



