Iterator和ListIterator的区别是什么.md

### Iterator和ListIterator的区别是什么？

1. Iterator可用来遍历Set和List集合，但是ListIterator只能用来遍历List。
2. Iterator对集合只能是前向遍历，ListIterator既可以前向也可以后向。
3. ListIterator实现了Iterator接口，并包含其他的功能，比如：增加元素，替换元素，获取前一个和后一个元素的索引，等等。

```
// Here "c" is any Collection object. itr is of type Iterator interface and refers to "c"
Iterator itr = c.iterator();

// Here "l" is any List object, ltr is of type ListIterator interface and refers to "l"
ListIterator ltr = l.listIterator();

```

```
//Iterator接口
public interface Iterator<E> {
    boolean hasNext();
    E next();
    void remove();
}

//ListIterator接口
public interface ListIterator<E> extends Iterator<E> {
    //继承自Iterator的接口
    boolean hasNext();         //后面是否有元素
    E next();                  //游标向后移的，取得后面的元素
    void remove();             //刪除最后一个返回的元素

    //ListIterator新增的接口
    boolean hasPrevious();     //前面是否有元素
    E previous();              //游标往前移动，取得前面的元素
    int previousIndex();       //获取前一个元素的索引
    int nextIndex();           //获取后一个元素的索引
    void set(E e);             //替换元素
    void add(E e);             //增加元素
}
```

Iterator<E>
- hasNext(): boolean
- next(): E
- remove(): void

ListIterator<E
- hasNext(): boolean
- next(): E
- remove(): void
2. Iterator对集合只能是前向遍历，ListIterator既可以前向也可以后向。
- hasPrevious():boolean  
3. 获取前一个和后一个元素的索引
- nextIndex():int
- previousIndex():int 
4. 增加元素，替换元素
- set(E): void
- add(E): void


