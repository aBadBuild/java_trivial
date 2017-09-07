# 接口

定义接口使用interface关键字完成，接口类里只有抽象方法和全局常量。在整个Java里面，接口的主要功能是解决单继承局限问题。

## 基本概念

由于接口里面存在有抽象方法，所以接口对象不可能直接使用关键字new实例化操作：

1. 接口必须要有子类，一个子类可以使用implements关键字实现多个接口，接口与接口之间可以通过子类的实例化对象向下转型进行转换；
2. 接口的子类（如果不是抽象类），必须覆写接口中的全部抽象方法；
3. 接口对象可以利用子类对象向上转型进行实例化操作。

如果接口子类需要继承其他类时，先写extends，再写implements。

接口里面的抽象方和全局常量就算不用public abstract和public static final来修饰，也没事，最终的访问权限也是public。但是定义方法的时候一定要写上public。

一个接口可以使用extends关键字同时继承多个接口，当时不能继承抽象类。

可以在接口内用static关键字再定义接口类，而该类属于外部接口，我们要用到这个外部接口的做法是implements a.b，b就是外部接口。

## 接口与回调

回调是一种常见的设计模式，在该模式中，可以指定某个特定事件发生时应该采取的动作。

以下以一个例子来说明：

员工把活干完的时候，告诉老板，老板知道后对此进行做出回应。

首先是定义一个接口，是员工找到老板的接口，其中接口中有一个方法，是员工做完工作后，告诉老板用的

```java
public interface ToDoInterface {
    public void toDo();//员工工作做完后通过这个告诉老板
}
```

然后是老板对员工做完工作后的回应，通过实现这个接口

```java
public class BossImp implements ToDoInterface{
    @Override
    public void toDo() {//老板的回应
        System.out.println("继续工作吧你");
    }    
}
```

然后是员工，员工完成工作后，告诉老板

```java
public class Worker {    
    public void finishWork(ToDoInterface toDoInterface){
        System.out.println("员工工作完成");
        toDoInterface.toDo();//工作完成，告诉老板
    }    
}
```

测试类的调用

```java
new Worker().finishWork(new BossImp());
//员工工作完成
//继续工作吧你
```



