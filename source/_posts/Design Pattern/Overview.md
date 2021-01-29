---
title: 设计模式
date: 2021-01-29 19:14:02
categories: 设计模式
sticky: 999
---

设计模式是编程界的前辈们，根据自己对面向对象程序编码开发的经验所总结出来的、解决特定问题的一系列套路，他并不是语法规定，而是一套用来提高提高代码复用率、可维护性、可读性、稳健性以及安全性的解决方案。本次学习基于：<a href="./reference/Design Patterns- Elements of Reusable Object-Oriented Software.pdf">Design Patterns- Elements of Reusable Object-Oriented Software</a>一书，该书由Erich Gamma、Richard Helm、Ralph Johnson、John Vlissides四个人合著，他们四个人被称为Gang of Four，缩写为Gof。这本书介绍了23中设计模式，就是指GoF的23种设计模式。

## 六大原则 SOLID

所有的设计模式均遵循以下六个基本的设计原则：

{% post_link SRP %}

* [单一职责原则：Single responsibility principle(SRP)](./Design-principles/SRP.md)
* [开放封闭原则: Open Closed Principle(OCP)](./Design-principles/OCP.md)
* [里氏替换原则: Liskov Substitution Principle(LSP)](./Design-principles/LSP.md)
* [迪米特法则: Law of Demeter(LD)](./Design-principles/LD.md)
* [接口隔离原则: Interface Segregation Principle(ISP)](./Design-principles/ISP.md)
* [依赖倒置原则: Dependency Inversion Principle(DIP)](./Design-principles/DIP.md)
  
另外，在平时的代码设计中，还涉及到其他的四个原则：

* [DRY原则: Don't repeat yourself](./Design-principles/DRY.md)
* [YAGNI原则:  You aren't gonna need it](./Design-principles/YAGNI.md)
* [三次原则: Rule of three](./Design-principles/ROT.md)
* [合成复用原则: Composite Reuse Principle](./Design-principles/CRP.md)

### [总结](./Design-principles/summary.md)

## 三大设计模式

GoF的23种设计模式一般分为三大类

## 创建型模式

* 工厂方法模式
* 抽象工厂模式
* 单例模式
* 创建型模式
* 原型模式

## 结构型模式

* 适配器模式
* 外观模式
* 享元模式
* 组合模式
* 装饰器模式
* 代理模式
* 桥接模式

## 行为型模式

* 策略模式
* 状态模式
* 职责链模式
* 观察者模式
* 模板方法模式
* 命令模式
* 备忘录模式
* 迭代器模式
* 调停者模式
* 解释器模式
* 访问者模式
