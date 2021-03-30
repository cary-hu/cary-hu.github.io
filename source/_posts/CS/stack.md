---
title: stack
date: 2021-03-30 21:17:01
categories: [CS, stack]
---
聊聊老生常谈的栈
<!-- more-->

堆栈在计算机科学学科中是重要的数据结构，今天我们就来聊聊栈在计算机中的应用。

## 定义

栈：一种先进后出的数据结构

什么叫先进后出呢，打个比方：

现在有一个空桶，你需要将一摞与桶口径大小相同的盘子，放到桶里，以常理来讲，我们需要将这些盘子按照顺序，一个一个的放入桶中摞起来，取出的时候也需要从上到下，依次取出。

而这个桶，就是我们今天要聊的数据结构：栈，而放入盘子和取出盘子，分别对应了栈的两个基础操作：push、pop，同样的，这两个操作，也只能通过栈顶来进行操作。

关于栈，还有以下几个基础定义：
    - 栈顶：允许进行操作的一端，相当于例子中桶顶
    - push: 进栈，栈的基础操作，可以将元素放置在栈的顶部，相当于将盘子放入桶的顶端
    - pop：出栈，栈的基础操作，可以将元素从栈顶取出，相当于从桶中取出一个盘子

## 计算机中的应用

关于计算机中的应用，在这里可以举几个例子：

1. C#中变量的内存分配

在C#中，通过某种方式声明变量的时候：
```c#
int a = 6;
int b = 10;
```
这时，系统会按照变量的声明顺序，将他们压入栈中。
当代码块执行结束之后，按照栈先进后出的原则，系统会按照出栈顺序分别对内存进行回收。

2. 多项式的计算

给定一个多项式：[3*(5+1)]/5。

如果按照人的思维，进行这个多项式计算是一件很简单的事情，而计算机程序则需要借用到今天我们聊到的栈。

开始计算的时候，计算机程序从左至右按照字符读入这个多项式，
当遇到右括号((、[)的时候计算机会将当前字符压入栈中，
当遇到左括号()、])的时候计算机会将当前字符与栈顶元素进行比较，观察是否匹配，
如果匹配，则将当前括号中的式子进行计算。

## 一个简单实现

```c++
#pragma once
#ifndef MYSTACK_H
#define MYSTACK_H
#include <iostream>
using namespace std;

template <typename T>
class MyStack
{
public:
	MyStack(int size);
	~MyStack();
	bool stackEmpty();
	bool stackFull();
	void clearStack();
	int stackLength();
	void push(T element);
	T pop();
	T top();
	void stackTraverse();
private:
	T* m_pBuffer;
	int m_iSize;
	int m_iTop;
};

template <typename T> MyStack<T>::MyStack(int size)
{
	m_iSize = size;
	m_pBuffer = new T[size];
	m_iTop = 0;
}

template <typename T> MyStack<T>::~MyStack()
{
	delete[]m_pBuffer;
}

template <typename T> bool MyStack<T>::stackEmpty()
{
	return m_iTop == 0;
}

template <typename T> bool MyStack<T>::stackFull()
{
	return m_iTop == m_iSize;
}

template <typename T> void MyStack<T>::clearStack()
{
	m_iTop = 0;
}

template <typename T> int MyStack<T>::stackLength()
{
	return m_iTop;
}

template <typename T> void MyStack<T>::push(T element)
{
	if (stackFull())
	{
		cout << "The Stack is Full! Please Pop Something Before You Push Something." << endl;
		return;
	}
	m_pBuffer[m_iTop++] = element;
}
template <typename T> T MyStack<T>::pop()
{
	if (stackEmpty())
	{
		cout << "The Stack is Empty! Please Push Something Before You Pop Something." << endl;
		return NULL;
	}
	return m_pBuffer[--m_iTop];
}
template <typename T> T MyStack<T>::top()
{
	if (stackEmpty())
	{
		cout << "The Stack is Empty! Please Push Something." << endl;
		return NULL;
	}
	int currentTop = m_iTop - 1;
	return m_pBuffer[currentTop];
}
template <typename T> void MyStack<T>::stackTraverse()
{
	for (int i = 0; i < m_iTop; i++)
	{
		cout << m_pBuffer[i] << endl;
	}
}
#endif // !MYSTACK_H

```
