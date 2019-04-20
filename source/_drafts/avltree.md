---
title: AVL树原理与实现
url: 202.html
id: 202
categories:
  - 默认
tags:
---

AVL树介绍
======

avl树高度平衡搜索二叉树的一种实现方式。 高度平衡二叉树：每个节点的左右子树的高度差不大于1。 ![281623404229547.jpg](https://upload-images.jianshu.io/upload_images/11238837-d4a7d4e3f79dedbc.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 如上图，左边是AVL树，右边不是AVL树。因为节点7的左子树的高度是3，右子树的高度是1。高度差等于2了。不满足条件

AVL树的实现
=======

要实现AVL的树的关键就是让每个节点的左右树的高度差相差1。旋转成为了必不可少的一部分。下面介绍4种旋转，通过这几种旋转可以将任何节点的高度差从2变成小于2。

LL旋转
----

![281626153129361.jpg](https://upload-images.jianshu.io/upload_images/11238837-6eee69b8bed00ec5.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) LL旋转的原因是，节点的左子树的左子树上还有节点，造成的左子树高了。旋转方法如图：

    /*
     * LL：左左对应的情况(左单旋转)。
     *
     * 返回值：旋转后的根节点
     */
    private AVLTreeNode<T> leftLeftRotation(AVLTreeNode<T> k2) {
        AVLTreeNode<T> k1;
    
        k1 = k2.left;
        k2.left = k1.right;
        k1.right = k2;
    
        k2.height = max( height(k2.left), height(k2.right)) + 1;
        k1.height = max( height(k1.left), k2.height) + 1;
    
        return k1;
    }