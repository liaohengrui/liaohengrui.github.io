---
title: 哈希表的概念与表现方式
url: 166.html
id: 166
categories:
  - 哈希表
  - 基本概念
  - 数据结构
date: 2018-11-22 18:16:41
tags:
---

概念
==

哈希表是种数据结构,用于存储**非重复**的值。有两种实现方式哈希集合（Set）哈希映射（Map）

### 为什么要引入hash表这种数据结构？

为了快速**插入和搜索**。数组查询快，插入慢。链表插入快，查询慢。 哈希表综合上述，将存储分成了很多数组，这样有效的降低了插入的复杂度，但同时也稍微的增加了查找的复杂度

简单图解哈希表
=======

![无标题.png](https://upload-images.jianshu.io/upload_images/11238837-4472139fec2efa29.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 1\. 要存储的元素放入hash函数里，得到hash值 2. 在hash的的存储数组里，寻找是否有存储记录 3. 若无冲突，存入。有冲突，说明已经存储过了，所以不做操作。

使用Java内置的哈希集合实践
===============

Set集合。有了上述的图解，我们可以理解，当我们想存储一个自定义类Node：

     static class Node {
            public int i;
    
            public Node(int i) {
                this.i = i;
            }
     }
    

我只关心Node里面的I的大小，以I的大小判断这个Node的唯一性。我需要重写

            @Override
            public int hashCode() {
                return i;
            }
    

这个用于Hash函数的映射。但这仅仅够了吗？当然是否定的，Hash表还要判断这个Node是否已近在HashCode的存储数组里了，所以还应该重写

            @Override
            public boolean equals(Object obj) {
                Node node = (Node) obj;
                return this.i == node.i;
            }
    

用于判断这个Node是否存在