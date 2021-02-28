
### CAS中CPU消耗高的问题如何解决?

> 如果是 JDK8，推荐使用 LongAdder 对象，比 AtomicLong 性能更好(减少乐观锁的重试次数)。


**使用AtomicLong时:**
1. 在高并发下大量线程会同时去竞争更新同一个原子变量，
2. 但是由于同时只有一个线程的CAS会成功，
3. 所以其他线程会不断尝试自旋尝试CAS操作，这会浪费不少的CPU资源。

**而LongAdder可以概括成这样：**
1. 高并发时前者将对单一变量的CAS操作分散为对数组cells中多个元素的CAS操作，取值时进行求和
2. 而在并发较低时仅对base变量进行CAS操作，与AtomicLong类原理相同。


>作者：海涛_meteor
链接：https://www.jianshu.com/p/ec045c38ef0c
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

>作者：Java3y
链接：https://www.zhihu.com/question/39130725/answer/1006948362
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。>