---
title: 合成复用原则(Composite Reuse Principle)
date: 2021-01-29 19:14:02
categories: 设计模式
---

尽量使用对象的组合，而不是继承来达到复用的目的，类与类之间的关系应该是has-a而不是is-a。

## 优点

* 降低主类的复杂度

## 示例

现有一个银行卡类的设计需求，简单分析后，将代码设计如下：

```c#
public interface ICard
{
    string Id { get; set }
    void Withdraw();
    void Deposit();
    void Overdraw();
}
public class MyCard : ICard
{
    public void Withdraw()
    {
        // do something
    }
    public void Deposit()
    {
        // do something
    }
    public void Overdraw()
    {
        // do something
    }
}
```

如此设计，我们办理的所有卡都将具有这个功能，此时使用了继承关系。为了更灵活的拥有各种功能，可以分别设立储蓄卡和信用卡两种，并拥有银行卡来对衙门进行聚合使用，此时采用了合成复用的原则：

``` c#
public interface ICard
{
    public string Id { get; set }
    public SaveCard saveCard();
    public CreditCard creditCard();
}
public class SaveCard
{
    public void Withdraw()
    {
        // do something
    }
    public void Deposit()
    {
        // do something
    }
}
public class CreditCard
{
    public void Overdraw()
    {
        // do something
    }
}
public class MyCard : ICard
{
    
}
```
