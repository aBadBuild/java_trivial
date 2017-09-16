# 多线程

线程是在进程的基础上进一步划分的结果，即：一个进程上可以同时创建多个线程。线程是比进程更快的处理单元，而且所占的资源也小。线程离不开进程，进程消失后线程也不存在，但线程消失进程未必消失。所有的线程和进程都是一样的，都必须轮流去抢占资源。

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

```



