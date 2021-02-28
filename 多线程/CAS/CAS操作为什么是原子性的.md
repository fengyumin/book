
### CAS操作为什么是原子性的?

JDK8中,原子变量类在java.util.concurrent.atomic包下，总体来看有这么多个：

1. 基本类型：AtomicBoolean：布尔型AtomicInteger：整型AtomicLong：长整型
2. 数组：AtomicIntegerArray：数组里的整型AtomicLongArray：数组里的长整型AtomicReferenceArray：数组里的引用类型
3. 引用类型：AtomicReference：引用类型AtomicStampedReference：带有版本号的引用类型AtomicMarkableReference：带有标记位的引用类型
4. 对象的属性：AtomicIntegerFieldUpdater：对象的属性是整型AtomicLongFieldUpdater：对象的属性是长整型AtomicReferenceFieldUpdater：对象的属性是引用类型

JDK8新增DoubleAccumulator、LongAccumulator、DoubleAdder、LongAdder是对AtomicLong等类的改进。比如LongAccumulator与LongAdder在高并发环境下比AtomicLong更高效。

**Atomic包里的类基本都是使用Unsafe实现的包装类。**
从原理上概述就是：
1. Atomic包的类的实现绝大调用Unsafe的方法，
2. 而Unsafe底层实际上是调用C代码，
3. C代码调用汇编，最后生成出一条CPU指令cmpxchg，完成操作。
> 这也就为啥CAS是原子性的，因为它是一条CPU指令，不会被打断。





> 作者：Java3y
链接：https://www.zhihu.com/question/39130725/answer/1006948362
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

