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

> thows关键字用于方法的声明上，指的是当方法中出现异常后交由被调用处进行处理，用于抛出已检测异常。调用了具有thows声明的方法之后，不管操作是否出现异常，都要使用try….catch来进行异常处理，如果在调用thows声明的方法的方法也有thows声明，那么无需使用try….catch也可以。如果在主方法用上了thows关键字，那么抛出的异常则交给JVM采用默认的处理方式进行处理，即输出异常信息，结束程序调用。
>
> thow关键字，可以手动抛出一个异常类的实例化对象。格式：_thow new Exception\(String异常（可自定义）\)_或者thow已存在的异常。

## 异常的捕获

一般格式：

```java
try{
 //TODO
}catch(异常类型 对象){
//异常处理
}catch(异常类型 对象){
//异常处理
}…finally{
//不管有没有异常，都要执行的语句
}
```

两点说明：

* 在使用多个catch的时候，捕获范围大的一定要放在捕获范围小的后面否则程序编译错误；
* 然捕获Exception比较方便，这样也不好，因为所有的异常都会按照同样的方式进行处理，如果在一些要求严格的项目当中，异常要分开处理会更好。

### 带资源的try（try-with-resources）语句

我们以常规的异常捕获的处理方法的时候，喜欢把关闭资源的语句写在final里面，然而，一些关闭资源的语句本身也会抛出异常，所以我们可以使用带资源的try语句。

格式例子：

```java
try(Scanner in = new Scanner(new FileInputStream("..."))){
    //TODO
}
```

当然每一个资源都属于实现了AutoCloseable接口的类：

```java
void close() throws Exception
```

### 堆栈踪迹

> 如果没有任何地方捕获异常，就会显示异常踪迹——列出异常抛出时，所有未决方法的调用信息。该信息会被送到错误消息的流System.err。

如果想存储异常的堆栈踪迹，可以像这样将其放到字符串里：

```java
ByteArrayOutPutStream out = new ByteArrayOutPutStream();
ex.printStackTrace(out);
String description = out.toString();
```

## 自定义异常

自定义异常类可以通过继承Exception或者RuntimeException来实现。可以通过构造一个传入字符串的构造方法，方法里面调用super\(传入的字符串\)，来实现对自定义错误信息的输出。

很多时候，我们可以通过创建自定义异常来规划程序当中遇到的各种情况，以及抛出自定义让方法调用的客户端来处理。

