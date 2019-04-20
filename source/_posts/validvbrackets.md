---
title: 有效的括号
url: 99.html
id: 99
categories:
  - 数据结构
  - 队列 &amp; 栈
date: 2018-11-06 05:32:50
tags:
---

题目
==

给定一个只包括 '('，')'，'{'，'}'，'\['，'\]' 的字符串，判断字符串是否有效。 有效字符串需满足： 1\. 左括号必须用相同类型的右括号闭合。 2. 左括号必须以正确的顺序闭合。 注意空字符串可被认为是有效字符串。

#### 示例 1:

    输入: "()[]{}"
    输出: true
    

思路
==

使用栈结构,**后进先出**,左括号入栈,发现右括号,弹出栈顶元素,进行左右括号匹配,若匹配失败返回false [代码实现连接](https://github.com/liaohengrui/CodeDesign/blob/master/LeetCode/Queue%26Stack/stack/ValidBrackets.java "代码实现连接")