### Java集合有哪些?
> 在 Java 中除了以 Map 结尾的类之外， 其他类都实现了 Collection 接口。并且，以 Map 结尾的类都实现了 Map 接口。
- Java 集合框架主要包括两种类型的容器，一种是集合（Collection），存储一个元素集合，另一种是图（Map），存储键/值对映射。
- Collection 接口又有 3 种子类型，List、Set 和 Queue，
- 再下面是一些抽象类，最后是具体实现类，常用的有 ArrayList(线程不安全)、LinkedList、HashSet、LinkedHashSet、HashMap、LinkedHashMap 等等。
   
### 说说 List,Set,Map 三者的区别？
- List：一种有序列表的集合，例如，按索引排列的Student的List；
- Set：一种保证没有重复元素的集合，例如，所有无重复名称的Student的Set；
- Map：一种通过键值（key-value）查找的映射表集合，例如，根据Student的name查找对应Student的Map。Key 是无序的、不可重复的，value 是无序的、可重复的，每个键最多映射到一个值。

###  Arraylist 和 Vector 的区别?
ArrayList 是 List 的主要实现类，底层使用 Object[ ]存储，适用于频繁的查找工作，线程不安全 ；
Vector 是 List 的较早的实现类，底层使用 Object[ ] 存储，线程安全的。



