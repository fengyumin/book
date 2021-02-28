Hash集合中需要重写hashCode和equals吗.md


### Hash集合中需要重写hashCode和equals吗?
> 这样的集合包括HashMap、HashSet和Hashtable。

一. 要正确使用HashMap，作为key的类必须正确覆写equals()和hashCode()方法；

二. 
1. 一个类如果覆写了equals()，就必须覆写hashCode()，并且覆写规则是：
- 如果equals()返回true，则hashCode()返回值必须相等；
- 如果equals()返回false，则hashCode()返回值尽量不要相等。
> 即对应两个实例a和b：
> - 如果a和b相等，那么a.equals(b)一定为true，则a.hashCode()必须等于b.hashCode()；
> - 如果a和b不相等，那么a.equals(b)一定为false，则a.hashCode()和b.hashCode()尽量不要相等。
3. 上述第一条规范是正确性，必须保证实现，否则HashMap不能正常工作。
4. 而第二条如果尽量满足，则可以保证查询效率，因为不同的对象，如果返回相同的hashCode()，会造成Map内部存储冲突，使存取的效率下降。

三. 实现hashCode()方法可以通过Objects.hashCode()辅助方法实现。





> 参考:https://www.liaoxuefeng.com/wiki/1252599548343744/1265117217944672


