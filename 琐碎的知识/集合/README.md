# 集合

Collection接口是集合类的根接口，Java中没有提供这个接口的直接的实现类。但是却让其被继承产生了两个接口，就是Set和List。Set中不能包含重复的元素。List是一个有序的集合，可以包含重复的元素，提供了按索引访问的方式。

Map是Java.util包中的另一个接口，它和Collection接口没有关系，是相互独立的，但是都属于集合类的一部分。Map包含了key-value对。Map不能包含重复的key，但是可以包含相同的value。

Iterator，所有的集合类都实现了Iterator接口，这是一个用于遍历集合中元素的接口，主要包含以下三种方法：

1. `hasNext()`是否还有下一个元素。
2. `next()`返回下一个元素。
3. `remove()`删除当前元素。

![](/assets/aggregate.png)![](/assets/specific_aggregate.png)

