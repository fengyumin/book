
### 如果HashMap的大小超过了负载因子(load factor)定义的容量，怎么办？

- 在HashMap中有两个很重要的参数，容量(Capacity)和负载因子(Load factor)
- 简单的说，Capacity就是buckets的数目，Load factor就是buckets填满程度的最大比例。
- 如果对迭代性能要求很高的话不要把capacity设置过大，也不要把load factor设置过小。
- 当bucket填充的数目（即hashmap中元素的个数）大于capacity*load factor时就需要调整buckets的数目为当前的2倍。


- HashMap的一些重要的特性是它的容量(capacity)，负载因子(load factor)和扩容极限(threshold resizing)。