### HashMap中equals()和hashCode()的都有什么作用？

> HashMap的很多函数要基于equal()函数和hashCode()函数。hashCode()用来定位要存放的位置，equal()用来判断是否相等。

**在put数据的过程中会用到hashCode和equals** 
1. 先通过hashCode确定数组下标
- HashMap存储键值对时,会计算key的hashCode,然后做一个扰动处理得到它的hash值; 
- 然后再将这个hash值与数组长度做一个运算h & (length-1), 得到这个键值对的存储位置,即数组下标.
2. 再遍历这个位置上的链表或树,使用equals确定是否有相同的key:
- 如果有相同的key,那么更新对应的value值,并返回老的value;
- 如果无重复,则直接在链表最后添加结点，并返回null;

**在get数据的过程中会用到hashCode和equals**
1. 先用hash函数确定在哪个位置，
2. 后遍历这个位置上对应的链表或树，使用equals比较是否相等,直到找到这个Key，然后返回value, 查找的时间复杂度分别为O(n), O(logn)


>来一篇好文，Java中==和equals的区别，equals和hashCode的区别
（1）如果两个对象根据equals()方法比较是相等的，那么调用这两个对象中任意一个对象的hashCode方法都必须产生同样的整数结果。
（2）如果两个对象根据equals()方法比较是不相等的，那么调用这两个对象中任意一个对象的hashCode方法，则不一定要产生相同的整数结果
（3）从而在集合操作的时候有如下规则：
将对象放入到集合中时，
回过来说get的时候，HashMap也先调key.hashCode()算出数组下标，然后看equals如果是true就是找到了，所以就涉及了equals。



> 参考: https://juejin.cn/post/6844904202271981581