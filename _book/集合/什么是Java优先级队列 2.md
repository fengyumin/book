什么是Java优先级队列.md

### 什么是Java优先级队列(Priority Queue)？

- PriorityQueue实现了一个优先队列：从队首获取元素时，总是获取优先级最高的元素。
- PriorityQueue默认按元素比较的顺序排序（必须实现Comparable接口），也可以通过Comparator自定义排序算法（元素就不必实现Comparable接口）。

**优先队列**
> - 可以每个人先取一个号，例如：A1、A2、A3……然后，按照号码顺序依次办理，实际上这就是一个Queue。
如果这时来了一个VIP客户，他的号码是V1，虽然当前排队的是A10、A11、A12……但是柜台下一个呼叫的客户号码却是V1。
> - 这个时候，我们发现，要实现“VIP插队”的业务，用Queue就不行了，因为Queue会严格按FIFO的原则取出队首元素。我们需要的是优先队列：PriorityQueue。

- Queue是一个先进先出（FIFO）的队列
- PriorityQueue和Queue的区别在于，它的出队顺序与元素的优先级有关，对PriorityQueue调用remove()或poll()方法，返回的总是优先级最高的元素。

**实现Comparable接口**
- 要使用PriorityQueue，我们就必须给每个元素定义“优先级”。
- 因此，放入PriorityQueue的元素，必须实现Comparable接口，PriorityQueue会根据元素的排序顺序决定出队的优先级。
- 如果我们要放入的元素并没有实现Comparable接口怎么办？PriorityQueue允许我们提供一个Comparator对象来判断两个元素的顺序


```
public class Main {
    public static void main(String[] args) {
        Queue<User> q = new PriorityQueue<>(new UserComparator());
        // 添加3个元素到队列:
        q.offer(new User("Bob", "A1"));
        q.offer(new User("Alice", "A2"));
        q.offer(new User("Boss", "V1"));
        System.out.println(q.poll()); // Boss/V1
        System.out.println(q.poll()); // Bob/A1
        System.out.println(q.poll()); // Alice/A2
        System.out.println(q.poll()); // null,因为队列为空
    }
}

//实现PriorityQueue的关键在于提供的UserComparator对象，它负责比较两个元素的大小（较小的在前）。UserComparator总是把V开头的号码优先返回，只有在开头相同的时候，才比较号码大小。
class UserComparator implements Comparator<User> {
    public int compare(User u1, User u2) {
        if (u1.number.charAt(0) == u2.number.charAt(0)) {
            // 如果两人的号都是A开头或者都是V开头,比较号的大小:
            return u1.number.compareTo(u2.number);
        }
        if (u1.number.charAt(0) == 'V') {
            // u1的号码是V开头,优先级高:
            return -1;
        } else {
            return 1;
        }
    }
}

class User {
    public final String name;
    public final String number;

    public User(String name, String number) {
        this.name = name;
        this.number = number;
    }

    public String toString() {
        return name + "/" + number;
    }
}

```




***

PriorityQueue(int initialCapacity, Comparator<? super E> comparator)
          使用指定的初始容量创建一个 PriorityQueue，并根据指定的比较器comparator来排序其元素。

PriorityQueue 是用数组实现，但是大小可以动态增加，容量无限。


PriorityQueue 的实现不是同步的。不是线程安全的。如果多个线程中的任意线程从结构上修改了列表， 则这些线程不应同时访问 PriorityQueue实例。保证线程安全可以使用PriorityBlockingQueue 类。。




- PriorityQueue是一个基于优先级堆的无界队列，它的元素是按照自然顺序(natural order)排序的。在创建的时候，我们可以给它提供一个负责给元素排序的比较器。
- PriorityQueue不允许null值，因为他们没有自然顺序，或者说他们没有任何的相关联的比较器。
- 最后，PriorityQueue不是线程安全的，
- 入队和出队的时间复杂度是O(log(n))。


PriorityQueue 是基于优先堆的一个无界队列，这个优先队列中的元素可以默认自然排序或者通过提供的
Comparator 在队列实例化的时排序。

PriorityQueue 不允许空值，而且不支持 non-comparable（不可比较）的对象，比如用户自定义的类。优先队列要求使用 Java Comparable 和 Comparator 接口给对象排序，并且在排序时会按照优先级处理其中的元素。





作者：专职跑龙套
链接：https://www.jianshu.com/p/c577796e537a
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

> 参考: 
> - https://www.liaoxuefeng.com/wiki/1252599548343744/1265120632401152
> - https://www.jianshu.com/p/c577796e537a