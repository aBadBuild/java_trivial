# 大数值

如果基本的整数和浮点数精度不能满足需求，那么可以使用java.math包下的两个类：BigInteger和BigDecimal。

使用静态方法valueOf将普通数值转换为大数值：

```java
BigInteger a = BigInteger.valueOf(100);
```

当时大数值不能使用算术运算符进行运算，而是使用大数值里面的方法进行运算，例如：

```java
BigInteger c = b.add(a); // c = b + a
BigInteger d = c.multiply(b.add(BigInteger.valueOf(100))); // d = c * (b + 100)
```



