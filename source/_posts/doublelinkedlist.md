---
title: 设计双向链表
url: 163.html
id: 163
categories:
  - 数据结构
  - 链表
date: 2018-11-21 17:52:41
tags:
---

链表
==

链表是一种数据结构。但它不像数组，语法已经实现了。所以我们要通过自己的定义来实现 ![screen-shot-2018-04-17-at-161130.png](https://upload-images.jianshu.io/upload_images/11238837-3ebacfa9cf4bef89.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) easy,一个连接一个,就完事了,每一个都是一个独立体。所以先定义独立体结构 1. Value 字段：表示大小 2. prev 字段： 表示上一个节点 2. next 字段： 表示下一个节点

    private class Node {
       int val;
       Node next, prev;
    
       public Node(int val) {
            this.val = val;
       }
    }
    

实现--注意事项
========

最容易犯错的地方是 **public void addAtIndex(int index, int val)** 这个方法，在某个位置加入一个新的节点 ![screen-shot-2018-04-28-at-173055.png](https://upload-images.jianshu.io/upload_images/11238837-7ce1efcf5a4528f5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 最容易想当然实现方法，找到前面的节点和后面的节点，按照图上所示连接起来就OK了。 但是这样做有个问题 万一增加的位置是**头节点或者尾节点**，这样就会报空指针错误，因为它的前面或者后面没有节点了。所以，实现这个方法的时候判断下即可 [代码实现](https://github.com/liaohengrui/CodeDesign/blob/master/LeetCode/LinkedList/double_linked_list/DesignLinkedList.java "代码实现")