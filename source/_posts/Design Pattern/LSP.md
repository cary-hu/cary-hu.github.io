---
title: 里氏替换原则(Liskov Substitution Principle(LSP))
date: 2021-01-29 19:14:02
tags:
---

里氏替换原则是用来解决当父类代码改变，子类功能也会受到影响的问题。在设计类的时候，如果有继承关系，其子类必须实现父类的所有抽象方法，但是不可以重写父类的非抽象（已实现）方法，子类可以新增自己特有的方法，在实现抽象方法时，其形参必须比父类的形参更为宽松，但返回值子类必须比父类更为严格。（isA）

## 优点

* 增强了程序的健壮性、兼容性
* 克服了继承中重写父类造成的可复用性变差的缺点
* 降低了代码出错的可能性

## 难点

*

## 示例

正方形到底是不是特殊的长方形~

~~~ c#
public class Rectangle
{
    private double width {get; set; }
    private double height {get; set; }
}
public class Square
{
    private double side {get; set; }
}
~~~

以此来看的话，正方形和长方形的结构完全不同，看起来正方形不应该是长方形的子类，所以长方形和正方形之间并不符合里氏替换原则，但是，将代码做如下修改：

~~~ c#
public interface IPolygon
{
    public double GetWidth();
    public double GetHeight();
}
public class Rectangle : IPolygon
{
    private double width;
    private double height;
    public double GetWidth()
    {
        return width;
    }
    public void SetWidth(double width)
    {
        this.width = width;
    }
    public double GetHeight()
    {
        return height;
    }
    public void SetHeight(double height)
    {
        this.height = height;
    }
}
public class Square : IPolygon
{
    private double side;
    public double GetWidth()
    {
        return this.GetSide();
    }
    public void SetWidth(double width)
    {
        this.SetSide(width);
    }
    public double GetHeight()
    {
        return this.GetSide();
    }
    public void SetHeight(double height)
    {
        this.SetSide(height);
    }
    public double GetSide()
    {
        return side;
    }
    public void SetSide(double side)
    {
        this.side = side;
    }
}
~~~

## 图例

![里氏替换原则](/images/DesignPattern/LSP.png)

{% /images/DesignPattern/LSP.png 里氏替换原则 %}
