---
title: 未名湖边的烦恼(JAVA版)
url: 180.html
id: 180
categories:
  - 蓝桥杯
date: 2018-12-06 00:58:59
tags:
---

问题描述 　　每年冬天，北大未名湖上都是滑冰的好地方。北大体育组准备了许多冰鞋，可是人太多了，每天下午收工后，常常一双冰鞋都不剩。 　　每天早上，租鞋窗口都会排起长龙，假设有还鞋的m个，有需要租鞋的n个。现在的问题是，这些人有多少种排法，可以避免出现体育组没有冰鞋可租的尴尬场面。（两个同样需求的人（比如都是租鞋或都是还鞋）交换位置是同一种排法）

    输入格式
    　　两个整数，表示m和n
    输出格式
    　　一个整数，表示队伍的排法的方案数。
    样例输入
    3 2
    样例输出
    5
    数据规模和约定
    　　m,n∈［0,18］
    

解题思路: 1\. 借鞋A人,换鞋子B人。如果当A=B的话，上一步必然是换完了B,借了A-1双鞋子。所以DP\[A\]\[B\]=DP\[A-1\]\[B\] 2. 当A>B时，上一步可能是借走了一双鞋，也可能是换进了一双鞋。DP\[A\]\[B\]=DP\[A-1\]\[B\]+DP\[A\]\[B-1\]。 [代码实现](https://github.com/liaohengrui/CodeDesign/blob/master/lanqiao/src/arithmetic/CharIegend.java "代码实现")

    package arithmetic;
    
    import java.util.Scanner;
    /**
     * Demo class
     *
     * @author HengruiLiao
     * @date 2018/12/6
     */
    public class UnnamedLate {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            int m = scanner.nextInt();
            int n = scanner.nextInt();
            int result = dpBorrow(m, n);
            System.out.print(result);
        }
    
        /**
         * m还鞋子
         * n借鞋子
         */
        private static int dpBorrow(int m, int n) {
            if (m < n) {
                return 0;
            }
            if (n == 0) {
                return 1;
            }
            if (m == n) {
                return dpBorrow(m, n - 1);
            }
            return dpBorrow(m - 1, n) + dpBorrow(m, n - 1);
        }
    }