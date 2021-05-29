---
title: Strategy
date: 2021-05-27 20:21:16
categories: 设计模式
modified: 2021-05-27 20:41:37
---

将实现和对象本身解耦，这将让对象的拓展更加方便！

<!--more -->

在编写一个软件的时候，经常会遇到一个对象里会有一个方法会有不同的实现，如果将这些实现都编码到对象中，对象将会变得异常复杂，后期维护也将变得十分艰难。

> 定义一系列算法，把他们一个个封装起来，并且使他们可互相替换。 ---《设计模式》

把算法抽象出来，建立公共的接口，通过不同的实现，完成不同的算法。
在需要使用的类中，需要哪个算法，实例化哪个算法，且可以进行动态的替换。

来一个简单的例子：

```csharp
public interface IFly
{
    void Fly();
}
class FlyWithWings : IFly
{
    public void Fly()
    {
        Console.WriteLine("我现在使用翅膀飞");
    }
}
class FlyWithHead : IFly
{
    public void Fly()
    {
        Console.WriteLine("我现在使用头飞");
    }
}
class Bird
{
    public string Name { get; set; }
    private IFly Fly;
    public Bird(string name)
    {
        this.Name = name;
    }
    public void DoSomeThing()
    {
        Fly = new FlyWithWings();
        Console.WriteLine($"我是一只鸟{this.Name}");
        Fly.Fly();
        Console.WriteLine($"我还是那个鸟{this.Name}");
        Fly = new FlyWithHead();
        Fly.Fly();
    }
}
```

另外一个例子，C#中的Sort函数，可以传入一个实现了ICompare接口的实例，从而实现不同的排序算法~

一个很简单的设计模式，将一些公共的,但是需要经常改变的方法抽象到接口中，通过编写不同的实现类，调用的时候动态的创建不同的实例，替换使用者的实现，即可做到对象和算法的解耦。

蛮好蛮好