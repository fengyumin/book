Iterator是什么有什么特点.md

### Iterator是什么?有什么特点?


1. Iterator是一种抽象的数据访问模型。
> 　　迭代器是一种设计模式，它是一个对象，它可以遍历并选择序列中的对象，而开发人员不需要了解该序列的底层结构。迭代器通常被称为“轻量级”对象，因为创建它的代价小。



2. 使用Iterator模式进行迭代的好处有：
- 调用方总是以统一的方式遍历各种集合类型，而不必关系它们内部的存储结构。
- 集合类返回的Iterator对象知道如何迭代。(Java提供了标准的迭代器模型，即集合类实现java.util.Iterable接口，返回java.util.Iterator实例。)


3. Java中的Iterator功能比较简单，并且只能单向移动：
- 使用方法iterator()要求容器返回一个Iterator。第一次调用Iterator的next()方法时，它返回序列的第一个元素。注意：iterator()方法是java.lang.Iterable接口,被Collection继承。
- 使用next()获得序列中的下一个元素。
- 使用hasNext()检查序列中是否还有元素。
- 用remove()将迭代器新返回的元素删除。

5. Iterator 和 ListIterator 有什么区别
　Iterator是Java迭代器最简单的实现，为List设计的ListIterator具有更多的功能，它可以从两个方向遍历List，也可以从List中插入和删除元素。

4. Iterator的基本用法
```
 list l = new ArrayList();
 l.add("aa");
 l.add("bb");
 l.add("cc");
 for (Iterator iter = l.iterator(); iter.hasNext();) {
    String str = (String)iter.next();
    System.out.println(str);
 }

Iterator iter = l.iterator();
while(iter.hasNext()){
    String str = (String) iter.next();
    System.out.println(str);
}
```

5. 例1
```
List<String> list = List.of("Apple", "Orange", "Pear");
for (String s : list) {
    System.out.println(s);
}
```

实际上，Java编译器并不知道如何遍历List。上述代码能够编译通过，只是因为编译器把for each循环通过Iterator改写为了普通的for循环：

```
for (Iterator<String> it = list.iterator(); it.hasNext(); ) {
     String s = it.next();
     System.out.println(s);
}

```

6. 例2
如果我们自己编写了一个集合类，想要使用for each循环，只需满足以下条件：
集合类实现Iterable接口，该接口要求返回一个Iterator对象；
用Iterator对象迭代集合内部数据。
```
import java.util.*;

public class Main {
    public static void main(String[] args) {
        ReverseList<String> rlist = new ReverseList<>();
        rlist.add("Apple");
        rlist.add("Orange");
        rlist.add("Pear");
        for (String s : rlist) {
            System.out.println(s);
        }
    }
}

class ReverseList<T> implements Iterable<T> {

    private List<T> list = new ArrayList<>();

    public void add(T t) {
        list.add(t);
    }

    @Override
    public Iterator<T> iterator() {
        return new ReverseIterator(list.size());
    }

    class ReverseIterator implements Iterator<T> {
        int index;

        ReverseIterator(int index) {
            this.index = index;
        }

        @Override
        public boolean hasNext() {
            return index > 0;
        }

        @Override
        public T next() {
            index--;
            return ReverseList.this.list.get(index);
        }
    }
}

```

> 参考
> https://www.liaoxuefeng.com/wiki/1252599548343744/1265124784468736