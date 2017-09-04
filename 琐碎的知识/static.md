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

如上面的代码所示，在student类里添加了实例域id和一个静态域numbers。每一个student实例里都有一个属于自己的id域，但是numbers域只有一个，由所有student类所共享。

