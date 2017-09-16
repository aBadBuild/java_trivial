# 多线程

线程是在进程的基础上进一步划分的结果，即：一个进程上可以同时创建多个线程。线程是比进程更快的处理单元，而且所占的资源也小。线程离不开进程，进程消失后线程也不存在，但线程消失进程未必消失。所有的线程和进程都是一样的，都必须轮流去抢占资源。

## 基本实现

实现多线程的两种途径：

* 继承Thread类；
* 实现Runnable接口（Callable接口）。

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
public class threadTest {
	public static void main(String[] args) {		
		ExtendsThread thread1 = new ExtendsThread();
		ExtendsThread thread2 = new ExtendsThread();
		thread1.start();
		thread2.start();		
	}
}
```



