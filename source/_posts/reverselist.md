---
title: 反转链表
url: 161.html
id: 161
categories:
  - 数据结构
  - 链表
date: 2018-11-21 02:17:11
tags:
---

序言
==

在**单链表**中，我们知道一个节点指向下一个节点，如此循环下去。直到链表结束。也就是说我们只知道**某个节点的下一个节点，上个节点却无法获知**。那么有什么好的办法在单链表中实现回退，找到**上个节点的办法**。

### 栈

把每个节点迭代进入栈里面 ![iterator.png](https://upload-images.jianshu.io/upload_images/11238837-5e4f9e79b4b9dec4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 利用栈的特性FILO,正好能满足条件。想知道某个节点的上一个节点，只需要在栈中弹出来即可。

实现模式
====

### Java的stack存储

这个比较节点，迭代下就可以了

### 递归形成调用栈

看图理好理解! ![20170517153542944.jpg](https://upload-images.jianshu.io/upload_images/11238837-76909e6af7f6c543.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 递归到最后面去 ![20170517153555749.jpg](https://upload-images.jianshu.io/upload_images/11238837-e962ecf32b6437b5.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 往上面返 ![20170517153616757.jpg](https://upload-images.jianshu.io/upload_images/11238837-32379f592794624a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 在往上面返 这样也可以实现栈的结构,只不过用的是内存栈

题目
==

[反转链表](https://leetcode-cn.com/explore/learn/card/linked-list/195/classic-problems/750/ "反转链表") 反转一个单链表。

    输入: 1->2->3->4->5->NULL
    输出: 5->4->3->2->1->NULL
    

实现
==

按照上面的实现模式,很好实现,我是使用递归解决的 [代码实现](https://github.com/liaohengrui/CodeDesign/blob/master/LeetCode/LinkedList/single_list/ReverseListRecursion.java "代码实现")