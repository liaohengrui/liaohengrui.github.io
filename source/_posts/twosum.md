---
title: 两数相加
url: 172.html
id: 172
categories:
  - 哈希表
  - 数据结构
date: 2018-11-22 23:25:56
tags:
---

序言
==

HashMap是一种常用的Hash映射。它存储的不仅仅是Key，还有Key对应的附加信息。通过哈希映射建立**钥匙与信息之间的映射关系**。一对一或多对一,也就是,多个key可能对应对应一个value。 ![f703738da9773912ca983490f3198618377ae281.jpg](https://upload-images.jianshu.io/upload_images/11238837-6db217d1acc335e1.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

用处
==

在我们需要返回更多信息，或者帮助我们判断时，从Map中取出有用的信息。

画图形象理解HashMap
=============

![无标题.png](https://upload-images.jianshu.io/upload_images/11238837-16ab7895fa9f53ed.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 就好比在存储Key的结构里面加了一个字段,用来存储Key的附带信息

题目
==

[原题链接](https://leetcode-cn.com/explore/learn/card/hash-table/205/practical-application-hash-map/811/ "原题链接") 给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的 两个 整数。 你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

### 实例

    给定 nums = [2, 7, 11, 15], target = 9
    因为 nums[0] + nums[1] = 2 + 7 = 9
    所以返回 [0, 1]
    

### 思路

有很多办法解决它，这里采用刚刚所说的，将nums\[i\]Key，i(所以)作为value。

      for (int i = 0; i < nums.length; i++) {
                int value = target - nums[i];
                if (map.containsKey(value) && (int) map.get(value) != i) {
                    ints[0] = i;
                    ints[1] = (int) map.get(value);
                    return ints;
                }
            }
    

好理解了吧，map中只要包含target - nums\[i\]的值，将索引取出来即可 [代码实现](https://github.com/liaohengrui/CodeDesign/blob/master/LeetCode/HashTable/HashMap/TwoSum.java "代码实现")