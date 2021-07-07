# JDBC
> JDBC（Java Data Base Connectivity,JAVA数据库连接）  
> J2EE的标准，定义了执行SQL语句的Java API  
> 各个数据库厂商(Mysql,Oracle,SqlServer,...)根据标准提供了对应的实现/驱动，使得开发人员能够以此编写执行SQL的程序

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
Connection conn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:database", "user", "password");
```

连接SqlServer数据库：
```java
Connection conn = DriverManager.getConnection("jdbc:microsoft:sqlserver://localhost:1433;DatabaseName=database", "user", "password");
```

### 3. 创建语句并执行

* Statement  
由createStatement创建，用于发送简单的SQL语句（不带参数）。
```java
String id = "5";
String sql = "delete from table where id=" +  id;
Statement st = conn.createStatement();
st.executeQuery(sql); 
// 存在sql注入风险
// 如果用户传入的id为“5 or 1=1”，那么将删除表中的所有记录
```

* PreparedStatement   
继承自Statement接口，由preparedStatement创建，用于发送含有一个或多个参数的SQL语句。  
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

* CallableStatement  
继承自PreparedStatement接口，由方法prepareCall创建，用于调用存储过程。
```java
CallableStatement cs = conn.prepareCall("{call proc_Ins_Dept(?,?,?)}");  //调用格式 {call 存储过程名(参数)}
cs.setObject(1, 76);
cs.setObject(2, "技术部");
cs.setObject(3, "zhengzhou");
cs.execute(); 
```

### 4. 处理执行结果
```java
ResultSet rs = ps.executeQuery();
While(rs.next()){
    rs.getString(“col_name”);
    rs.getInt(1);
    //…
}
```
### 5. 释放资源
```java
//数据库连接（Connection）非常耗资源，尽量晚创建，尽量早的释放 
try {
    ...
} catch (SQLException e) {
    e.printStackTrace();
} finally {
    try {
        if (resultSet!=null) resultSet.close();
        if (statement!=null) statement.close();
        if (connect!=null) connect.close();
    } catch (SQLException e) {
        e.printStackTrace();
    }        
}
```

### 6.事务
> 概念： 一组数据要么同时执行成功，要么同时执行失败。事务是数据库操作的一个执行单元。  

特点（ACID）：
* 原子性（Atomicity）  
  >原子性是指事务包含的所有操作要么全部成功，要么全部失败回滚，因此事务的操作如果成功就必须要完全应用到数据库，如果操作失败则不能对数据库有任何影响。
* 一致性（Consistency）  
  >事务开始前和结束后，数据库的完整性约束没有被破坏 。比如A向B转账，不可能A扣了钱，B却没收到。
* 隔离性（Isolation）  
  >隔离性是当多个用户并发访问数据库时，同一时间，只允许一个事务请求同一数据，不同的事务之间彼此没有任何干扰。比如A正在从一张银行卡中取钱，在A取钱的过程结束前，B不能向这张卡转账。
* 持久性（Durability）  
  >事务完成后，事务对数据库的所有更新将被保存到数据库，不能回滚。

手动处理事务

```java
conn.setAutoCommit(false); // 设为手动提交
conn.commit();  // 提交事务
conn.rollback(); // 回滚事务
```

事务的并发问题  

1. 脏读：事务A读取了事务B更新的数据，然后B回滚操作，那么A读取到的数据是脏数据

2. 不可重复读：事务 A 多次读取同一数据，事务 B 在事务A多次读取的过程中，对数据作了更新并提交，导致事务A多次读取同一数据时，结果 不一致。

3. 幻读：系统管理员A将数据库中所有学生的成绩从具体分数改为ABCDE等级，但是系统管理员B就在这个时候插入了一条具体分数的记录，当系统管理员A改结束后发现还有一条记录没有改过来，就好像发生了幻觉一样，这就叫幻读。