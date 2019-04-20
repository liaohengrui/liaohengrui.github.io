---
title: 克隆图
url: 101.html
id: 101
categories:
  - 数据结构
  - 队列 &amp; 栈
date: 2018-11-08 04:27:16
tags:
---

题目
==

[原题链接](https://leetcode-cn.com/explore/learn/card/queue-stack/219/stack-and-dfs/884/ "原题链接") 克隆一张无向图，图中的每个节点包含一个 label （标签）和一个 neighbors （邻接点）列表 。简单的说就是**遍历图**，把每个节点**对象**重新new出来，new出来的新对象，里面的值（neighbors 、label）与**原对象相同**

###### 节点对象表现如下

    class UndirectedGraphNode {
            int label;
            List<UndirectedGraphNode> neighbors;
    
            UndirectedGraphNode(int x) {
                label = x;
                neighbors = new ArrayList<UndirectedGraphNode>();
            }
        }
    

#### 示例 1:

节点被唯一标记。 我们用 # 作为每个节点的分隔符，用 , 作为节点标签和邻接点的分隔符。 例如，序列化无向图 {0,1,2#1,2#2,2}。 该图总共有三个节点, 被两个分隔符 # 分为三部分。 1. 第一个节点的标签为 0，存在从节点 0 到节点 1 和节点 2 的两条边。 2. 第二个节点的标签为 1，存在从节点 1 到节点 2 的一条边。 3. 第三个节点的标签为 2，存在从节点 2 到节点 2 (本身) 的一条边，从而形成自环。 我们将图形可视化如下：

           1
          / \
         /   \
        0 --- 2
             / \
             \_/
    

思路
==

采用**BFS（Queue）**遍历节点,且遍历避免**重复遍历（使用Set集合）**，因为要克隆对象所以采用**Map**保存原始对象和克隆对象。

1.  克隆Queue拿出来的节点

    if (cloneMap.containsKey(root)) {
            cloneNode = cloneMap.get(root);
            } else {
            cloneNode = new UndirectedGraphNode(root.label);
            cloneMap.put(root, cloneNode);
    }
    

2.  克隆节点的neighbors （邻接点)，并为其添加到上面的克隆节点的neighbors （邻接点)。

     for (UndirectedGraphNode neighborhood : root.neighbors) {
                    UndirectedGraphNode cloneNeighborhood;
                    if (cloneMap.containsKey(neighborhood)) {
                        cloneNeighborhood = cloneMap.get(neighborhood);
                    } else {
                        cloneNeighborhood = new UndirectedGraphNode(neighborhood.label);
                        cloneMap.put(neighborhood, cloneNeighborhood);
                    }
                    if (set.add(neighborhood)) {
                        BFSQueue.offer(neighborhood);
                        cloneNode.neighbors.add(cloneNeighborhood);
                    } else {
                        cloneNode.neighbors.add(cloneNeighborhood);
    }
    

[代码实现连接](https://github.com/liaohengrui/CodeDesign/blob/master/LeetCode/Queue%26Stack/stack/CloneGraph.java "代码实现连接")