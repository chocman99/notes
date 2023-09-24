

### MyBatis简介



#### 一.MyBatis历史

MyBatis最初是Apache的一个开源项目iBatis, 2010年6月这个项目由Apache Software Foundation迁 移到了Google Code。随着开发团队转投Google Code旗下， iBatis3.x正式更名为MyBatis。代码于 2013年11月迁移到Github。 

iBatis一词来源于“internet”和“abatis”的组合，是一个基于Java的持久层框架。 iBatis提供的持久层框架 包括SQL Maps和Data Access Objects（DAO）。



#### 二.MyBatis特性

1） MyBatis 是支持定制化 SQL、存储过程以及高级映射的优秀的持久层框架

2） MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集

3） MyBatis可以使用简单的XML或注解用于配置和原始映射，将接口和Java的POJO（Plain Old Java Objects，普通的Java对象）映射成数据库中的记录

4） MyBatis 是一个 半自动的ORM（Object Relation Mapping）框架



#### 三.MyBatis下载

MyBatis下载地址：https://github.com/mybatis/mybatis-3





#### 四.和其它持久化层技术对比

JDBC
		SQL 夹杂在Java代码中耦合度高，导致硬编码内伤
		维护不易且实际开发需求中 SQL 有变化，频繁修改的情况多见
		代码冗长，开发效率低

Hibernate 和 JPA
		操作简便，开发效率高
		程序中的长难复杂 SQL 需要绕过框架
		内部自动生产的 SQL，不容易做特殊优化
		基于全映射的全自动框架，大量字段的 POJO 进行部分映射时比较困难。
		反射操作太多，导致数据库性能下降
		（注：Hibernate 是全自动化的，不需要去写sql代码）

MyBatis
		轻量级，性能出色
		SQL 和 Java 编码分开，功能边界清晰。Java代码专注业务、SQL语句专注数据
		开发效率稍逊于HIbernate，但是完全能够接受
		（注：MyBatis是半自动化的）





### 搭建MyBatis



#### 一.开发环境

IDE：idea 2021.2.2
构建工具：maven 3.8.4
MySQL版本：MySQL 8.0.28
MyBatis版本：3.5.10



#### 二.创建maven工程

1.打包方式：jar

2.引入依赖

```xml
<packaging>jar</packaging>

<dependencies>
    <!-- Mybatis核心 -->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.10</version>
    </dependency>
    <!-- junit测试 -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
    <!-- MySQL驱动 -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.28</version>
    </dependency>
</dependencies>
```



#### 三.创建MyBatis的核心配置文件

习惯上命名为mybatis-config.xml，这个文件名仅仅只是建议，并非强制要求。将来整合Spring 之后，这个配置文件可以省略，所以大家操作时可以直接复制、粘贴。

核心配置文件主要用于配置连接数据库的环境以及MyBatis的全局配置信息

核心配置文件存放的位置是src/main/resources目录下

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--配置连接数据库的环境-->
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis"/>
                <property name="username" value="root"/>
                <property name="password" value="1234"/>
            </dataSource>
        </environment>
    </environments>
    <!--引入映射文件-->
    <mappers>
        <mapper resource="org/mybatis/example/BlogMapper.xml"/>
    </mappers>
</configuration>
```



注：spring的约束是xml，mybatis的约束是dtd。功能是一样的。
	   dtd约束的DOCTYPE标签后边的单词必定是底下当前配置文件的根标签，此处是configuration

​		mybatis官方文档里有各种配置信息



#### 四.创建mapper接口

MyBatis中的mapper接口相当于以前的dao。但是区别在于，mapper仅仅是接口，我们不需要提供实现类。

```java
    //添加用户信息
    int insertUser();

}
```



为什么要创建mapper接口，因为mybatis有面向接口编程的功能。每当我们调用接口中的方法，它就会自动匹配一个sql语句，并且去执行



#### 五.创建MyBatis的映射文件

相关概念：ORM（Object Relationship Mapping）对象关系映射。
		对象：Java的实体类对象
		关系：关系型数据库
		映射：二者之间的对应关系

| Java概念 | 数据库概念 |
| -------- | ---------- |
| 类       | 表         |
| 属性     | 字段/列    |
| 对象     | 记录/行    |



1、映射文件的命名规则：
		表所对应的实体类的类名+Mapper.xml
		例如：表t_user，映射的实体类为User，所对应的映射文件为UserMapper.xml
		因此一个映射文件对应一个实体类，对应一张表的操作
		MyBatis映射文件用于编写SQL，访问以及操作表中的数据
		MyBatis映射文件存放的位置是src/main/resources/mappers目录下

2、MyBatis中可以面向接口操作数据，要保证两个一致：
		1）mapper接口的全类名和映射文件的命名空间（namespace）保持一致
		2）mapper接口中方法的方法名和映射文件中编写SQL的标签的id属性保持一致

表--实体类--mapper接口--映射文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.yc.mybatis.mapper.UserMapper">
    
    <insert id="insertUser">
        insert into t_user value (null,'admin','123456'.'男','123@qq.com')
    </insert>
    
</mapper>
```



#### 六.通过junit测试功能

MyBatis提供了一个操作数据库的会话对象，SqlSession

```java
@Test
public void testMyBatis() throws IOException {
    //加载核心配置文件
    InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
    //获取SqlSessionFactoryBuilder
    SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();
    //获取SqlSessionFactory
    SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.build(is);
    //获取SqlSession
    SqlSession sqlSession = sqlSessionFactory.openSession();
    //获取mapper接口对象  getMapper底层使用的代理模式，使用方法getMapper 的好处是：可以不需要对接口中的方法进行实现，由Mybaits 框架实现
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);
    //测试功能
    int result = mapper.insertUser();
    //提交事务
    sqlSession.commit();
    System.out.println("result:" + result);
}
```



SqlSession：代表Java程序和数据库之间的会话。（HttpSession是Java程序和浏览器之间的 会话） SqlSessionFactory：是“生产”SqlSession的“工厂”。
工厂模式：如果创建某一个对象，使用的过程基本固定，那么我们就可以把创建这个对象的 相关代码封装到一个“工厂类”中，以后都使用这个工厂类来“生产”我们需要的对象。

![image-20220714210814310](https://raw.githubusercontent.com/chocman99/Image/main/Mybatis/image-20220714210814310.png)



#### 七.加入log4j日志功能

1.加入依赖

```xml
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
</dependency>
```

2.加入log4j的配置文件

log4j的配置文件名为log4j.xml，存放的位置是src/main/resources目录下：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">
<log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">
    <appender name="STDOUT" class="org.apache.log4j.ConsoleAppender">
        <param name="Encoding" value="UTF-8" />
        <layout class="org.apache.log4j.PatternLayout">
            <param name="ConversionPattern" value="%-5p %d{MM-dd HH:mm:ss,SSS}
%m (%F:%L) \n" />
        </layout>
    </appender>
    <logger name="java.sql">
        <level value="debug" />
    </logger>
    <logger name="org.apache.ibatis">
        <level value="info" />
    </logger>
    <root>
        <level value="debug" />
        <appender-ref ref="STDOUT" />
    </root>
</log4j:configuration>
```

日志的级别
		FATAL(致命)>ERROR(错误)>WARN(警告)>INFO(信息)>DEBUG(调试)
		从左到右打印的内容越来越详细



#### 八.总结：测试增删改查功能

1.mapper接口：

```java
public interface UserMapper {

    /*
        MyBatis面向接口编程的两个一致：
        1.映射文件的namespace要和mapper接口的全类名保持一致
        2.映射文件中SQL语句的id要和mapper接口中的方法名一致

        表--实体类--mapper接口--映射文件
    */

    //添加用户信息
    int insertUser();

    //修改用户信息
    void updateUser();

    //删除用户信息
    void deleteUser();

    //根据id查询用户信息
    User getUserById();

    //查询所有的用户信息
    List<User> getAllUser();
    
}
```

2.MyBatis的映射文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.yc.mybatis.mapper.UserMapper">

    <!--int insertUser();-->
    <insert id="insertUser">
        insert into t_user value (null,'admin','123456',20,'男','123@qq.com')
    </insert>

    <!--void updateUser();-->
    <update id="updateUser">
        update t_user set username = '张三' where id = 4
    </update>

    <!--void deleteUser();-->
    <delete id="deleteUser">
        delete from t_user where id = 5
    </delete>

    <!--User getUserById();-->
    <!--
        查询功能的标签必须设置resultType或resultMap
        resultType：设置默认的映射关系
        resultMap：设置自定义的映射关系
    -->
    <select id="getUserById" resultType="com.yc.mybatis.pojo.User">
        select * from t_user where id = 3
    </select>

    <!--List<User> getAllUser();-->
    <select id="getAllUser" resultType="com.yc.mybatis.pojo.User">
        select * from t_user
    </select>

</mapper>
```

3.测试功能：

```java
public class MyBatisTest {

    //SqlSession默认不自动提交事务，若需要自动提交事务。可以使用sqlSessionFactory.openSession(true);
    
    //添加用户信息
    @Test
    public void testMyBatis() throws IOException {
        //加载核心配置文件
        InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
        //获取SqlSessionFactoryBuilder
        SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();
        //获取SqlSessionFactory
        SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.build(is);
        //获取SqlSession
        SqlSession sqlSession = sqlSessionFactory.openSession(true);    //true：设置自动提交事务
        //获取mapper接口对象  getMapper底层使用的代理模式，使用方法getMapper 的好处是：可以不需要对接口中的方法进行实现，由Mybaits 框架实现
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        //测试功能
        int result = mapper.insertUser();
        //提交事务
        //sqlSession.commit();
        System.out.println("result:" + result);
    }

    //修改用户信息
    @Test
    public void testUpdate() throws IOException {
        InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);;
        SqlSession sqlSession = sqlSessionFactory.openSession(true);
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        mapper.updateUser();
    }

    //删除用户信息
    @Test
    public void testDetele() throws IOException {
        InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);;
        SqlSession sqlSession = sqlSessionFactory.openSession(true);
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        mapper.deleteUser();
    }

    //根据id查询用户信息
    @Test
    public void testSelectUserById() throws IOException {
        InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);;
        SqlSession sqlSession = sqlSessionFactory.openSession(true);
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        User user = mapper.getUserById();
        System.out.println(user);
    }

    //查询所有用户信息
    @Test
    public void testSelectAllUser() throws IOException {
        InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);;
        SqlSession sqlSession = sqlSessionFactory.openSession(true);
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        List<User> list = mapper.getAllUser();
        list.forEach(user -> System.out.println(user));
    }
}
```



查询一条数据，对应的是实体类对象
查询多条数据，对应的就是list集合





### 核心配置文件详解



核心配置文件中的标签必须按照固定的顺序：

properties?,settings?,typeAliases?,typeHandlers?,objectFactory?,objectWrapperFactory?,reflectorFactory?,plugins?,environments?,databaseIdProvider?,mappers?

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

    <!--MyBatis核心配置文件中，标签的顺序：
        properties?,settings?,typeAliases?,typeHandlers?,
        objectFactory?,objectWrapperFactory?,reflectorFactory?,plugins?,
        environments?,databaseIdProvider?,mappers?-->

    <!--引入properties文件-->
    <properties resource="jdbc.properties"></properties>

    <!--设置类型别名-->
    <typeAliases>
        <!--typeAlias:设置某个类型的别名     （用的少，通常用package标签）
            属性：type：设置需要设置别名的类型
                 alias：设置某个类型的别名
                 (注：类型别名不区分大小写
                 如果不写alias，那所设置的类型将拥有默认的别名，这个别名就是他的类名，且不区分大小写，即如果不写alias，那么他的类名就是他的别名，不区分大小写)
            -->
<!--        <typeAlias type="com.yc.mybatis.pojo.User" alias="User"></typeAlias>-->

        <!--以包为单位，将包下所有的类型设置默认的类型别名，即类名且不区分大小写-->
        <package name="com.yc.mybatis.pojo"/>
    </typeAliases>

    <!--environments：配置多个连接数据库的环境
        属性：default：设置默认使用的环境的id
    -->
    <environments default="development">
        <!--environment：配置某个具体的环境
            属性：id：表示连接数据库的环境的唯一标识，不能重复
        -->
        <environment id="development">
            <!--transactionManager：设置事务管理方式
                属性：type=“JDBC/MANAGED"
                     JDBC:表示当前环境中，执行SQL时，使用的是JDBC中原生的事务管理方式，事务的提交或回滚需要手动处理
                     MANAGED:被管理，例如Spring
            -->
            <transactionManager type="JDBC"/>
            <!--dataSource：配置数据源
                属性：type：设置数据源的类型
                     type=”POOLED/UNPOOLED/JNDI“
                     POOLED:表示使用数据库连接池缓存数据库连接
                     UNPOOLED：表示不使用数据库连接池
                     JNDI：表示使用上下文中的数据源
            -->
            <dataSource type="POOLED">
                <!--设置连接数据库的驱动-->
                <property name="driver" value="${jdbc.driver}"/>
                <!--设置连接数据库的连接地址-->
                <property name="url" value="${jdbc.url}"/>
                <!--设置连接数据库的用户名-->
                <property name="username" value="${jdbc.username}"/>
                <!--设置连接数据库的密码-->
                <property name="password" value="${jdbc.password}"/>
            </dataSource>
        </environment>
    </environments>

    <!--引入映射文件-->
    <mappers>
<!--        <mapper resource="mappers/UserMapper.xml"/>-->
        <!--以包为单位引入映射文件
            要求：1.mapper接口所在的包要和映射文件所在的包一致   (resources目录下创建包时用/分隔，若用.分隔，那么.会作为包名创建出来)
                 2.mapper接口要和映射文件的名字一致
            -->
        <package name="com.yc.mybatis.mapper"/>
    </mappers>
</configuration>
```



### MyBatis的增删改查



1.添加

```xml
<!--int insertUser();-->
<insert id="insertUser">
    insert into t_user value (null,'admin','123456',20,'男','123@qq.com')
</insert>
```



2.删除

```xml
<!--void deleteUser();-->
<delete id="deleteUser">
    delete from t_user where id = 5
</delete>
```



3.修改

```xml
<!--void updateUser();-->
<update id="updateUser">
    update t_user set username = '张三' where id = 4
</update>
```



4.查询一个实体类对象

```xml
<!--User getUserById();-->
<!--
    查询功能的标签必须设置resultType或resultMap
    resultType：设置默认的映射关系
    resultMap：设置自定义的映射关系
-->
<select id="getUserById" resultType="com.yc.mybatis.pojo.User">
    select * from t_user where id = 3
</select>
```



5.查询集合

```xml
<!--List<User> getAllUser();-->
<select id="getAllUser" resultType="User">
    select * from t_user
</select>
```



注意： 
		1、查询的标签select必须设置属性resultType或resultMap，用于设置实体类和数据库表的映射关系 
				resultType：自动映射，用于属性名和表中字段名一致的情况 
				resultMap：自定义映射，用于一对多或多对一或字段名和属性名不一致的情况 
		2、当查询的数据为多条时，不能使用实体类作为返回值，只能使用集合，否则会抛出异常
				TooManyResultsException；但是若查询的数据只有一条，可以使用实体类或集合作为返回值



### MyBatis获取参数值的两种方式（重点）



MyBatis获取参数值的两种方式：${}和#{} 

${}的本质就是字符串拼接，#{}的本质就是占位符赋值 

${}使用字符串拼接的方式拼接sql，若为字符串类型或日期类型的字段进行赋值时，需要手动加单引号；但是#{}使用占位符赋值的方式拼接sql，此时为字符串类型或日期类型的字段进行赋值时，可以自动添加单引号，不用手动添加了



#### 一.单个字面量类型的参数

若mapper接口中的方法参数为单个的字面量类型

此时可以使用${}和#{}以任意的名称获取参数的值，注意${}需要手动加单引号

一般情况下不使用字符串拼接：很麻烦，而且会造成Sql注入。
若能用#{}，就不用${}。除非必须要使用${}

案例：（获取sqlSession在utils工具类里SqlSessionUtils）

创建mapper接口

```java
//根据用户名查询用户信息
User getUserByUsername(String username);
```

创建映射文件

```xml
<!--User getUserByUsername(String username);-->
<select id="getUserByUsername" resultType="User">
    <!--select * from t_user where username = #{username}-->
    select * from t_user where username = '${username}'
</select>
```

实现功能

```java
@Test
public void testGetUserByUsername(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    ParameterMapper mapper = sqlSession.getMapper(ParameterMapper.class);
    User user = mapper.getUserByUsername("admin");
    System.out.println(user);
```

```java
//封装的sqlSession类，以后再实现功能直接调用即可
public class SqlSessionUtils {

    public static SqlSession getSqlSession(){
        SqlSession sqlSession = null;
        try {
            InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
            SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);
            sqlSession = sqlSessionFactory.openSession(true);
        } catch (IOException e) {
            e.printStackTrace();
        }
        return sqlSession;
    }

}
```



#### 二.多个字面量类型的参数

若mapper接口中的方法参数为多个时
此时MyBatis会自动将这些参数放在一个map集合中，以arg0,arg1...为键，以参数为值；以 param1,param2...为键，以参数为值；因此只需要通过${}和#{}访问map集合的键就可以获取相对应的 值，注意${}需要手动加单引号

理解：
在mybatis底层，如果检测到了当前mapper接口中的方法有多个参数时，它会自动把这些参数放在map集合里，这个mapper集合里会以两种方式存取数据：
		1.以arg0、arg1...为键，以参数为值
		2.以param1，param2...为键，以参数为值

案例：

创建mapper接口

```java
//验证登录
User checkLogin(String username , String password);
```

创建映射文件

```xml
<!--User checkLogin(String username , String password);-->
<select id="checkLogin" resultType="User">
    select * from t_user where username = #{param1} and password= #{param2}
</select>
```

实现功能

```java
@Test
public void testCheckLogin(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    ParameterMapper mapper = sqlSession.getMapper(ParameterMapper.class);
    User user = mapper.checkLogin("admin", "1234");
    System.out.println(user);
}
```



#### 三.map集合类型的参数

若mapper接口中的方法需要的参数为多个时，此时可以手动创建map集合，将这些数据放在map中
只需要通过${}和#{}访问map集合的键就可以获取相对应的值，注意${}需要手动加单引号

案例：

创建mapper接口

```java
//验证登录（参数为map）
User checkLoginByMap(Map<String,Object> map);
```

创建映射文件

```xml
<!--User checkLoginByMap(Map<String,Object> map);-->
<select id="checkLoginByMap" resultType="User">
    select * from t_user where username = #{username} and password= #{password}
</select>
```

实现功能

```java
@Test
public void testCheckLoginByMap(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    ParameterMapper mapper = sqlSession.getMapper(ParameterMapper.class);
    Map<String,Object> map = new HashMap<>();
    map.put("username","admin");
    map.put("password","123456");
    User user = mapper.checkLoginByMap(map);
    System.out.println(user);
```



#### 四.实体类类型的参数

若mapper接口中的方法参数为实体类对象时
此时可以使用${}和#{}，通过访问实体类对象中的属性名获取属性值，注意${}需要手动加单引号

案例：

创建mapper接口

```java
//添加用户信息
int insertUser(User user);
```

创建映射文件

```xml
<!--int insertUser(User user);-->
<insert id="insertUser">
    insert into t_user values(null,#{username},#{password},#{age},#{sex},#{email})
</insert>
```

实现功能

```java
@Test
public void testInsertUser(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    ParameterMapper mapper = sqlSession.getMapper(ParameterMapper.class);
    int result = mapper.insertUser(new User(null, "李四", "123", 23, "男", "1234@qq.com"));
    System.out.println(result);
}
```



#### 五.使用@Param标识参数

可以通过@Param注解标识mapper接口中的方法参数
此时，会将这些参数放在map集合中，以@Param注解的value属性值为键，以参数为值；以 param1,param2...为键，以参数为值；只需要通过${}和#{}访问map集合的键就可以获取相对应的值， 注意${}需要手动加单引号

案例：

创建mapper接口

```java
//验证登录（使用@Param）
User checkLoginByParam(@Param("username") String username , @Param("password") String password);
```

创建映射文件

```xml
<!--User checkLoginByParam(@Param("usernanme") String username , @Param("password") String password);-->
<select id="checkLoginByParam" resultType="User">
    select * from t_user where username = #{username} and password= #{password}
</select>
```

实现功能

```java
@Test
public void testCheckLoginByParam() {
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    ParameterMapper mapper = sqlSession.getMapper(ParameterMapper.class);
    User user = mapper.checkLoginByParam("admin", "123456");
    System.out.println(user);
}
```



#### 总结

MyBatis获取参数值的两种方式：${}和#{}
${}本质就是字符串拼接
#{}本质就是占位符赋值
若能用#{}，就不用${}。除非必须要使用${}

MyBatis获取参数的各种情况：
		1.mapper接口方法的参数为单个字面量类型
				可以通过${}和#{}以任意的名称获取参数值，但是需要注意${}的单引号问题
		2.mapper接口方法的参数为多个时
				此时MyBatis会将这些参数放在一个map集合中，以两种方式进行存储
						a> 以arg0、arg1...为键，以参数为值
						b> 以param1，param2...为键，以参数为值
				因此只需要通过#{}和${}以键的方式访问值即可，但是需要注意${}的单引号问题
		3.若mapper接口方法的参数有多个时，可以手动将这些参数放在一个map中存储
				只需要通过#{}和${}以键的方式访问值即可，但是需要注意${}的单引号问题
		4.mapper接口方法的参数是实体类类型的参数
				只需要通过#{}和${}以属性的方式访问属性值即可，但是需要注意${}的单引号问题
		5.使用@Param注解命名参数
				此时MyBatis会将这些参数放在一个map集合中，以两种方式进行存储
						a> 以@Param注解的值为键，以参数为值
						b> param1，param2...为键，以参数为值
				因此只需要通过#{}和${}以键的方式访问值即可，但是需要注意${}的单引号问题

**建议**：最终整合为两种情况使用：
		1.实体类对象（第4种）
		2.全部都用@Param（第5种）
（当然用哪种方法都可以）



### MyBatis的各种查询功能



#### 一.查询一个实体类对象

案例：

创建mapper接口

```java
//根据id查询用户信息
List<User> getUserById(@Param("id") Integer id);
```

创建映射文件

```xml
<!--User getUserById(@Param("id") Integer id);-->
<select id="getUserById" resultType="User">
    select * from t_user where id = #{id}
</select>
```

实现功能

```java
@Test
public void testGetUserById(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    SelectMapper mapper = sqlSession.getMapper(SelectMapper.class);
    System.out.println(mapper.getUserById(3));
}
```



#### 二.查询一个list集合

案例：

创建mapper接口

```java
//查询所有的用户信息
List<User> getAllUser();
```

创建映射文件

```xml
<!--List<User> getAllUser();-->
<select id="getAllUser" resultType="User">
    select * from t_user
</select>
```

实现功能

```java
@Test
public void testGetAllUser(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    SelectMapper mapper = sqlSession.getMapper(SelectMapper.class);
    System.out.println(mapper.getAllUser());
}
```



#### 三.查询单个数据

案例：

创建mapper接口

```java
//查询用户信息的总记录数
Integer getCount();
```

创建映射文件

```xml
<!--Integer getCount();-->
<select id="getCount" resultType="Integer">    <!--resultType里写java.long.Integer或者Integer或者integer或者Int或者int都可以，在MyBatis官方文档里可以看到是因为类型别名-->
    select count(*) from t_user
</select>
```

实现功能

```java
@Test
public void testGetCount(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    SelectMapper mapper = sqlSession.getMapper(SelectMapper.class);
    System.out.println(mapper.getCount());
}
```



#### 四.查询一条数据为map集合

案例：

创建mapper接口

```java
//根据用户id查询用户信息为map集合
Map<String,Object> getUserByIdToMap(@Param("id") Integer id);
```

创建映射文件

```xml
<!--Map<String,Object> getUserByIdToMap(@Param("id") Integer id);-->
<select id="getUserByIdToMap" resultType="map">
    select * from t_user where id = #{id}
</select>
```

实现功能

```java
@Test
public void testGetUserByIdToMap(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    SelectMapper mapper = sqlSession.getMapper(SelectMapper.class);
    System.out.println(mapper.getUserByIdToMap(3));
}
```



#### 五.查询多条数据为map集合

方法一：

案例：

创建mapper接口

```java
//查询所有用户信息为map集合        查询出来一条数据会转换为一个map。要是查询多条数据，每一条数据都会转换成map，那么不能用一个map集合去接收，因为这和用实体类对象接收多条数据是同一个性质。可以把多个map放到一个list集合中
List<Map<String,Object>> getAllUserToMap();
```

创建映射文件

```xml
<!--Map<String,Object> getAllUserToMap();-->
<select id="getAllUserToMap" resultType="map">
    select * from t_user
</select>
```

实现功能

```java
@Test
public void testGetAllUserToMap(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    SelectMapper mapper = sqlSession.getMapper(SelectMapper.class);
    System.out.println(mapper.getAllUserToMap());
}
```



方法二：

创建mapper接口（通过id作为标识查询多条数据）

```java
@MapKey("id")   //设置map集合的键，它会把当前查询出来的数据的某一个字段来作为键，把当前查询出来的数据转换成的map集合作为值
Map<String,Object> getAllUserToMap();
```

输出的结果：

```
{3={password=123456, sex=男, id=3, age=20, email=123@qq.com, username=admin}, 4={password=123456, sex=男, id=4, age=20, email=123@qq.com, username=张三}, 6={password=123, sex=男, id=6, age=23, email=1234@qq.com, username=李四}}
```





#### 总结

MyBatis的各种查询功能
1.若查询出的数据只有一条
		a>可以通过实体类对象接收
		b>可以通过list集合接收
		c>可以通过map集合接收（以字段为键，以字段所对应的值为值）
				结果：{password=123456, sex=男, id=3, age=20, email=123@qq.com, username=admin}
2.若查询出的数据有多条
		a>可以通过实体类类型的list集合接收
		b>可以通过map类型的list集合接收
		c>可以在mapper接口的方法上添加@MapKey注解，此时就可以将每条数据转换的map集合作为值，以某个字段的值作为键，放在同一个map结合中
注意：一定不能通过实体类对象接收，此时会抛出异常TooManyResultsException

MyBatis中设置了默认的类型别名：
		java.long.Integer-->int,integer
		Map-->map
		String-->string
		...





### 特殊SQL的执行



#### 一.模糊查询（前两种方法不能用#{}）

三种模糊查询的sql语句。前两种不能用#{}，第三种可以，第三种直接拼接是最常用的

案例：

创建mapper接口

```java
//根据用户名模糊查询用户信息
List<User> getUserByLike(@Param("username") String username);
```

创建映射文件

```xml
<!--List<User> getUserByLike(@Param("username") String username);-->
<select id="getUserByLike" resultType="User">
    <!--select * from t_user where username like '%${username}%'-->    <!--使用${}的方法。不能用#{}，因为sql语句中，单引号代表里面是字符串，那么问号就代表字符串，不会被解析成占位符-->
    <!--select * from t_user where username like concat('%',#{username},'%')-->    <!--使用字符串拼接的方法。concat进行字符串拼接-->
    select * from t_user where username like "%"#{username}"%"  <!--在两边百分号加上双引号，中间直接拼接#{}的内容-->
</select>
```

实现功能

```java
@Test
public void testGetUserByLike(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    SQLMapper mapper = sqlSession.getMapper(SQLMapper.class);
    List<User> list = mapper.getUserByLike("a");
    System.out.println(list);
}
```



#### 二.批量删除（不能用#{}）

案例：

创建mapper接口

```java
//批量删除
int deleteMore(@Param("ids") String ids);
```

创建映射文件

```xml
<!--int deleteMore(@Param("ids") String ids);-->
<delete id="deleteMore">
    delete from t_user where id in(${ids})
</delete>
```

实现功能

```java
@Test
public void testDeleteMore(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    SQLMapper mapper = sqlSession.getMapper(SQLMapper.class);
    int result = mapper.deleteMore("1,2,3");
    System.out.println(result);
}
```



#### 三.动态设置表名（不能用#{}）

案例：

创建mapper接口

```java
//动态设置表名,查询指定表中的数据
List<User> getUserByTableName(@Param("tableName") String tableName);
```

创建映射文件

```xml
<!--List<User> getUserByTableName(@Param("tableName") String tableName);-->
<select id="getUserByTableName" resultType="User">
    select * from ${tableName}  <!--不能用#{}，否则有单引号-->
</select>
```

实现功能

```java
@Test
public void testGetUserByTableName(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    SQLMapper mapper = sqlSession.getMapper(SQLMapper.class);
    List<User> list = mapper.getUserByTableName("t_user");
    System.out.println(list);
}
```



#### 四.添加功能获取自增的主键

案例：

创建mapper接口

```java
//添加用户信息
void insertUser(User user);
```

创建映射文件

```xml
<!--void insertUser(User user);-->
<!--
    useGeneratedKeys:设置当前标签中的sql使用了自增的id
    keyProperty：将自增的主键的值赋值给传输到映射文件中参数的某个属性
    （若不加这两个属性，idea里输出的结果的id就是null，不会显示出来，不过数据库上边的id还是会自增）
-->
<insert id="insertUser" useGeneratedKeys="true" keyProperty="id">
    insert into t_user values(null,#{username},#{password},#{age},#{sex},#{email})
</insert>
```

实现功能

```java
@Test
public void testInsertUser(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    SQLMapper mapper = sqlSession.getMapper(SQLMapper.class);
    User user = new User(null,"王五","123",24,"男","123@163.com");
    mapper.insertUser(user);
    System.out.println(user);
}
```





### 自定义映射resultMap



#### 一.resultMap处理字段和属性的映射关系

若字段名和实体类中的属性名不一致，字段名符合数据库的规则（使用_），实体类中的属性名符合Java的规则（使用驼峰），即若字段名和实体类中的属性名不一致，那就赋不了值，则可以通过三种方法解决

有三种方法：

1.为字段名起别名，保持和属性名的一致

案例：

创建mapper接口

```java
//查询所有的员工信息
List<Emp> getAllEmp();
```

创建映射文件

```xml
<!--List<Emp> getAllEmp();-->
<select id="getAllEmp" resultType="Emp">
    select eid,emp_name empName,age sex,email from t_emp
</select>
```

实现功能

```java
@Test
public void testGetAllEmp(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    EmpMapper mapper = sqlSession.getMapper(EmpMapper.class);
    List<Emp> list = mapper.getAllEmp();
    list.forEach(emp -> System.out.println(emp));
}
```



2.全局配置

在mybatis配置文件中，设置全局配置mapUnderscoreToCamelCase：

```xml
<!--设置全局配置-->
<settings>
    <!--将下划线自动映射为驼峰，emp_name:empName-->
    <setting name="mapUnderscoreToCamelCase" value="ture"/>
</settings>
```

配置完后就可以在mapper映射文件里写select * from t_emp



3.resultMap

```xml
<!--
    resultMap：设置自定义映射关系
    id：唯一标识，不能重复
    type：设置映射关系中的实体类类型
    子标签：
        id：设置主键的映射关系
        result：设置普通字段的映射关系
    属性：
        property：设置映射关系中的属性名，必须是type属性所设置的实体类类型中的属性名
        column：设置映射关系中的字段名，必须是sql语句查询出的字段名
-->
<resultMap id="empResulterMap" type="Emp">
    <id property="eid" column="eid"></id>
    <result property="empName" column="emp_name"></result>
    <result property="age" column="age"></result>
    <result property="sex" column="sex"></result>
    <result property="email" column="email"></result>
</resultMap>

<select id="getAllEmp" resultMap="empResulterMap">
    select * from t_emp
</select>
```



#### 二.多对一映射处理（对一，对对象）

有三种方式：

##### 1.处理多对一映射关系方式一：级联属性

案例：

创建mapper接口

```java
//查询员工以及员工所对应的部门信息
List<Emp> getEmpAndDept(@Param("eid") Integer eid);
```

创建映射文件

```xml
<!--处理多对一映射关系方式一：级联属性-->
<resultMap id="empAndDeptResultMapOne" type="Emp">
    <id property="eid" column="eid"></id>
    <result property="empName" column="emp_name"></result>
    <result property="age" column="age"></result>
    <result property="sex" column="sex"></result>
    <result property="email" column="email"></result>
    <result property="dept.did" column="did"></result>
    <result property="dept.deptName" column="dept_name"></result>
</resultMap>
<!--Emp getEmpAndDept(@Param("eid") Integer eid);-->
<select id="getEmpAndDept" resultMap="empAndDeptResultMapOne">
    select * from t_emp left join t_dept on t_emp.did = t_dept.did where t_emp.did = #{eid}
</select>
```

实现功能

```java
@Test
public void testGetEmpAndDept(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    EmpMapper mapper = sqlSession.getMapper(EmpMapper.class);
    List<Emp> emp = mapper.getEmpAndDept(1);
    System.out.println(emp);
}
```



##### 2.处理多对一映射关系方式二：association

创建映射文件

```xml
<!--处理多对一映射关系方式二：association-->
<resultMap id="empAndDeptResultMapTwo" type="Emp">
    <id property="eid" column="eid"></id>
    <result property="empName" column="emp_name"></result>
    <result property="age" column="age"></result>
    <result property="sex" column="sex"></result>
    <result property="email" column="email"></result>
    <!--association：处理多对一的映射关系
        property：需要处理多对一的映射关系的属性名
        javaType：该属性的类型
    -->
    <association property="dept" javaType="Dept">
        <id property="did" column="did"></id>
        <result property="deptName" column="dept_name"></result>
    </association>
</resultMap>
<!--Emp getEmpAndDept(@Param("eid") Integer eid);-->
<select id="getEmpAndDept" resultMap="empAndDeptResultMapTwo">
    select * from t_emp left join t_dept on t_emp.did = t_dept.did where t_emp.did = #{eid}
</select>
```



##### 3.处理多对一映射关系方式二：分步查询

1）查询员工信息

EmpMapper接口中：

```java
/*
    通过分布查询，查询员工以及员工所对应的部门信息
    分布查询第一步：查询员工信息
 */
List<Emp> getEmpAndDeptByStepOne(@Param("eid") Integer eid);
```

EmpMapper映射文件中：

```xml
<resultMap id="empAndDeptByStepResultMap" type="Emp">
    <id property="eid" column="eid"></id>
    <result property="empName" column="emp_name"></result>
    <result property="age" column="age"></result>
    <result property="sex" column="sex"></result>
    <result property="email" column="email"></result>
    <!--select:设置分布查询的sql的唯一标识（namespace.SQLId或mapper接口的全类名.方法名）、
        column:设置分布查询的条件
    -->
    <association property="dept"
                 select="com.yc.mybatis.mapper.DeptMapper.getEmpAndDeptByStepTwo"
                 column="did">
    </association>
</resultMap>
<!--List<Emp> getEmpAndDeptByStepOne(@Param("eid") Integer eid);-->
<select id="getEmpAndDeptByStepOne" resultMap="empAndDeptByStepResultMap">
    select * from t_emp where eid = #{eid}
</select>
```

2）根据员工所对应的部门id查询部门信息

DeptMapper接口中：

```java
/*
    通过分布查询，查询员工以及员工所对应的部门信息
    分布查询第二步：通过did查询员工所对应的部门
 */
Dept getEmpAndDeptByStepTwo(@Param("did") Integer did);
```

DeptMapper映射文件中（开启驼峰自动转换，用resultType即可）：

```xml
<!--Dept getEmpAndDeptByStepTwo(@Param("did") Integer did);-->
<select id="getEmpAndDeptByStepTwo" resultType="Dept">
    select * from t_dept where  did = #{did}
</select>
```

3）实现功能

```java
@Test
public void testGetEmpAndDeptByStep(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    EmpMapper mapper = sqlSession.getMapper(EmpMapper.class);
    List<Emp> emp = mapper.getEmpAndDeptByStepOne(1);
    System.out.println(emp);
}
```



分步查询的优点：可以实现延迟加载，但是必须在核心配置文件中设置全局配置信息：

lazyLoadingEnabled：延迟加载的全局开关。当开启时，所有关联对象都会延迟加载

aggressiveLazyLoading：当开启时，任何方法的调用都会加载该对象的所有属性。 否则，每个属性会按需加载

此时就可以实现按需加载，获取的数据是什么，就只会执行相应的sql。此时可通过association和collection中的fetchType属性设置当前的分步查询是否使用延迟加载，fetchType="lazy(延迟加载)|eager(立即加载)"



#### 三.一对多映射处理（对多，对集合）

有两种方式：

##### 1.collection

创建mapper接口

```java
//获取部门以及部门中所有的员工信息
Dept getDeptAndEmp(@Param("did") Integer did);
```

创建映射文件

```xml
<resultMap id="deptAndEmpResultMap" type="Dept">
    <id property="did" column="did"></id>
    <result property="deptName" column="dept_name"></result>
    <!--collection：处理一对多的映射关系
        ofType：表示该属性所对应的集合中存储数据的类型
    -->
    <collection property="emps" ofType="Emp">
        <id property="eid" column="eid"></id>
        <result property="empName" column="emp_name"></result>
        <result property="age" column="age"></result>
        <result property="sex" column="sex"></result>
        <result property="email" column="email"></result>
    </collection>
</resultMap>
<!--Dept getDeptAndEmp(@Param("did") Integer did);-->
<select id="getDeptAndEmp" resultMap="deptAndEmpResultMap">
    select * from t_dept left join t_emp on t_dept.did = t_emp.did where t_dept.did = #{did}
</select>
```

实现功能

```java
@Test
public void testGetDeptAndEmp(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    DeptMapper mapper = sqlSession.getMapper(DeptMapper.class);
    Dept dept = mapper.getDeptAndEmp(1);
    System.out.println(dept);
}
```



##### 2.分步查询

1）查询部门信息

EmpMapper接口中：

```java
/*
    通过分步查询，查询部门以及部门中所有的员工信息
    分步查询第一步：查询部门信息
 */
Dept getDeptAndEmpByStepOne(@Param("did") Integer did);
```

EmpMapper映射文件中：

```xml
<resultMap id="deptAndEmpByStepResultMap" type="Dept">
    <id property="did" column="did"></id>
    <result property="deptName" column="dept_name"></result>
    <collection property="emps"
                select="com.yc.mybatis.mapper.EmpMapper.getDeptAndEmpByStepTwo"
                column="did"
                fetchType="eager"></collection>
</resultMap>
<!--Dept getDeptAndEmpByStepOne(@Param("did") Integer did);-->
<select id="getDeptAndEmpByStepOne" resultMap="deptAndEmpByStepResultMap">
    select * from t_dept where did = #{did}
</select>
```

2）根据部门id查询部门中的所有员工

EmpMapper接口中：

```java
    /*
    通过分步查询，查询部门以及部门中所有的员工信息
    分步查询第二步：根据did查询员工信息 （跟上边的第一步不是一起的，和DeptMapper里的第一步是一起的）
 */
List<Emp> getDeptAndEmpByStepTwo(@Param("did") Integer did);
```

EmpMapper映射文件中：

```xml
<!--List<Emp> getDeptAndEmpByStepTwo(@Param("did") Integer did);-->
<select id="getDeptAndEmpByStepTwo" resultType="Emp">
    select * from t_emp where did = #{did}
</select>
```



3）实现功能

```java
    @Test
    public void testGetDeptAndEmpByStep(){
        SqlSession sqlSession = SqlSessionUtils.getSqlSession();
        DeptMapper mapper = sqlSession.getMapper(DeptMapper.class);
        Dept dept = mapper.getDeptAndEmpByStepOne(1);
//        System.out.println(dept);
        System.out.println(dept.getDeptName());
    }
```



一对多分步查询的优点与多对一的分步查询的优点相同



#### 总结：

```
/*
* 解决字段名和属性名不一致的情况：
*   a>为字段名起别名，保持和属性名的一致
*   b>设置全局配置，将下划线自动映射为驼峰
*       <setting name="mapUnderscoreToCamelCase" value="ture"/>
*   c>通过resultMap设置自定义的映射关系
*       <resultMap id="empResulterMap" type="Emp">
            <id property="eid" column="eid"></id>
            <result property="empName" column="emp_name"></result>
            <result property="age" column="age"></result>
            <result property="sex" column="sex"></result>
            <result property="email" column="email"></result>
        </resultMap>
*
* 处理多对一的映射关系：
*   a>级联属性赋值
*   b>association
*   c>分步查询
*
* 处理一对多的映射关系：
*   a>collection
*   b>分步查询
*/
```





### 动态SQL



Mybatis框架的动态SQL技术是一种根据特定条件动态拼装SQL语句的功能，它存在的意义是为了解决
拼接SQL语句字符串时的痛点问题



#### 一.if

if标签可通过test属性的表达式进行判断，若表达式的结果为true，则标签中的内容会执行；反之标签中
的内容不会执行

mapper接口：

```java
//多条件查询
List<Emp> getEmpByCondition(Emp emp);
```

映射文件：

```xml
<!--List<Emp> getEmpByCondition(Emp emp);-->
<select id="getEmpByCondition" resultType="Emp">
    select * from t_emp where 1=1
    <if test="empName != null and empName != ''">
        and emp_name = #{empName}
    </if>
    <if test="age != null and age != ''">
        and age = #{age}
    </if>
    <if test="sex != null and sex != ''">
        and sex = #{sex}
    </if>
    <if test="email != null and email != ''">
        and email = #{email}
    </if>
</select>
```

测试：

```java
@Test
public void testGetEmpByCondition(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    DynamicSQLMapper mapper = sqlSession.getMapper(DynamicSQLMapper.class);
    List<Emp> list = mapper.getEmpByCondition(new Emp(null, "张三", 23, "男", "123@qq.com"));
    System.out.println(list);
}
```



#### 二.where

映射文件：

```xml
<!--List<Emp> getEmpByCondition(Emp emp);-->    <!--同样的接口，把上边的sql语句标识改了，让程序匹配这个标识的SQL语句-->
<select id="getEmpByCondition" resultType="Emp">
    select * from t_emp
    <where>
        <if test="empName != null and empName != ''">
            and emp_name = #{empName}
        </if>
        <if test="age != null and age != ''">
            and age = #{age}
        </if>
        <if test="sex != null and sex != ''">
            and sex = #{sex}
        </if>
        <if test="email != null and email != ''">
            and email = #{email}
        </if>
    </where>
</select>
```



where和if一般结合使用：
a>若where标签中的if条件都不满足，则where标签没有任何功能，即不会添加where关键字
b>若where标签中的if条件满足，则where标签会自动添加where关键字，并将条件最前方多余的and去掉
注意：where标签不能去掉条件最后多余的and



#### 三.trim

映射文件：

```xml
<!--List<Emp> getEmpByCondition(Emp emp);-->    <!--同样的接口，把上边的sql语句标识改了，让程序匹配这个标识的SQL语句-->
<select id="getEmpByCondition" resultType="Emp">
    select * from t_emp
    <trim prefix="where" prefixOverrides="and|or">
        <if test="empName != null and empName != ''">
            and emp_name = #{empName}
        </if>
        <if test="age != null and age != ''">
            and age = #{age}
        </if>
        <if test="sex != null and sex != ''">
            and sex = #{sex}
        </if>
        <if test="email != null and email != ''">
            and email = #{email}
        </if>
    </trim>
</select>
```



trim用于去掉或添加标签中的内容
常用属性：
prefix：在trim标签中的内容的前面添加某些内容
prefixOverrides：在trim标签中的内容的前面去掉某些内容
suffix：在trim标签中的内容的后面添加某些内容
suffixOverrides：在trim标签中的内容的后面去掉某些内容



#### 四.choose、when、otherwise

choose、when、otherwise相当于if...else if..else

mapper接口：

```java
//测试choose、when、otherwise
List<Emp> getEmpByChoose(Emp emp);
```

映射文件：

```xml
<!--List<Emp> getEmpByChoose(Emp emp);-->   <!--如果有一个when标签里的语句成立，那么后边的就都不会执行了，就相当于if else语句-->
<select id="getEmpByChoose" resultType="Emp">
    select * from t_emp
    <where>
        <choose>
            <when test="empName != null and empName !=''">
                emp_name = #{empName}
            </when>
            <when test="age != null and age !=''">
                age = #{age}
            </when>
            <when test="sex != null and sex !=''">
                sex = #{sex}
            </when>
            <when test="email != null and email !=''">
                email = #{email}
            </when>
            <otherwise>
                did = 1
            </otherwise>
        </choose>
    </where>
</select>
```

测试：

```java
@Test
public void testGetEmpByChoose(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    DynamicSQLMapper mapper = sqlSession.getMapper(DynamicSQLMapper.class);
    List<Emp> list = mapper.getEmpByChoose(new Emp(null, "张三", 23, "男", "123@qq.com"));
    System.out.println(list);
}
```



#### 五.foreach

可以通过foreach实现批量删除和批量添加的操作



##### 1.通过数组实现批量删除

mapper接口：

```java
//通过数组实现批量删除
int deleteMoreByArray(@Param("eids") Integer[] eids);
```

映射文件：

```xml
<!--int deleteMoreByArray(@Param("eids") Integer[] eids);-->
<delete id="deleteMoreByArray">
    <!--第一种写法
        delete from t_emp where eid in
        <foreach collection="eids" item="eid" separator="," open="(" close=")">
            #{eid}
        </foreach>
    -->

    <!--第二种写法-->
    delete from t_emp where
    <foreach collection="eids" item="eid" separator="or">
        eid = #{eid}
    </foreach>

</delete>
```

测试：

```java
@Test
public void testdeleteMoreByArray(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    DynamicSQLMapper mapper = sqlSession.getMapper(DynamicSQLMapper.class);
    int result = mapper.deleteMoreByArray(new Integer[]{6, 7, 8});
    System.out.println(result);
}
```



##### 2.通过List集合实现批量添加

mapper接口：

```java
//通过List集合实现批量添加
int insertMoreByList(@Param("emps") List<Emp> emps);
```

映射文件：

```xml
<!--int insertMoreByList(@Param("emps") List<Emp> emps);-->
<insert id="insertMoreByList">
    insert into t_emp value
    <foreach collection="emps" item="emp" separator=",">
        (null,#{emp.empName},#{emp.age},#{emp.sex},#{emp.email},null)	<!--如果是集合，需要指明集合里对象的属性 -->
    </foreach>
</insert>
```

测试：

```java
@Test
public void testInsertMoreByList(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    DynamicSQLMapper mapper = sqlSession.getMapper(DynamicSQLMapper.class);
    Emp emp1 = new Emp(null,"a",23,"男","1234@qq.com");
    Emp emp2 = new Emp(null,"b",32,"男","1234@qq.com");
    Emp emp3 = new Emp(null,"c",22,"男","1234@qq.com");
    List<Emp> emps = Arrays.asList(emp1, emp2, emp3);
    System.out.println(mapper.insertMoreByList(emps));
}
```



属性：
collection：设置要循环的数组或集合
item：表示集合或数组中的每一个数据
separator：设置循环体之间的分隔符
open：设置foreach标签中的内容的开始符
close：设置foreach标签中的内容的结束符



#### 六.SQL片段

sql片段，可以记录一段公共sql片段，在使用的地方通过include标签进行引入

```xml
<!--设置sql片段-->
<sql id="empColumns">eid,emp_name,age,sex,email</sql>
```

```xml
<!--查询语句时可用sql片段来代替-->
select <include refid="empColumns"></include> from t_emp
```





#### 总结

```
/**
 * 动态SQL：
 * 1.if：根据标签中test属性所对应的表达式决定标签中的内容是否需要拼接到SQL中
 * 2.where:
 *      当where标签中有内容时，会自动生成where关键字，并且将内容前多余的and或or去掉
 *      where标签中没有内容时，此时where标签没有任何效果
 *      注意：where标签不能将其中内容后面多余的and或or去掉
 * 3.trim：
 * 若标签中有内容时：
 *      prefix:将trim标签中内容前面添加指定内容
 *      suffix:将trim标签中内容后面添加指定内容
 *      prefixOverrides:将trim标签中内容前面去掉指定内容
 *      suffixOverrides:将trim标签中内容后面去掉指定内容
 * 若标签中没有内容时，trim标签也没有任何效果
 * 4.choose、when、otherwise，相当于if...else if...else
 *      when至少要有一个，otherwise最多只能有一个
 * 5.foreach
 *      collection:设置需要循环的数组或集合
 *      item：表示数组或集合中的每一个数据
 *      separator：循环体之间的分隔符
 *      open：表示foreach标签所循环的所有内容的开始符
 *      close：表示foreach标签所循环的所有内容的结束符
 * 6.sql标签
 *      设置SQL片段：<sql id="empColumns">eid,emp_name,age,sex,email</sql>
 *      引用SQL片段：<include refid="empColumns"></include>
 */
```





### MyBatis的缓存

缓存只对查询功能有效果



#### 一.MyBatis的一级缓存

一级缓存是默认开启的

一级缓存是SqlSession级别的，通过同一个SqlSession查询的数据会被缓存，下次查询相同的数据，就会从缓存中直接获取，不会从数据库重新访问

使一级缓存失效的四种情况：

1) 不同的SqlSession对应不同的一级缓存
2) 同一个SqlSession但是查询条件不同
3) 同一个SqlSession两次查询期间执行了任何一次增删改操作
4) 同一个SqlSession两次查询期间手动清空了缓试，即使用clearCache()，不过clearCache()只会对一级缓存有效果







```java
//测试一级缓存
Emp getEmpByEid(@Param("eid") Integer eid);

void insertEmp(Emp emp);
```

```xml
<!--Emp getEmpByEid(@Param("eid") Integer eid);-->
<select id="getEmpByEid" resultType="Emp">
    select * from t_emp where eid =#{eid}
</select>

<!--void insertEmp(Emp emp);-->
<insert id="insertEmp">
    insert into t_emp value (null,#{empName},#{age},#{sex},#{email},null)
</insert>
```

```java
//测试一级缓存，通过两个SqlSession使缓存失效
@Test
public void testCache(){
    SqlSession sqlSession1 = SqlSessionUtils.getSqlSession();
    CacheMapper mapper1 = sqlSession1.getMapper(CacheMapper.class);
    Emp emp1 = mapper1.getEmpByEid(1);
    System.out.println(emp1);

    SqlSession sqlSession2 = SqlSessionUtils.getSqlSession();
    CacheMapper mapper2 = sqlSession2.getMapper(CacheMapper.class);
    Emp emp2 = mapper2.getEmpByEid(1);
    System.out.println(emp2);
}

//通过增删改和手动清空缓存使缓存失效
@Test
public void testCache2(){
    SqlSession sqlSession1 = SqlSessionUtils.getSqlSession();
    CacheMapper mapper1 = sqlSession1.getMapper(CacheMapper.class);
    Emp emp1 = mapper1.getEmpByEid(1);
    System.out.println(emp1);

    //两次查询中增加一次添加的操作（增删改会造成清空缓存）
//    mapper1.insertEmp(new Emp(null,"abc",23,"男","12345@qq.com"));

    //手动清空缓存
    sqlSession1.clearCache();

    Emp emp2 = mapper1.getEmpByEid(1);
    System.out.println(emp2);
}
```



#### 二.MyBatis的二级缓存

二级缓存需要手动开启

二级缓存是SqlSessionFactory级别，通过同一个SqlSessionFactory创建的SqlSession查询的结果会被缓存；此后若再次执行相同的查询语句，结果就会从缓存中获取

二级缓存开启的条件：
		1.在核心配置文件中，设置全局配置属性cacheEnabled="true"，默认为true，不需要设置
		2.在映射文件中设置标签<cache />
		3.二级缓存必须在SqlSession关闭或提交之后有效
		4.查询的数据所转换的实体类类型必须实现序列化的接口

使二级缓存失效的情况：
		两次查询之间执行了任意的增删改，会使一级和二级缓存同时失效



在映射文件中设置标签：

```xml
<cache/>
```

在要查询的实体类上实现序列化的接口：

```java
public class Emp implements Serializable {
    ...
}
```

测试：

```java
@Test
public void testTwoCache(){
    try {
        InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);
        SqlSession sqlSession1 = sqlSessionFactory.openSession(true);
        CacheMapper mapper1 = sqlSession1.getMapper(CacheMapper.class);
        System.out.println(mapper1.getEmpByEid(1));
        sqlSession1.close();
        SqlSession sqlSession2 = sqlSessionFactory.openSession(true);
        CacheMapper mapper2 = sqlSession2.getMapper(CacheMapper.class);
        System.out.println(mapper2.getEmpByEid(1));
        sqlSession2.close();

    } catch (IOException e) {
        e.printStackTrace();
    }
}
```



#### 三.二级缓存的相关配置

在mapper配置文件中添加的cache标签可以设置一些属性：

eviction属性：缓存回收策略
		LRU（Least Recently Used） – 最近最少使用的：移除最长时间不被使用的对象。
		FIFO（First in First out） – 先进先出：按对象进入缓存的顺序来移除它们。
		SOFT – 软引用：移除基于垃圾回收器状态和软引用规则的对象。
		WEAK – 弱引用：更积极地移除基于垃圾收集器状态和弱引用规则的对象。
	默认的是 LRU。

flushInterval属性：刷新间隔，单位毫秒
		默认情况是不设置，也就是没有刷新间隔，缓存仅仅调用语句时刷新

size属性：引用数目，正整数
		代表缓存最多可以存储多少个对象，太大容易导致内存溢出

readOnly属性：只读，true/false
		true：只读缓存；会给所有调用者返回缓存对象的相同实例。因此这些对象不能被修改。这提供了很重要的性能优势。
		false：读写缓存；会返回缓存对象的拷贝（通过序列化）。这会慢一些，但是安全，因此默认是false。



#### 四.MyBatis缓存查询的顺序

先查询二级缓存，因为二级缓存中可能会有其他程序已经查出来的数据，可以拿来直接使用。
如果二级缓存没有命中，再查询一级缓存
如果一级缓存也没有命中，则查询数据库
SqlSession关闭之后，一级缓存中的数据会写入二级缓存



#### 五.整合第三方缓存EHCache

1.添加依赖

```xml
<!-- Mybatis EHCache整合包 -->
<dependency>
    <groupId>org.mybatis.caches</groupId>
    <artifactId>mybatis-ehcache</artifactId>
    <version>1.2.2</version>
</dependency>

<!-- slf4j日志门面的一个具体实现 -->
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-classic</artifactId>
    <version>1.2.11</version>
    <scope>test</scope>
</dependency>
```



2.各jar包功能

| jar包功能       | 作用                            |
| :-------------- | ------------------------------- |
| mybatis-ehcache | Mybatis和EHCache的整合包        |
| ehcache         | EHCache核心包                   |
| slf4j-api       | SLF4J日志门面包                 |
| logback-classic | 支持SLF4J门面接口的一个具体实现 |



3.创建EHCache的配置文件ehcache.xml

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="../config/ehcache.xsd">
    <!-- 磁盘保存路径 -->
    <diskStore path="D:\Java\Mybatis\ehcache"/>
    <defaultCache
            maxElementsInMemory="1000"
            maxElementsOnDisk="10000000"
            eternal="false"
            overflowToDisk="true"
            timeToIdleSeconds="120"
            timeToLiveSeconds="120"
            diskExpiryThreadIntervalSeconds="120"
            memoryStoreEvictionPolicy="LRU">
    </defaultCache>
</ehcache>
```



4.设置二级缓存的类型

```xml
<cache type="org.mybatis.caches.ehcache.EhcacheCache"/>
```



5.加入logback日志

存在SLF4J时，作为简易日志的log4j将失效，此时我们需要借助SLF4J的具体实现logback来打印日志。

创建logback的配置文件logback.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration debug="true">
    <!-- 指定日志输出的位置 -->
    <appender name="STDOUT"
              class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <!-- 日志输出的格式 -->
            <!-- 按照顺序分别是：时间、日志级别、线程名称、打印日志的类、日志主体内容、换行 -->
            <pattern>[%d{HH:mm:ss.SSS}] [%-5level] [%thread] [%logger]
                [%msg]%n
            </pattern>
        </encoder>
    </appender>
    <!-- 设置全局日志级别。日志级别按顺序分别是：DEBUG、INFO、WARN、ERROR -->
    <!-- 指定任何一个日志级别都只打印当前级别和后面级别的日志。 -->
    <root level="DEBUG">
        <!-- 指定打印日志的appender，这里通过“STDOUT”引用了前面配置的appender -->
        <appender-ref ref="STDOUT"/>
    </root>
    <!-- 根据特殊需求指定局部日志级别 -->
    <logger name="com.atguigu.crowd.mapper" level="DEBUG"/>
</configuration>
```



6.EHCache配置文件说明

| 属性名                          | 是否必须 | 作用                                                         |
| ------------------------------- | -------- | ------------------------------------------------------------ |
| maxElementsInMemory             | 是       | 在内存中缓存的element的最大数目                              |
| maxElementsOnDisk               | 是       | 在磁盘上缓存的element的最大数目，若是0表示无穷大             |
| eternal                         | 是       | 设定缓存的elements是否永远不过期。 如果为true，则缓存的数据始终有效， 如果为false那么还要根据timeToIdleSeconds、timeToLiveSeconds判断 |
| overflowToDisk                  | 是       | 设定当内存缓存溢出的时候是否将过期的element缓存到磁盘上      |
| timeToIdleSeconds               | 否       | 当缓存在EhCache中的数据前后两次访问的时间超过timeToIdleSeconds的属性取值时， 这些数据便会删除，默认值是0,也就是可闲置时间无穷大 |
| timeToLiveSeconds               | 否       | 缓存element的有效生命期，默认是0.,也就是element存活时间无穷大 |
| diskSpoolBufferSizeMB           | 否       | DiskStore(磁盘缓存)的缓存区大小。默认是30MB。每个Cache都应该有自己的一个缓冲区 |
| diskPersistent                  | 否       | 在VM重启的时候是否启用磁盘保存EhCache中的数据，默认是false。 |
| diskExpiryThreadIntervalSeconds | 否       | 磁盘缓存的清理线程运行间隔，默认是120秒。每个120s， 相应的线程会进行一次EhCache中数据的清理工作 |
| memoryStoreEvictionPolicy       | 否       | 当内存缓存达到最大，有新的element加入的时候， 移除缓存中element的策略。 默认是LRU（最近最少使用），可选的有LFU（最不常使用）和FIFO（先进先出） |



### MyBatis的逆向工程

正向工程：先创建Java实体类，由框架负责根据实体类生成数据库表。Hibernate是支持正向工程的。

逆向工程：先创建数据库表，由框架负责根据数据库表，反向生成如下资源：
		Java实体类
		Mapper接口
		Mapper映射文件



#### 一.创建逆向工程的步骤

1.添加依赖和插件

```xml
<!-- 依赖MyBatis核心包 -->
<dependencies>
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.10</version>
    </dependency>
</dependencies>
<!-- 控制Maven在构建过程中相关配置 -->
<build>
    <!-- 构建过程中用到的插件 -->
    <plugins>
        <!-- 具体插件，逆向工程的操作是以构建过程中插件形式出现的 -->
        <plugin>
            <groupId>org.mybatis.generator</groupId>
            <artifactId>mybatis-generator-maven-plugin</artifactId>
            <version>1.4.1</version>
            <!-- 插件的依赖 -->
            <dependencies>
                <!-- 逆向工程的核心依赖 -->
                <dependency>
                    <groupId>org.mybatis.generator</groupId>
                    <artifactId>mybatis-generator-core</artifactId>
                    <version>1.4.1</version>
                </dependency>
                <!-- 数据库连接池 -->
                <dependency>
                    <groupId>com.mchange</groupId>
                    <artifactId>c3p0</artifactId>
                    <version>0.9.5.5</version>
                </dependency>
                <!-- MySQL驱动 -->
                <dependency>
                    <groupId>mysql</groupId>
                    <artifactId>mysql-connector-java</artifactId>
                    <version>8.0.28</version>
                </dependency>
            </dependencies>
        </plugin>
    </plugins>
</build>
```



2.创建MyBatis的核心配置文件

比如需要的jdbc.properties、log4j.xml、mybatis-config.xml等等



3.创建逆向工程的配置文件

文件名必须是：generatorConfig.xml	（里边的信息根据自身要求做修改）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">  <!--此处报红不需要管-->
<generatorConfiguration>
    <!--
        targetRuntime: 执行生成的逆向工程的版本
            MyBatis3Simple: 生成基本的CRUD（清新简洁版）（只有增删改查5个方法：增、删、改、查一条、查所有）
            MyBatis3: 生成带条件的CRUD（奢华尊享版）
    -->
    <context id="DB2Tables" targetRuntime="MyBatis3">
        <!-- 数据库的连接信息 -->
        <jdbcConnection driverClass="com.mysql.cj.jdbc.Driver"
                        connectionURL="jdbc:mysql://localhost:3306/mybatis"
                        userId="root"
                        password="1234">
        </jdbcConnection>
        <!-- javaBean的生成策略-->
        <javaModelGenerator targetPackage="com.yc.mybatis.bean"
                            targetProject=".\src\main\java">
            <property name="enableSubPackages" value="true"/>   <!--是否能够使用子包-->
            <property name="trimStrings" value="true"/>
        </javaModelGenerator>
        <!-- SQL映射文件的生成策略 -->
        <sqlMapGenerator targetPackage="com.yc.mybatis.mapper"
                         targetProject=".\src\main\resources">
            <property name="enableSubPackages" value="true"/>
        </sqlMapGenerator>
        <!-- Mapper接口的生成策略 -->
        <javaClientGenerator type="XMLMAPPER"
                             targetPackage="com.yc.mybatis.mapper" targetProject=".\src\main\java">
            <property name="enableSubPackages" value="true"/>
        </javaClientGenerator>
        <!-- 逆向分析的表 -->
        <!-- tableName设置为*号，可以对应所有表，此时不写domainObjectName -->
        <!-- domainObjectName属性指定生成出来的实体类的类名 -->
        <table tableName="t_emp" domainObjectName="Emp"/>
        <table tableName="t_dept" domainObjectName="Dept"/>
    </context>
</generatorConfiguration>
```



4.执行MBG插件的generate目标

双击maven下的mybatis-generator:generate插件

![image-20220802100015993](https://raw.githubusercontent.com/chocman99/Image/main/Mybatis/image-20220802100015993.png)



效果：

![image-20220802113724409](https://raw.githubusercontent.com/chocman99/Image/main/Mybatis/image-20220802113724409.png)



#### 二.QBC查询



```java
    @Test
    public void testMBG(){
        try {
            InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
            SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);
            SqlSession sqlSession = sqlSessionFactory.openSession(true);
            EmpMapper mapper = sqlSession.getMapper(EmpMapper.class);

            //查询所有数据
//            List<Emp> list = mapper.selectByExample(null);
//            list.forEach(emp -> System.out.println(emp));

            //根据条件查询
            EmpExample example = new EmpExample();
            example.createCriteria().andEmpNameEqualTo("张三").andAgeGreaterThanOrEqualTo(20);
            example.or().andDidIsNotNull();
            List<Emp> list = mapper.selectByExample(example);
            list.forEach(emp -> System.out.println(emp));

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```





### 分页插件



#### 一.分页插件使用步骤

1.添加依赖

```xml
<!-- 分页插件 -->
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper</artifactId>
    <version>5.3.1</version>
</dependency>
```



2.配置分页插件

在MyBatis的核心配置文件中配置插件

```xml
<plugins>
    <!--设置分页插件-->
    <plugin interceptor="com.github.pagehelper.PageInterceptor"></plugin>
</plugins>
```



#### 2.分页插件的使用

1..分页相关数据

（1）

Page{count=true, pageNum=2, pageSize=5, startRow=5, endRow=10, total=9, pages=2, reasonable=false, pageSizeZero=false}[Emp{eid=9, empName='a', age=23, sex='男', email='1234@qq.com', did=null}, Emp{eid=10, empName='b', age=32, sex='男', email='1234@qq.com', did=null}, Emp{eid=11, empName='c', age=22, sex='男', email='1234@qq.com', did=null}, Emp{eid=12, empName='abc', age=23, sex='男', email='12345@qq.com', did=null}]



（2）

```java
public void testPageHelper(){
    try {
        InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);
        SqlSession sqlSession = sqlSessionFactory.openSession(true);
        EmpMapper mapper = sqlSession.getMapper(EmpMapper.class);
        //在查询功能之前开启分页
        //Page<Object> page = PageHelper.startPage(2, 5);//获取第二页，每页显示5条数据
        PageHelper.startPage(6, 5);//获取第6页，每页显示5条数据
        List<Emp> list = mapper.selectByExample(null);
        PageInfo<Emp> page = new PageInfo<>(list, 5);
        //list.forEach(emp -> System.out.println(emp));
        System.out.println(page);

    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

PageInfo{pageNum=6, pageSize=5, size=5, startRow=26, endRow=30, total=47, pages=10,
 prePage=5, nextPage=7, isFirstPage=false, isLastPage=false, hasPreviousPage=true, hasNextPage=true, navigatePages=5, navigateFirstPage=4, navigateLastPage=8, navigatepageNums=[4, 5, 6, 7, 8]}

常用数据：
pageNum：当前页的页码
pageSize：每页显示的条数
size：当前页显示的真实条数
total：总记录数
pages：总页数
prePage：上一页的页码
nextPage：下一页的页码
isFirstPage/isLastPage：是否为第一页/最后一页
hasPreviousPage/hasNextPage：是否存在上一页/下一页
navigatePages：导航分页的页码数
navigatepageNums：导航分页的页码，[4, 5, 6, 7, 8]



#### 总结

```java
/*
    limit index,pageSize
        index:当前页的起始索引。比如第一页第一条数据的索引应该是0，条数减一
        pageSize：每页显示的条数
        pageNum：当前页的页码
        index=(pageNum-1)*pageSize

        使用MyBatis的分页插件实现分页功能
            1.需要在查询功能之前开启分页
                PageHelper.startPage(int pageNum , int pageSize);
            2.在查询功能之后获取分页相关信息、
                PageInfo<Emp> page = new PageInfo<>(list, 5);
                    list表示分页数据
                    5：表示当前导航分页的数量
 */
```









### 补充



#### 一.配置过程

1.加入依赖

mybatis、junit、mysql-connector-java、slf4j或log4j

2.创建核心配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

    <properties resource="jdbc.properties"></properties>

    <typeAliases>
        <package name="com.yc.mybatis.pojo"/>
    </typeAliases>

    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="${jdbc.driver}"/>
                <property name="url" value="${jdbc.url}"/>
                <property name="username" value="${jdbc.username}"/>
                <property name="password" value="${jdbc.password}"/>
            </dataSource>
        </environment>
    </environments>

    <!--引入映射文件-->
    <mappers>
        <package name="com.yc.mybatis.mapper"/>
    </mappers>
</configuration>
```

为连接数据库创建properties文件

```properties
jdbc.driver=com.mysql.cj.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/mybatis
jdbc.username=root
jdbc.password=1234
```

![image-20220720212803880](https://raw.githubusercontent.com/chocman99/Image/main/Mybatis/image-20220720212803880.png)

3.创建mapper接口，创建映射文件，实现功能

4.实现功能前可以将获取sqlSession对象封装成工具类，再用就直接调

```java
package com.yc.mybatis.utils;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;

/**
 * @Description: utils工具类：因为获取sqlSession对象是一个重复的过程，所以将获取sqlSession对象的过程封装起来，以后再用直接调就可以了
 * @Author: YC
 * @CreateTime:2022/7/20 21:46
 */
public class SqlSessionUtils {

    public static SqlSession getSqlSession(){
        SqlSession sqlSession = null;
        try {
            InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
            SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);
            sqlSession = sqlSessionFactory.openSession(true);
        } catch (IOException e) {
            e.printStackTrace();
        }
        return sqlSession;
    }

}
```

4.创建mapper接口（写方法）

5.创建映射文件（Mybatis.xml里写sql语句）

6.实现功能（测试类里测试代码）







#### 二.集合添加元素方法

map集合用put方法

list集合用add方法











