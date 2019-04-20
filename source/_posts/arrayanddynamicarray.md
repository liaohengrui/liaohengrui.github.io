---
title: 数组与动态数组
url: 120.html
id: 120
categories:
  - 数据结构
  - 数组 &amp; 字符串
date: 2018-11-12 02:57:48
tags:
---

数组
==

数组是一种基本的数据结构，用于按顺序存储元素的集合。但是元素可以任意存取，因为数组中的每个元素都可以通过数组索引来识别。 ![screen-shot-2018-03-20-at-191856.png](https://upload-images.jianshu.io/upload_images/11238837-81568d45e40ee69f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 优点：任意存储，效率高 缺点：不能长度有限，有局限性

动态数组
====

大多数编程语言都提供内置的**动态数组**,JAVA中是ArrayList。

#### 数组转换动态数组：

    new ArrayList<>(Arrays.asList(a));
    

### 注意

注意如果a是一个**原始类型的数组**（也就是int\[\]、boolean\[\]），会出现如下效果[![ArrayConversion](https://i.loli.net/2018/11/12/5be9527852ed1.png "ArrayConversion")](https://i.loli.net/2018/11/12/5be9527852ed1.png "ArrayConversion")

### 原因

int自身**是原始类型不是类**，所以是int\[\]**就变成了1个类而已，不是数组(java语法，请勿与人类眼中的数组相提并论)**。所以在**asList(T... a)这个方法被使用的时候，a仅仅表达了1**，而不是个数组。也就产生了上图所示的结果**dynamicArry中只有一个元素，这个元素就是int\[\]对象**

解决办法
----

将**int\[\]变成Integer\[\]，因为Integer本身就是个对象**，所以Integer\[\]在java语法中被理解成数组了,上面的asList(T... a),这个a也就是Integer\[\]数组长度了