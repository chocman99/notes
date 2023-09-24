

### Spring介绍



#### 一.课程内容介绍

1.Spring框架概述
2.IOC容器
3.Aop
4.JdbcTemplate
5.事务管理
6.Spring5新特性



#### 二.Spring框架概述

1.Spring是轻量级的开源的JavaEE框架
2.Spring可以解决企业应用开发的
3.Spring有两个核心部分：IOC和Aop
     （1）IOC：控制反转，把创建对象过程交给Spring进行管理
     （2）Aop：面向切面，不修改源代码进行功能增强
4.Spring特点
     （1）方便解耦，简化开发
     （2）Aop编程支持
     （3）方便程序测试
     （4）方便和其他框架进行整合
     （5）方便进行事物操作
     （6）降低API开发难度
5.此课程选取Spring版本5.x



#### 三.入门案例

1.下载Spring5
      （1）使用Spring最新稳定版本（版本号后带GA的是稳定版本）
               Spring官网 -> Project -> Spring Framework -> LEARN

​      （2）下载地址：https://repo.spring.io/ui/native/release/org/springframework/spring/
​               点击右上角github图标 -> 往下拉看到Access to Binaries -> 点击 Spring Framework Artifacts -> 往下拉找到Downloading a Distribution -> 点击[https://repo.spring.io](https://repo.spring.io/).   ->  打开Artifactory下的Artifacts -> 找到release下的org下的springframework下的spring -> 将Repository Path后的地址拼接到该网页网址的io后面，即上边的下载地址 -> 找到确认的稳定版本号 -> 点进去后下载dist.zip的即可

2.打开idea工具，创建普通java工程

3.导入Spring5相关jar包
      基础先找到刚刚下载的spring里libs里的Beans，Core，Context，Expression四个jar包，外加上commons-logging的包

4.创建普通类，在这个类创建普通方法

```java
public class User {
    public void add(){
        System.out.println("add....");
    }
}
```

5.创建Spring怕配置文件，在配置文件配置创建的对象
      （1）Spring配置文件使用xml格式

![image-20220504223547071](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220504223547071.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--配置User对象创建-->
    <bean id="user" class="com.company.spring5.User"></bean>
</beans>
```

6.进行测试代码编写

```java
@Test
public void testAdd(){
    //1.加载spring配置文件,参数是配置文件的路径，在src下直接写（相对路径）
    ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");

    //2.获取配置文件chuan的对象，参数user是配置文件里id的值
    User user = context.getBean("user", User.class);

    //输出
    System.out.println(user);
    user.add();
}
```





### IOC容器



（1）IOC底层原理
（2）IOC接口（BeanFactory）
（3）IOC操作Bean管理（基于xml）
（4）IOC操作Bean管理（基于注解）



#### 一.IOC概念和原理

1.什么是IOC
        （1）控制反转，把对象创建和对象之间的调用过程，交给Spring进行管理
        （2）使用 IOC目的：为了耦合度降低
        （3）做入门案例就是IOC实现

2.IOC底层原理
        （1）xml解析、工厂模式、反射

3.画图讲解IOC底层原理

![image-20220505095528424](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220505095528424.png)

![image-20220505095456284](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220505095456284.png)

工厂模式的目的是为了降低耦合度，但它没有降到最低限度

IOC过程：

![image-20220506180159712](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220506180159712.png)





#### 二.IOC（接口）

1.IOC思想基于IOC容器完成，IOC容器底层就是对象工厂

2.Spring提供IOC容器实现两种方式：（两个接口）
        1）.BeanFactory：IOC容器基本实现，是Spring内部的使用的接口，不提供开发人员进行使用
                   *加载配置文件的时候不会创建对象，在获取对象（使用）才去创建对象

​        2）.ApplicationContext：BeanFactory接口的子接口，提供更多更强大的功能，一般由开发人员进行使用
​                   *加载配置文件的时候就会把在配置文件对象进行创建

3.ApplicationContext接口有实现类

​             （鼠标点到ApplicationContext然后按ctrl+h查看接口的实现类）

![image-20220510094023947](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220510094023947.png)

FileSystemXmlApplicationContext：后面的参数要用绝对路径（带盘符路径）
ClassPathXmlApplicationContext：后面的参数用类路径，比如bean.xml文件就在src下，那么直接写文件名字



#### 三.IOC操作Bean管理（概念）

1.什么是Bean管理
          0）.Bean管理指的是两个操作
          1）.Spring创建对象
          2）.Spring注入属性

2.Bean管理操作有两种方式
          1）.基于xml配置文件方式实现
          2）.基于注解方式实现

#### 四.IOC操作Bean管理（基于xml方式）

##### 1.基于xml方式创建对象

![image-20220510100103471](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220510100103471.png)

​          1）.在Spring配置文件中，使用bean标签，标签里面添加对应属性，就可以实现对象创建
​          2）.在bean标签里有很多属性，介绍常用的属性
​                     *id属性：唯一标识（取得一个别名）
​                     *class属性：类的全路径（包类路径）
​          3）.创建对象的时候，默认也是执行无参构造方法

##### 2.基于xml方式注入属性

​          DI：依赖注入，就是注入属性          （DI是IOC中一种具体实现，就表示注入属性，但注入属性需要在创建对象的基础之上进行完成）

######                     *第一种注入方式：使用set方式进行注入

​                               （1）.创建类，定义属性和对应的set方法

```java
/*
* 使用set方式进行注入
*/
public class Book {

    //创建属性
    private String Bname;
    private String bauthor;

    //使用set方式进行注入
    public void setBname(String bname) {
        Bname = bname;
    }

    public void setBauthor(String bauthor) {
        this.bauthor = bauthor;
    }
}
```

​                               （2）.在spring配置文件 配置对象创建 ，配置属性注入

```xml
<!--2.set方法注入属性-->
<bean id="book" class="com.company.spring5.Book">
<!--使用property完成属性注入
    name：类里面属性名称
    value：向属性注入的值
-->
    <property name="bname" value="西游记"></property>
    <property name="bauthor" value="吴承恩"></property>
</bean>
```



######                     *第二种注入方式：使用有参构造进行注入

​                               （1）.创建类，定义属性，创建属性对应有参构造方法

```java
/*
* 使用有参构造进行注入
*/
public class Orders {

    //两个属性
    private String oname;
    private String address;

    //有参数构造
    public Orders(String oname, String address) {
        this.oname = oname;
        this.address = address;
    }
}
```

​                               （2）.在spring配置文件中进行配置

```xml
<!--3.有参构造注入属性-->
<bean id="orders" class="com.company.spring5.Orders">
    <constructor-arg name="oname" value="电脑"></constructor-arg>
    <constructor-arg name="address" value="china"></constructor-arg>
    <!--也可以通过索引值注入，写个0就代表有参构造中的第一个参数：  <constructor-arg index="0" value="鼠标"></constructor-arg>-->
</bean>
```



##### 3.p名称空间注入（了解）

​           1）.使用p名称空间注入，可以简化基于xml配置方式
​                      第一步：添加p名称空间在配置文件中

![image-20220510111649514](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220510111649514.png)

​                      第二步：进行属性注入，在bean标签里面进行操作

![image-20220510112058225](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220510112058225.png)



#### 五.IOC操作Bean管理（xml注入其他类型属性）

##### 1.字面量

​          1）.null值

```xml
<!--设置null值-->
<property name="address">
    <null/>
</property>
```

​          2）.属性值包含特殊符号

```xml
<!--属性值包含特殊符号
    1.把<>进行转义：&lt，&gt
    2.把特殊符号的内容写到CDATA
-->
<property name="address">
    <value><![CDATA[<<南京>>]]></value>
</property>
```



##### 2.注入属性-外部bean

​        1）.创建两个类service类和dao类
​        2）.在service调用dao里面的方法
​        3）.在spring配置文件中进行配置

```java
public class UserService {

    //创建UserDao类型属性，生成set方法   (对象类型)
    private UserDao userDao;

    public void setUserDao(UserDao userdao) {
        this.userDao = userdao;
    }

    public void add(){
        System.out.println("service add........");
        userDao.update();
        
    }

}
```

```xml
<!--1.service和dao对象创建-->
<bean id="userService" class="com.company.spring5.service.UserService">
    <!--注入userDao对象
        name属性值：类里面属性名称
        ref属性：创建userDao对象bean标签的id值
    -->
    <property name="userDao" ref="userDaoImpl"></property>
</bean>

<bean id="userDaoImpl" class="com.company.spring5.dao.UserDaoImpl"></bean>
```



##### 3.注入属性-内部bean

​         1）.一对多关系：部门和员工
​                      一个部门有多个员工，一个员工属于一个部门
​                      部门是一，员工是多

​         2）.在实体类之间表示一对多关系，员工表示所属部门，使用对象类型属性进行表示

```java
//部门类
public class Dept {

    private String dname;

    public void setDname(String dname) {
        this.dname = dname;
    }
}
```

```java
//员工类
public class Emp {

    private String ename;
    private String gender;
    //员工属于某一个部门，使用对象形式表示
    private Dept dept;

    public void setDept(Dept dept) {
        this.dept = dept;
    }

    public void setEname(String ename) {
        this.ename = ename;
    }

    public void setGender(String gender) {
        this.gender = gender;
    }
}
```



​        3）.在spring配置文件中进行配置

```xml
<!--内部bean-->
<bean id="emp" class="com.company.spring5.bean.Emp">
    <!--先设置两个普通属性-->
    <property name="ename" value="lucy"></property>
    <property name="gender" value="女"></property>
    <!--设置对象类型属性-->
    <property name="dept">
        <bean id="dept" class="com.company.spring5.bean.Dept">
            <property name="dname" value="安保部"></property>
        </bean>
    </property>
</bean>
```



##### 4.注入属性-级联赋值

​       1）.第一种写法

```xml
<!--级联赋值-->
<bean id="emp" class="com.company.spring5.bean.Emp">
    <!--先设置两个普通属性-->
    <property name="ename" value="lucy"></property>
    <property name="gender" value="女"></property>
    <!--级联赋值-->
    <property name="dept" ref="dept"></property>
</bean>
<bean id="dept" class="com.company.spring5.bean.Dept">
    <property name="dname" value="财务部"></property>
</bean>
```

​      2）.第二种写法

```xml
<!--级联赋值-->
<bean id="emp" class="com.company.spring5.bean.Emp">
    <!--先设置两个普通属性-->
    <property name="ename" value="lucy"></property>
    <property name="gender" value="女"></property>
    <!--级联赋值-->
    <property name="dept" ref="dept"></property>
    <property name="dept.dname" value="技术部"></property>       //需要写出dept的get方法
</bean>
<bean id="dept" class="com.company.spring5.bean.Dept">
    <property name="dname" value="财务部"></property>
</bean>
```



#### 六.IOC操作Bean管理（xml注入集合属性）

1.注入数组类型属性
2.注入List集合类型属性
3.注入Map集合类型属性

1）.创建类、定义数组、list、map、set类型属性，生成对应set方法

```java
public class Stu {
    //1.数组类型属性
    private String[] courses;

    //2.list集合类型属性
    private List<String> list;

    //3.map集合类型属性
    private Map<String,String> maps;

    //4.set集合类型属性
    private Set<String> sets;

    public void setCourses(String[] courses) {
        this.courses = courses;
    }

    public void setList(List<String> list) {
        this.list = list;
    }

    public void setMaps(Map<String, String> maps) {
        this.maps = maps;
    }

    public void setSets(Set<String> sets) {
        this.sets = sets;
    }
}
```

2）.在spring配置文件进行配置

```xml
<!--1.集合类型属性注入-->
<bean id="stu" class="com.company.spring5.collectiontype.Stu">
    
    <!--数组类型属性注入-->
    <property name="courses">
        <array>
            <value>java课程</value>
            <value>数据库课程</value>
        </array>
    </property>

    <!--list类型属性注入-->
    <property name="list">
        <list>
            <value>张三</value>
            <value>小三</value>
        </list>
    </property>

    <!--map类型属性注入-->
    <property name="maps">
        <map>
            <entry key="JAVA" value="java"></entry>
            <entry key="PHP" value="php"></entry>
        </map>
    </property>

    <!--set类型属性注入-->
    <property name="sets">
        <set>
            <value>MySQL</value>
            <value>Redis</value>
        </set>
    </property>
    
</bean>
```



4.在集合里面设置对象类型值   （上面设置的都是字符串，这是对象类型）

```xml
<!--创建多个course对象-->
<bean id="course1" class="com.company.spring5.collectiontype.Course">
    <property name="cname" value="Spring5框架课程"></property>
</bean>
<bean id="course2" class="com.company.spring5.collectiontype.Course">
    <property name="cname" value="MyBatis框架"></property>
</bean>
```

```xml
<!--注入list集合类型，值是对象-->
<property name="courseList">
    <list>
        <ref bean="course1"></ref>
        <ref bean="course2"></ref>
    </list>
</property>
```



5.把集合注入部分提取出来

​      1）.在spring配置文件中引入名称空间util           （加两个东西）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:util="http://www.springframework.org/schema/util"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util.xsd">
```

​      2）.使用util标签完成list集合注入提取

```xml
<!--1.提取list集合类型属性注入-->
<util:list id="bookList">
    <value>西游记</value>
    <value>三国演义</value>
    <value>红楼梦</value>
</util:list>

<!--2.提取list集合类型属性注入使用-->
<bean id="book" class="com.company.spring5.collectiontype.Book">
    <property name="list" ref="bookList"></property>
</bean>
```



#### 七.IOC操作Bean管理（FactoryBean）

1.Spring有两种类型bean，一种普通bean，另外一种工厂bean（FactoryBean）

2.普通bean：在配置文件中定义bean类型就是返回类型        （之前做的都是普通bean）

3.工厂bean：在配置文件中定义bean类型可以和返回类型不一样
                   第一步：创建类，让这个类作为工厂bean，实现接口FactoryBean
                   第二步：实现接口里面的方法，在实现的方法中定义返回的bean类型

```java
public class MyBean implements FactoryBean<Course> {

    //定义返回bean
    @Override
    public Course getObject() throws Exception {
        Course course = new Course();
        course.setCname("abc");
        return course;
    }

    @Override
    public Class<?> getObjectType() {
        return null;
    }

    @Override
    public boolean isSingleton() {
        return FactoryBean.super.isSingleton();
    }
}
```

```xml
<bean id="myBean" class="com.company.spring5.factorybean.MyBean">
</bean>
```

```java
@Test
public void testCollection3(){
    ApplicationContext context = new ClassPathXmlApplicationContext("bean3.xml");
    Course course = context.getBean("myBean", Course.class);
    System.out.println(course);
}
```



#### 八.IOC操作Bean管理（bean作用域）

1.在Spring里面，设置创建bean实例是单实例还是多实例

2.在Spring里面，默认情况下，bean是单实例对象

![image-20220511115907659](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220511115907659.png)

![image-20220511120020202](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220511120020202.png)

3.如何设置单实例还是多实例
           1）.在spring配置文件bean标签里面有属性（scope）用于设置单实例还是多实例
           2）.scope属性值
                      第一个值：默认值，singleton，表示是单实例对象（什么都不写即默认值）
                      第二个值：prototype，表示是多实例对象

![image-20220511140059798](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220511140059798.png)

![image-20220511140326794](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220511140326794.png)

​           3）.singleton和prototype区别
​                      第一：singleton单实例，prototype多实例
​					  第二：设置scope值是singleton的时候（或不写），加载spring配置文件的时候就会创建单实例对象
​    							 设置scope值是prototype的时候，不是在加载spring配置文件的时候创建对象，在调用getBean方法的时候创建多实例对象





#### 九.IOC操作Bean管理（bean生命周期）

1.生命周期
			1）.从对象创建到对象销毁的过程

2.bean生命周期
			1）.通过构造器创建bean实例（无参构造）
			2）.为bean的属性设置值和对其他bean的引用（调用set方法）
			3）.调用bean的初始化的方法（需要进行配置）
			4）.bean可以使用了（对象获取到了）
			5）.当容器关闭的时候，调用bean销毁的方法（需要进行配置销毁的方法）

3.演示bean生命周期

```java
public class Orders {

    
    private String oname;
    
    //无参构造
    public Orders() {
        System.out.println("第一步：执行无参构造创建bean实例");
    }

    public void setOname(String oname) {
        this.oname = oname;
        System.out.println("第二步：调用set方法设置属性值");
    }

    //创建执行的初始化的方法
    public void initMethod(){
        System.out.println("第三步：执行初始化的方法");
    }

    //创建执行的销毁的方法
    public void destroyMethod(){
        System.out.println("第五步：执行销毁的方法");
    }
}
```

```xml
<!--初始化和销毁需要在配置文件中配置，加上相的属性：初始化init-method；销毁destroy-method-->
<!--init-method-->
<bean id="orders" class="com.company.spring5.bean.Orders" init-method="initMethod" destroy-method="destroyMethod">
    <property name="oname" value="手机"></property>
</bean>
```

```java
    @Test
    public void testbean(){
//        ApplicationContext context = new ClassPathXmlApplicationContext("bean4.xml");     (ApplicationContext中没有close方法，需要用他的子接口或实现类 )
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean4.xml");
        Orders orders = context.getBean("orders", Orders.class);
        System.out.println("第四步：获取创建bean实例对象");
        System.out.println(orders);

        //手动让bean实例销毁
        context.close();
    }
```

执行结果：

![image-20220511154232535](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220511154232535.png)

4.bean的后置处理器，bean生命周期有七步
            1）.通过构造器创建bean实例（无参构造）
			2）.为bean的属性设置值和对其他bean的引用（调用set方法）
            **3）.把bean实例传递bean后置处理器的方法：postProcessBeforeInitialization**
			4）.调用bean的初始化的方法（需要进行配置）
            **5）.把bean实例传递bean后置处理器的方法：postProcessAfterInitialization**
			6）.bean可以使用了（对象获取到了）
			7）.当容器关闭的时候，调用bean销毁的方法（需要进行配置销毁的方法）

5.演示添加后置处理器效果
			1）.创建类，实现接口BeanPostProcessor，创建后置处理器

```java
public class MyBeanPost implements BeanPostProcessor {
    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("在初始化之前执行的方法");
        return bean;
    }

    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("在初始化之后执行的方法");
        return bean;
    }
```

执行结果：

![image-20220511160625599](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220511160625599.png)

spring怎么知道后置处理器的：因为类实现的是个接口，当实现接口之后，spring就把他作为后置处理器执行。
而后置处理器会对当前配置文件中所有bean都添加后置处理器的处理。

（网上的说明：https://www.jb51.net/article/225253.htm）



#### 十.IOC操作Bean管理（自动装配）

1.什么是自动装配
		1）.根据指定装配规则（属性名称或者属性类型），Spring自动将匹配的属性值进行注入

2.演示自动装配过程
		1）.根据属性名称自动注入

```xml
<!--    实现自动装配
        bean标签属性autowire，配置自动装配
        autowire属性常用两个值：
            1.byName根据属性名称注入。注入值bean的id值和属性名称一样（即bean中的id值和Emp类中的属性名一样）
            2.byType根据属性类型注入。
-->
    <bean id="emp" class="com.company.spring5.autowire.Emp" autowire="byName">
<!--以前用到的手动装配        <property name="dept" ref="dept"></property>-->
    </bean>
    <bean id="dept" class="com.company.spring5.autowire.Dept"></bean>
```

​		2）.根据属性类型自动注入

```xml
<!--    实现自动装配
        bean标签属性autowire，配置自动装配
        autowire属性常用两个值：
            1.byName根据属性名称注入。注入值bean的id值和属性名称一样（即bean中的id值和Emp类中的属性名一样）
            2.byType根据属性类型注入。相同类型的bean，不能定义多个，因为他就找不到，会报错。
-->
    <bean id="emp" class="com.company.spring5.autowire.Emp" autowire="byType">
<!--以前用到的手动装配        <property name="dept" ref="dept"></property>-->
    </bean>
    <bean id="dept" class="com.company.spring5.autowire.Dept"></bean>
```



#### 十一.IOC操作Bean管理（外部属性文件）

1.直接配置数据库信息
		1）.配置德鲁伊连接池
		2）.引入德鲁伊连接池依赖jar包

```xml
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
    <property name="driverClassName" value="com.mysql.jdbc.Driver"></property>
    <property name="url" value="jdbc:mysql://localhost:3306/userDb"></property>
    <property name="username" value="root"></property>
    <property name="password" value="123456"></property>
</bean>
```

2.引入外部属性文件配置数据库的连接池
		1）.创建外部属性文件，properties格式文件，写数据库信息

![image-20220511171711506](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220511171711506.png)

​		2）.把外部properties属性文件引入到spring配置文件中
​				*引入context名称空间（）

![image-20220511172205817](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220511172205817.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:util="http://www.springframework.org/schema/util"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
```

​				*在spring配置文件使用标签引入外部属性文件

```xml
<!--引入外部属性文件-->
<context:property-placeholder location="classpath:jdbc.properties"/>

    <!--直接配置连接池-->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${prop.driverClass}"></property>
        <property name="url" value="${prop.url}"></property>
        <property name="username" value="${prop.userName}"></property>
        <property name="password" value="${prop.password}"></property>
    </bean>
```





#### 十二.IOC操作Bean管理（基于注解方式）

1.什么是注解
		1）.注解是代码特殊标记，格式：@注解名称（属性名称=属性值，属性名称=属性值，...）
		2）.使用注解，注解作用在类上面，方法上面，属性上面
		3）.使用注解目的：简化xml配置

2.Sping针对Bean管理中创建对象提供的注解
		1）.@Component	
		2）.@Service
		3）.@Controller
		4）.@Repository
*上面的四个注解功能是一样的，都可以用来创建bean实例

3.基于注解方式实现对象创建
		第一步：引入依赖：spring-aop-5.3.19.jar
		第二部：开启组件扫描     （让spring知道哪个位置有注解，好去创建对象）

```xml
    <!--开启组件扫描
        1.如果扫描多个包，多个包使用逗号隔开
        2.扫描包上层目录
    -->
<!--    <context:component-scan base-package="com.company.spring5.dao,com.company.spring5.service"></context:component-scan>-->
    <context:component-scan base-package="com.company"></context:component-scan>
```

​		3）.第三步：创建类，在类上面添加创建对象注解

```java
//在注解里面value属性值可以省略不写，即默认值，默认值格式是类名称，把首字母小写
//四种注解哪个都能实现对象创建，一般按习惯把不同注解放到不同层中
@Component(value = "userService")   //这句话和之前学的xml配置是类似的   <bean id="userService" class="com.company.spring5.service.UserService"/>
public class UserService {
    public void add(){
        System.out.println("service add......");
    }
}
```



4.开启 组件扫描细节配置

```xml
<!--示例一
    use-default-filters="false" ：表示现在不使用默认filter，自己配置filter
    context:include-filter  ：设置扫描哪些内容
-->
<context:component-scan base-package="com.company" use-default-filters="false">
    <context:include-filter type="annotation"
                            expression="org.springframework.stereotype.Controller"/>

</context:component-scan>

<!--示例二
    下面配置扫描包所有内容，用的默认filters
    context:exclude-filter  ：设置哪些内容不进行扫描
-->
<context:component-scan base-package="com.company">
    <context:exclude-filter type="annotation"
                            expression="org.springframework.stereotype.Controller"/>

</context:component-scan>
```



5.基于注解方式实现属性注入
		1）.@AutoWired：根据属性类型进行自动装配
				第一步：把service和dao对象创建，在service和dao类添加创建对象注解
				第二部：在service注入dao对象，在service类添加dao类型属性，在属性上面使用注解

```java
@Service
public class UserService {

    //定义dao类型属性
    //不需要添加set方法
    //添加注入属性注解
    @Autowired    //根据类型进行注入
    private UserDao userDao;

    public void add(){
        System.out.println("service add......");
        userDao.add();
    }

}
```

​		2）.@Qualifier：根据属性名称进行注入
​				这个注解的使用，和上面@AutoWired一起使用

```java
//定义dao类型属性
//不需要添加set方法
//添加注入属性注解
@Autowired    //根据类型进行注入
@Qualifier(value = "userDaoImpl")   //根据名称进行注入
private UserDao userDao;
```

​		3）.@Resource：可以根据类型注入，也可以根据名称注入
​				这个注解的包是import javax.annotation.Resource;   说明不是spring官方提供的，而是javax扩展包中的

```java
//    @Resource    //根据类型进行注入
    @Resource(name = "userDaoImpl1")    //根据名称进行注入
    private UserDao userDao;
```

​		4）.@Value：注入普通类型属性

```java
@Value(value = "abc")
private String name;
```



6.完全注解开发
		1）.创建配置类，替代xml配置文件

```java
@Configuration    //作为配置类，替代xml配置文件
@ComponentScan(basePackages = "com.company")   //替代xml里的配置组件扫描
public class SpringConfig {

}
```

此时xml配置可以删掉了，没用了

​		2）.编写测试类

```java
    @Test
    public void testService2(){
        //加载配置类
        ApplicationContext context = new AnnotationConfigApplicationContext(SpringConfig.class);
        UserService userService = context.getBean("userService", UserService.class);
        System.out.println(userService);
        userService.add();

    }

}
```





另：对IOC的理解
		https://www.cnblogs.com/liubin1988/p/8909610.html     （标题三或二）





### AOP



#### 一.AOP（概念）

1.什么是AOP？
		1）.面向切面编程（面向方面编程）：利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的[耦合度](https://baike.baidu.com/item/耦合度/2603938)降低，提高程序的可重用性，同时提高了开发的效率
		2）.通俗描述：不通过修改源代码方式，在主干功能里面添加新功能
		3）.使用登录例子说明AOP

![image-20220523100018545](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220523100018545.png)



#### 二.AOP（底层原理）

1.AOP底层使用动态代理
		1）.有两种情况的动态代理
				第一种：有接口的情况 ，使用JDK动态代理
						*创建接口实现类代理对象，增强类的方法

![image-20220523101036130](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220523101036130.png)

​				第二种：没有接口的情况，使用CGLIB动态代理
​						*创建子类的代理对象，增强类的方法

![image-20220523101631387](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220523101631387.png)



#### 三.AOP（JDK动态代理）

1.使用JDK动态代理，使用Proxy类里面的方法创建代理对象
		API中的proxy类：

![image-20220523111130469](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220523111130469.png)

​		1）.调用newProxyInstance方法

![image-20220523111717328](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220523111717328.png)

​				方法中有三个参数：
​						第一个参数：类加载器
​						第二个参数：增强方法所在的的类，这个类实现的接口，支持多个接口
​						第三个参数：实现这个接口InvocationHandler，创建代理对象，写增强的方法

2.编写JDK动态代理代码
		1）.创建接口，定义方法

```java
public interface UserDao {

    public int add(int a, int b);
    public void update(String id);

}
```

​		2）.创建接口实现类，实现方法

```java
public class UserDaoImpl implements UserDao{

    @Override
    public int add(int a, int b) {
        System.out.println("add方法执行了...");
        return a+b;
    }

    @Override
    public String update(String id) {
        System.out.println("update方法执行了...");
        return id;
    }
}
```

​		3）.使用Proxy类创建接口代理对象

```java
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;
import java.util.Arrays;

/**
 * @Description:
 * @Author: YC
 * @CreateTime: 2022/05/23 11:47
 */
public class JDKProxy {
    public static void main(String[] args) {
        //创建接口实现类代理对象
        Class[] interfaces = {UserDao.class};

//        //第三个参数直接new，用匿名内部类实现
//        Proxy.newProxyInstance(JDKProxy.class.getClassLoader(), interfaces, new InvocationHandler() {
//            @Override
//            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
//                return null;
//            }
//        });

        //
        UserDaoImpl userDao = new UserDaoImpl();
        UserDao dao = (UserDao) Proxy.newProxyInstance(JDKProxy.class.getClassLoader(), interfaces, new UserDaoProxy(userDao));
        int result = dao.add(1,2);
        System.out.println("result：" + result);

    }
}

//创建代理对象代码
class UserDaoProxy implements  InvocationHandler {

    //1.把创建的是谁的代理对象，把谁传递过来
    //有参构造
    private Object  obj;
    public UserDaoProxy(Object obj){
        this.obj = obj;
    }

    //该方法写增强的逻辑
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {

        //方法之前
        System.out.println("方法之前执行..." + method.getName() + "传递的参数" + Arrays.toString(args));

        //被增强的方法执行
        Object res = method.invoke(obj, args);

        //方法之后
        System.out.println("方法之后执行..." + obj);

        return res;
    }
}
```



#### 四.AOP（操作术语）

1.连接点
		类里面哪些方法可以被增强，这些方法称为连接点

2.切入点
		实际被真正增强的方法，称为切入点

3.通知（增强）
		1）.实际增强的逻辑部分称为通知（增强）
		2）.通知有多种类型
				*前置通知：方法前执行
				*后置通知：方法后执行
				*环绕通知：方法前后都执行
				*异常通知：方法异常执行
				*最终通知：相当于try catch的finally，不管异不异常都执行

4.切面
		是动作
		1）.把通知应用到切入点的过程



#### 五.AOP操作（准备）

1.Spring框架中一般基于AspectJ实现AOP操作	
		1）.什么是AspectJ
				AspectJ不是Spring组成部分，独立AOP框架，一般把AspectJ和Spring框架一起使用，进行AOP操作

2.基于AspectJ实现AOP操作
		1）.基于xml配置文件
		2）.基于注解方式实现（使用此）

3.在项目工程里面引入AOP相关依赖

![image-20220523171406260](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220523171406260.png)

4.切入点表达式
		1）.切入点表达式的作用：知道对哪个类里边的哪个 方法 进行增强
		2）.语法结构
				execution( [权限修饰符] [返回类型] [类全路径] [参数列表] )

​		举例1：对com.yc.dao.BookDao类里面的add进行增强
​				execution(* com.yc.dao.BookDao.add(..))        //星号表示任意修饰符，后边有空格；返回类型可以省略不写

​		举例2：对com.yc.dao.BookDao类里面的所有的方法进行增强
​				execution(* com.yc.dao.BookDao.*(..))         //后面的星号代表对类中的所有的方法进行增强

​		举例3：对com.yc.dao包里面的所有类，类里面的所有的方法进行增强
​				execution(* com.yc.dao`*.*`(..))



#### 六.AOP操作（AspectJ注解）

1.创建类，在类里面定义方法

```java
/**
 * @Description: 被增强的类
 * @Author: YC
 * @CreateTime: 2022/05/24 9:36
 */
public class User {

    public void add(){
        System.out.println("add......");
    }
}
```

2.创建增强类（编写增强逻辑）
		1）.在增强类里面，创建方法，让不同方法代表不同通知类型

```java
/**
 * @Description: 增强的类
 * @Author: YC
 * @CreateTime: 2022/05/24 9:37
 */
public class UserProxy {

    //前置通知
    public void before(){
        System.out.println("before...");
    }
}
```

3.进行通知配置
		1）.在spring配置文件中，开启注解扫描

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
                           http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">

    <!--开启注解扫描-->
    <context:component-scan base-package="com.company.spring5.aopanno"></context:component-scan>

</beans>
```

​		2）.使用注解创建User和UserProxy对象（类上边加spring注解）

```java
@Component
public class User {

    public void add(){
        System.out.println("add...");
    }
}
```

```java
@Component
public class UserProxy {

    //前置通知
    public void before(){
        System.out.println("before...");
    }
}
```

​		3）.在增强类上面添加注解@Aspect

```java
@Component
@Aspect    //生成代理对象
public class UserProxy {

    //前置通知
    public void before(){
        System.out.println("before...");
    }
}
```

​		4）.在spring配置文件中开启生成代理对象

```xml
<!--开启Aspect生成代理对象-->
<aop:aspectj-autoproxy></aop:aspectj-autoproxy>
```

4.配置不同类型的通知
		1）.在增强类中的里面，在作为通知方法上面添加通知类型的注解，使用切入点表达式配置

```java
/**
 * @Description: 增强的类
 * @Author: YC
 * @CreateTime: 2022/05/24 9:37
 */
@Component
@Aspect    //生成代理对象
public class UserProxy {

    //前置通知
    //@Before注解表示作为前置通知
    @Before(value = "execution(* com.company.spring5.aopanno.User.add(..))")
    public void before(){
        System.out.println("before...");
    }

    //最终通知     （方法之后执行，有没有异常都执行）
    @After(value = "execution(* com.company.spring5.aopanno.User.add(..))")
    public void after(){
        System.out.println("after...");
    }

    //后置通知（或叫返回通知）     （返回值之后进行执行，有异常不执行）
    @AfterReturning(value = "execution(* com.company.spring5.aopanno.User.add(..))")
    public void afterReturning(){
        System.out.println("afterReturning...");
    }

    //异常通知        （有异常才执行）
    @AfterThrowing(value = "execution(* com.company.spring5.aopanno.User.add(..))")
    public void afterThrowing(){
        System.out.println("afterThrowing...");
    }

    //环绕通知
    @Around(value = "execution(* com.company.spring5.aopanno.User.add(..))")
    public void around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
        System.out.println("环绕之前...");

        //被增强的方法执行
        proceedingJoinPoint.proceed();

        System.out.println("环绕之后...");
    }

}
```

5.相同的切入点抽取

```java
/**
 * @Description: 增强的类
 * @Author: YC
 * @CreateTime: 2022/05/24 9:37
 */
@Component
@Aspect    //生成代理对象
public class UserProxy {

    //抽取相同切入点
    @Pointcut(value = "execution(* com.company.spring5.aopanno.User.add(..))")
    public void pointdemo(){

    }

    //前置通知
    //@Before注解表示作为前置通知
    @Before(value = "pointdemo()")
    public void before(){
        System.out.println("before...");
    }

    //最终通知     （方法之后执行，有没有异常都执行）
    @After(value = "pointdemo()")
    public void after(){
        System.out.println("after...");
    }

    //后置通知（或叫返回通知）     （返回值之后进行执行，有异常不执行）
    @AfterReturning(value = "pointdemo()")
    public void afterReturning(){
        System.out.println("afterReturning...");
    }

    //异常通知        （有异常才执行）
    @AfterThrowing(value = "pointdemo()")
    public void afterThrowing(){
        System.out.println("afterThrowing...");
    }

    //环绕通知
    @Around(value = "pointdemo()")
    public void around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
        System.out.println("环绕之前...");

        //被增强的方法执行
        proceedingJoinPoint.proceed();

        System.out.println("环绕之后...");
    }

}
```

6.有多个增强类对同一个方法进行增强，设置增强类优先级
		1）.在增强类上面添加注解@Order（数字类型值），数字类型值越小优先级越高

```java
@Component
@Aspect
@Order(1)
public class PersonProxy 
```



7.完全使用注解开发
		1）.创建配置类，不需要创建xml配置文件

```java
@Configuration
@ComponentScan(basePackages = {"com.company"})
@EnableAspectJAutoProxy(proxyTargetClass = true)   //此注解等同于在xml中配置 <aop:aspectj-autoproxy>，也就是生成代理对象，表示开启spring对注解AOP的支持。默认不写就是false。
public class ConfigAop {
}
```



#### 七.AOP操作（AspectJ配置文件）

开发过程中一般都用注解方式

1.创建两个类，增强类和被增强类，创建方法

```java
public class Book {

    public void buy(){
        System.out.println("buy......");
    }
}
```

```java
public class BookProxy {

    public void befor(){
        System.out.println("before......");
    }

}
```

2.在spring配置文件中创建两个类对象

```xml
<!--创建对象-->
<bean id="book" class="com.company.spring5.aopxml.Book"></bean>
<bean id="bookProxy" class="com.company.spring5.aopxml.BookProxy"></bean>
```

3.在spring配置文件中配置切入点

```xml
    <!--创建对象-->
    <bean id="book" class="com.company.spring5.aopxml.Book"></bean>
    <bean id="bookProxy" class="com.company.spring5.aopxml.BookProxy"></bean>

    <!--配置aop增强-->
    <aop:config>

        <!--切入点-->
        <aop:pointcut id="p" expression="execution(* com.company.spring5.aopxml.Book.buy(..))"/>

        <!--配置切面-->
        <aop:aspect ref="bookProxy">
            <!--增强作用在具体的方法上-->
            <aop:before method="befor" pointcut-ref="p"></aop:before>
        </aop:aspect>

    </aop:config>

</beans>
```





### JdbcTemplate



#### 一.JdbcTemplate（概念和准备）

1.什么是JdbcTemplate
		1）.Spring框架对JDBC进行封装，使用JdbcTemplate方便实现对数据库操作

2.准备工作
		1）.引入相关jar包

![image-20220524135912682](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220524135912682.png)



​		2）.在spring配置文件配置数据库连接池

```xml
<!--数据库连接池-->
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource" destroy-method="close">
    <property name="url" value="jdbc:mysql://jdbctemplatetest"></property>
    <property name="username" value="root"></property>
    <property name="password" value="123456"></property>
    <property name="driverClassName" value="com.mysql.jdbc.Driver"></property>
</bean>
```

​		3）.配置JdbcTemplate对象，注入DataSource

```xml
<!--JdbcTemplate对象-->
<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
    <!--set方法注入dataSource-->   <!--点进JdbcTemplate源码，发现注入dataSource的方法有有参构造和set，但是有参构造有个set方法，所以注入dataSource其实是用set方法-->
    <property name="dataSource" ref="dataSource"></property>
</bean>
```

​		4）.创建service类，创建dao类，在dao注入jdbcTemplate对象
​				*配置文件

```xml
<!--组件扫描-->
<context:component-scan base-package="com.company"></context:component-scan>
```

​				*Service

```java
@Service
public class BookService {

    //注入dao
    @Autowired
    private BookDao bookDao;

}
```

​				*Dao

```java
@Repository
public class BookDaoImpl implements BookDao{

    //注入JdbcTemplate
    @Autowired
    private JdbcTemplate jdbcTemplate;

}
```



#### 二.JdbcTemplate操作数据库（添加）

1.对应数据库创建实体类    （数据库表中对应的属性和它们的get，set方法）

```java
package com.company.spring5.entity;

/**
 * @Description:
 * @Author: YC
 * @CreateTime: 2022/05/24 14:35
 */
public class Book {

    private String userId;
    private String username;
    private String ustatus;

    public String getUserId() {
        return userId;
    }

    public void setUserId(String userId) {
        this.userId = userId;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getUstatus() {
        return ustatus;
    }

    public void setUstatus(String ustatus) {
        this.ustatus = ustatus;
    }
}
```

2.编写service和dao

​		service里注入dao，添加add方法

```java
@Service
public class BookService {

    //注入dao
    @Autowired
    private BookDao bookDao;

    //添加的方法
    public void addBook(Book book){
        bookDao.add(book);
    }
```

​		dao接口

```java
public interface BookDao {

    //添加的方法
    void add(Book book);
}
```

​		1）.在dao进行数据库添加操作
​		2）.调用Jdbctemplate对象里面update方法实现添加操作
​				![image-20220524144847441](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220524144847441.png)

​				有两个参数：
​						第一个参数：sql语句
​						第二个参数：可变参数，设置sql语句的值

```java
@Repository
public class BookDaoImpl implements BookDao{

    //注入JdbcTemplate
    @Autowired
    private JdbcTemplate jdbcTemplate;

    //添加的方法
    @Override
    public void add(Book book) {

        //1.创建sql语句
        String sql = "insert into book values(?,?,?)";
        //2.调用方法实现
        int update = jdbcTemplate.update(sql, book.getUserId(), book.getUsername(), book.getUstatus());
        System.out.println(update);      //上边返回的int值，代表影响的行数，成功添加了几条记录

/*      //或者这样写，因为update第二个参数是可变的，实际上就是一个数组形式，可以先把他们放到数组里，再把数组传进去
        //2.调用方法实现
        Object[] args = {book.getUserId(), book.getUsername(), book.getUstatus()};
        int update = jdbcTemplate.update(sql, args);
        System.out.println(update);      //上边返回的int值，代表影响的行数，成功添加了几条记录
*/
    }
}
```



3.测试类

```java
@Test
public void testJdbcTemplate(){
    ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
    BookService bookService = context.getBean("bookService", BookService.class);

    Book book = new Book();
    book.setUserId("1");
    book.setUsername("java");
    book.setUstatus("a");
    bookService.addBook(book);
}
```

![image-20220524155053367](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220524155053367.png)



#### 三.JdbcTemplate操作数据库（修改和删除）

1.修改

```java
//修改的方法
@Override
public void updateBook(Book book) {
    String sql = "update book set username = ? , ustatus = ? where user_id = ?";
    Object[] args = {book.getUsername(), book.getUstatus(), book.getUserId()};
    int update = jdbcTemplate.update(sql, args);
    System.out.println(update);
}
```

```java
    @Test
    public void testJdbcTemplate(){
        ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
        BookService bookService = context.getBean("bookService", BookService.class);

//        //添加
//        Book book = new Book();
//        book.setUserId("1");
//        book.setUsername("java");
//        book.setUstatus("a");
//        bookService.addBook(book);

        //修改
        Book book = new Book();
        book.setUserId("1");
        book.setUsername("java123");
        book.setUstatus("b");
        bookService.updateBook(book);

    }
```

2.删除

```java
    //删除的方法
    @Override
    public void delete(String id) {
        String sql = "delete from book where user_id =?";
        int update = jdbcTemplate.update(sql, id);
        System.out.println(update);
    }
}
```

```java
    @Test
    public void testJdbcTemplate(){
        ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
        BookService bookService = context.getBean("bookService", BookService.class);

//        //添加
//        Book book = new Book();
//        book.setUserId("1");
//        book.setUsername("java");
//        book.setUstatus("a");
//        bookService.addBook(book);

//        //修改
//        Book book = new Book();
//        book.setUserId("1");
//        book.setUsername("java123");
//        book.setUstatus("b");
//        bookService.updateBook(book);

        //删除
        bookService.deleteBook("1");
    }
```



#### 四.JdbcTemplate操作数据库（查询返回某个值）

1.查询表里面有多少条记录，返回是某个值

2.使用JdbcTemplate实现查询返回某个值代码
		![image-20220524164014317](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220524164014317.png)
		有两个参数：
				第一个参数：sql语句
				第二个参数：返回类型Class（返回int，就是int类型Class；返回String，就是String类型Class)

```java
//查询表记录数
@Override
public int selectCount() {
    String sql = "select count(*) from book";
    Integer count = jdbcTemplate.queryForObject(sql, Integer.class);
    return count;
}
```



#### 五.JdbcTemplate操作数据库（查询返回对象）

1.场景：查询图书详情

2.JdbcTemplate实现查询返回对象
		![image-20220524165625628](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220524165625628.png)
		有三个参数：
				第一个参数：sql语句
				第二个参数：RowMapper，是接口，针对返回不同类型的数据，使用这个接口里面的实现类完成数据封装
				第三个参数：sql语句的值

```java
//查询返回对象
@Override
public Book findBookInfo(String id) {
    String sql = "select * from book where user_id = ?";
    //调用方法
    Book book = jdbcTemplate.queryForObject(sql, new BeanPropertyRowMapper<Book>(Book.class), id);
    return book;
}
```



#### 六.JdbcTemplate操作数据库（查询返回集合）

1.场景：查询图书列表分页...

2.调用JdbcTemplate方法实现查询返回集合
		![image-20220524171752297](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220524171752297.png)
		有三个参数：
				第一个参数：sql语句
				第二个参数：RowMapper，是接口，针对返回不同类型的数据，使用这个接口里面的实现类完成数据封装
				第三个参数：sql语句的值

```java
//查询返回集合
@Override
public List<Book> findAllBook() {
    String sql = "select * from book";
    //调用方法
    List<Book> bookList = jdbcTemplate.query(sql, new BeanPropertyRowMapper<Book>(Book.class));
    return bookList;
}
```



#### 七.JdbcTemplate操作数据库（批量操作）

1.批量操作：操作表里面多条记录

2.JdbcTemplate实现批量添加操作
		![image-20220524173418269](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220524173418269.png)
		有两个参数：
				第一个参数：sql语句
				第二个参数：List集合，表示添加的多条记录数据

dao层实现类进行批量添加：

```java
//批量添加
@Override
public void batchAddBook(List<Object[]> batchArgs) {
    String sql = "insert into book values(?,?,?)";
    int[] ints = jdbcTemplate.batchUpdate(sql, batchArgs);
    System.out.println(Arrays.toString(ints));
}
```

测试：

```java
//批量添加
List<Object[]> batchArgs = new ArrayList<>();
Object[] o1 = {"3","java","a"};
Object[] o2 = {"4","c++","b"};
Object[] o3 = {"5","musql","c"};
//将三个数组放到list集合里边
batchArgs.add(o1);
batchArgs.add(o2);
batchArgs.add(o3);
//调用批量添加
bookService.batchAdd(batchArgs);
```



3.JdbcTemplate实现批量修改操作

批量修改
dao层实现类：

```java
//批量修改
@Override
public void batchUpdateBook(List<Object[]> batchArgs) {
    String sql = "update book set username = ? , ustatus = ? where user_id = ?";
    int[] ints = jdbcTemplate.batchUpdate(sql, batchArgs);
    System.out.println(Arrays.toString(ints));
```

测试：

```java
//批量修改   （参数顺序有要求）
List<Object[]> batchArgs = new ArrayList<>();
Object[] o1 = {"java1","aa","3"};
Object[] o2 = {"c++2","bb","4"};
Object[] o3 = {"musql3","cc","5"};
//将三个数组放到list集合里边
batchArgs.add(o1);
batchArgs.add(o2);
batchArgs.add(o3);
//调用方法实现批量修改
bookService.batchUpdate(batchArgs);
```



批量删除
dao层实现类：

```java
@Override
public void batchDeleteBook(List<Object[]> batchArgs) {
    String sql = "delete from book where user_id=?";
    int[] ints = jdbcTemplate.batchUpdate(sql, batchArgs);
    System.out.println(Arrays.toString(ints));
```

测试：

```java
//批量删除
List<Object[]> batchArgs = new ArrayList<>();
Object[] o1 = {"3"};
Object[] o2 = {"4"};
Object[] o3 = {"5"};
//将三个数组放到list集合里边
batchArgs.add(o1);
batchArgs.add(o2);
batchArgs.add(o3);
//调用方法实现批量修改
bookService.batchDelete(batchArgs);
```







### 事务



#### 一.事务操作（事务概念）

1.什么是事务
		1）.事务是数据库操作最基本单元，逻辑上一组操作，要么都成功，如果有一个失败所有操作都失败
		2）.典型场景：银行转账
				张三转账100给李四，张三少100，李四多100。有任何一方有问题，都失败

2.事务四个特性（ACID）
		1）.原子性：过程中不可分割，要么都成功，一个失败都失败
		2）.一致性：操作之前和操作之后总量是不变的
		3）.隔离性：多事务操作的时候，他们之间不会产生影响
		4）.持久性：提交事务之后，表中数据真正发生变化



#### 二.事务操作（搭建事务操作环境）

![image-20220525110309064](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220525110309064.png)



1.创建数据库表，添加记录

![image-20220525111206199](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220525111206199.png)

2.创建service，搭建dao，完成对象创建 和注入关系
		1）.service注入dao，在dao注入JdbcTemplate，在JdbcTemplate注入DataSource

```java
@Service
public class UserService {

    //注入dao
    @Autowired
    private UserDao userDao;
}
```

```java
@Repository
public class UersDaoImpl implements UserDao{

    @Autowired
    private JdbcTemplate jdbcTemplate;
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
                           http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">

    <!--组件扫描-->
    <context:component-scan base-package="com.company"></context:component-scan>

    <!--数据库连接池-->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource" destroy-method="close">
        <property name="url" value="jdbc:mysql:///jdbctemplatetest"></property>
        <property name="username" value="root"></property>
        <property name="password" value="1234"></property>
        <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"></property>
    </bean>

    <!--JdbcTemplate对象-->
    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        <!--set方法注入dataSource-->   <!--点进JdbcTemplate源码，发现注入dataSource的方法有有参构造和set，但是有参构造有个set方法，所以注入dataSource其实是用set方法-->
        <property name="dataSource" ref="dataSource"></property>
    </bean>
    
</beans>
```



3.在dao创建两个方法：多钱和少钱的方法，在service创建方法（转账的方法）

```java
public interface UserDao {

    //多钱
    public void addMoney();

    //少钱
    public void reduceMoney();
}
```

```java
@Repository
public class UersDaoImpl implements UserDao{

    @Autowired
    private JdbcTemplate jdbcTemplate;

    //zhangsan转账100给李四
    //少钱
    @Override
    public void reduceMoney() {
        String sql = "update account set money=money-? where username=?";
        jdbcTemplate.update(sql,100,"zhangsan");
    }

    //多钱
    @Override
    public void addMoney() {
        String sql = "update account set money=money+? where username=?";
        jdbcTemplate.update(sql,100,"lisi");
    }
}
```

```java
@Service
public class UserService {

    //注入dao
    @Autowired
    private UserDao userDao;

    //转账的方法
    public void accountMoney(){
        //zhangsan少100
        userDao.reduceMoney();

        //lisi多100
        userDao.addMoney();
    }
}
```



4.上面代码，如果正常执行没有问题的，但如果代码执行过程中出现异常，有问题

![image-20220525134621757](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220525134621757.png)

​		1）.上面问题如何解决呢
​				使用事务进行解决

​		2）.事务操作过程

![image-20220525135320982](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220525135320982.png)



#### 三.事务操作（Spring管理）

1.事务添加到JavaEE三层结构里面Service层（业务逻辑层）

2.在Spring进行事务管理操作
		1）.有两种方式：编程式事务管理和声明式事务管理（通常使用后者）

3.声明式事务管理（通常用第一种）
		1）.基于注解方式
		2）.基于xml配置文件方式

4.在Spring进行声明式事务管理，底层使用AOP原理

5.Spring事务管理API
		1）.提供一个接口，代表事务管理器，这个接口针对不同的框架提供不同的实现类
				PlatformTransactionManager

![image-20220525140624716](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220525140624716.png)



#### 四.事务操作（注解声明式事务管理）

1.在spring配置文件配置事务管理器

```xml
<!--创建事务管理器-->
<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    <!--注入数据源-->    <!--指定自己创建数据源的部分，上边的数据库连接池-->
    <property name="dataSource" ref="dataSource"></property>
</bean>
```

2.在spring配置文件，开启事务注解
		1）.在spring配置文件中引入名称空间tx

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
                           http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd
                           http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd">
```

​		2）.开启事务注解

```xml
<!--开启事务注解-->
<tx:annotation-driven transaction-manager="transactionManager"></tx:annotation-driven>
```

3.在service类上面（或者service类里面的方法上面）添加事务注解
		1）.@Transactional，这个注解可以添加到类上面，也可以添加到方法上面
		2）.如果把这个注解添加类上面，这个类里面所有的方法都添加事务
		3）.如果把这个注解添加方法上面，为这个方法添加事务

```java
@Service
@Transactional
public class UserService {
    ...
}
```



#### 五.事务管理（声明式事务管理参数配置）

在service类上面添加注解@Transactional，在这个注解里面可以配置事务相关参数

![image-20220525143451041](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220525143451041.png)

1.propagation：事务传播行为
		1）.多事务方法之间进行调用，这个过程中事务是如何进行管理的

![image-20220525155900667](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220525155900667.png)

![image-20220525155924393](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220525155924393.png)

```java
@Service
@Transactional(propagation = Propagation.REQUIRED)   //不写默认就是REQUIRED
public class UserService {
    ...
}
```

2.isolation：事务隔离级别
		1).事务有个特性称为隔离性，多事务操作之间不会产生影响，不考虑隔离性会产生很多问题
		2）.有三个读的问题：脏读、不可重复读、虚（幻）读
				(1).脏读：一个未提交的事务读取到另一个未提交事务的数据

![image-20220525161113503](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220525161113503.png)

![d01373f082025aaf5be5454896a1dd6d024f1a37](https://raw.githubusercontent.com/chocman99/Image/main/Spring/d01373f082025aaf5be5454896a1dd6d024f1a37.jpeg)

​				(2).不可重复读：一个未提交事务读取到另一提交事务修改数据（事务之间应该不会产生影响 ）

![image-20220525161757035](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220525161757035.png)

![不可重复读](https://raw.githubusercontent.com/chocman99/Image/main/Spring/%E4%B8%8D%E5%8F%AF%E9%87%8D%E5%A4%8D%E8%AF%BB.jpeg)

​				(3).幻读：一个未提交的事务读取到另一提交事务添加数据

![虚读](https://raw.githubusercontent.com/chocman99/Image/main/Spring/%E8%99%9A%E8%AF%BB.jpeg)

​		3）.解决：通过设置事务隔离性，解决读问题

![image-20220525163432191](https://raw.githubusercontent.com/chocman99/Image/main/Spring/image-20220525163432191.png)

​				隔离级别设置：（第二个参数）（Mysql默认隔离级别是REPEATABLE_READ）

```java
@Service
@Transactional(propagation = Propagation.REQUIRED,isolation = Isolation.REPEATABLE_READ)
public class UserService {
    ...
}
```

3.timeout：超时时间
		1）.事务需要在一定的时间内进行提交，如果不提交就会进行回滚
		2）.默认值是-1，代表不超时。设置的话时间以秒单位进行计算
				第一个参数：

```java
@Service
@Transactional(timeout = -1 ,propagation = Propagation.REQUIRED，isolation = Isolation.REPEATABLE_READ)
public class UserService {
    ...
}
```

4.readOnly：是否只读
		1）.读：查询操作，写：添加修改删除操作
		2）.readOnly默认值false，表示可以查询，可以增加修改删除操作
		3）.设置readOnly值是true，设置成true之后，只能查询

5.rollbackFor：回滚
		1）.设置出现哪些异常进行事务回滚

6.noRollbackFor：不回滚
		1）.设置出现哪些异常不进行事务回滚



#### 六.事务操作（XML声明式事务管理）

1.在spring配置文件中进行
		第一步：配置事务管理器
		第二步：配置通知
		第三步：配置切入点和切面

```xml
    <!--1.创建事务管理器-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <!--注入数据源-->    <!--指定自己创建数据源的部分，上边的数据库连接池-->
        <property name="dataSource" ref="dataSource"></property>
    </bean>

    <!--2.配置通知-->
    <tx:advice id="txadvice">
        <!--配置事务参数-->
        <tx:attributes>
            <!--指定哪种规则的方法上面添加事务
            两种方式：1.在哪个方法添加事务，就写那个方法名
                     2.比如account*代表方法名只要以account开头的，都加上事务操作
            -->
            <tx:method name="accountMoney" propagation="REQUIRED"/>
<!--            <tx:method name="account*"/>-->
        </tx:attributes>
    </tx:advice>

    <!--3.配置切入点和切面-->
    <aop:config>
        <!--配置切入点-->
        <aop:pointcut id="pt" expression="execution(* com.company.spring5.service.UserService.*(..))"/>
        <!--配置切面-->
        <aop:advisor advice-ref="txadvice" pointcut-ref="pt"></aop:advisor>
    </aop:config>
```



#### 七.事务操作（完全注解声明式事务管理）

1.创建配置类，使用配置类替代xml配置文件

```java
/**
 * @Description: 完全注解声明式事务管理（完全替代xml配置文件）
 * @Author: YC
 * @CreateTime: 2022/05/25 17:13
 */
@Configuration  //配置类
@ComponentScan(basePackages = "com.company")    //组件扫描
@EnableTransactionManagement     //开启事务
public class TxConfig {

    //创建数据库连接池
    @Bean
    public DruidDataSource getDruidDataSource(){
        DruidDataSource  dataSource = new DruidDataSource();
        dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
        dataSource.setUrl("jdbc:mysql:///jdbctemplatetest");
        dataSource.setUsername("root");
        dataSource.setPassword("1234");
        return dataSource;
    }

    //创建JdbcTemplate对象
    @Bean
    public JdbcTemplate getJdbcTemplate(DataSource dataSource){    //参数的意思是到ioc容器中根据类型找到dataSource，传给下面的setDataSource方法里
        JdbcTemplate jdbcTemplate = new JdbcTemplate();
        //注入dataSource
        jdbcTemplate.setDataSource(dataSource);
        return jdbcTemplate;
    }

    //创建事务管理器
    @Bean
    public DataSourceTransactionManager dataSourceTransactionManager(DataSource dataSource){
        DataSourceTransactionManager transactionManager = new DataSourceTransactionManager();
        transactionManager.setDataSource(dataSource);
        return transactionManager;
    }
}
```

测试：

```java
//完全注解测试
@Test
public void testAccount2(){
    ApplicationContext context = new AnnotationConfigApplicationContext(TxConfig.class);
    UserService userService = context.getBean("userService", UserService.class);
    userService.accountMoney();
}
```



