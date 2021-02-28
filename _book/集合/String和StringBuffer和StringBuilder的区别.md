### String和StringBuffer和StringBuilder的区别?

考虑以下带有三个串联函数的代码，该函数具有三种不同类型的参数：String，StringBuffer和StringBuilder。

```
// Java program to demonstrate difference between String, 
// StringBuilder and StringBuffer 
class Geeksforgeeks 
{ 
    // Concatenates to String 
    public static void concat1(String s1) 
    { 
        s1 = s1 + "forgeeks"; 
    } 
  
    // Concatenates to StringBuilder 
    public static void concat2(StringBuilder s2) 
    { 
        s2.append("forgeeks"); 
    } 
  
    // Concatenates to StringBuffer 
    public static void concat3(StringBuffer s3) 
    { 
        s3.append("forgeeks"); 
    } 
  
    public static void main(String[] args) 
    { 
        String s1 = "Geeks"; 
        concat1(s1);  // s1 is not changed 
        System.out.println("String: " + s1); 
  
        StringBuilder s2 = new StringBuilder("Geeks"); 
        concat2(s2); // s2 is changed 
        System.out.println("StringBuilder: " + s2); 
  
        StringBuffer s3 = new StringBuffer("Geeks"); 
        concat3(s3); // s3 is changed 
        System.out.println("StringBuffer: " + s3); 
    } 
} 
```

```
> Output:
String: Geeks
StringBuilder: Geeksforgeeks
StringBuffer: Geeksforgeeks
```

1. Concat1：在此方法中，我们传递字符串“Geeks”并执行s1 = s1 +”forgeeks”。从main（）传递的字符串未更改，这是由于String是不可变的。更改字符串的值将创建另一个对象，并且concat1（）中的s1将存储对新字符串的引用。main（）和cocat1（）中的s1引用的是不同的字符串。
2. Concat2：在此方法中，我们传递字符串“Geeks”并执行“ s2.append（“ forgeeks”）”，该操作将字符串的实际值（在main中）更改为“ Geeksforgeeks”。这是由于StringBuilder是可变的，因此更改了它的值。
3. Concat3：StringBuffer与StringBuilder相似，不同之处在于StringBuffer是线程安全的，即，多个线程可以使用它而没有任何问题。线程安全性会降低性能。

### 何时使用哪一个：
 
- 如果字符串在整个程序中保持不变，请使用String类对象，因为String对象是不可变的。
- 如果字符串可以更改（例如：字符串构造中的大量逻辑和操作）并且只能从单个线程访问，那么使用StringBuilder就足够了。
- 如果字符串可以更改，并且可以从多个线程访问，请使用StringBuffer，因为StringBuffer是同步的，所以您具有线程安全性。


> 参考资料: https://www.geeksforgeeks.org/string-vs-stringbuilder-vs-stringbuffer-in-java/
