
### CAS是什么?

全称是compare and swap, 比较并交换, 是更新数据的一种方式.也属于乐观锁类型;

> 背景: 共享变量存放在主内存中,工作内存中会保留共享变量的一份副本;

1.乐观锁认为更新数据时有很多线程来抢夺资源;
2.所以CAS每次更新数据前,会对比主内存和副本中的值是否相同;
- 如果相同,直接更新工作内存中值,再同步回主内存中;
- 如果不相同,先将主内存中的值同步到工作内存的副本中, 再更新工作内存中值,最后再同步回主内存中;
3. 以上操作是原子性的.所以CAS机制可以解决多线程并发编程对共享变量读写的原子性问题





> 参考: https://www.cnblogs.com/54chensongxia/p/12160085.html#3823243204
> https://www.zhihu.com/question/39130725
