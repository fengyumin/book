Java中字符串类型之间的转换.md

### 将不同类（例如String，StringBuffer，StringBuilder）的字符串对象相互转换

#### 从String到StringBuffer和StringBuilder

- 方法: 这很容易。我们可以直接将String类对象传递给StringBuffer和StringBuilder类构造函数。
- 使用场景: 由于String类在Java中是不可变的，因此对于编辑字符串，我们可以通过将其转换为StringBuffer或StringBuilder类对象来执行相同的操作。

```
// Java program to demonstrate conversion from  
// String to StringBuffer and StringBuilder. 
public class Test  
{ 
    public static void main(String[] args) 
    { 
        String str = "Geeks"; 
          
        // conversion from String object to StringBuffer 
        StringBuffer sbr = new StringBuffer(str); 
        sbr.reverse(); 
        System.out.println(sbr); 
          
        // conversion from String object to StringBuilder 
        StringBuilder sbl = new StringBuilder(str); 
        sbl.append("ForGeeks"); 
        System.out.println(sbl); 
    } 
} 
```

```
输出：

SkeeG 
GeeksForGeeks
```

#### 从StringBuffer和StringBuilder到String

- 可以使用toString（）方法执行此转换，该方法在StringBuffer和StringBuilder类中都被覆盖。下面是演示相同的Java程序。
- 请注意，虽然我们使用toString（）方法，但会分配一个新的String对象（在Heap区域中）并初始化为StringBuffer对象当前表示的字符序列，这意味着对StringBuffer对象的后续更改不会影响String对象的内容。

```
// Java program to demonstrate conversion from  
// String to StringBuffer and StringBuilder. 
public class Test  
{ 
    public static void main(String[] args) 
    { 
        StringBuffer sbr = new StringBuffer("Geeks"); 
        StringBuilder sbdr = new StringBuilder("Hello"); 
          
        // conversion from StringBuffer object to String 
        String str = sbr.toString(); 
        System.out.println("StringBuffer object to String : "); 
        System.out.println(str); 
          
        // conversion from StringBuilder object to String 
        String str1 = sbdr.toString(); 
        System.out.println("StringBuilder object to String : "); 
        System.out.println(str1); 
          
        // changing StringBuffer object sbr 
        // but String object(str) doesn't change 
        sbr.append("ForGeeks"); 
        System.out.println(sbr); 
        System.out.println(str); 
          
    } 
} 

输出：

StringBuffer对象转换为String：
Geeks 
StringBuilder对象转换为String：
Hello 
GeeksForGeeks 
Geeks
```

#### 从StringBuffer到StringBuilder或反之亦然：
这种转换是棘手的。没有直接的方法可以将其转换。
- 在这种情况下，我们可以使用String类对象。
- 我们首先使用toString（）方法将StringBuffer / StringBuilder对象转换为String ，
- 然后使用构造函数将StringBuffer / StringBuilder对象从String转换为StringBuilder / StringBuffer。

```
// Java program to demonstrate conversion from  
// String to StringBuffer and StringBuilder. 
public class Test  
{ 
    public static void main(String[] args) 
    { 
        StringBuffer sbr = new StringBuffer("Geeks"); 
          
        // conversion from StringBuffer object to StringBuilder 
        String str = sbr.toString(); 
        StringBuilder sbl = new StringBuilder(str); 
          
        System.out.println(sbl); 
          
    } 
} 

Output:

Geeks
```
