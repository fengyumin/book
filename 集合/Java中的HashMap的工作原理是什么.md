
> - 什么时候会使用HashMap？他有什么特点？
> - 你知道HashMap的工作原理吗？
> - 你知道get和put的原理吗？equals()和hashCode()的都有什么作用？
> - 你知道hash的实现吗？为什么要这样实现？
> - 如果HashMap的大小超过了负载因子(load factor)定义的容量，怎么办？

> 参考资料:https://yikun.github.io/2015/04/01/Java-HashMap%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86%E5%8F%8A%E5%AE%9E%E7%8E%B0/
### 什么时候会使用HashMap？他有什么特点？

```
HashMap<String, Integer> map = new HashMap<String, Integer>();
map.put("语文", 1);
map.put("数学", 2);å
map.put("英语", 3);
map.put("历史", 4);
map.put("政治", 5);
map.put("地理", 6);
map.put("生物", 7);
map.put("化学", 8);
for(Entry<String, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}
//运行结果: 政治: 5 生物: 7 历史: 4 数学: 2 化学: 8 语文: 1 英语: 3 地理: 6
```

是基于Map接口的实现，存储键值对时，它可以接收null的键值，是线程不安全的，HashMap存储着Entry(hash, key, value, next)对象。



### 你知道HashMap的工作原理吗？
HashMap采⽤Entry数组来存储key-value对，每⼀个键值对组成了⼀个Entry实体，Entry类实际上是⼀个单向的链表结构，它具有Next指针，可以连接下⼀个Entry实体。 只是在JDK1.8中，链表⻓度⼤于8的时候，链表会转成红⿊树！

- Java中的HashMap是以键值对(key-value)的形式存储元素的。
- HashMap需要一个hash函数，它使用hashCode()和equals()方法来向集合/从集合添加和检索元素。
- HashMap的一些重要的特性是它的容量(capacity)，负载因子(load factor)和扩容极限(threshold resizing)。

### 为什么使用链表+数组?
由于我们的数组的值是限制死的，我们在对key值进行散列取到下标以后，放入到数组中时，难免出现两个key值不同，但是却放入到下标相同的格子中，此时我们就可以使用链表来对其进行链式的存放。

***

### 你知道get和put的原理吗？

```
    Map<String, String> hashMap = new HashMap<String, String>();
    hashMap.put("name", "josan");
    String name = hashMap.get("name");
```
**put函数大致的思路为：**
![](https://tva1.sinaimg.cn/large/008eGmZEgy1gmu4vvhoqjj30l20fz41q.jpg)
> 当调用put()方法的时候，HashMap会计算key的hash值，然后把键值对存储在集合中合适的索引上。如果key已经存在了，value会被更新成新值。
1. 对key的hashCode()做hash运算，计算index;
2. 如果没碰撞直接放到bucket里；
3. 如果碰撞了，以链表的形式存在buckets后；
4. 如果碰撞导致链表过长(大于等于TREEIFY_THRESHOLD)，就把链表转换成红黑树；
5. 如果节点已经存在就替换old value(保证key的唯一性)
6. 如果bucket满了(超过load factor*current capacity)，就要resize。


**在理解了put之后，get就很简单了。大致思路如下：**
1. bucket里的第一个节点，直接命中；
2. 如果有冲突，则通过key.equals(k)去查找对应的entry
- 若为树，则在树中通过key.equals(k)查找，O(logn)；
- 若为链表，则在链表中通过key.equals(k)查找，O(n)。

### equals()和hashCode()的都有什么作用？
通过对key的hashCode()进行hashing，并计算下标( n-1 & hash)，从而获得buckets的位置。如果产生碰撞，则利用key.equals()方法去链表或树中去查找对应的节点



***

### 如果HashMap的大小超过了负载因子(load factor)定义的容量，怎么办？
- 在HashMap中有两个很重要的参数，容量(Capacity)和负载因子(Load factor)
- 简单的说，Capacity就是buckets的数目，Load factor就是buckets填满程度的最大比例。
- 如果对迭代性能要求很高的话不要把capacity设置过大，也不要把load factor设置过小。
- 当bucket填充的数目（即hashmap中元素的个数）大于capacity*load factor时就需要调整buckets的数目为当前的2倍。

