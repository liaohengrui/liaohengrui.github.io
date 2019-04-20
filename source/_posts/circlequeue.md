---
title: 循环队列
url: 53.html
id: 53
categories:
  - 数据结构
  - 队列 &amp; 栈
date: 2018-11-02 20:26:18
tags:
---

循环队列实现--JAVA版
=============

需求:
---

设计你的循环队列实现。 循环队列是一种**线性数据结构**，其操作表现基于 **FIFO**（先进先出）原则并且队尾被连接在队首之后以形成一个循环。 循环队列的一个好处是我们可以利用这个队列之前用过的空间。在一个普通队列里，一旦一个队列满了，我们就不能插入下一个元素，即使在队列前面仍有空间。但是使用循环队列，我们能使用这些空间去存储新的值。 你的实现应该支持如下操作：

*   MyCircularQueue(k): 构造器，设置队列长度为 k 。
*   Front: 从队首获取元素。如果队列为空，返回 -1 。
*   Rear: 获取队尾元素。如果队列为空，返回 -1 。
*   enQueue(value): 向循环队列插入一个元素。如果成功插入则返回真。
*   deQueue(): 从循环队列中删除一个元素。如果成功删除则返回真。
*   isEmpty(): 检查循环队列是否为空。
*   isFull(): 检查循环队列是否已满。

示例：
---

        MyCircularQueue circularQueue = new MycircularQueue(3); // 设置长度为3
    
        circularQueue.enQueue(1);  // 返回true
    
        circularQueue.enQueue(2);  // 返回true
    
        circularQueue.enQueue(3);  // 返回true
    
        circularQueue.enQueue(4);  // 返回false,队列已满
    
        circularQueue.Rear();  // 返回3
    
        circularQueue.isFull();  // 返回true
    
        circularQueue.deQueue();  // 返回true
    
        circularQueue.enQueue(4);  // 返回true
    
        circularQueue.Rear();  // 返回4
    

思路&实现:
------

因为是结构是**数组,让数组成为循环队列**所以移动起来必定会出现head指针或者tail指针位置超出数组。所以只要解决好指针的问题，那么问题也迎刃而解。如下图增加元素Tail就会溢出. [![循环队列](https://upload-images.jianshu.io/upload_images/11238837-574d05eb6221c2b5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240 "循环队列")](https://upload-images.jianshu.io/upload_images/11238837-574d05eb6221c2b5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240 "循环队列") 所以增加两个函数,专门处理**指针位置**! \- nextHead() - nextTail() 这样问题就好解决了,加元素时,先调用**isFull判断能不能操作**,然后调用**nextTail**改变指针位置,最后赋值!减元素反之!**over**

    /**
     * Demo class
     *
     * @author HengruiLiao
     * @date 2018/11/2
     */
    public class CircularQueue {
        int[] ints;
        int head, tail;
        int size;
    
        /**
         * Initialize your data structure here. Set the size of the queue to be k.
         */
        public CircularQueue(int k) {
            ints = new int[k];
            tail = -1;
            head = 0;
            size = 0;
        }
    
        /**
         * Insert an element into the circular queue. Return true if the operation is successful.
         */
        public boolean enQueue(int value) {
            if (isFull()) {
                return false;
            } else {
                nextTail();
                ints[tail] = value;
                size++;
                return true;
            }
        }
    
        /**
         * Delete an element from the circular queue. Return true if the operation is successful.
         */
        public boolean deQueue() {
            if (isEmpty()) {
                return false;
            } else {
                nextHead();
                size--;
                return true;
            }
        }
    
        /**
         * Get the front item from the queue.
         */
        public int Front() {
            if (isEmpty()) {
                return -1;
            }
            return ints[head];
        }
    
        /**
         * Get the last item from the queue.
         */
        public int Rear() {
            if (isEmpty()) {
                return -1;
            }
            return ints[tail];
        }
    
        /**
         * Checks whether the circular queue is empty or not.
         */
        public boolean isEmpty() {
            return size == 0;
        }
    
        /**
         * Checks whether the circular queue is full or not.
         */
        public boolean isFull() {
            return size == ints.length;
        }
    
        public void nextTail() {
            tail++;
            if (tail == ints.length) {
                tail = 0;
            }
        }
    
        public void nextHead() {
            head++;
            if (head == ints.length) {
                head = 0;
            }
        }
    }