# 静态域与静态方法

## 静态域

如果把域定义为static，每个类中只有一个这样的域。

```java
class student{
    private static int numbers = 1;
    private int id = 1;
    ...
}
```

如上面的代码所示，在student类里添加了实例域id和一个静态域numbers。每一个student实例里都有一个属于自己的id域，但是numbers域只有一个，由所有student类所共享。如果其中一个student实例对其的值进行改变，则会影响到所有的student类的实例。

## 静态常量

可以观察Math类中定义的一个静态常量：

```java
public class Math{
    ...
    public static final double PI = 3.14159265358979323846;
    ...
}
```

在程序中可以采用Math.PI的形式来获取这个常量。

如果static关键字被忽略，那么PI就变成了Math类的一个实例域，想要访问PI则需要先通过实例化Math对象来获取，而且，每个Math类的对象都拥有属于自己的PI。

