final在java中有什么作用.md

> - final在java中有什么作用?
> - 初始化final variable有哪些方式?
> - C++中的const variable与Java中variable有什么区别?
> - foreach循环中使用final关键字会报错吗? for (final int i : arr) 

### final在java中有什么作用?

final是一个不可访问的修饰符,可用于修饰类、方法、变量:
- final variable 常量
- final methods 防止被覆盖
- final classes 防止被继承

#### final variable

- 变量被final关键字修饰后,它的值就不能再更改了,相当于一个常量. 这也意味着我们需要初始化一个final变量;
- 如果初始化的final变量是引用类型，则它不能再指向其他对象.但它本身所指向对象的内部状态是可以更改的. eg.final array, final collection中的元素可以添加或删除;
- **语法**: 使用大写形式来表示final变量, 并使用下划线来分割单词. 

```
// a final variable
final int THRESHOLD = 5;
// a blank final variable
final int THRESHOLD;
// a final static variable PI
static final double PI = 3.141592653589793;
// a  blank final static  variable
static final double PI;
```

```
class Man{
    private final int I = 0;
    public Man(){
        I = 1;//变量I的重新赋值报错: 
        final Object OBJ = new Object();
        OBJ = new Object();//变量OBJ的重新赋值报错: 
    }
}
```



#### final类
- final类不能被继承。
- final类中的成员变量可以根据需要设为final.
- final类中的所有成员方法都会被隐式地指定为final方法

> 使用场景: 在使用final修饰类的时候，要注意谨慎选择，除非这个类真的在以后不会用来继承或者出于安全的考虑，尽量不要将类设计为final类。

```
final class People{
    public People(){

    }
}

//报错: 类型man不能成为final类People的子类
class Man extends People{ 

}
```

#### final方法

> 使用场景: 
> - 只有在想明确禁止 该方法在子类中被覆盖的情况下才将方法设置为final的;
> - 类的private方法会隐式地被指定为final方法


***

### 初始化final variable有哪些方式?
我们必须初始化一个final variable,否则编译时会抛出异常.且final variable只能被初始化一次.方法如下:
**在声明时直接初始化final variable** 
```
    // a final variable 
    // direct initialize 
    final int THRESHOLD = 5; 

    // a final static variable PI 
    // direct initialize 
    static final double PI = 3.141592653589793;
```

**使用instance-initialzer block, 或构造函数来初始化 blank final variable**
- 如果类中有多个构造函数,则必须在所有构造函数中对其进行初始化,否则将引发编译错误

```
    // a blank final variable 
    final int CAPACITY; 

    // instance initializer block for  
    // initializing CAPACITY 
    { 
        CAPACITY = 25; 
    } 

    // constructor for initializing MINIMUM 
    // Note that if there are more than one  constructor, you must initialize MINIMUM in them also 
    public GFG()  
    { 
        MINIMUM = -1; 
    } 
```

**使用static block来初始化一个blank final static variable**
```
    // a  blank final static  variable 
    static final double EULERCONSTANT; 

    // static initializer block for  
    // initializing EULERCONSTANT 
    static{ 
        EULERCONSTANT = 2.3; 
    }
```


***

### C++中的const variables 与Java中final variables有什么区别?

- C++中的const variables必须在声明时赋值;
- Java中final variables可以在声明时赋值,也可以先声明,再在后续的赋值语句(构造函数或初始化块)中赋值;


### foreach循环中使用final关键字会报错吗? for (final int i : arr) 
- 因为变量i是在每次循环迭代的范围外,因此实际上是在每个循环中重新声明一次,是多个局部变量i,

```
// Java program to demonstrate final with for-each statement 
  
class Gfg  
{ 
    public static void main(String[] args)  
    { 
        int arr[] = {1, 2, 3}; 
          
        // final with for-each statement 
        // legal statement 
        for (final int i : arr) 
            System.out.print(i + " "); 
    }     
} 
// Output: 1 2 3
```










> 参考资料: https://www.cnblogs.com/dolphin0520/p/3736238.html