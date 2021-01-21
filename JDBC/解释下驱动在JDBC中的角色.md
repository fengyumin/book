
### 解释下驱动(Driver)在JDBC中的角色?

JDBC驱动提供了特定厂商对JDBC API接口类的实现，驱动必须要提供java.sql包下面这些类的实现：Connection, Statement, PreparedStatement,CallableStatement, ResultSet和Driver。

> 各数据库厂商使用相同的接口，Java代码不需要针对不同数据库分别开发；
Java程序编译期仅依赖java.sql包，不依赖具体数据库的jar包；
可随时替换底层数据库，访问数据库的Java代码基本不变。