---
title: 接口隔离原则(Interface Segregation Principle(ISP))
date: 2021-01-29 19:14:02
tags:
---

通俗的来说，就是一个接口里不要放很多方法，这样会显得这个接口臃肿不堪，接口应当尽量细化，一个接口对应一个功能模块，同时接口里的方法应当尽可能的小，使接口更加轻便灵活。

## 优点

* 避免接口污染
* 提高灵活性
* 提供定制服务
* 实现了高内聚

## 难点

* 设计时必须根据实际需要实际考虑，没有一个通用的办法

## 示例

举一个很常见的例子，现在有一个需求，我们需要一个接口用来定义美女，给出的要求：美女包括面貌、身材和气质，那么根据需求定义如下接口：

~~~ c#
public interface IBeauty
{
    public bool IsLookNice(beauty beautyEntity)
    {
        // do some logic judge this beautyEntity is look nice or not
    }
    public bool IsNiceFigure(beauty beautyEntity)
    {
        // do some logic judge this beautyEntity has nice figure or not
    }
    public bool GreatTemperament(beauty beautyEntity)
    {
        // do some logic judge this beautyEntity has great temperament or not
    }
}
~~~

看起来代码如此设计并没有什么问题，但是现实生活中不乏有长得一般，但是气质很好的气质美女，那么上面的接口就不再适用，于是我们将代码做如下修改：

~~~ c#
public interface ILookBeauty
{
    public bool IsLookNice(beauty beautyEntity)
    {
        // do some logic judge this beautyEntity is look nice or not
    }
    public bool IsNiceFigure(beauty beautyEntity)
    {
        // do some logic judge this beautyEntity has nice figure or not
    }
}
public interface ITemperamentBeauty
{
    public bool GreatTemperament(beauty beautyEntity)
    {
        // do some logic judge this beautyEntity has great temperament or not
    }
}
~~~

然后通过这两个接口的组合，便能完成之前提到的需求。

## 图例

![接口隔离原则](/images/DesignPattern/ISP.png)
