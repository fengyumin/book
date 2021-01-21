
### 什么是JDBC?

Java为关系数据库定义了一套标准的访问接口：JDBC（Java Database Connectivity）
> JDBC是允许用户在不同数据库之间做选择的一个抽象层。JDBC允许开发者用JAVA写数据库应用程序，而不需要关心底层特定数据库的细节。

各数据库厂商使用相同的接口，Java代码不需要针对不同数据库分别开发；
Java程序编译期仅依赖java.sql包，不依赖具体数据库的jar包；
可随时替换底层数据库，访问数据库的Java代码基本不变。