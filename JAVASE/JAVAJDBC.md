---





---

# JAVAJDBC


JDBC: Java DataBase Connection
      Java连接数据库的规范 -> 接口 JDK提供接口
      实现类: 数据库厂商实现 -> 驱动类 jar
      Connection Statement ResultSet
      PreparedStatement: 预编译的执行器

JDBC连接数据库步骤:
1.导入驱动jar包
2.Class.forName(); // 注册驱动
3.获得链接 DriverManager.getConnection("url", username, password); 
		驱动名, url, username, password
           jdbc:mysql://ip:port/database
           oracle默认端口号: 1521
4.操作数据库 DML DQL DDL(一般不用)

常见错误
```
//ClassNotFoundException:类未找到/jar包未导入
//协议错误 No suitable driver found
//地址错误 运行卡住一直尝试连接
//端口错误 Connection refused: connect
//数据库错误 Unknown database 'mybati'
```

JDBC连接过程做成utils工具类

  Connection Statement->PreparedStatement ResultSet
  Connection: 管理事务, 获得statement对象
  Statement: 执行sql, executeUpdate, executeQuery
             setXXX(index, value)
  ResultSet: next(), getXXX(index, columnName)

JdbcTemplate: 取代JDBC中 Statement ResultSet
   Spring的一个组件
   更方便的方式操作数据库(执行\\传参\\结果封装)
   使用步骤:
     1.导入jar包
     2.创建对象JdbcTemplate
常用方法
   update:用于DML处理可输入(sql,...args)
   query: 查询一个List<T>, 不可能是null,
          查不到任何结果, list.size() = 0
          如果只需要一条, 需要手动list.get(0)
   queryForObject: 只能查询一个结果
          如果结果不是1条, 报错, 抛异常
          EmptyResultDataAccessException
    封装结果集
		RowMapper (接口)->实现类 BeanPropertyRowMapper
```
String sq1 = "insert into account values(8000,?,?)";
int count = jt.update(sq1,"ling",5000);

String sq2 = "select * from emp where ename like ?";
String sq3 = "select count(ename) from emp";
String sq4 = "select * from emp where empno = 7934";
List<Emp> emps = jt.query(sq2, new BeanPropertyRowMapper<>(Emp.class),"%A%");
Emp emp = jt.queryForObject(sq4, new BeanPropertyRowMapper<>(Emp.class));
Integer i = jt.queryForObject(sq3, Integer.class);
emps.forEach(System.out::println);
System.out.println(i);
System.out.println(emp);
```

  连接池: DataSource
    ComboPooledDataSource -> C3P0
    DruidDataSource - >druid

Other:
    url: 链接地址  通用路径
    http://180.101.50.242:80
    ftp://192.168.0.1:23
    jdbc:mysql://127.0.0.1:3306

 协议://ip:port

