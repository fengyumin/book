Synchronized和Volatile有什么区别.md

### Synchronized和Volatile有什么区别?
> Java多线程之内存可见性和原子性：Synchronized和Volatile的比较

1. Synchronized：保证可见性和原子性; 
**Synchronized的内存可见性**
保证共享变量的修改能够及时可见,其实是通过Java内存模型中以下规则实现的:
- 如果对一个变量进行lock操作,则将会清空工作内存中此变量的值,在执行引擎使用这个变量前需要重新执行load或assign操作初始化变量的值
- 对一个变量unlock操作之前,必须先将此变量要同步到主内存中(执行store和write操作);

**Synchronized的原子性**
- 持有同一个锁的两个同步块只能串行地进入


***

2. Volatile：保证可见性，但不保证操作的原子性
**对volatile变量执行写操作时**
> volatile本质是在告诉JVM当前变量在寄存器中的值是不确定的，使用前，需要先从主存中读取，因此可以实现可见性。
- 在写操作后加入一条store指令，即强迫线程将最新的值刷新到主内存中;
- 在读操作时，会加入一条load指令，即强迫从主内存中读入变量的值。

**不保证volatile变量的原子性**
> 而对n=n+1,n++等操作时，volatile关键字将失效，不能起到像synchronized一样的线程同步（原子性）的效果。

```
Private int Num=0;
Num++;//Num不是原子操作
```
- Num不是原子操作，因为其可以分为：读取Num的值，将Num的值+1，写入最新的Num的值。
- 对于Num++;操作，线程1和线程2都执行一次，最后输出Num的值可能是：1或者2


3. Synchronized和Volatile的比较

- Synchronized保证内存可见性和操作的原子性; Volatile只能保证内存可见性
- Volatile不需要加锁，比Synchronized更轻量级，并不会阻塞线程（volatile不会造成线程的阻塞；synchronized可能会造成线程的阻塞。）
- volatile标记的变量不会被编译器优化,而synchronized标记的变量可以被编译器优化（如编译器重排序的优化）.
- volatile是变量修饰符，仅能用于变量，而synchronized是一个方法或块的修饰符。
> volatile关键字是一种类型修饰符，用它声明的类型变量，编译器对访问该变量的代码就不再进行优化，从而可以提供对特殊地址的稳定访问。 精确地说就是，优化器在用到这个变量时必须每次都小心地重新读取这个变量的值，而不是使用保存在寄存器里的备份。




> 参考: https://blog.csdn.net/guyuealian/article/details/52525724
> 