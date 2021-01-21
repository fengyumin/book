
### HashMap的工作原理？

> 1. 实际是一个数组+链表的结构
> 2. 在JDK1.8之后, 如果链表长度大于8, 会不再使用链表,改成红黑树存储;
> 3. 因为它本身是用来存储键值对的,每个键值对会组成一个Entry实体,这个实体就是一个单向链表,具有Next指针,可以连接下一个Entry实体.

> 参考资料:https://yikun.github.io/2015/04/01/Java-HashMap%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86%E5%8F%8A%E5%AE%9E%E7%8E%B0/

HashMap采⽤Entry数组来存储key-value对，每⼀个键值对组成了⼀个Entry实体，Entry类实际上是⼀个单向的链表结构，它具有Next指针，可以连接下⼀个Entry实体。 只是在JDK1.8中，链表⻓度⼤于8的时候，链表会转成红⿊树！

- HashMap的一些重要的特性是它的容量(capacity)，负载因子(load factor)和扩容极限(threshold resizing)。