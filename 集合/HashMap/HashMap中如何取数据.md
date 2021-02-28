HashMap中如何取数据.md

### HashMap中如何取数据?

1. 先用hash函数确定在哪个位置，
2. 后遍历这个位置上对应的链表或树，使用equals比较是否相等,直到找到这个Key，然后返回value, 查找的时间复杂度分别为O(n), O(logn).

![](https://tva1.sinaimg.cn/large/008eGmZEgy1gmu4vvhoqjj30l20fz41q.jpg)

```
    //HashMap中get和put的使用
    Map<String, String> hashMap = new HashMap<String, String>();
    hashMap.put("name", "josan");
    String name = hashMap.get("name");
```

