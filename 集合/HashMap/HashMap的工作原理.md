
### HashMap的工作原理？

一. HashMap的结构:
1. 实际是一个数组+链表的结构
2. 因为它本身是用来存储键值对的,采用Entry数组来存储键值对,每个键值对会组成一个Entry实体,Entry类实际上是一个单向的链表结构,它具有Next指针,可以连接下一个Entry实体.
3. 在JDK1.8之后, 如果链表长度大于8, 会不再使用链表,改成红黑树存储;


> 参考资料:https://yikun.github.io/2015/04/01/Java-HashMap%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86%E5%8F%8A%E5%AE%9E%E7%8E%B0/


