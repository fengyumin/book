synchronized的使用场景.md

### synchronized的使用场景?

1. 多线程同时读写共享变量时，可能会出现线程不安全的情况,这时需要通过加锁的方式实现原子操作; 
2. 加锁的方式有乐观锁和悲观锁: 并发量高的情况下使用synchronized, 并发量低的情况下可使用乐观锁CAS操作;
3. 如果是JVM中已经定义的原子操作则不需要加锁:
- 基本类型（long和double除外）赋值 
> long和double是64位数据，JVM没有明确规定64位赋值操作是不是一个原子操作，不过在x64平台的JVM是把long和double的赋值作为原子操作实现的。
- 引用类型赋值
```
//基本类型赋值的原子操作
int n = m；

//引用类型赋值的原子操作
List<String> list = anotherList。

String a = "ss";
```





> 参考资料:
> https://www.liaoxuefeng.com/wiki/1252599548343744/1306580844806178