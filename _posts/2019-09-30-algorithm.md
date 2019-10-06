---
layout:     post
title:      "Algorithm"
subtitle:   ""
date:       2019-09-28
author:     "LiuBiyongge"
header-img: "img/in-post/ACM.jpg"
tags:

  - ACM
---

# 算法

[TOC]

- NP-complete问题

no polynomial complete, 不可以在多项式时间内求解。

一个NPC问题的例子是[子集合加总问题](https://zh.wikipedia.org/wiki/子集合加總問題)，题目为:

​	给予一个有限数量的整数集合，找出任何一个此集合的非空子集且此子集内整数和为零。

​	即: S是一个包括若干整数的集合，找出任一一个$S^{'} \subset S$且$\sum_{x \in S^{`}}s=0$

这个问题的答案非常容易验证，但当前没有任何一个够快的方法可以在合理的时间内（意即多项式时间）找到答案。只能一个个将它的子集取出来一一测试，它的时间复杂度是Ο(2n)，n是此集合的元素数量。

## 算法基础

### 插入排序

<span style="color:red">最坏运行时间: $\theta (n^2)$</span>

**类似排序扑克牌**

**循环不变式:** 

- 初始化: 循环第一次迭代前为真
- 保存：循环每次迭代之前为真，迭代之后为真
- 终止

```c++
#include <iostream>
#include <vector>
using namespace std;

int main(){
    int arr[6] = {5, 2, 4, 6, 1, 3};
    vector<int> vec(6);
    for(int i = 0; i < vec.size(); i++){
        vec[i] = arr[i];
    }

    int key, j;
    for(int i = 1; i < vec.size(); i++){
        key = vec[i];
        j = i -1;
        while (j >= 0 && key < vec[j]){
            vec[j+1] = vec[j];
            j--;
        }
        vec[j+1] = key;
    }

    for(int i = 0; i < vec.size(); i++){
        cout << vec[i] << " ";
    }
}
```

## 分析算法

- 时间复杂度

### 设计算法

- 增量法

### 分治法

把原问题分解为几个规模较小但类似于原问题的子问题。

- 分解
- 解决
- 合并

#### 归并排序

<span style="color:red">最坏运行时间:$\theta (nlgn)$</span>

```c++
#include <iostream>
#include <vector>
using namespace std;

void merge(vector<int>& vec, int i, int p, int j){
    vector<int> L(vec.begin() + i, vec.begin() + p + 1);
    vector<int> R(vec.begin() + p + 1, vec.begin() + j + 1);
    int x = 0, y = 0, m;
    for(m = i; m <= j; m++){
        if(L[x] < R[y]){
            if(x < L.size()) {
                vec[m] = L[x];
                x++;
            } else{
                break;
            }
        } else {
            if (y < R.size()) {
                vec[m] = R[y];
                y++;

            } else{
                break;
            }
        }
    }
    while (m <= j && x < L.size()){
        vec[m] = L[x];
        m++, x++;
    }
    while (m <= j && y < R.size()){
        vec[m] = R[y];
        m++, y++;
    }
}

void sort(vector<int>& vec, int i, int j){
    if(j - i > 0){
        int p = (i + j)/2;
        sort(vec, i, p);
        sort(vec, p + 1, j);
        merge(vec, i, p, j);
    } else{
        return;
    }
}

int main(){
    int arr[8] = {23 ,11 ,5, 2, 4, 6, 1, 3};
    vector<int> vec(8);
    for(int i = 0; i < vec.size(); i++){
        vec[i] = arr[i];
    }

    sort(vec, 0, vec.size() - 1);
    for(int i = 0; i < vec.size(); i++){
        cout << vec[i] << " ";
    }

}
```

## 函数的增长

渐近符号

- Θ(g(n))Θ(g(n)) 用来表示一类函数 f(n)f(n) ，存在 c1、c2c1、c2 和 n0n0，使得对于所有 n≥n0n≥n0，都有 0≤c1g(n)≤f(n)≤c2g(n)0≤c1g(n)≤f(n)≤c2g(n)。

- O(g(n))O(g(n)) 表示一类函数 f(n)f(n)，存在 cc 和 n0n0，使得对于所有 n≥n0n≥n0，都有 0≤f(n)≤cg(n)0≤f(n)≤cg(n)。一般读作“大 O”或者“Big-Oh”。
- Ω(g(n))Ω(g(n)) 表示一类函数 f(n)f(n)，存在 cc 和 n0n0，使得对于所有 n≥n0n≥n0，都有 0≥cg(n)≥f(n)0≥cg(n)≥f(n)

- $n = O(n^2)$ 表示$n \in O(n)$
- $T(n) = 2T(n/2) + \theta (n)$ $\theta (n)$表示匿名函数

## 分治策略

递归式求解<span style="color:red">$\theta$</span>或<span style="color:red">$O$</span>的方法

- **代入法** 预测一个界限，然后用数学归纳法证明
- **递归树法** 化成棵树求解
- **主方法** 使用递归公式。

- strassen

strassen算法的关键不在于是乘法还是加法，而是在于算法内部递归调用的次数。

其实算法导论上说的很清楚了，用分治的方法也可以普通方法实现，时间复杂度和循环一样都是 O(n^3)。

strassen算法的关键在于内部递归调用的次数减少了1（从普通的8次变为特殊的7次）。这里的一个结论就是递归算法中递归调用次数少，时间复杂度底。这很容易理解，在算法导论中用了“茂盛”度来描述这一时间复杂度在递归算法中的变化。

所以strassen算法的关键在于，递归调用的次数怎么从8次减少一次的。

反推理解一下，这说明8次递归调用中有一次是冗余的，即第8次递归乘法的结果信息已经包含在了前7次的结果里，前7次的计算结果通过线性组合就能得到第8个递归的结果了。而该线性组合的时间复杂度低于该算法本身（即一次递归调用）的时间复杂度。

做一个结论。但凡是能够优化时间复杂度的算法，高复杂度的算法中必然是有一些计算是冗余的，如能用更少的计算代替冗余，就能提高效率。

（因为算法递归的刚好是乘法，所以此处看起来似乎是重点放在了乘法上）

\-------------

至于为什么传统矩阵相乘算法中有冗余计算，也尝试分析一下：

冗余的根本原因应该在于基本的乘法分配律a*(b+c)=a*b+a*c。同样的计算结果，前一种（等号前）方法计算需要2次基本运算，而后一种（等号后）方法需要3次。（假设乘法运算和加法运算是同等开销的基本运算）。

而一般的矩阵乘法算法中是大量的单步乘法运算后求和，即采用的是上述等号右边的计算式。如果能有一种方法，将乘法运算中的相同因子提到前边来，运用上述乘法分配律转换计算形式，那么就能提高计算效率。

这应该就是strassen算法的本质。

看strassen算法的过程，就是先将一部分子矩阵进行加（减）运算，再进行乘法运算。其实就是构造了上述分配律的左式。

