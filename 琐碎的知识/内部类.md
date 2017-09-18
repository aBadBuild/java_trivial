# 内部类

内部类是定义在另一个类中的类，而为什么需要使用内部类：

1. 内部类方法可以访问该类定义所在的作用域中的数据，包括私有的数据；
2. 内部类可以对同一个包中的其他类隐藏起来；
3. 当想要定义一个回调函数且不想编写大量代码时，使用匿名内部类比较便捷。

## 内部类的访问对象状态

内部类的对象总有一个隐式引用，它指向了创建它的外部类对象，称为outer，我们可以使用_outer._ 来引用外围类对象的域。

outer并不是关键字。

外围类的引用在构造器中设置，如果没有内部类没有定义构造方法，那么编译器会为这个类生成一个默认的构造器：

```java
public 内部类(外围类 外围类对象){
    outer = 外围类对象;
}
```

在访问外围类的private的对象时，无需调用外围类的get方法，或者外围类也无需写get方法，直接调用即可。

然而在这样的一种情况，当多个内部类嵌套时，即内部类中还有内部类时，outer就不好用了，最好的引用方式为_OuterClass.this._

```java
public class User {//外围类
        private String name = "yu";

        public void printName(){
            GetName getName = new GetName();
            System.out.print(getName.printName());
        }

        public class GetName{//内部类
            public String printName(){
                return User.this.name;
            }
        }
    }
```

在外围类的的作用域之外，可以这样引用内部类：

```java
User.GetName un = new User().new GetName();
```

## 局部内部类

类似于这种情况，该内部类只被一个方法所调用，可以使用局部内部类：

```java
public class User {//外围类
        private String name = "yu";

        public void printName(){//方法
            class GetName{//方法里的局部类
                public String printName(){
                    System.out.print(User.this.name);
                    return User.this.name;
                }
            }
            GetName getName = new GetName();
            System.out.print(getName.printName());
        }
    }
```

局部类不能使用public或private进行声明。

局部类对外部隐藏，即使是外围类也无法对其进行访问。

## 静态内部类

不能生成它的外围类对象。

外部访问静态内部类：

```java
User.GetInner ui = new User.GetInner();
```

在内部类不需要访问外围类对象的时候，应该使用静态内部类。

声明在接口中的内部类自动成为static和public类。

