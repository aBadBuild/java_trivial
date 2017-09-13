# 异常

> “异常情形”是指阻止当前方法或作用域继续执行的问题。

![](/assets/exception1.png)

所有异常类都是Throwable的子类，包括Error和Exception：

*  Error：指的是JVM错误，此时程序还没有运行，用户无法处理；
*  Exceprion：指的是程序运行过程中的异常，用户可以处理。

```java
异常对象.printStackTrace();//打印异常信息
```



