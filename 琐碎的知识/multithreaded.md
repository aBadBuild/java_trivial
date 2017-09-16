# 多线程

线程是在进程的基础上进一步划分的结果，即：一个进程上可以同时创建多个线程。线程是比进程更快的处理单元，而且所占的资源也小。线程离不开进程，进程消失后线程也不存在，但线程消失进程未必消失。所有的线程和进程都是一样的，都必须轮流去抢占资源。

> 通常的用法是，你程序中某一部分与一个特定的事件或资源联系在一起，而你又不想让这种联系阻碍程序其余部分的运行。这时，就可以创建一个与这个事件或资源相关联的线程，并且让此线程独立于主线程运行。

## 基本实现

实现多线程的两种途径：

* 继承Thread类；
* 实现Runnable接口（Callable接口）。

两者的区别：

* Thread是Runnable的子类，使用Runnable可以避免但单继承的局限；
* Runnable接口实现可以比Thread类实现多线程更加的描述数据共享的概念。

### 继承Thread类

在多线程的每个主体类中都必须覆写Thread类的run\(\)方法，该方法没有返回值，意味着线程一旦执行就要一直执行，不能返回内容。

```java
public class ExtendsThread extends Thread {
    public void run(){
        for(int i = 0; i<500; i++){
            System.out.println(i);
        }
    }
}
```

如果直接调用run\(\)方法，并不能启动多线程，想要启动多线程必须使用Thread类的star\(\)方法（调用此方法执行的方法体是run\(\)方法定义的）。

```java
public class ThreadTest {
    public static void main(String[] args) {        
        ExtendsThread thread1 = new ExtendsThread();
        ExtendsThread thread2 = new ExtendsThread();
        thread1.start();
        thread2.start();        
    }
}
//测试的结果是两个线程的数值交替打印 0 1 2 3 4 0 1 2 3 4 5
```

### 实现Runnable接口

虽然Thread可以实现多线程的主体类定义，但是他有一个问题，java具有单继承局限，为了解决这一问题，提出了该接口。与继承Thread类相比较，并没有继承到star\(\)方法，一个接口可以创建多个互不干扰的线程对象。

通过写run\(\)方法，然后实例化一个Thread对象，实例选用的构造方法为传入一个Runnable对象，如Thread thread = new Thread\(Runnable对象\)，再调用thread的star\(\)方法。

```java
public class RunnableImp implements Runnable {
    @Override
    public void run() {
        for(int i = 0; i<500; i++){
            System.out.println(i);
        }
    }
}
```

客户端的调用：

```java
public class ThreadTest {
    public static void main(String[] args) {
        new Thread(new RunnableImp()).start();
        new Thread(new RunnableImp()).start();
        //需要一个Thread对象来调用star()方法。
    }
}
```

### 实现Callable接口

执行完线程主体方法call\(\)后可以返回一个结果，而返回的结果类型由Callable接口上的泛型来决定。

```java
public class CallableImp implements Callable<Object> {    
    @Override
    public Object call() throws Exception {
        int i =0;
        for(; i<500; i++){
            System.out.println(i);
        }
        return i;
    }    
}
```

运行Callable任务可以拿到一个Future对象，表示异步计算的结果。它提供了检查计算是否完成的方法，以等待计算的完成，并检索计算的结果。通过Future对象可以了解任务执行情况，可取消任务的执行，还可获取执行结果。

```java
public class ThreadTest {
    public static void main(String[] args) throws InterruptedException, ExecutionException {        
        CallableImp ca1 = new CallableImp();
        FutureTask<Object> result1 = new FutureTask<>(ca1);

        CallableImp ca2 = new CallableImp();
        FutureTask<Object> result2 = new FutureTask<>(ca2);

        new Thread(result1).start();
        new Thread(result2).start();
        System.out.println(result1.get());//通过FutureTask的父接口Future的get()方法来获取返回的结果
        System.out.println(result2.get());        
    }
}
```

## 线程的状态

线程可以有以下6中状态：

* **New（新创建）**
  * > 当new操作符创建一个新线程时，如new Thread\(r\)，该线程还没有开始运行。
* **Runnble（可运行）**
  * > 调用star\(\)方法后线程处于该状态。在任何的给定时刻，一个可运行的线程可能出于正在运行也可能没有运行，因为抢占式的调度系统给每一个可运行线程一个时间片来执行任务。
* **Blocked（被阻塞）**
  * > 线程暂时不活动，不运行任何代码且消耗最少的资源，直到线程调度器重新激活它。  
    > 当一个线程试图获取一个内部的对象锁，而该锁被其他线程所持有，则线程进入阻塞状态。当所有其他线程释放该锁，并且线程调度器允许本线程持有它的时候，该线程将变为非阻塞状态。
* **Waiting（等待）**
  * > 线程暂时不活动，不运行任何代码且消耗最少的资源，直到线程调度器重新激活它。  
    > 当线程等待另一个线程通知调度器一个条件时，它自己进入等待状态。在调用Object.wait方法或Thread.join方法，或者是等待java.util.concurrent库中的Lock或Condition时，就会出现这种情况。
* **Timed waiting（计时等待）**
  * > 线程暂时不活动，不运行任何代码且消耗最少的资源，直到线程调度器重新激活它。  
    > 有几个方法有一个超时参数，调用它们导致线程进入计时等待状态，这一状态将一直保持到超时期满或接受到适当的通知。带有超时参数的方法有Thread.sleep和Object.wait、Thread.join、Lock.tryLock以及Condition.await的计时版。
* **Terminated（被终止）**
  * > 线程因两个原因之一而被终止：  
    > 1、因为run方法正常退出而自然死亡；  
    > 2、因为一个没有捕获的异常终止的run方法而意外死亡。  
    > 特别的是，可以调用线程的stop方法杀死一个线程。该方法抛出ThreadDeath错误对象。但是该方法已过时，不要用。

## 线程属性

### 线程的优先级

默认情况下，一个线程继承它的父线程的优先级。

可以用setPriority方法提高 或减低任何一个线程的优先级，可以将优先级设置为在MIN_PRIORITY_（在Thread定义为1）与MAXPRIORITY（定义为10）之间的任何值，NORM\_PRIORITY被定义为5。

如果有几个高优先级的线程没有进入非活动状态，第优先级的线程可能永远也不能执行。

### 守护线程

可以通过setDaemon\(true\)将线程转化为守护线程。

守护线程的用途是为其他线程提供服务。

守护线程应该永远不去访问固有资源，如文件、数据库，因为它会在任何时候甚至一个操作的中间发生中断。

当只剩下守护线程时，虚拟机就退出了，由于如果只剩下守护线程，就没有必要继续运行程序。

### 未捕获异常处理器

线程的run方法不能抛出任何被检测的异常，但是，不被检测的异常会导致线程终止。

在线程死亡之前，异常常被传递到一个用于未捕获异常的处理器。该处理器必须属于一个实现Thread.UncaughtExceptionHandler接口的类，这个接口只有一个方法：void uncaughtException\(Thread t, Throwable e\)。可以用setUncaughtExceptionHandler方法为任何线程安装一个处理器。

也可以用Thread类的静态方法setDefaultUncaughtExceptionHandler为所有线程安装一个默认的处理器。

替换处理器可以使用日志API发送未捕获异常的报告到日志文件。

如果不安装处理器，默认的处理器为空。

## 同步

在一个银行转账的场景中，用户之间的转账访问到同一对象资源时，在没有经过处理的线程可能会导致个人账户出现错误。现模拟一个多线程对同一对象修改的场景。

资源类：

```java
public class Bank {
	public static int sumMoney = 10000;	
	public void transfer(int from, int to, int number){
		if(number > 10000 || number < 0){
			System.out.println(from + "..error");
			return;
		}
		sumMoney -= number;
		sumMoney += number;
		System.out.println(from + ", "  + to + "..sum = " + sumMoney);
	}
}
```

线程类：

```java
public class TransferThread implements Runnable {    
    @Override
    public void run() {
        int money = (int)(Bank.sumMoney * Math.random());
        new Bank().transfer(money, money, money);
    }
}
```

测试类：

```java
public class SynchronizationTest {
    public static void main(String[] args) {        
        for(int i = 0; i < 50; i++){
            new Thread(new TransferThread()).start();
        }        
    }
}
```



