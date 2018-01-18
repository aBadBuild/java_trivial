# 集合\_关于Iterator

所有集合类都实现了Iterator接口，Iterator接口主要用于依此访问集合中的元素。

```java
public interface Iterator<E> {
    E next();
    boolean hasNext();
    void remove();
}
```



