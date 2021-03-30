---
title: DRY原则(Don't repeat yoursel)
date: 2021-01-29 19:14:02
categories: 设计模式
modified: 2021-02-04 19:41:37
---

DRY原则是指在编程过程中不写重复的代码，将公共的部分抽象出来，封装成一个基础类，在使用的时候再进行调用。

## 优点

* 降低了代码的耦合度
* 提高代码的灵活性、健壮性以及可读性，方便了后期的维护和修改

## 难点

* 抽象需要恰到好处，过多的抽象可能会导致简单的代码复杂化
* 可能会导致降低代码的可读性

## 示例

现有一个根据不同的url获取不同路径的需求，分析后设计代码如下：

~~~ c#
public string GetBody(string url)
{
    String body = "";
    if (url.Equals("/index.html")) 
    {
        body = "./public/index.html";
    }
    if (url.Equals("/css/index.css"))
    {
        body = "./public/css/index.html"
    }
    if (url.Equals("/js/index.js"))
    {
        body = "./public/js/index.html";
    }
    return body;
}
~~~

当情况比较多之后，这么一个简单的功能的代码量就会变得非常庞当，而且更麻烦的是维护的过程中，如果文件夹位置改变或者文件名改动，就会牵一发而动全身，如果某个位置漏改了，就会引起程序出错。即便改完所有地方，也是一件挺麻烦的事。所以我对代码进行抽象、修改。修改之后 代码如下：

~~~ c#
public string GetBodyFunction(url)
{
    var body = new StringBuilder();
    return body.AppendFormat("./public{0}",url);
}
public string GetBody(string url)
{
    String body = GetBodyFunction(url);
    return body;
}
~~~

## 图例

![DRY原则原则](https://cdn.jsdelivr.net/gh/cary-hu/blog-image@master/DesignPattern/DRY.jpg)
