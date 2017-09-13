# 异常

> “异常情形”是指阻止当前方法或作用域继续执行的问题。

![](/assets/exception1.png)

所有异常类都是Throwable的子类，包括Error和Exception：

* Error：指的是JVM错误，此时程序还没有运行，用户无法处理；
* Exceprion：指的是程序运行过程中的异常，用户可以处理；
* RuntimeException类，是Exception的子类，程序在编译的时候不会强制性的要求用户处理异常，应该用户没有处理异常，则交给JVM进行处理。RuntimeException的异常子类可以由用户根据需要选择进行处理。

```java
异常对象.printStackTrace();//打印异常信息
```

## 异常的捕获

一般格式：

```java
try{
 //TODO
}catch(异常类型 对象){
//异常处理
}catch(异常类型 对象){
//异常处理
}…
finally{
//不管有没有异常，都要执行的语句
}
```



