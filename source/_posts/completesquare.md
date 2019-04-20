---
title: BFS暴力求解完全平方数
url: 97.html
id: 97
categories:
  - 数据结构
  - 队列 &amp; 栈
date: 2018-11-04 22:54:57
tags:
---

题目
==

[原题链接](https://leetcode-cn.com/explore/learn/card/queue-stack/217/queue-and-bfs/874/ "原题") 给定正整数 n，找到若干个完全平方数（比如 1, 4, 9, 16, ...）使得它们的和等于 n。你需要让组成和的完全平方数的个数最少。

#### 示例 1:

    输入: n = 12
    输出: 3 
    解释: 12 = 4 + 4 + 4.
    

思路
==

![CompleteSquare.png](https://upload-images.jianshu.io/upload_images/11238837-faa5f56374e76ecb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 使用BFS广度遍历，每个节点的子节点就是**本身值减去所有完全平方数（ 1, 4, 9, 16, ...），且减完后自身大于0**。如果子节点出现了**0**，那么它的层数就是结果（**BFS特点离根节点越近越早被访问到**）

实现
==

    package com.example.demo;
    
    import java.util.HashSet;
    import java.util.LinkedList;
    import java.util.Queue;
    import java.util.Set;
    
    /**
     * Demo class
     *
     * @author HengruiLiao
     * @date 2018/11/5
     */
    public class CompleteSquare {
        Queue<Integer> queue = new LinkedList<>();
        Queue<Integer> assistQueue = new LinkedList<>();
        Set<Integer> set = new HashSet<>();
        int step = 0;
    
        public int numSquares(int n) {
            queue.offer(n);
            while (!queue.isEmpty()) {
                int root = queue.poll();
                if (root == 0) {
                    return step;
                }
                subSquareNum(assistQueue, root);
                if (queue.isEmpty()) {
                    step++;
                    queue = assistQueue;
                    assistQueue = new LinkedList<>();
                }
            }
            return -1;
        }
    
        private void subSquareNum(Queue<Integer> assistQueue, int root) {
            int square = 1;
            while (true) {
                int subNum = root - square * square;
                if (subNum < 0) {
                    break;
                }
                if (set.add(subNum)) {
                    assistQueue.offer(subNum);
                }
                square++;
            }
        }
    
    
    }