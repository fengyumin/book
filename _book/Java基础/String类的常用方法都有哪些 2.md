String类的常用方法都有哪些.md

### String类的常用方法都有哪些?

- public char charAt(int index):
返回String对象中下标为index的字符, 注意String的下标是从0开始
```
String x = "airplane";
System.out.println( x.charAt(2) ); // output is 'r'
```

- public String concat(String s)
返回值为两者拼接后的String对象
```
public String concat(String s)
System.out.println( x.concat(" author") ); 
// output is "book author"
```

与+,+=的用法相似
```
String x = "library";
System.out.println( x + " card"); 
// output is "library card"
String x = "United";
x += " States"
System.out.println( x ); 
// output is "United States"
```

- public boolean equalsIgnoreCase(String s)
比较两者的值是否一致
```
tring x = "Exit"; 
System.out.println( x.equalsIgnoreCase("EXIT")); // is "true" 
System.out.println( x.equalsIgnoreCase("tixe")); // is "false"
```

- public int length()
- public String replace(char old, char new)
- public String substring(int begin)/ public String substring(int begin, int end)
- public String toLowerCase()
- public String toUpperCase()
- public String trim()
- ppublic char[] toCharArray()
- public boolean contains(“searchString”)

```
public class StringMethodsDemo {
    public static void main(String[] args) {
        String targetString = "Java is fun to learn";
        String s1= "JAVA";
        String s2= "Java";
        String s3 = "  Hello Java  ";
        
        System.out.println("Char at index 2(third position): " + targetString.charAt(2));
        System.out.println("After Concat: "+ targetString.concat("-Enjoy-"));
        System.out.println("Checking equals ignoring case: " +s2.equalsIgnoreCase(s1));
        System.out.println("Checking equals with case: " +s2.equals(s1));
        System.out.println("Checking Length: "+ targetString.length());
        System.out.println("Replace function: "+ targetString.replace("fun", "easy"));
        System.out.println("SubString of targetString: "+ targetString.substring(8));
        System.out.println("SubString of targetString: "+ targetString.substring(8, 12));
        System.out.println("Converting to lower case: "+ targetString.toLowerCase());
        System.out.println("Converting to upper case: "+ targetString.toUpperCase());
        System.out.println("Triming string: " + s3.trim());
        System.out.println("searching s1 in targetString: " + targetString.contains(s1));
        System.out.println("searching s2 in targetString: " + targetString.contains(s2));

        char [] charArray = s2.toCharArray();
        System.out.println("Size of char array: " + charArray.length);
        System.out.println("Printing last element of array: " + charArray[3]);

    }

}

```



> 参考:https://www.w3resource.com/java-tutorial/exploring-methods-of-string-class.php





