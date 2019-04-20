---
title: 长度最小的子数组
url: 134.html
id: 134
categories:
  - 数据结构
  - 数组 &amp; 字符串
date: 2018-11-15 18:22:08
tags:
---

题目
==

[原题链接](https://leetcode-cn.com/problems/minimum-size-subarray-sum/description/ "原题链接") 给定一个含有 n 个正整数的数组和一个正整数 s ，找出该数组中满足其和 ≥ s 的长度最小的连续子数组。如果不存在符合条件的连续子数组，返回 0。

#### 示例:

    输入: s = 7, nums = [2,3,1,2,4,3]
    输出: 2
    解释: 子数组 [4,3] 是该条件下的长度最小的连续子数组。
    

思路
==

使用双指针，head，tail。构成一个区间，区间总和小了，tail后移增加区间总和。区间数总和大了，head后移，缩小区间。设置一个result用于记录最小的tail-head，result就是结果了

    2  3  1  2  4  3
    h ------ t
    

核心控制好tail和head的移动逻辑即可 [实现代码](https://github.com/liaohengrui/CodeDesign/blob/master/LeetCode/Arrays%26Strings/string/MinSubarray.java "实现代码")