---
title: 加一
url: 125.html
id: 125
categories:
  - 数据结构
  - 数组 &amp; 字符串
date: 2018-11-12 03:15:04
tags:
---

题目
==

[原题链接](https://leetcode-cn.com/explore/learn/card/array-and-string/198/introduction-to-array/772/ "原题链接") 给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。 最高位数字存放在数组的首位， 数组中每个元素只存储一个数字。 你可以假设除了整数 0 之外，这个整数不会以零开头。

示例
--

    输入: [1,2,3]
    输出: [1,2,4]
    解释: 输入数组表示数字 123。
    

思路
--

设置一个temp作为进位标志，当运算到了数组首位，temp不为0，说明首位存在进位关系,调用jdk的API复制一个比原数组长一个单位的数组,0号位用来存temp。api**System.arraycopy(digits, 0, newDigits, 1, digits.length),从digits的0号位复制到newDigits的1号位,复制长度为digits的长度(相当于克隆digits)** [解题代码](https://github.com/liaohengrui/CodeDesign/blob/master/LeetCode/Arrays%26Strings/array/PlusOne.java "解题代码")