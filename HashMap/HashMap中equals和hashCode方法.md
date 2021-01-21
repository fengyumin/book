### HashMap中equals()和hashCode()的都有什么作用？

> 1. 一个是用来存储, 一个是用来查找

1. 通过对key的hashCode()进行hashing，并计算下标( n-1 & hash)，从而获得buckets的位置。
2. 如果产生碰撞，则利用key.equals()方法去链表或树中去查找对应的节点

