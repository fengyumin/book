### ArrayList和LinkedList有什么区别?

1.ArrayList是实现了基于动态数组的数据结构，LinkedList基于链表的数据结构。
2.对于随机访问get和set，ArrayList绝对优于LinkedList，因为LinkedList要移动指针。
3.对于新增和删除操作add和remove，LinedList比较占优势，因为ArrayList要移动数据。
>但是实际情况并非这样，对于新增或删除，LinkedList和ArrayList并不能明确说明谁快谁慢

**改查**
- ArrayList的所有数据是在同一个地址上,而LinkedList的每个数据都拥有自己的地址.
- 所以在对数据进行查找的时候，由于LinkedList的每个数据地址不一样，get数据的时候ArrayList的速度会优于LinkedList，
- 而更新数据的时候，虽然都是通过循环循环到指定节点修改数据，但LinkedList的查询速度已经是慢的，而且对于LinkedList而言，更新数据时不像ArrayList只需要找到对应下标更新就好，LinkedList需要修改指针，速率不言而喻

> - 从源码可以看出，ArrayList想要get(int index)元素时，直接返回index位置上的元素，
> - 而LinkedList需要通过for循环进行查找，虽然LinkedList已经在查找方法上做了优化，比如index < size / 2，则从左边开始查找，反之从右边开始查找，但是还是比ArrayList要慢。这点是毋庸置疑的。

```
//ArrayList: 获取index位置的元素值
public E get(int index) {
    rangeCheck(index); //首先判断index的范围是否合法

    return elementData(index);
}

//LinkedList: 获得第index个节点的值
public E get(int index) {
    checkElementIndex(index);
    return node(index).item;
}

//定位index处的节点
Node<E> node(int index) {
    // assert isElementIndex(index);
    //index<size/2时，从头开始找
    if (index < (size >> 1)) {
        Node<E> x = first;
        for (int i = 0; i < index; i++)
            x = x.next;
        return x;
    } else { //index>=size/2时，从尾开始找
        Node<E> x = last;
        for (int i = size - 1; i > index; i--)
            x = x.prev;
        return x;
    }
}
```




**增删**
对于数据的增加元素，ArrayList是通过移动该元素之后的元素位置，其后元素位置全部+1，所以耗时较长，而LinkedList只需要将该元素前的后续指针指向该元素并将该元素的后续指针指向之后的元素即可。与增加相同，删除元素时ArrayList需要将被删除元素之后的元素位置-1，而LinkedList只需要将之后的元素前置指针指向前一元素，前一元素的指针指向后一元素即可。当然，事实上，若是单一元素的增删，尤其是在List末端增删一个元素，二者效率不相上下。

> - ArrayList想要在指定位置插入或删除元素时，主要耗时的是System.arraycopy动作，会移动index后面所有的元素；
> - LinkedList主耗时的是要先通过for循环找到index，然后直接插入或删除。这就导致了两者并非一定谁快谁慢，下面通过一个测试程序来测试一下两者插入的速度：

```
//将index位置的值设为element，并返回原来的值
public E set(int index, E element) {
    rangeCheck(index);
 
    E oldValue = elementData(index);
    elementData[index] = element;
    return oldValue;
}
 
//将element添加到ArrayList的指定位置
public void add(int index, E element) {
    rangeCheckForAdd(index);
 
    ensureCapacityInternal(size + 1);  // Increments modCount!!
    //将index以及index之后的数据复制到index+1的位置往后，即从index开始向后挪了一位
    System.arraycopy(elementData, index, elementData, index + 1,
                     size - index); 
    elementData[index] = element; //然后在index处插入element
    size++;
}
 
//删除ArrayList指定位置的元素
public E remove(int index) {
    rangeCheck(index);
 
    modCount++;
    E oldValue = elementData(index);
 
    int numMoved = size - index - 1;
    if (numMoved > 0)
        //向左挪一位，index位置原来的数据已经被覆盖了
        System.arraycopy(elementData, index+1, elementData, index,
                         numMoved);
    //多出来的最后一位删掉
    elementData[--size] = null; // clear to let GC do its work
 
    return oldValue;
}
```

```

 
//设置第index元素的值
public E set(int index, E element) {
    checkElementIndex(index);
    Node<E> x = node(index);
    E oldVal = x.item;
    x.item = element;
    return oldVal;
}
 
//在index个节点之前添加新的节点
public void add(int index, E element) {
    checkPositionIndex(index);
 
    if (index == size)
        linkLast(element);
    else
        linkBefore(element, node(index));
}
 
//删除第index个节点
public E remove(int index) {
    checkElementIndex(index);
    return unlink(node(index));
}

```

> 参考zi