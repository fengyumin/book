### synchronized的用法?

> - 同步的本质就是给指定对象加锁，加锁后才能继续执行后续代码；
> - 注意加锁对象必须是同一个实例；

1. 找出修改共享变量的线程代码块；
2. 选择一个共享实例作为锁；
3. 使用synchronized(lockObject) { ... }。


1. 修饰代码块
2. 修饰方法(实例方法或者静态方法)
3. 修饰类

> todo

