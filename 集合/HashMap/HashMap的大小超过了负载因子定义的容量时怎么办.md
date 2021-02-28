
### HashMap的大小超过了负载因子(load factor)定义的容量时，怎么办？

- 在HashMap中有两个很重要的参数，容量(Capacity)和负载因子(Load factor)
- 简单的说，Capacity就是buckets的数目，Load factor就是buckets填满程度的最大比例。
- 当bucket填充的数目（即hashmap中元素的个数）大于扩容极限threshold (= capacity*load factor)时就需要调整buckets的数目为当前的2倍。
- 如果对迭代性能要求很高的话不要把capacity设置过大，也不要把load factor设置过小。



> **bucket** :当系统开始初始化HashMap 时，系统会创建一个长度为capacity 的Entry 数组，这个数组里可以存储元素的位置被称为“桶（bucket）”，每个bucket 都有其指定索引，系统可以根据其索引快速访问该bucket里存储的元素。

