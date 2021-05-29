---
title: Observer
date: 2021-05-29 09:52:52
categories: 设计模式
modified: 2021-05-29 19:41:37
---

在对象中定义一对多的依赖，这样一来，当一个对象状态发生改变，依赖他的所有对象状态都会被更新

<!--more -->

简单的来说，就是需要有一个可以通知其他人的地方，这个地方就叫订阅者，被通知的人就是观察者。

举个例子，邮局送报，邮局就是订阅者，而拿到报纸的那些人就是观察者，他们告诉了邮局，有新报纸，就给他们送。

一个简单的实现：

```csharp
public class Subject
{
    private List<Observer> observers = new List<Observer>();
    public void CallAllObservers()
    {
        notifyAllObservers();

    }
    public void notifyAllObservers()
    {
        foreach (var observer in observers)
        {
            observer.Update();
        }
    }
    public void Regisiter(Observer observer)
    {
        observers.Add(observer);
    }
}
public abstract class Observer
{
    protected Subject Subject;
    public abstract void Update();
}

public class Angel : Observer
{
    public Angel(Subject subject)
    {
        this.Subject = subject;
        this.Subject.Regisiter(this);
    }
    public override void Update()
    {
        Console.WriteLine("Don't Do It!, I'm Angle");
    }
}
public class Devil : Observer
{
    public Devil(Subject subject)
    {
        this.Subject = subject;
        this.Subject.Regisiter(this);
    }
    public override void Update()
    {
        Console.WriteLine("Do It!, I'm Devil");
    }
}
```

C#官方也对观察者模式进行了实现，利用C#的官方实现，对以上例子进行重写：

```csharp
public class Subject : IObservable<int>
{
    List<IObserver<int>> observers = new List<IObserver<int>>();
    public IDisposable Subscribe(IObserver<int> observer)
    {
        observers.Add(observer);
        return new UnSubscribe(this.observers, observer);
    }
    private class UnSubscribe : IDisposable
    {
        List<IObserver<int>> _observers;
        IObserver<int> _observer;
        public UnSubscribe(List<IObserver<int>> observers, IObserver<int> observer)
        {
            _observers = observers;
            _observer = observer;
        }
        public void Dispose()
        {
            if(_observers != null)
            {
                _observers.Remove(_observer);
            }
        }
    }
    private void NotifyAll(int state)
    {
        foreach (var observer in observers)
        {
            
            observer.OnNext(state);
        }
    }
    public void ReciveNewData(int state)
    {
        NotifyAll(state);
    }
}

public abstract class ObserverBase : IObserver<int>
{
    public virtual void OnCompleted()
    {
    }

    public virtual void OnError(Exception error)
    {
    }

    public abstract void OnNext(int value);
}

public class Angel : ObserverBase
{
    public override void OnNext(int value)
    {
        Console.WriteLine("Don't Do It!, I'm Angle");
    }
}
public class Devil : ObserverBase
{
    public override void OnNext(int value)
    {
        Console.WriteLine("Do It!, I'm Devil");
    }
}
```

观察者模式能让类与类之间的耦合关系变松，订阅者不需要知道观察者的细节，只需要知道观察者实现的接口即可，之后会在MVC上再试试观察者模式，一定会有新体验，hh
