# JDBC
> JDBC（Java Data Base Connectivity,JAVA数据库连接）  
> J2EE的标准，定义了执行SQL语句的Java API  
> 各个数据库厂商(Mysql，Oracle...)根据标准提供了对应的实现/驱动，使得开发人员能够以此编写执行SQL的程序

<img src="https://raw.githubusercontent.com/XuLinSheng/J2EE/main/1.JDBC/jdbc1.png?token=AGHOI44H7GLLMZGASVGYTMTA3SJNY" width="80%">

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
Connection conn = DriverManager.getConnection("jdbc:mysql://host:port/database", "user", "password");
```
连接Oracle数据库：
```java
Connection conn = DriverManager.getConnection("jdbc:oracle:thin:@host:port:database", "user", "password");
```

连接SqlServer数据库：
```java
Connection conn = DriverManager.getConnection("jdbc:microsoft:sqlserver://host:port; DatabaseName=database", "user", "password");
```

### 3. 创建语句并执行

### 4. 处理执行结果

### 5. 释放资源

