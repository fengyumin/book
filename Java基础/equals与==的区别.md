equals与==的区别.md

### equals与==的区别?

1. 首先的区别是，equals 是方法，而 == 是操作符；
2. 对于基本类型的变量来说（如 short、 int、 long、 float、 double），只能使用 == ，因为这些基本类型的变量没有 equals 方法。对于基本类型变量的比较，使用 == 比较， 一般比较的是它们的值。
3. 对于引用类型的变量来说（例如 String 类）才有 equals 方法，因为 String 继承了 Object 类， 
- equals 是 Object 类的通用方法。
- 对于该类型对象的比较，默认情况下，也就是没有复写 Object 类的 equals 方法，使用 == 和 equals 比较是一样效果的，都是比较的是它们在内存中的存放地址。
- 但是对于某些类来说，为了满足自身业务需求，可能存在 equals 方法被复写的情况，这时使用 equals 方法比较需要看具体的情况，例如 String 类，使用 equals 方法会比较它们的值；


> 对于上述第三点理解起来可能有点复杂，因为这里 equals 方法比较需要分两种情况来讨论，一种情况是该方法没有被重写，另外一种是该方法被重写。

**对于 equals 方法没有被重写的情况。**
如果类没有重写该方法，那么默认使用的就是 Object 类的方法，以下是 Object 类的 equals 方法：
```
  public boolean equals(Object obj) {
      return (this == obj);
  }
```
从源码可以看出，里面使用的就是 == 比较，所以这种情况下比较的就是它们在内存中的存放地址。


**对于 equals 方法被重写的情况**
以 String 类为例，以下是 String 类中的 equals 方法：

- 从源码可以看出， String 类复写了 equals 方法，当使用 == 比较内存的存放地址不相等时，接下来会比较字符串的内容是否 相等，
- 所以 String 类中的 equals 方法会比较两者的字符串内容是否一样。

我们来看看下面的例子：

- 因为 String b 通过 new 的方式已经开辟了新的堆内存，而 String a = "Hello World" 是存放在常量池里的，两者在 Java 内存里存在放的位置是不同的，所以 a == b 为 false；而 equals 方法当两者存放的内存地址不同时，会比较两者的值，两者的值都是 "Hello World" ，所以 a.equals(b) 为 true。




> 作者：chocolatezhu
链接：https://www.jianshu.com/p/9cbed9f33a4d
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


>作者：chocolatezhu
链接：https://www.jianshu.com/p/9cbed9f33a4d
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。