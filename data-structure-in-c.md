title: 数据结构笔记
date: 2023-09-27 18:07:21
mdate: 2023-10-09 14:37:25
categories: GEE
tags: 

> 参考书籍：数据结构与算法分析（C语言描述） 原书第二版

<!-- more -->

## 第1章 引论

递归的四条基本法则
- **基准情形**：不用递归就能求解
- **不断推进**：递归调用必须能够朝着产生基本情形的方向推进
- **设计法则**：假设所有的递归调用都能运行
- **合成效益法则**（compound interest rule）：在求解一个问题的同一实例时，切勿在不同的递归调用中做重复性的工作

## 第2章 算法分析

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

## 第3章 表、栈和队列

### 表

``` C
#ifndef _List_H

struct Node;
typedef struct Node *PtrToNode;
typedef PtrToNode List;
typedef PtrToNode Position;

List MakeEmpty(List L);
int IsEmpty(List L);
int IsLast(Position P, List L);
Position Find(ElementType X);
void Delete(ElementType X, List L);
```

## 第 4 章 树

### 二叉树

二叉树的一个性质是**平均二叉树的深度要比 N 小的多**，这个平均深度为**O(根号 N)**；对于二叉查找树（binary search tree），深度的平均值为**O(log N)**。

#### 平均情形分析

假设所有树出现的机会均等，则树的所有节点的平均深度为**O(log N)**。

- 平衡条件：任何节点的深度均不得过深
- 放弃平衡条件，允许树有任意的深度，但是在每次操作之后要使用一个规则进行调整，使得后面的操作效率更高。**自调查（self-adjusting）类结构**。

### AVL 树

一颗 AVL 树是其每个节点的左子树和右子树的高度最多差 1 的二叉查找树。（空树的高度定义为-1。）在高度为 h 的 AVL 树中，最少节点数 S(h) 由 S(h)=






