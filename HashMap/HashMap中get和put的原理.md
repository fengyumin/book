### HashMap中get和put的原理？

> 一、put函数
> 1. 

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

