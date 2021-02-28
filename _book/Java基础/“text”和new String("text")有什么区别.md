“text”和new String("text")有什么区别.md

### “text”和new String("text")有什么区别?

以下语句有什么区别?
```
String s = "text";
String s = new String("text");
```

#### new String("text") 
- 显式的创建了一个String对象的实例.
- 使用new运算符，将在堆中创建一个新字符串对象，并将其值设为“text“
- 新的字符串值存储在字符串常量池中

####  String s = "text"
- 在常量池中有可用实例的情况下会复用这个实例.
- 引用s指向了字符串常量池中已存储的值


#### new String("text")一般很少被使用,以下是它的API说明
> API: String(String original)
> - 初始化一个String对象,且它代表着与参数original相同的字符串. 这个新创建的String对象是这个参数original的String对象的副本.
> - 除非确实需要显式给orignal创建副本.否则没必要使用这个构造函数.因为String对象是不可变的.

```
    String s1 = "foobar";
    String s2 = "foobar";

    System.out.println(s1 == s2);      // true

    s2 = new String("foobar");
    System.out.println(s1 == s2);      // false 比较对象
    System.out.println(s1.equals(s2)); // true 比较引用对象指向的值
```


***
String literals will go into String Constant Pool.

The below snapshot might help you to understand it visually to remember it for longer time.
> 见参考链接

Object creation line by line:

`String str1 = new String("java5");`
Using string literal "java5" in the constructor, a new string value is stored in string constant pool. Using new operator, a new string object is created in the heap with "java5" as value.

`String str2 = "java5"`
Reference "str2" is pointed to already stored value in string constant pool

`String str3 = new String(str2);`
A new string object is created in the heap with the same value as reference by "str2"

`String str4 = "java5";`
Reference "str4" is pointed to already stored value in string constant pool

Total objects : Heap - 2, Pool - 1


> 参考资料:https://stackoverflow.com/questions/3052442/what-is-the-difference-between-text-and-new-stringtext