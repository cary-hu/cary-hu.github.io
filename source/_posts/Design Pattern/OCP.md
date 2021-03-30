---
title: 开放封闭原则(Open Closed Principle(OCP))
date: 2021-01-29 19:14:02
categories: 设计模式
modified: 2021-02-04 19:41:37
---

对于类的设计来说，他应该是可以拓展的，但不应该可以进行修改，也就是说，对拓展是开放的，而对修改是封闭的。对拓展开放，意味着有新的需求或变化时，可以对现有代码进行拓展，以适应新的情况。对修改封闭，意味着类一旦设计完成，就可以进行独立的工作，而不需要对类进行任何修改。而在设计类的时候要符合这个原则，只有依赖于抽象，实现开放封闭的核心思想就是抽象编程，而不是具体编程，因为抽象相对稳定，让类依赖于固定的抽象，所以对修改是封闭的，而通过面向对象的继承和多态机制，可以实现对抽象体的继承，通过重写方法来改变其固有的行为，实现新的拓展方法，这是实施开放封闭原则的基本思路。

## 优点

* 代码可读性高，可维护性强
* 单一类的逻辑简单，复用性强

## 难点

* 类的设计要做到完全对修改封闭，几乎是不可能完成的任务，视情况而定，不用强求。
* 对设计类的人员要求较高，因为要考虑到以后所有有可能变化的因素，留下接口

## 示例

现有一个计算器的设计需求，要求实现加减乘除，最简单的实现：

~~~ c#
public class Calculator
{
    public double Add(double numberA,double numberB)
    {
        return numberA + numberB;
    }
    public double Minus(double numberA,double numberB)
    {
        return numberA - numberB;
    }
    public double Multiply(double numberA,double numberB)
    {
        return numberA * numberB;
    }
    public double Divide(double numberA,double numberB)
    {
        return numberA / numberB;
    }
}
~~~

这样的设计在使用初期可能会显得并没有什么问题，但如果现在加入了新的算法，将会导致程序员不得不对这个类进行修改，这就违反了我们的设计原则。于是，进行了如下修改：

~~~ c#
public interface ICalculator
{
    double GetResult(double numberA, double numberB);
}
class Add : ICalculator
{
    public double GetResult(double numberA, double numberB)
    {
        return numberA + numberB;
    }
}

...

class Divide : ICalculator
{
    public double GetResult(double numberA,double numberB)
    {
        return numberA / numberB;
    }
}
~~~

设计一个getResult的接口，需要不同的算法，就对他进行不同的实现，从而实现不对原类进行修改，只进行拓展，从而实现不同的需求，从而满足开放封闭原则。

## 图例

![开放封闭原则](https://cdn.jsdelivr.net/gh/cary-hu/blog-image@master/DesignPattern/OCP.png)
