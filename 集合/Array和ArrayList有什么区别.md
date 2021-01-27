Array和ArrayList有什么区别.md

### 数组(Array)和列表(ArrayList)有什么区别？什么时候应该使用Array而不是ArrayList？

ArrayList可以算是Array的加强版，（对array有所取舍的加强）。
1. 存储内容比较：
Array数组可以包含基本类型和对象类型，
ArrayList却只能包含对象类型。
但是需要注意的是：Array数组在存放的时候一定是同种类型的元素。ArrayList就不一定了，因为ArrayList可以存储Object。


2. 空间大小比较：
Array数组的空间大小是固定的，空间不够时也不能再次申请，所以需要事前确定合适的空间大小。
ArrayList的空间是动态增长的，如果空间不够，它会创建一个空间比原空间大一倍的新数组，然后将所有元素复制到新数组中，接着抛弃旧数组。而且，每次添加新的元素的时候都会检查内部数组的空间是否足够。（比较麻烦的地方）。

3. 方法上的比较：
ArrayList作为Array的增强版，当然是在方法上比Array更多样化，比如添加全部addAll()、删除全部removeAll()、返回迭代器iterator()等。

**适用场景：**
- 如果预先知道大小并确定它不会改变，则应该使用数组作为数据结构来存储对象；如果不确定，则只需使用ArrayList。
- 如果我们需要对元素进行频繁的移动或删除，或者是处理的是超大量的数据，那么，使用ArrayList就真的不是一个好的选择，因为它的效率很低，使用数组进行这样的动作就很麻烦，那么，我们可以考虑选择LinkedList。

>链接：https://www.nowcoder.com/questionTerminal/a94a9896128a4498bb0df936da62f36f?toCommentId=89441
来源：牛客网