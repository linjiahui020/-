#PreparedStatement：
+ PreparedStatement是java.sql包下面的一个接口，用来执行SQL语句查询，通过调用connection.preparedStatement(sql)方法可以获得PreparedStatment对象。数据库系统会对sql语句进行预编译处理（如果JDBC驱动支持的话），预处理语句将被预先编译好，这条预编译的sql查询语句能在将来的查询中重用，这样一来，它比Statement对象生成的查询速度更快。

## Statement
+ 使用 Statement 对象。在对数据库只执行一次性存取的时侯，用 Statement 对象进行处理。PreparedStatement 对象的开销比Statement大，对于一次性操作并不会带来额外的好处。

## 深入理解statement 和prepareStatement
+ 使用Statement而不是PreparedStatement对象
JDBC驱动的最佳化是基于使用的是什么功能. 选择PreparedStatement还是Statement取决于你要怎么使用它们. 对于只执行一次的SQL语句选择Statement是最好的. 相反, 如果SQL语句被多次执行选用PreparedStatement是最好的.

+ PreparedStatement的第一次执行消耗是很高的. 它的性能体现在后面的重复执行. 例如, 假设我使用Employee ID, 使用prepared的方式来执行一个针对Employee表的查询. JDBC驱动会发送一个网络请求到数据解析和优化这个查询. 而执行时会产生另一个网络请求.在JDBC驱动中，减少网络通讯是最终的目的. 如果我的程序在运行期间只需要一次请求, 那么就使用Statement. 对于Statement, 同一个查询只会产生一次网络到数据库的通讯.

+ 对于使用PreparedStatement池的情况下, 本指导原则有点复杂. 当使用PreparedStatement池时, 如果一个查询很特殊, 并且不太会再次执行到, 那么可以使用Statement. 如果一个查询很少会被执行,但连接池中的Statement池可能被再次执行, 那么请使用PreparedStatement. 在不是Statement池的同样情况下, 请使用Statement.

+ 数据库驱动：Driver

+ 加载mysql驱动：Class.forName("com.mysql.jdbc.Driver");

+ 加载oracle驱动：Class.forName("oracle.jdbc.driver.OracleDriver");

+ 加载相应的驱动需要导入相应的包，如MySQL则需要导入：mysql-connector-java-5.1.13-bin.jar

否则无法正常执行。



## 获取数据库链接：Connection

+ Connetion类主要用来链接数据库，常通过DriverManager.getConnection()来获取一个连接对象。
这里有3个参数，分别是url，user，passwrod。对应的是要链接的数据库，用户名，密码等。如：
url=jdbc:mysql://localhost:3306/jdbc?useUnicode=true&characterEncoding=utf-8
user=root
password=root


## 执行sql语句：Statement

# Statement对象用于执行sql语句，有以下3种：

+ Statement对象用于执行不带参数的简单的SQL语句；

+ PerparedStatement对象用于执行带或不带参数的预编译SQL语句；

+ CallableStatement对象用于执行对数据库已存储过程的调用；

# Statement的常用方法：

+ executeQuery()方法：运行查询语句，返回ReaultSet对象。

+ executeUpdata()方法：运行增，删，改操作，返回更新的行数。

+ addBatch(String sql) ：把多条sql语句放到一个批处理中。

+ executeBatch()：向数据库发送一批sql语句执行。



# 结果集：ResultSet

执行executeQuery()方法后返回的结果集

  常用方法：
+ getString(String columnName)：获得当前行的某一string类型的字段
+ getFloat(String columnName)：获得当前行的某一string类型的字段
+ getDate(String columnName)：获得当前行的某一date类型的字段
+ getBoolean(String columnName)：获得在当前行的某一Boolean类型的字段
+ getObject(String columnName)：获取当前行的某一任意类型的字段
+ next()：移动到下一行
