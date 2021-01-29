---
title: 依赖倒置原则(Dependency Inversion Principle(DIP))
date: 2021-01-29 19:14:02
categories: 设计模式
---

该原则的定义为：1. 上层模块不应该依赖于底层模块，他们应该依赖于抽象。 2. 抽象不应该依赖于细节，细节应该依赖于抽象

## 优点

* 减少类之间的耦合性
* 提高系统的稳定性
* 降低并行开发引起的风险
* 提高代码的可读性和可维护性

## 难点

* 设计之初就应该将整体的框架想好，提前抽象出应当抽象的东西

## 示例

现有一个输出消息的需求，要求不同设备能输出不同的消息，那么给出如下代码：

~~~ c#
public class DeviceA
{
    public void ConsoleLog()
    {
        Console.WriteLine("I'm DeviceA");
    }
}
public class DeviceB
{
    public void ConsoleLog()
    {
        Console.WriteLine("I'm DeviceB");
    }
}
public class ComputerControl()
{
    public void ConsoleLog(DeviceA device)
    {
        device.ConsoleLog();
    }
    public void ConsoleLog(DeviceB device)
    {
        device.ConsoleLog();
    }
}
~~~

这样设计的话，设计之初可能没什么大的问题，但随着设备的增加，每次增加设备都要在电脑控制台进行性的实现，使我们的代码变得愈发的臃肿，难以维护，这里可以发现，ComputerControl这个类是一个高级模块，而DeviceA、DeviceB都是细节实现类，这样的设计不符合依赖倒置的设计原则，于是将代码做出如下修改：

~~~ c#
public interface IConsoleLog
{
    void ConsoleLog();
}
public class DeviceA : IConsoleLog
{
    public void ConsoleLog()
    {
        Console.WriteLine("I'm DeviceA");
    }
}
public class DeviceB : IConsoleLog
{
    public void ConsoleLog()
    {
        Console.WriteLine("I'm DeviceB");
    }
}
public class ComputerControl()
{
    public void ConsoleLog(IConsoleLog device)
    {
        device.ConsoleLog();
    }
}
~~~

将代码修改成这样之后，以后再加设备，仅需增加该设备的具体实现，让他实现ConsoleLog的接口即可，这里让ComputerControl依赖于抽象IConsoleLog，其他的设备依赖于该抽象，以后的拓展和维护变得更加的方便了。

## 图例

![依赖倒置原则](/images/DesignPattern/DIP.png)
