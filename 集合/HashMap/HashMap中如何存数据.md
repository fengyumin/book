HashMap中如何存数据.md

### HashMap中如何存数据?

1. 先通过hashCode确定数组下标
- HashMap存储键值对时,会计算key的hashCode,然后做一个扰动处理得到它的hash值; 
- 然后再将这个hash值与数组长度做一个运算h & (length-1), 得到这个键值对的存储位置,即数组下标.

2. 如果这个数组位置为空,直接放到bucket里;
3. 如果这个数组位置不为空(发生了碰撞),则遍历这个位置上的链表或树,使用equals确定是否有相同的key:
- 如果有相同的key,那么更新对应的value值,并返回老的value;
- 如果无重复,则直接在链表或树最后添加结点，并返回null;

4. 如果存放时,发现碰撞导致链表过长(大于等于TREEIFY_THRESHOLD)，就把链表转换成红黑树；

5. 如果存放后,发现bucket满了(超过load factor*current capacity)，就要resize。

![](https://tva1.sinaimg.cn/large/008eGmZEgy1gmu4vvhoqjj30l20fz41q.jpg)

```
    //HashMap中get和put的使用
    Map<String, String> hashMap = new HashMap<String, String>();
    hashMap.put("name", "josan");
    String name = hashMap.get("name");
```
