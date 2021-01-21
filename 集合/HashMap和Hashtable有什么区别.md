### HashMap和Hashtable有什么区别?

> ? HashMap提供了可供应用迭代的键的集合，因此，HashMap是快速失败的。另一方面，Hashtable提供了对键的列举(Enumeration)。


**共有API**
1. HashMap和Hashtable都实现了Map接口，所以从公开的方法上来看，这两个类提供的，是一样的功能。都提供键值映射的服务，可以增、删、查、改键值对，可以对键、值、键值对提供遍历视图。支持浅拷贝，支持序列化。



**使用ConcurrentHashMap替代HashTable**
- 如果你不需要线程安全，那么使用HashMap，
- 如果需要线程安全，那么使用ConcurrentHashMap。HashTable已经被淘汰了，不要在新的代码中再使用它。


**线程安全性**
- 我们说HashTable是同步的，HashMap不是，也就是说HashTable在多线程使用的情况下，不需要做额外的同步. 
- HashTable是怎么做到的呢？就是公开的方法比如get都使用了synchronized描述符。而遍历视图比如keySet都使用了Collections.synchronizedXXX进行了同步包装。

```
//以下代码及注释来自java.util.HashTable

public synchronized V get(Object key) {
    Entry tab[] = table;
    int hash = hash(key);
    int index = (hash & 0x7FFFFFFF) % tab.length;
    for (Entry<K,V> e = tab[index] ; e != null ; e = e.next) {
        if ((e.hash == hash) && e.key.equals(key)) {
            return e.value;
        }
    }
    return null;
}

public Set<K> keySet() {
    if (keySet == null)
        keySet = Collections.synchronizedSet(new KeySet(), this);
    return keySet;
}
```


**Null Key & Null Value**
1. HashMap是支持null键和null值的，而HashTable在遇到null时，会抛出NullPointerException异常。
2. 因为HashMap在实现时对null做了特殊处理，将null的hashCode值定为了0，从而将其存放在哈希表的第0个bucket中。
3. 我们一put方法为例，看一看代码的细节：
```
//以下代码及注释来自java.util.HashTable

public synchronized V put(K key, V value) {

    // 如果value为null，抛出NullPointerException
    if (value == null) {
        throw new NullPointerException();
    }

    // 如果key为null，在调用key.hashCode()时抛出NullPointerException

    // ...
}

//以下代码及注释来自java.util.HasMap

public V put(K key, V value) {
    if (table == EMPTY_TABLE) {
        inflateTable(threshold);
    }
    // 当key为null时，调用putForNullKey特殊处理
    if (key == null)
        return putForNullKey(value);
    // ...
}

private V putForNullKey(V value) {
    // key为null时，放到table[0]也就是第0个bucket中
    for (Entry<K,V> e = table[0]; e != null; e = e.next) {
        if (e.key == null) {
            V oldValue = e.value;
            e.value = value;
            e.recordAccess(this);
            return oldValue;
        }
    }
    modCount++;
    addEntry(0, null, value, 0);
    return null;
}

```


> 参考资料:https://www.cnblogs.com/xinzhao/p/5644175.html