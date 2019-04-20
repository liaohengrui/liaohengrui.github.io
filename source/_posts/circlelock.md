---
title: 利用BFS解决旋转锁
url: 95.html
id: 95
categories:
  - 数据结构
  - 队列 &amp; 栈
date: 2018-11-03 21:11:30
tags:
---

题目
==

[原题链接](https://leetcode-cn.com/explore/learn/card/queue-stack/217/queue-and-bfs/873/ "原题") 你有一个带有四个圆形拨轮的转盘锁。每个拨轮都有10个数字： '0', '1', '2', '3', '4', '5', '6', '7', '8', '9' 。每个拨轮可以自由旋转：例如把 '9' 变为 '0'，'0' 变为 '9' 。每次旋转都只能旋转一个拨轮的一位数字。 锁的初始数字为 '0000' ，一个代表四个拨轮的数字的字符串。 列表 deadends 包含了一组死亡数字，一旦拨轮的数字和列表里的任何一个元素相同，这个锁将会被永久锁定，无法再被旋转。 字符串 target 代表可以解锁的数字，你需要给出最小的旋转次数，如果无论如何不能解锁，返回 -1。

#### 示例 1:

    输入：deadends = ["0201","0101","0102","1212","2002"], target = "0202"
    输出：6
    解释：
    可能的移动序列为 "0000" -> "1000" -> "1100" -> "1200" -> "1201" -> "1202" -> "0202"。
    注意 "0000" -> "0001" -> "0002" -> "0102" -> "0202" 这样的序列是不能解锁的，
    因为当拨动到 "0102" 时这个锁就会被锁定。
    

思路
==

![旋转锁.png](https://upload-images.jianshu.io/upload_images/11238837-34f68103fc167397.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 按照BFS特性:**离根节点越近越早被访问到**,也就是只要我们遍历到了Target,那么,他在第几层,也就是我们需要的求解值!

实现
==

    package com.example.demo;
    
    import java.util.*;
    
    /**
     * Demo class
     *
     * @author HengruiLiao
     * @date 2018/11/3
     */
    public class CircularLock {
        Queue<String> queue;
        Set<String> set;
        int step = 0;
        Queue<String> assistQueue;
        Set<String> dead;
    
        public CircularLock() {
            queue = new LinkedList();
            set = new HashSet();
            assistQueue = new LinkedList<>();
        }
    
    
        public int openLock(String[] deadends, String target) {
            queue.add("0000");
            dead = new HashSet<>(Arrays.asList(deadends));
            if (dead.contains("0000")) {
                return -1;
            }
            while (!queue.isEmpty()) {
                String root = queue.poll();
                if (target.equals(root)) {
                    return step;
                }
                bfsRoot(root, assistQueue, deadends);
                if (queue.isEmpty()) {
                    queue = assistQueue;
                    assistQueue = new LinkedList<>();
                    step++;
                }
            }
            return -1;
        }
    
        private void bfsRoot(String root, Queue<String> assistQueue, String[] deadends) {
            for (int i = 0; i < 4; i++) {
                char c = root.charAt(i);
                StringBuffer addBuffer = new StringBuffer(root);
                StringBuffer subBuffer = new StringBuffer(root);
                addBuffer.setCharAt(i, change(c, 1));
                subBuffer.setCharAt(i, change(c, -1));
                String temp = addBuffer.toString();
                if (!dead.contains(temp) && set.add(temp)) {
                    assistQueue.add(temp);
                }
                temp = subBuffer.toString();
                if (!dead.contains(temp) && set.add(temp)) {
                    assistQueue.add(temp);
                }
            }
        }
    
        private char change(char c, int i) {
            if (1 == i) {
                return c == '9' ? '0' : (char) (c + i);
            } else {
                return c == '0' ? '9' : (char) (c + i);
            }
        }
    
    
      /*  public static void main(String[] args) {
    
            CircularLock lock = new CircularLock();
            int i = lock.openLock(new String[]{"8888"}, "0009");
            System.out.println(i);
    
        }*/
    
    
    }