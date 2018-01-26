# 集合\_关于Iterator

所有集合类都实现了Iterator接口，Iterator接口主要用于依此访问集合中的元素。

```java
public interface Iterator<E> {
    E next();
    boolean hasNext();
    void remove();
}
```

集合通过`iterator()`来获取迭代器。

通过不断调用`next()`，可以逐个访问集合中的每个元素，但是当到了集合的末尾，在调用`next()`，会抛出`NoSuchElementException`。所以在调用`next()`前，最好先调用`hasNext()`，看是否存在还有下一个元素。

`next()`和`remove()`的调用是相互依赖的，在调用`remove()`之前没有调用`next()`是不合法的，会抛出`IllegalStateException`。类似于`remove(); remove();`也是不对的。

## ListIterator

专用于List接口的迭代器，即List接口实现了该接口。

![](/assets/ListIteratorAPI.png)

