

## SpringBoot2核心技术-基础入门



1.学习要求

熟悉Spring基础
熟悉Maven使用



2.环境要求

Java8及以上
Maven 3.3及以上

官网：https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started.html#getting-started-system-requirements





### 一.Spring与SpringBoot



#### 1.Spring能做什么

##### 	1.1 Spring的能力

![image-20220803100938667](D:\Typora\images\image-20220803100938667.png)



##### 	1.2 Spring的生态

官网：https://spring.io/projects/spring-boot

覆盖了：
	web开发
	数据访问
	安全控制
	分布式
	消息服务
	移动开发
	批处理
	......



##### 	1.3 Spring5重大升级

​		1.3.1 响应式编程

![image-20220803101418162](D:\Typora\images\image-20220803101418162.png)



​		1.3.2 内部源码设计

基于Java8的一些新特性，如：接口默认实现。重新设计源码架构。



#### 2.为什么用SpringBoot

> Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run".
>
> 能快速创建出生产级别的Spring应用



##### 	2.1 SpringBoot优点

- Create stand-alone Spring applications
- 创建独立Spring应用

- Embed Tomcat, Jetty or Undertow directly (no need to deploy WAR files)
- 内嵌web服务器

- Provide opinionated 'starter' dependencies to simplify your build configuration
- 自动starter依赖，简化构建配置

- Automatically configure Spring and 3rd party libraries whenever possible
- 自动配置Spring以及第三方功能

- Provide production-ready features such as metrics, health checks, and externalized configuration
- 提供生产级别的监控、健康检查及外部化配置

- Absolutely no code generation and no requirement for XML configuration
- 无代码生成、无需编写XML



> SpringBoot是整合Spring技术栈的一站式框架
> SpringBoot是简化Spring技术栈的快速开发脚手架



##### 	2.2 SpringBoot缺点

- 人称版本帝，迭代快，需要时刻关注变化
- 封装太深，内部原理复杂，不容易精通



#### 3.时代背景

##### 	3.1 微服务

In short, the microservice architectural style is an      approach to developing a single application as a **suite of small      services**, each **running in its own process** and communicating with      lightweight mechanisms, often an HTTP resource API. These      services are **built around business capabilities** and      **independently deployable** by fully automated deployment      machinery. There is a **bare minimum of centralized management** of      these services, which may be written in different programming      languages and use different data storage      technologies.

- 微服务是一种架构风格
- 一个应用拆分为一组小型服务
- 每个服务运行在自己的进程内，也就是可独立部署和升级
- 服务之间使用轻量级HTTP交互
- 服务围绕业务功能拆分
- 可以由全自动部署机制独立部署
- 去中心化，服务自治。服务可以使用不同的语言、不同的存储技术

官网：https://martinfowler.com/microservices/



##### 	3.2 分布式

![image-20220803110310279](D:\Typora\images\image-20220803110310279.png)



分布式的困难：

- 远程调用
- 服务发现
- 负载均衡
- 服务容错
- 配置管理
- 服务监控
- 链路追踪
- 日志管理
- 任务调度
- ......



分布式的解决

- SpringBoot + SpringCloud

![image-20220803110432904](D:\Typora\images\image-20220803110432904.png)



##### 	3.3 云原生

原生应用如何上云。 Cloud Native



上云的解决

![image-20220803110515553](D:\Typora\images\image-20220803110515553.png)





#### 4.如何学习SpringBoot

官网文档架构

https://spring.io/projects/spring-boot#learn

CURRENT：稳定版本
SNAPSHOT：快照版本

![image-20220803110930179](D:\Typora\images\image-20220803110930179.png)

![image-20220803112144661](D:\Typora\images\image-20220803112144661.png)

![image-20220803113048966](D:\Typora\images\image-20220803113048966.png)



查看版本新特性；

https://github.com/spring-projects/spring-boot/wiki#release-notes

或者

![image-20220803113156307](D:\Typora\images\image-20220803113156307.png)





### 二.SpringBoot2入门

#### 1.系统要求

- [Java 8](https://www.java.com/) & 兼容java18
- Maven 3.5+
- idea 2019.1.2



#### 2.HelloWorld

需求：浏览发送/hello请求，响应 Hello，Spring Boot 2

##### 	2.1 创建maven工程

##### 	2.2 引入依赖

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.7.2</version>
</parent>

<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```



##### 	2.3 创建主程序

```java
/**
 * 主程序类
 * @SpringBootApplication：这是一个springboot应用
 *
 */
@SpringBootApplication
public class MainApplication {
    public static void main(String[] args) {
        SpringApplication.run(MainApplication.class,args);
    }
}
```



##### 	2.4 编写业务

```java
//@RestController:整合和@ResponseBody和@Controller。无需写两个，只要写一个@RestController就可以
@RestController
public class HelloController {

    @RequestMapping("/hello")
    public String handle01(){
        return "hello,Spring Boot 2!";
    }

}
```



##### 	2.5 测试

直接运行main方法



##### 	2.6 简化配置

SpringBoot为了简化，将未来所有的配置都可以抽取在一个配置文件里，配置文件固定名字：application.properties

比如：

```properties
server.port=8888
```



##### 	2.7 简化部署

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

把项目打成jar包，直接在目标服务器执行即可。

注意点：
	取消掉cmd的快速编辑模式



### 三.了解自动配置原理

#### 1.SpringBoot特点

##### 	1.1 依赖管理

​		（1）父项目做依赖管理

子项目只要继承了父项目，子项目写依赖就不需要版本号了

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.7.2</version>
</parent>

<!--他的父项目（这个不要写到pom.xml里）-->
<parent>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-dependencies</artifactId>
  <version>2.7.2</version>
</parent>
```



​		（2）开发导入starter场景启动器

```xml
1、见到很多 spring-boot-starter-* ： *就代表某种场景
2、只要引入starter，这个场景的所有常规需要的依赖我们都自动引入
3、SpringBoot所有支持的场景
https://docs.spring.io/spring-boot/docs/current/reference/html/using-spring-boot.html#using-boot-starter
4、见到的  *-spring-boot-starter： 第三方为我们提供的简化开发的场景启动器。
5、所有场景启动器最底层的依赖
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter</artifactId>
  <version>2.3.4.RELEASE</version>
  <scope>compile</scope>
</dependency>
```

官方说明：https://docs.spring.io/spring-boot/docs/current/reference/html/using-spring-boot.html#using-boot-starter

![image-20220804103301513](D:\Typora\images\image-20220804103301513.png)



​		（3）无需关注版本号，自动版本仲裁

1、引入依赖默认都可以不写版本
2、引入非版本仲裁的jar，要写版本号。



​		（4）可以修改默认版本号

```xml
1、查看spring-boot-dependencies里面规定当前依赖的默认版本用的key。
2、若想要修改，在当前项目的pom.xml里面重写配置。比如
    <properties>
        <mysql.version>8.0.28</mysql.version>
    </properties>
```



##### 	1.2 自动配置

​		（1）自动配好Tomcat
​			引入Tomcat依赖
​			配置Tomcat

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-tomcat</artifactId>
  <version>2.7.2</version>
  <scope>compile</scope>
</dependency>
```



​		（2）自动配好SpringMVC
​			引入SpringMVC全套组件
​			自动配好SpringMVC常用组件（功能）

​		（3）自动配好Web常见功能，如：字符编码问题
​			SpringBoot帮我们配置好了所有web开发的常见场景

​		（4）默认的包结构
​			主程序所在包及其下面的所有子包里面的组件都会被默认扫描进来
​			无需以前的包扫描配置
​			想要改变扫描路径，@SpringBootApplication(scanBasePackages="com.yc")，或者@ComponentScan 指定扫描路径（@SpringBootApplication等同于@SpringBootConfiguration、@EnableAutoConfiguration、@ComponentScan("com.yc.boot")）

​		（5）各种配置拥有默认值
​			默认配置最终都是映射到某个类上，如：MultipartProperties
​			配置文件的值最终会绑定每个类上，这个类会在容器中创建对象

​		（6）按需加载所有自动配置项
​			非常多的starter
​			引入了哪些场景这个场景的自动配置才会开启
​			SpringBoot所有的自动配置功能都在 spring-boot-autoconfigure 包里面

​		......



#### 	2.容器功能

##### 			2.1 组件添加

​		1.@Configuration
​			（1）基本使用
​			（2）Full模式与Lite模式
​				示例
​				最佳实战
​					配置 类组件之间无依赖关系用Lite模式加速容器启动过程，减少判断
​					配置类组件之间有依赖关系，方法会被调用得到之前单实例组件，用Full模式

配置类：

```java
/**
 * @Configuration： 告诉SpringBoot这是一个配置类 == spring中的配置文件
 * 类里也不再写标签了，而是写方法
 * 1.配置类里面使用@Bean标注在方法上给容器注册组件，默认也是单实例的     (注册的组件继续保持spring的特性，组件默认是单实例的)
 * 2.配置类本身也是组件
 * 3.proxyBeanMethods：代理bean的方法 （Configuration标签里的属性）
 *      Full:(proxyBeanMethods = true)  如果为true，配置类里边每一个给容器中组件注册的方法，在外边随便调用，都会去容器中找组件
 *      Lite:(proxyBeanMethods = false) 如果为false，配置类在容器中再也不会保存代理对象，在外边无限次调用这些方法，每一次调用都会产生一个新的对象
 *      解决场景：组件依赖   (比如User类里加一个Pet属性)
 *
 */
//@Configuration：告诉SpringBoot这是一个配置类 == spring中的配置文件
@Configuration(proxyBeanMethods = true)
public class MyConfig {

    /**
     *Full外部无论对配置类中的这个组件注册方法调用多少次获取的都是之前注册容器中的单实例对象
     */
    //给容器中添加组件。以方法名作为组建的id，想自定义可以在bean标签后面输入一个值，如@Bean("user02")。返回类型就是组件类型。返回的值，就是组件在容器中的实例
    @Bean
    public User user01(){
        User zhangsan = new User("zhangsan", 18);
        //user组件依赖了Pet组件
        zhangsan.setPet(tomcatPet());
        return zhangsan;
    }

    @Bean("tom")
    public Pet tomcatPet(){
        return new Pet("tomcat");
    }

}
```

主程序类：

```java
/**
 * 主程序类
 * @SpringBootApplication：这是一个springboot应用
 *
 */
@SpringBootApplication
public class MainApplication {
    public static void main(String[] args) {
        //1.返回IOC容器
        ConfigurableApplicationContext run = SpringApplication.run(MainApplication.class, args);

        //2.查看容器里面的组件
        String[] names = run.getBeanDefinitionNames();
        for(String name : names){
            System.out.println(name);
        }

        //3.从容器中获取组件
        Pet tom01 = run.getBean("tom", Pet.class);
        Pet tom02 = run.getBean("tom", Pet.class);
        System.out.println("组件" + (tom01 == tom02));

        //4.配置类本身也是组件：获取配置类。com.yc.boot.config.MyConfig$$EnhancerBySpringCGLIB$$99d42727@1ee29c84
        MyConfig bean = run.getBean(MyConfig.class);
        System.out.println(bean);

        //5.如果@Configuration(proxyBeanMethods = true)代理对象调用方法。springboot总会检查这个组件是否在容器中有。
        //保持组件单实例
        User user = bean.user01();
        User user1 = bean.user01();
        System.out.println(user == user1);

        User user01 = run.getBean("user01", User.class);
        Pet tom = run.getBean("tom", Pet.class);
        System.out.println("用户的宠物" + (user01.getPet() == tom));
    }
}
```

注意：
	若(proxyBeanMethods = true)，输出结果为：

![image-20220805123418401](D:\Typora\images\image-20220805123418401.png)

​	若(proxyBeanMethods = false)，输出结果为：

![image-20220805123511426](D:\Typora\images\image-20220805123511426.png)



​		2.@Import

@Bean、@Component、@Controller、@Service、@Repository、@ComponentScan这些以前都学过了，不过多介绍了

@Import({User.class, AbstractMatcherFilter.class})

*      给容器中自动创建出这两个类型的组件、默认组建的名字就是全类名

@Import:通过@Import注解可以给容器导入非常多的组件。可以导入自己的User，或者第三方的jar包等等,底层是数组，大括号内可以写多个，用逗号隔开



​		3.@Conditional

条件装配：满足Conditional指定的条件，则进行组件注入（注意顺序问题）

![image-20220807144611966](D:\Typora\images\image-20220807144611966.png)



##### 2.2 原生配置文件引入

​		1.@ImportResource

导入Spring的配置文件，让它生效



##### 2.3 配置绑定

如何使用Java读取到properties文件中的内容，并且把它封装到JavaBean中，以供随时使用；

​		1.@ConfigurationProperties

```java
/**
 * 只有在容器中的组件，才会拥有SpringBoot提供的强大功能
 */
@Component
@ConfigurationProperties(prefix = "mycar")  //已经与配置文件application.properties里的前缀为mycar的绑定上了
public class Car {

    private String brand;
    private Integer price;

    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }

    public Integer getPrice() {
        return price;
    }

    public void setPrice(Integer price) {
        this.price = price;
    }

    @Override
    public String toString() {
        return "Car{" +
                "brand='" + brand + '\'' +
                ", price=" + price +
                '}';
    }
}
```



​		2.@Component + @ConfigurationProperties

```java
@Component	//只有在容器中的组件，才会拥有SpringBoot提供的强大功能
@ConfigurationProperties(prefix = "mycar")  //已经与配置文件application.properties里的前缀为mycar的绑定上了
public class Car {
	...
}
```

```properties
mycar.brand=YD
mycar.price=10
```



​	3.@EnableConfigurationProperties + @ConfigurationProperties

在配置类MyConfig中加入该注解

```java
//1.开启Car的配置绑定功能。2.把Car这个组件自动注册到容器中
@EnableConfigurationProperties(Car.class)
```

```java
@ConfigurationProperties(prefix = "mycar")  //已经与配置文件application.properties里的前缀为mycar的绑定上了
public class Car {
    	...
}
```



#### 3.自动配置原理入门

##### 3.1 引导加载自动配置类

@SpringBootApplication是个复合注解，里边有三个注解：

```java
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(
    excludeFilters = {@Filter(
    type = FilterType.CUSTOM,
    classes = {TypeExcludeFilter.class}
), @Filter(
    type = FilterType.CUSTOM,
    classes = {AutoConfigurationExcludeFilter.class}
)}
)
public @interface SpringBootApplication {}
```



1.@SpringBootConfiguration

点进去后发现是一个@Configuration，代表当前是一个配置类

2.@ComponentScan

指定扫描哪些，spring注解

3.@EnableAutoConfiguration

点进去发现又有几个注解：

```java
@AutoConfigurationPackage
@Import({AutoConfigurationImportSelector.class})
public @interface EnableAutoConfiguration {}
```

​	（1）.@AutoConfigurationPackage

​		自动配置包

```java
@Import({Registrar.class})	//给容器中导入一个组件
public @interface AutoConfigurationPackage {}

//利用Registrar给容器中导入一系列组件
//将指定的一个包下的所有组件导入进来：MainApplication所在的包下。
```



​	（2）.@Import({AutoConfigurationImportSelector.class})

​		1、利用getAutoConfigurationEntry(annotationMetadata)方法；给容器中批量导入一些组件
​		2、调用List<String> configurations = getCandidateConfigurations(annotationMetadata, attributes)获取到所有需要导入到容器中的配置类
​		3、利用工厂加载 Map<String, List<String>> loadSpringFactories(@Nullable ClassLoader classLoader)；得到所有的组件
​		4、从META-INF/spring.factories位置来加载一个文件。
​			默认扫描我们当前系统里面所有META-INF/spring.factories位置的文件
​    		spring-boot-autoconfigure-2.7.2.jar包里面也有：META-INF/spring./org.springframework.boot.autoconfigure.AutoConfiguration.imports

![image-20220808102719499](D:\Typora\images\image-20220808102719499.png)

<details>     <summary>144个自动配置</summary>
org.springframework.boot.autoconfigure.admin.SpringApplicationAdminJmxAutoConfiguration
org.springframework.boot.autoconfigure.aop.AopAutoConfiguration
org.springframework.boot.autoconfigure.amqp.RabbitAutoConfiguration
org.springframework.boot.autoconfigure.batch.BatchAutoConfiguration
org.springframework.boot.autoconfigure.cache.CacheAutoConfiguration
org.springframework.boot.autoconfigure.cassandra.CassandraAutoConfiguration
org.springframework.boot.autoconfigure.context.ConfigurationPropertiesAutoConfiguration
org.springframework.boot.autoconfigure.context.LifecycleAutoConfiguration
org.springframework.boot.autoconfigure.context.MessageSourceAutoConfiguration
org.springframework.boot.autoconfigure.context.PropertyPlaceholderAutoConfiguration
org.springframework.boot.autoconfigure.couchbase.CouchbaseAutoConfiguration
org.springframework.boot.autoconfigure.dao.PersistenceExceptionTranslationAutoConfiguration
org.springframework.boot.autoconfigure.data.cassandra.CassandraDataAutoConfiguration
org.springframework.boot.autoconfigure.data.cassandra.CassandraReactiveDataAutoConfiguration
org.springframework.boot.autoconfigure.data.cassandra.CassandraReactiveRepositoriesAutoConfiguration
org.springframework.boot.autoconfigure.data.cassandra.CassandraRepositoriesAutoConfiguration
org.springframework.boot.autoconfigure.data.couchbase.CouchbaseDataAutoConfiguration
org.springframework.boot.autoconfigure.data.couchbase.CouchbaseReactiveDataAutoConfiguration
org.springframework.boot.autoconfigure.data.couchbase.CouchbaseReactiveRepositoriesAutoConfiguration
org.springframework.boot.autoconfigure.data.couchbase.CouchbaseRepositoriesAutoConfiguration
org.springframework.boot.autoconfigure.data.elasticsearch.ElasticsearchDataAutoConfiguration
org.springframework.boot.autoconfigure.data.elasticsearch.ElasticsearchRepositoriesAutoConfiguration
org.springframework.boot.autoconfigure.data.elasticsearch.ReactiveElasticsearchRepositoriesAutoConfiguration
org.springframework.boot.autoconfigure.data.elasticsearch.ReactiveElasticsearchRestClientAutoConfiguration
org.springframework.boot.autoconfigure.data.jdbc.JdbcRepositoriesAutoConfiguration
org.springframework.boot.autoconfigure.data.jpa.JpaRepositoriesAutoConfiguration
org.springframework.boot.autoconfigure.data.ldap.LdapRepositoriesAutoConfiguration
org.springframework.boot.autoconfigure.data.mongo.MongoDataAutoConfiguration
org.springframework.boot.autoconfigure.data.mongo.MongoReactiveDataAutoConfiguration
org.springframework.boot.autoconfigure.data.mongo.MongoReactiveRepositoriesAutoConfiguration
org.springframework.boot.autoconfigure.data.mongo.MongoRepositoriesAutoConfiguration
org.springframework.boot.autoconfigure.data.neo4j.Neo4jDataAutoConfiguration
org.springframework.boot.autoconfigure.data.neo4j.Neo4jReactiveDataAutoConfiguration
org.springframework.boot.autoconfigure.data.neo4j.Neo4jReactiveRepositoriesAutoConfiguration
org.springframework.boot.autoconfigure.data.neo4j.Neo4jRepositoriesAutoConfiguration
org.springframework.boot.autoconfigure.data.r2dbc.R2dbcDataAutoConfiguration
org.springframework.boot.autoconfigure.data.r2dbc.R2dbcRepositoriesAutoConfiguration
org.springframework.boot.autoconfigure.data.redis.RedisAutoConfiguration
org.springframework.boot.autoconfigure.data.redis.RedisReactiveAutoConfiguration
org.springframework.boot.autoconfigure.data.redis.RedisRepositoriesAutoConfiguration
org.springframework.boot.autoconfigure.data.rest.RepositoryRestMvcAutoConfiguration
org.springframework.boot.autoconfigure.data.web.SpringDataWebAutoConfiguration
org.springframework.boot.autoconfigure.elasticsearch.ElasticsearchRestClientAutoConfiguration
org.springframework.boot.autoconfigure.flyway.FlywayAutoConfiguration
org.springframework.boot.autoconfigure.freemarker.FreeMarkerAutoConfiguration
org.springframework.boot.autoconfigure.graphql.GraphQlAutoConfiguration
org.springframework.boot.autoconfigure.graphql.data.GraphQlReactiveQueryByExampleAutoConfiguration
org.springframework.boot.autoconfigure.graphql.data.GraphQlReactiveQuerydslAutoConfiguration
org.springframework.boot.autoconfigure.graphql.data.GraphQlQueryByExampleAutoConfiguration
org.springframework.boot.autoconfigure.graphql.data.GraphQlQuerydslAutoConfiguration
org.springframework.boot.autoconfigure.graphql.reactive.GraphQlWebFluxAutoConfiguration
org.springframework.boot.autoconfigure.graphql.rsocket.GraphQlRSocketAutoConfiguration
org.springframework.boot.autoconfigure.graphql.rsocket.RSocketGraphQlClientAutoConfiguration
org.springframework.boot.autoconfigure.graphql.security.GraphQlWebFluxSecurityAutoConfiguration
org.springframework.boot.autoconfigure.graphql.security.GraphQlWebMvcSecurityAutoConfiguration
org.springframework.boot.autoconfigure.graphql.servlet.GraphQlWebMvcAutoConfiguration
org.springframework.boot.autoconfigure.groovy.template.GroovyTemplateAutoConfiguration
org.springframework.boot.autoconfigure.gson.GsonAutoConfiguration
org.springframework.boot.autoconfigure.h2.H2ConsoleAutoConfiguration
org.springframework.boot.autoconfigure.hateoas.HypermediaAutoConfiguration
org.springframework.boot.autoconfigure.hazelcast.HazelcastAutoConfiguration
org.springframework.boot.autoconfigure.hazelcast.HazelcastJpaDependencyAutoConfiguration
org.springframework.boot.autoconfigure.http.HttpMessageConvertersAutoConfiguration
org.springframework.boot.autoconfigure.http.codec.CodecsAutoConfiguration
org.springframework.boot.autoconfigure.influx.InfluxDbAutoConfiguration
org.springframework.boot.autoconfigure.info.ProjectInfoAutoConfiguration
org.springframework.boot.autoconfigure.integration.IntegrationAutoConfiguration
org.springframework.boot.autoconfigure.jackson.JacksonAutoConfiguration
org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration
org.springframework.boot.autoconfigure.jdbc.JdbcTemplateAutoConfiguration
org.springframework.boot.autoconfigure.jdbc.JndiDataSourceAutoConfiguration
org.springframework.boot.autoconfigure.jdbc.XADataSourceAutoConfiguration
org.springframework.boot.autoconfigure.jdbc.DataSourceTransactionManagerAutoConfiguration
org.springframework.boot.autoconfigure.jms.JmsAutoConfiguration
org.springframework.boot.autoconfigure.jmx.JmxAutoConfiguration
org.springframework.boot.autoconfigure.jms.JndiConnectionFactoryAutoConfiguration
org.springframework.boot.autoconfigure.jms.activemq.ActiveMQAutoConfiguration
org.springframework.boot.autoconfigure.jms.artemis.ArtemisAutoConfiguration
org.springframework.boot.autoconfigure.jersey.JerseyAutoConfiguration
org.springframework.boot.autoconfigure.jooq.JooqAutoConfiguration
org.springframework.boot.autoconfigure.jsonb.JsonbAutoConfiguration
org.springframework.boot.autoconfigure.kafka.KafkaAutoConfiguration
org.springframework.boot.autoconfigure.availability.ApplicationAvailabilityAutoConfiguration
org.springframework.boot.autoconfigure.ldap.embedded.EmbeddedLdapAutoConfiguration
org.springframework.boot.autoconfigure.ldap.LdapAutoConfiguration
org.springframework.boot.autoconfigure.liquibase.LiquibaseAutoConfiguration
org.springframework.boot.autoconfigure.mail.MailSenderAutoConfiguration
org.springframework.boot.autoconfigure.mail.MailSenderValidatorAutoConfiguration
org.springframework.boot.autoconfigure.mongo.embedded.EmbeddedMongoAutoConfiguration
org.springframework.boot.autoconfigure.mongo.MongoAutoConfiguration
org.springframework.boot.autoconfigure.mongo.MongoReactiveAutoConfiguration
org.springframework.boot.autoconfigure.mustache.MustacheAutoConfiguration
org.springframework.boot.autoconfigure.neo4j.Neo4jAutoConfiguration
org.springframework.boot.autoconfigure.netty.NettyAutoConfiguration
org.springframework.boot.autoconfigure.orm.jpa.HibernateJpaAutoConfiguration
org.springframework.boot.autoconfigure.quartz.QuartzAutoConfiguration
org.springframework.boot.autoconfigure.r2dbc.R2dbcAutoConfiguration
org.springframework.boot.autoconfigure.r2dbc.R2dbcTransactionManagerAutoConfiguration
org.springframework.boot.autoconfigure.rsocket.RSocketMessagingAutoConfiguration
org.springframework.boot.autoconfigure.rsocket.RSocketRequesterAutoConfiguration
org.springframework.boot.autoconfigure.rsocket.RSocketServerAutoConfiguration
org.springframework.boot.autoconfigure.rsocket.RSocketStrategiesAutoConfiguration
org.springframework.boot.autoconfigure.security.servlet.SecurityAutoConfiguration
org.springframework.boot.autoconfigure.security.servlet.UserDetailsServiceAutoConfiguration
org.springframework.boot.autoconfigure.security.servlet.SecurityFilterAutoConfiguration
org.springframework.boot.autoconfigure.security.reactive.ReactiveSecurityAutoConfiguration
org.springframework.boot.autoconfigure.security.reactive.ReactiveUserDetailsServiceAutoConfiguration
org.springframework.boot.autoconfigure.security.rsocket.RSocketSecurityAutoConfiguration
org.springframework.boot.autoconfigure.security.saml2.Saml2RelyingPartyAutoConfiguration
org.springframework.boot.autoconfigure.sendgrid.SendGridAutoConfiguration
org.springframework.boot.autoconfigure.session.SessionAutoConfiguration
org.springframework.boot.autoconfigure.security.oauth2.client.servlet.OAuth2ClientAutoConfiguration
org.springframework.boot.autoconfigure.security.oauth2.client.reactive.ReactiveOAuth2ClientAutoConfiguration
org.springframework.boot.autoconfigure.security.oauth2.resource.servlet.OAuth2ResourceServerAutoConfiguration
org.springframework.boot.autoconfigure.security.oauth2.resource.reactive.ReactiveOAuth2ResourceServerAutoConfiguration
org.springframework.boot.autoconfigure.solr.SolrAutoConfiguration
org.springframework.boot.autoconfigure.sql.init.SqlInitializationAutoConfiguration
org.springframework.boot.autoconfigure.task.TaskExecutionAutoConfiguration
org.springframework.boot.autoconfigure.task.TaskSchedulingAutoConfiguration
org.springframework.boot.autoconfigure.thymeleaf.ThymeleafAutoConfiguration
org.springframework.boot.autoconfigure.transaction.TransactionAutoConfiguration
org.springframework.boot.autoconfigure.transaction.jta.JtaAutoConfiguration
org.springframework.boot.autoconfigure.validation.ValidationAutoConfiguration
org.springframework.boot.autoconfigure.web.client.RestTemplateAutoConfiguration
org.springframework.boot.autoconfigure.web.embedded.EmbeddedWebServerFactoryCustomizerAutoConfiguration
org.springframework.boot.autoconfigure.web.reactive.HttpHandlerAutoConfiguration
org.springframework.boot.autoconfigure.web.reactive.ReactiveMultipartAutoConfiguration
org.springframework.boot.autoconfigure.web.reactive.ReactiveWebServerFactoryAutoConfiguration
org.springframework.boot.autoconfigure.web.reactive.WebFluxAutoConfiguration
org.springframework.boot.autoconfigure.web.reactive.WebSessionIdResolverAutoConfiguration
org.springframework.boot.autoconfigure.web.reactive.error.ErrorWebFluxAutoConfiguration
org.springframework.boot.autoconfigure.web.reactive.function.client.ClientHttpConnectorAutoConfiguration
org.springframework.boot.autoconfigure.web.reactive.function.client.WebClientAutoConfiguration
org.springframework.boot.autoconfigure.web.servlet.DispatcherServletAutoConfiguration
org.springframework.boot.autoconfigure.web.servlet.ServletWebServerFactoryAutoConfiguration
org.springframework.boot.autoconfigure.web.servlet.error.ErrorMvcAutoConfiguration
org.springframework.boot.autoconfigure.web.servlet.HttpEncodingAutoConfiguration
org.springframework.boot.autoconfigure.web.servlet.MultipartAutoConfiguration
org.springframework.boot.autoconfigure.web.servlet.WebMvcAutoConfiguration
org.springframework.boot.autoconfigure.websocket.reactive.WebSocketReactiveAutoConfiguration
org.springframework.boot.autoconfigure.websocket.servlet.WebSocketServletAutoConfiguration
org.springframework.boot.autoconfigure.websocket.servlet.WebSocketMessagingAutoConfiguration
org.springframework.boot.autoconfigure.webservices.WebServicesAutoConfiguration
org.springframework.boot.autoconfigure.webservices.client.WebServiceTemplateAutoConfiguration
</details>



##### 3.2 按需开启自动配置项

虽然我们144个场景的所有自动配置启动的时候默认全部加载。xxxxAutoConfiguration
按照条件装配规则（@Conditional），最终会按需配置。



##### 3.3 修改默认配置



```java
    @Bean
	@ConditionalOnBean(MultipartResolver.class)  //容器中有这个类型组件
	@ConditionalOnMissingBean(name = {"multipartResolver"}) //容器中没有这个名字 multipartResolver 的组件
	public MultipartResolver multipartResolver(MultipartResolver resolver) {
        //给@Bean标注的方法传入了对象参数，这个参数的值就会从容器中找。
        //SpringMVC multipartResolver。防止有些用户配置的文件上传解析器不符合规范
		// Detect if the user has created a MultipartResolver but named it incorrectly
		return resolver;
	}
	//给容器中加入了文件上传解析器；
```


SpringBoot默认会在底层配好所有的组件。但是如果用户自己配置了以用户的优先

```java
@Bean
	@ConditionalOnMissingBean
	public CharacterEncodingFilter characterEncodingFilter() {
    }
```



总结：

- SpringBoot先加载所有的自动配置类  xxxxxAutoConfiguration
- 每个自动配置类按照条件进行生效，默认都会绑定配置文件指定的值。xxxxProperties里面拿。xxxProperties和配置文件进行了绑定
- 生效的配置类就会给容器中装配很多组件
- 只要容器中有这些组件，相当于这些功能就有了
- 定制化配置

- - 用户直接自己@Bean替换底层的组件
  - 用户去看这个组件是获取的配置文件什么值就去修改。

xxxxxAutoConfiguration ---> 组件  ---> xxxxProperties里面拿值  ----> application.properties



##### 3.4 最佳实践

​	1.引入场景依赖

https://docs.spring.io/spring-boot/docs/current/reference/html/using.html#using.build-systems.starters

​	2.查看自动配置了哪些（选做）

​		1）自己分析，引入场景对应的自动配置一般都生效了
​		2）配置文件中debug=true开启自动配置报告。Negative（不生效）\Positive（生效）

​	3.是否需要修改

​		1）参照文档修改配置项：
​			①https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#appendix.application-properties
​			②自己分析。xxxxProperties绑定了配置文件的哪些。

​		2）自定义加入或者替换组件
​			@Bean、@Component。。。

​	4.自定义器  **XXXXXCustomizer**；

​	...



#### 4.开发小技巧

##### 4.1 Lombok

简化JavaBean开发

1.引入lombok依赖

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
</dependency>
```

2.idea中搜索安装lombok插件

3.使用即可
	@Data：是lombok的注解，帮我们生成已有属性的getter、setter方法
	@ToString：在编译该类时，自动生成ToString
	@AllArgsConstructor：全参构造器
	@NoArgsConstructor：无参构造器
	@EqualsAndHashCode：重写Equals和HashCode的方法
	@Slf4j：注入日志类



##### 4.2 dev-tools

热更新：项目或者页面修改以后：Ctrl+F9；

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <optional>true</optional>
</dependency>
```



##### 4.3 Spring Initailizr（项目初始化向导）

1.创建项目时，选择Spring Initailizr，这样创建的时候可以选择我们需要的开发场景
2.项目创建好之后依赖自动引入了，并且已经创建好项目结构，也自动编写好主配置类

![image-20220820115204457](D:\Typora\images\image-20220820115204457.png)

![image-20220820132754698](D:\Typora\images\image-20220820132754698.png)

![image-20220820132833330](D:\Typora\images\image-20220820132833330.png)

![image-20220820132904345](D:\Typora\images\image-20220820132904345.png)







## SpringBoot2核心技术-核心功能



### 一.配置文件

#### 1.文件类型

1.1 properties

同以前的properties用法



1.2 yaml

​	1.2.1 简介
​	YAML 是 "YAML Ain't Markup Language"（YAML 不是一种标记语言）的递归缩写。在开发的这种语言时，YAML 的意思其实是："Yet Another Markup Language"（仍是一种标记语言）。 被戏称为薛定谔的YAML

非常适合用来做以数据为中心的配置文件

​	

​	1.2.2 基本语法

​	key: value；kv之间有空格（冒号后边有个空格）
​	大小写敏感
​	使用缩进表示层级关系
​	缩进不允许使用tab，只允许空格
​	缩进的空格数不重要，只要相同层级的元素左对齐即可
​	'#'表示注释
​	字符串无需加引号，如果要加，''与""表示字符串内容 会被 转义/不转义



​	1.2.3 数据类型

​	字面量：单个的、不可再分的值。date、boolean、string、number、null

```yaml
k: v
```

​	对象：键值对的集合。map、hash、set、object 

```yaml
行内写法：  k: {k1:v1,k2:v2,k3:v3}
#或
k: 
	k1: v1
  k2: v2
  k3: v3
```

​	数组：一组按次序排列的值。array、list、queue

```yaml
行内写法：  k: [v1,v2,v3]
#或者
k:
 - v1
 - v2
 - v3
```



​	1.2.4 示例

像创建两个类：Person和Pet

```java
@ConfigurationProperties(prefix = "person")
@Component
@Data
@ToString
public class Person {
    private String userName;
    private Boolean boss;
    private Date birth;
    private Integer age;
    private Pet pet;
    private String[] interests;
    private List<String> animal;
    private Map<String, Object> score;
    private Set<Double> salarys;
    private Map<String, List<Pet>> allPets;
}
```

```java
@Data
@ToString
public class Pet {
    private String name;
    private Double weight;
}
```

在yaml配置文件上表示以上对象：

```yml
person:
  #单引号会将\n作为字符串输出   双引号会将\n作为换行输入
  #双引号不会转义，单引号会转义（\n代表转义，单引号会将其在转义一遍，相当于没转义）
  #userName: 'zhangsan'
  userName: zhangsan
  boss: true
  birth: 2019/12/9
  age: 20
#  interests: [篮球,足球]
  interests:  #数组表示法
    - 篮球
    - 足球
  animal: [阿猫,阿狗]   #数组表示法2
#  score:
#    english: 80
#    math: 90
  score: {english: 80,math: 90}   #对象表示法
  salarys:
    - 9999.98
    - 9999.99
  pet:
    name: 阿狗
    weight: 30
  allPets:
    sick:
      - {name: 阿狗,weight: 30}
      - name: 阿猫    #对象表示法2
        weight: 20
      - name: 阿虫
        weight: 10
    health:
      - {name: 阿花,weight: 100}
      - {name: 阿明,weight: 110}
```



未来写配置首选yaml



#### 2.配置提示

自定义的类和配置文件绑定一般没有提示。

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
    <optional>true</optional>
</dependency>
```





### 二.Web开发



![image-20220821102534134](D:\Typora\images\image-20220821102534134.png)



#### 1.SpringMVC自动配置概览

​	摘抄自官方文档：https://docs.spring.io/spring-boot/docs/current/reference/html/web.html#web.servlet.spring-mvc.auto-configuration

Spring Boot provides auto-configuration for Spring MVC that works well with most applications.
	Spring Boot为Spring MVC提供了自动配置，适用于大多数应用程序。(大多场景我们都无需自定义配置)

The auto-configuration adds the following features on top of Spring’s defaults:
	自动配置在Spring的默认值之上添加了以下功能：

- Inclusion of `ContentNegotiatingViewResolver` and `BeanNameViewResolver` beans.
  内容协商视图解析器和BeanName视图解析器
- Support for serving static resources, including support for WebJars (covered [later in this document](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#web.servlet.spring-mvc.static-content)).
  静态资源（包括webjars）
- Automatic registration of `Converter`, `GenericConverter`, and `Formatter` beans.
  自动注册 Converter，GenericConverter，Formatter 
- Support for `HttpMessageConverters` (covered [later in this document](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#web.servlet.spring-mvc.message-converters)).
  支持 `HttpMessageConverters` （后来我们配合内容协商理解原理）
- Automatic registration of `MessageCodesResolver` (covered [later in this document](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#web.servlet.spring-mvc.message-codes)).
  自动注册 `MessageCodesResolver` （国际化用）
- Static `index.html` support.
  静态index.html 页支持
- Automatic use of a `ConfigurableWebBindingInitializer` bean (covered [later in this document](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#web.servlet.spring-mvc.binding-initializer)).
  自动使用 `ConfigurableWebBindingInitializer` ，（DataBinder负责将请求数据绑定到JavaBean上）

If you want to keep those Spring Boot MVC customizations and make more [MVC customizations](https://docs.spring.io/spring-framework/docs/5.3.22/reference/html/web.html#mvc) (interceptors, formatters, view controllers, and other features), you can add your own `@Configuration` class of type `WebMvcConfigurer` but **without** `@EnableWebMvc`.
不用@EnableWebMvc注解。使用 `@Configuration` **+** `WebMvcConfigurer` 自定义规则

If you want to provide custom instances of `RequestMappingHandlerMapping`, `RequestMappingHandlerAdapter`, or `ExceptionHandlerExceptionResolver`, and still keep the Spring Boot MVC customizations, you can declare a bean of type `WebMvcRegistrations` and use it to provide custom instances of those components.
声明 `WebMvcRegistrations` 改变默认底层组件

If you want to take complete control of Spring MVC, you can add your own `@Configuration` annotated with `@EnableWebMvc`, or alternatively add your own `@Configuration`-annotated `DelegatingWebMvcConfiguration` as described in the Javadoc of `@EnableWebMvc`.
使用 `@EnableWebMvc+@Configuration+DelegatingWebMvcConfiguration 全面接管SpringMVC`



#### 2.简单功能分析

##### 2.1 静态资源访问

2.1.1 静态资源目录

只要静态资源放在类路径下：`/static` (or `/public` or `/resources` or `/META-INF/resources`)

访问 ： 当前项目根路径/ + 静态资源名 

原理： 静态映射/**。
请求进来，先去找Controller看能不能处理。不能处理的所有请求又都交给静态资源处理器。静态资源也找不到则响应404页面

改变默认的静态资源路径

```yml
spring:
  web:
    resources:
      static-locations: classpath:/haha/
```



摘抄自官方文档：https://docs.spring.io/spring-boot/docs/current/reference/html/web.html#web.servlet.spring-mvc.static-content



2.1.2 静态资源访问前缀

默认是无前缀

```yaml
spring:
  mvc:
    static-path-pattern: "/res/**"
```

当前项目 + static-path-pattern + 静态资源名 = 静态资源文件夹下找



2.1.3 webjar

自动映射 /[webjars](http://localhost:8080/webjars/jquery/3.5.1/jquery.js)/**



##### 2.2 欢迎页支持

静态资源路径下  index.html
	可以配置静态资源路径
	但是不可以配置静态资源的访问前缀。否则导致 index.html不能被默认访问

```yml
spring:
#  mvc:
#    static-path-pattern: "/res/**"   #欢迎页不能设置访问前缀，否则访问不到。会导致welcome page功能失效
  web:
    resources:
      static-locations: classpath:/haha/
```

controller能处理/index

参考官方文档：https://docs.spring.io/spring-boot/docs/current/reference/html/web.html#web.servlet.spring-mvc.welcome-page



##### 2.3 自定义 `Favicon`

设置小图标

favicon.ico 放在静态资源目录下即可。

```
spring:
#  mvc:
#    static-path-pattern: "/res/**"   #这个会导致 Favicon 功能失效
```



参考官方文档：https://docs.spring.io/spring-boot/docs/current/reference/html/web.html#web.servlet.spring-mvc.favicon



##### 2.4 静态资源配置原理

SpringBoot启动默认加载  xxxAutoConfiguration 类（自动配置类）

SpringMVC功能的自动配置类 WebMvcAutoConfiguration，生效
（在Maven:org.springframework.boot:spring-boot-autoconfigure:2.7.2/spring-boot-autoconfigure-2.7.2.jar/org/springframework/boot/autoconfigure/web/servlet/WebMvcAutoConfiguration）

```java
@AutoConfiguration(
    after = {DispatcherServletAutoConfiguration.class, TaskExecutionAutoConfiguration.class, ValidationAutoConfiguration.class}
)
@ConditionalOnWebApplication(
    type = Type.SERVLET
)
@ConditionalOnClass({Servlet.class, DispatcherServlet.class, WebMvcConfigurer.class})
@ConditionalOnMissingBean({WebMvcConfigurationSupport.class})
@AutoConfigureOrder(-2147483638)
public class WebMvcAutoConfiguration {
    ...
}
```



给容器中配了什么。

```java
@Configuration(
    proxyBeanMethods = false
)
@Import({WebMvcAutoConfiguration.EnableWebMvcConfiguration.class})
@EnableConfigurationProperties({WebMvcProperties.class, WebProperties.class})
@Order(0)
public static class WebMvcAutoConfigurationAdapter implements WebMvcConfigurer, ServletContextAware {...}
```

配置文件的相关属性和xxx进行了绑定。WebMvcProperties==**spring.mvc**、ResourceProperties==**spring.resources******



2.4.1 配置类只有一个有参构造器

有参构造器所有参数的值都会从容器中确定

```java
public WebMvcAutoConfigurationAdapter(WebProperties webProperties, WebMvcProperties mvcProperties, ListableBeanFactory beanFactory, ObjectProvider<HttpMessageConverters> messageConvertersProvider, ObjectProvider<WebMvcAutoConfiguration.ResourceHandlerRegistrationCustomizer> resourceHandlerRegistrationCustomizerProvider, ObjectProvider<DispatcherServletPath> dispatcherServletPath, ObjectProvider<ServletRegistrationBean<?>> servletRegistrations) {
    this.resourceProperties = webProperties.getResources();
    this.mvcProperties = mvcProperties;
    this.beanFactory = beanFactory;
    this.messageConvertersProvider = messageConvertersProvider;
    this.resourceHandlerRegistrationCustomizer = (WebMvcAutoConfiguration.ResourceHandlerRegistrationCustomizer)resourceHandlerRegistrationCustomizerProvider.getIfAvailable();
    this.dispatcherServletPath = dispatcherServletPath;
    this.servletRegistrations = servletRegistrations;
    this.mvcProperties.checkConfiguration();
}
```

ResourceProperties resourceProperties：获取和spring.resources绑定的所有的值的对象
WebMvcProperties mvcProperties：获取和spring.mvc绑定的所有的值的对象
ListableBeanFactory beanFactory Spring的beanFactory
HttpMessageConverters：找到所有的HttpMessageConverters
ResourceHandlerRegistrationCustomizer：找到 资源处理器的自定义器。=========
DispatcherServletPath
ServletRegistrationBean：给应用注册Servlet、Filter....



2.4.2 资源处理的默认规则

```java
public void addResourceHandlers(ResourceHandlerRegistry registry) {
    if (!this.resourceProperties.isAddMappings()) {
        logger.debug("Default resource handling disabled");
    } else {
        this.addResourceHandler(registry, "/webjars/**", "classpath:/META-INF/resources/webjars/");
        this.addResourceHandler(registry, this.mvcProperties.getStaticPathPattern(), (registration) -> {
            registration.addResourceLocations(this.resourceProperties.getStaticLocations());
            if (this.servletContext != null) {
                ServletContextResource resource = new ServletContextResource(this.servletContext, "/");
                registration.addResourceLocations(new Resource[]{resource});
            }

        });
    }
}
```

```yml
spring:
#  mvc:
#    static-path-pattern: /res/**

  resources:
    add-mappings: false   禁用所有静态资源规则
```



2.4.3 欢迎页的处理规则

HandlerMapping：处理器映射。保存了每一个Handler能处理哪些请求。	

```java
@Bean
public WelcomePageHandlerMapping welcomePageHandlerMapping(ApplicationContext applicationContext, FormattingConversionService mvcConversionService, ResourceUrlProvider mvcResourceUrlProvider) {
    WelcomePageHandlerMapping welcomePageHandlerMapping = new WelcomePageHandlerMapping(new TemplateAvailabilityProviders(applicationContext), applicationContext, this.getWelcomePage(), this.mvcProperties.getStaticPathPattern());
    welcomePageHandlerMapping.setInterceptors(this.getInterceptors(mvcConversionService, mvcResourceUrlProvider));
    welcomePageHandlerMapping.setCorsConfigurations(this.getCorsConfigurations());
    return welcomePageHandlerMapping;
}
```

```java
WelcomePageHandlerMapping(TemplateAvailabilityProviders templateAvailabilityProviders, ApplicationContext applicationContext, Resource welcomePage, String staticPathPattern) {
    if (welcomePage != null && "/**".equals(staticPathPattern)) {
        //要用欢迎页功能，必须是/**
        logger.info("Adding welcome page: " + welcomePage);
        this.setRootViewName("forward:index.html");
    } else if (this.welcomeTemplateExists(templateAvailabilityProviders, applicationContext)) {
        // 调用Controller  /index
        logger.info("Adding welcome page template: index");
        this.setRootViewName("index");
    }

}
```



2.4.4 favicon

/favicon.ico



#### 3.请求参数处理

##### 3.1 请求映射

3.1.1 rest使用与原理



P26











































