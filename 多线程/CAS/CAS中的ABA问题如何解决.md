
### CAS中的ABA问题如何解决?

> 思路: 增加一个版本号存储,每次操作时提升一个版本号.A——>B——>A问题就变成了1A——>2B——>3A


1. JDK提供的AtomicStampedReference和AtomicMarkableReference类。
2. atomicStampedReference类中维护了一个Pair对象,Pair对象中存储了对象引用和一个stamp值,每次CAS操作时,会检查对象引用和stamp值,只有全部相等时才更新值




> 参考:https://www.zhihu.com/question/39130725