---
title: 深入浅出理解递归和迭代
url: 110.html
id: 110
categories:
  - 基本概念
  - 数据结构
date: 2018-11-09 23:38:05
tags:
---

**刷题碰到LeetCode** [94\. 二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/description/ "94. 二叉树的中序遍历") **本来想用递归解决本问题，突然发现底下要求用进阶方法，迭代算法解决本题。所以来总结一下递归和迭代。**

何为迭代？
=====

首先我们来看下面这段简单的代码：

    int sum(int n )
    {
        int sum =0;
        for(int i = 1 ; i <= n;i++) sum+=n;//求解1~n的和
        return sum;
    }
    

从上述例子看,1一直加到N，每一次的运算结果都是上一次的结果加上新的i。因此，不难理解，迭代就是用**旧数据不断的推导出新数据**

### 迭代的代码形式

1.  for、while循环：因为迭代需要不断的推导，所以for、while循环可以在代码中满足这点条件。
2.  有结束条件：也就是迭代次数，如for循环的i<n。while循环的while（条件）
3.  for、while循环里面有推导规则：因为要用旧值推导新值，所以每次循环就是推导的运算法则。如：sum+=n

何为递归？
=====

还是一样，让我们看看下面这个例子。

    int sum(int n )
    {
        if(n==1) return 1;
        ﻿else return n+sum(n-1);
    }
    

同样求1一直加到N的和，递归采用的是不断减少运算数据，一层一层的减下去，直到最后i=1返回1，然后在一层一层的返回上去。因此递归的本质就是**自己调用自己**

### 递归的代码形式

1.  自身调用：不断的调用自身达到拆分数据，最后求解
2.  有结束条件： if（满足条件）return 结果;

递归和迭代举例
=======

#### 斐波那契数列 f（n）=f（n-1）+f（n-2）

    //1、迭代版本
    int fib(int n )
    {
        if(n<2) return 1;
        int f0 = 1,f1=1;
        for(int i = 2 ; i < n ; i++){
            int f2= f0+f1;
            f0=f1;f1=f2;
        }
        return f1;
    }
    //2、递归版本
    int fib1(int n)
    {
        if (n <= 1) return 1;
        return fib1(n-1) + fib1(n-2);
    }
    
    

递归转迭代
=====

### 尾递归转换成迭代

尾递归：递归的特殊情况，函数调用出现在函数尾部的递归方式。上述两个例子都输入尾递归。 尾递归可以轻松的转换成迭代方式。这里就不在具体说明了。

### 非尾递归转换成迭代

非尾递归转换成迭代就必须用到堆栈，简而言之，就是用**栈结构来模拟函数调用**（调用栈）。

    //快速排序的迭代版本
    //注：这里的partition函数省略
    void QuickSort1(int beg, int end)
    {
        if (end - beg <= 1) return;
        int pos = partition(beg, end);
        QuickSort1(beg, pos);
        QuickSort1(pos + 1, end);
    }
    //利用堆栈转成成迭代版本
    void QuickSort2(int beg, int end) 
    {
        ﻿stack<pair<int ,int>> temp_stack;//利用堆栈来保存begin和end的值
        ﻿temp_stack.push(pair<int,int>(begin,end));
        ﻿while(!temp.empty())//堆栈不为空则继续循环
        ﻿{
        ﻿    ﻿pair<int,int>  tmp = temp_stack.top();
        ﻿    ﻿temp_stack.pop();//模拟函数调用，去除栈顶元素，对其进行处理
        ﻿    ﻿if(temp.second - tmp.first > 1)//和递归版本一样，只剩两个数的时候结束递归，否则继续压栈
        ﻿    ﻿{
        ﻿    ﻿    ﻿int pos = partition(beg, end);  
        ﻿    ﻿    ﻿temp_stack.push(pair<int,int>(tmp.first,pos));
        ﻿    ﻿    ﻿temp_stack.push(pair<int,int>(pos+1,tmp.second));
        ﻿    ﻿}
        ﻿}
    }