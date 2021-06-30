# JDBC
> JDBC（Java Data Base Connectivity,JAVA数据库连接）  
> J2EE的标准，定义了执行SQL语句的Java API  
> 各个数据库厂商(Mysql，Oracle...)根据标准提供了对应的实现/驱动，使得开发人员能够以此编写执行SQL的程序

<img src="https://raw.githubusercontent.com/XuLinSheng/J2EE/main/1.JDBC/jdbc1.png" width="60%">

## JDBC流程

### 1. 加载数据库驱动

Driver接口由数据库厂家提供实现，作为java开发人员，只需要使用Driver接口就可以了。  
在编程中要连接数据库，必须先装载特定厂商的数据库驱动程序，不同的数据库有不同的装载方法。如：  

装载MySql驱动：
```java
Class.forName("com.mysql.jdbc.Driver");
```

装载Oracle驱动：
```java
Class.forName("oracle.jdbc.driver.OracleDriver");
```

装载SqlServer驱动：
```java
Class.forName("com.microsoft.jdbc.sqlserver.SQLServerDriver");
```
### 2. 建立数据库连接

连接MySql数据库：
```java
Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/database", "user", "password");
```
连接Oracle数据库：
```java
Connection conn = DriverManager.getConnection("jdbc:oracle:thin:localhost:1521:database", "user", "password");
```

连接SqlServer数据库：
```java
Connection conn = DriverManager.getConnection("jdbc:microsoft:sqlserver://localhost:1433;DatabaseName=database", "user", "password");
```

### 3. 创建语句并执行

Statement：由createStatement创建，用于发送简单的SQL语句（不带参数）。
```java
String id = "5";
String sql = "delete from table where id=" +  id;
Statement st = conn.createStatement();
st.executeQuery(sql); 
// 存在sql注入风险
// 如果用户传入的id为“5 or 1=1”，那么将删除表中的所有记录
```

PreparedStatement ：继承自Statement接口，由preparedStatement创建，用于发送含有一个或多个参数的SQL语句。  
PreparedStatement对象比Statement对象的效率更高，并且可以防止SQL注入，所以我们一般都使用PreparedStatement。
```java
/** PreparedStatement 有效的防止sql注入
  * SQL语句在程序运行前已经进行了预编译
  * 当运行时动态地把参数传给PreprareStatement时
  * 即使参数里有敏感字符如 or '1=1'也数据库会作为一个参数一个字段的属性值来处理而不会作为一个SQL指令
 **/
String sql = “insert into user (name,pwd) values(?,?)”;  
PreparedStatement ps = conn.preparedStatement(sql);  
ps.setString(1, “col_value”);  //占位符顺序从1开始
ps.setString(2, “123456”); //也可以使用setObject
ps.executeQuery(); 
```
### 4. 处理执行结果

### 5. 释放资源

