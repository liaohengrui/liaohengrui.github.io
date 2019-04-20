---
title: Java泛型小总结
url: 232.html
id: 232
categories:
  - java学习笔记
date: 2019-01-09 03:43:49
tags:
---

什么是泛型
=====

C++通过模板技术可以指定集合的元素类型，而Java在1.5之前一直没有相对应的功能。一个集合可以放任何类型的对象，相应地从集合里面拿对象的时候我们也不得不对他们进行强制得类型转换。 而泛型的目的就是在编译的期间，指定特定对象，从而达到使用特定对象的效果。它的好处就是 1. 可以得到强类型在编译时刻进行类型检查的好处。 2. 无需进行强制类型转化

Java中如何使用泛型
===========

java中使用泛型有两种。**泛型类和泛型方法**

泛型类
---

    /**
     * Demo class
     *
     * @author HengruiLiao
     * @date 2019/1/9
     */
    public class FruitMachine<T> {
    
        public void handleFruit(T t) {
            System.out.println(t.getClass().getSimpleName()+"被成功处理");
        }
    
        public static void main(String[] args) {
            FruitMachine<Apple> machine=new FruitMachine<>();
            Apple apple=new Apple();
            machine.handleFruit(apple);
        }
    
    }
    class Apple{}
    class Banana{}
    

这里定义了个叫做水果机器的类。handleFruit方法用于处理特定泛型的水果T。 结果输出: Apple被成功处理

泛型方法
----

        public <T> void handleOtherFruit(T t) {
            System.out.println(t.getClass().getSimpleName() + "被成功处理");
        }
    

在方法的作用域和返回值中间填入泛型T,**注意此处T与类中T重名了**。普通变量的作用域一样，内部覆盖外部。所以这里的T指的是函数的T，不是勒种的T。 为了测试上述的结论

      public static void main(String[] args) {
            FruitMachine<Apple> machine = new FruitMachine<>();
            Apple apple = new Apple();
            Banana banana=new Banana();
            machine.handleFruit(apple);
            machine.handleOtherFruit(banana);
        }
    

结果输出： Apple被成功处理 Banana被成功处理

泛型方法/类型通配符
==========

1.  你会发现所有能用类型通配符（?）解决的问题都能用泛型方法解决，并且泛型方法可以解决的更好。
    1.  类型通配符： `void func(List<? extends A> list);`
    2.  完全可以用泛型方法完美解决 `<T extends A> void func(List<T> list);`
2.  两者最明显的区别 “?”泛型对象是只读的，不可修改，因为“?”类型是不确定的，可以代表范围内任意类型； 而泛型方法中的泛型参数对象是可修改的，因为类型参数T是确定的（在调用方法时确定），因为T可以用范围内任意类型指定；
    

extend 与 super的区别
=================

`? extend A`:表示 ?是A类或者A的子类 `? super A`:表示 ?是A类或者A的父类