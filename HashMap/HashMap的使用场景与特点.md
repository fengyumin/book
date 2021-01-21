### HashMap的使用场景与特点?

> 1. 首先HashMap是继承了Map接口, 可以用来存储键值对的
> 2. 它的键值对可以存储null
> 3. 它是线程不安全的

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
