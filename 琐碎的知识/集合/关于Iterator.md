# 集合\_关于Iterator

所有集合类都实现了Iterator接口，Iterator接口主要用于依此访问集合中的元素。

```java
public interface Iterator<E> {
    E next();
    boolean hasNext();
    void remove();
}
```

通过不断调用`next()`，可以逐个访问集合中的每个元素，但是当到了集合的末尾，在调用`next()`，会抛出`NoSuchElementException`。所以在调用`next()`方法前，最好先调用`hasNext()`方法，看是否存在还有下一个元素。

`next()`和`remove()`的调用是相互依赖的，在调用`remove()`之前没有调用`next()`是不合法的，会抛出`IllegalStateException`。类似于`remove(); remove();`也是不对的。

