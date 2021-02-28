synchronized修饰实例方法和静态方法时锁对象分别是什么.md

### synchronized修饰实例方法和静态方法时,锁对象分别是什么?

> 用synchronized修饰方法可以把整个方法变为同步代码块，synchronized方法加锁对象是this；


1. 用synchronized修饰的方法就是同步方法，它表示整个方法都必须用this实例加锁
```
public void add(int n) {
    synchronized(this) { // 锁住this
        count += n;
    } // 解锁
}

//等价于
public synchronized void add(int n) { // 锁住this
    count += n;
} // 解锁
```

2. 对一个静态方法添加synchronized修饰符: 对于static方法，是没有this实例的，因为static方法是针对类而不是实例。但是我们注意到任何一个类都有一个由JVM自动创建的Class实例，因此，对static方法添加synchronized，锁住的是该类的Class实例。
```
public class Counter {
    public synchronized static void test(int n) {
        ...
    }
」
//等价于
public class Counter {
    public static void test(int n) {
        synchronized(Counter.class) {
            ...
        }
    }
}
```



> 参考资料:
> https://www.liaoxuefeng.com/wiki/1252599548343744/1306580844806178
