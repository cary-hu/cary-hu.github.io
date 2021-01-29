---
title: 迪米特法则(Law of Demeter(LD))
date: 2021-01-29 19:14:02
categories: 设计模式
---

迪米特法则的意义在于降低类之间的耦合，它要求一个对象应该对其他对象有最少的了解（也就是说，设计的每个类、每个功能点应该相对独立，互相之间不存在或者说很少有依赖关系）。在实践中，通常采用只暴露必须要暴露的方法，来保证迪米特法则，其他一些不必要暴露的方法，全都设置为私有方法，不允许外部类使用和查看。以此降低两个类之间的耦合。

## 优点

* 提高了类的复用性
* 降低了类变更的风险

## 难点

* 采用该法则应当适度，解耦是有限度的，要根据经验来避免过犹不及。

## 示例

现有一个场景，一个男人要煮咖啡，现有两个类，分别是咖啡机和这个男人，代码如下：

~~~ c#
public class CoffeeMachine
{
    public void AddCoffeeBean()
    {
        // do something
    }
    public void AddWater()
    {
        // do something
    }
    public void StartMachine()
    {
        // do something
    }
}
public class Man
{
    public void MakeCoffee()
    {
        CoffeeMachine coffeeMachine = new CoffeeMachine(){ };
        coffeeMachine.AddCoffeeBean();
        coffeeMachine.AddWater();
        coffeeMachine.StartMachine();
    }
}
~~~

在以上代码中，男人对于咖啡机内部的方法了解过多，其实他并不用关注这些具体的过程，所以将代码进行优化：

~~~ c#
public class CoffeeMachine
{
    public void MakeCoffee()
    {
        AddCoffeeBean();
        AddWater();
        StartMachine();
    }
    private void AddCoffeeBean()
    {
        // do something
    }
    private void AddWater()
    {
        // do something
    }
    private void StartMachine()
    {
        // do something
    }
}
public class Man
{
    public void MakeCoffee()
    {
        CoffeeMachine coffeeMachine = new CoffeeMachine(){ };
        coffeeMachine.MakeCoffee();
    }
}
~~~

这样修改了之后，暴露给男人的接口变少，减少了男人类对咖啡机类的了解，降低了它们之间的耦合。
