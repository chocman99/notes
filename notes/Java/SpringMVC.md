### SpringMVC简介



#### 一.什么是MVC

MVC是一种软件架构的思想，将软件按照模型、视图、控制器来划分

M：Model，模型层，指工程中的JavaBean，作用是处理数据
		JavaBean分为两类：
				一类称为实体类Bean：专门存储业务数据的，如Student、User等
				一类称为业务处理Bean：指Service或Dao对象，专门用于处理业务逻辑和数据访问

V：View，视图层，指工程中的html或jsp等页面，作用是与用户进行交互，展示数据

C：Controller，控制层，指工程中的servlet，作用是接收请求和响应浏览器

MVC的工作流程：
		用户通过视图层发送请求到服务器，在服务器中请求被Controller，Controller调用相应的Model层处理请求，处理完毕将结果返回到Controller，Controller再根据请求处理的结果找到相应的View视图，渲染数据后最终响应给浏览器



#### 二.什么是SpringMVC

SpringMVC是spring的一个后续产品，是Spring的一个子项目

SpringMVC是Spring为表述层开发提供的一整套完备的解决方案。在表述层框架经历Strust、WebWork、Strust2等诸多产品的历经迭代之后，目前业界普遍选择了SpringMVC作为JavaEE项目表述层开发的首选方案。

注：三层架构分别为表述层（或表示层）、业务逻辑层、数据访问层。表述层表示前台页面和后台servlet



#### 三.SpringMVC的特点

Spring家族原生产品，与IOC容器等基础设施无缝对接
基于原生的Servlet，通过了功能强大的前端控制器DispatcherServlet，对请求和响应进行统一处理
表述层各细分领域需要解决的问题全方位覆盖，提供全面解决方案
代码清新简洁，大幅度提升开发效率
内部组件化程度高，可插拔式组件即插即用，想要什么功能配置相应组件即可
性能卓越，尤其适合现代大型，超大型互联网项目要求





### HelloWorld



#### 一.开发环境

目前用的是：
		IDE：idea 2021.2.2
		构建工具：maven 3.8.4
		服务器：tomcat 10.0.17
		Spring版本：5.3.19



#### 二.创建maven工程

1.添加web模块
2.打包方式：war
3.引入依赖

```xml
<dependencies>

        <!--SpringMVC-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.3.15</version>
        </dependency>

        <!--日志-->
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>1.2.10</version>
        </dependency>

        <!--ServletAPI-->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>4.0.1</version>
            <scope>provided</scope>
        </dependency>

        <!--Spring5和Thymeleaf整合包-->
        <dependency>
            <groupId>org.thymeleaf</groupId>
            <artifactId>thymeleaf-spring5</artifactId>
            <version>3.0.15.RELEASE</version>
        </dependency>

    </dependencies>
```



#### 三.配置web.xml

注册SpringMVC的前端控制器DispatcherServlet

1.默认配置方式（默认：SpringMVC配置文件位置默认，名称默认）

​		此配置作用下，SpringMVC的配置文件默认位于WEB-INF下，默认名称为`<servlet-name>`-servlet.xml，例如，以下配置所对应的SpringMVC的配置文件 位于WEB-INF下，文件名为springMVC-servlet.xml

```xml
<!--配置SpringMVC的前端控制器，对浏览器发送的请求进行统一处理-->
<servlet>
    <servlet-name>SpringMVC</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>SpringMVC</servlet-name>
    <!--设置springMVC的核心控制器所能处理的请求的请求路径
        /所匹配的请求可以是/login或.html或.js或.css方式的请求路径
        但是/不能匹配.jsp请求路径的请求
    -->
    <url-pattern>/</url-pattern>
</servlet-mapping>
```

2.扩展配置方式（推荐）

​		可通过init-param标签设置SpringMVC配置文件的位置和名称，通过load-on-startup标签设置SpringMVC前端控制器DispatcherServlet的初始空间

```xml
<servlet>
    <servlet-name>SpringMVC</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>

    <!--配置SpringMVC配置文件的位置和名称-->
    <init-param>
        <param-name>contextConfigLocation</param-name>  <!--contextConfigLocation为固定值-->
        <param-value>classpath:springMVC.xml</param-value>  <!--使用classpath:表示从路径查找配置文件，例如maven工程中的src/main/resources-->
    </init-param>

    <!--将前端控制器DiapatcherServlet的初始化时间提前到服务器启动时
        作为框架的核心组件，在启动过程中有大量的初始化操作要做，而这些操作放在第一次请求时才执行会严重影响访问速度，因此需要通过此标签将启动控制DispatcherServlet的初始化时间提前到服务器启动时
    -->
    <load-on-startup>1</load-on-startup>

</servlet>
<servlet-mapping>
    <servlet-name>SpringMVC</servlet-name>
    <!--设置springMVC的核心控制器所能处理的请求的请求路径
        /所匹配的请求可以是/login或.html或.js或.css方式的请求路径
        但是/不能匹配.jsp请求路径的请求
    -->
    <url-pattern>/</url-pattern>
</servlet-mapping>
```



#### 四.创建请求控制器

由于前端控制器对浏览器发送的请求进行了统一的处理，但是具体的请求有不同的处理过程，因此需要创建处理具体请求的类，即请求控制器

请求控制器中每一个处理请求的方法成为控制器方法

因为SpringMVC的控制器由一个POJO（普通的Java类）担任，因此需要通过@Controller注解将其标识为一个控制层组件，交给Spring的IOC容器管理，此时SpringMVC才能够识别控制器的存在

```java
@Controller
public class HelloController {
}
```



#### 五.创建springMVC的配置

```xml
<!--扫描组件-->
<context:component-scan base-package="com.yc.mvc.controller"></context:component-scan>

<!-- 配置Thymeleaf视图解析器 -->
<bean id="viewResolver" class="org.thymeleaf.spring5.view.ThymeleafViewResolver">
    <property name="order" value="1"/>
    <property name="characterEncoding" value="UTF-8"/>
    <property name="templateEngine">
        <bean class="org.thymeleaf.spring5.SpringTemplateEngine">
            <property name="templateResolver">
                <bean class="org.thymeleaf.spring5.templateresolver.SpringResourceTemplateResolver">

                    <!-- 视图前缀 -->
                    <property name="prefix" value="/WEB-INF/templates/"/>

                    <!-- 视图后缀 -->
                    <property name="suffix" value=".html"/>

                    <property name="templateMode" value="HTML5"/>
                    <property name="characterEncoding" value="UTF-8" />
                </bean>
            </property>
        </bean>
    </property>
</bean>
```



#### 六.测试HelloWorld

1.实现对首页的访问（Tomcat10启动报404，换成8可以启动）

在请求控制器中创建处理请求的方法

```java
@Controller
public class HelloController {

    //"/"-->/WEB-INF/templates/index.html

    //方法名无所谓
    //@RequestMapping注解：处理请求和控制器方法之间的映射关系
    //@RequestMapping注解的value属性可以通过请求地址匹配请求，/表示的当前工程的上下文路径。localhost:8080/springMVC/
    @RequestMapping(value ="/")     //只有value一个值的时候，可以省略不写value，直接@RequestMapping("/")
    public String index(){
        //返回视图名称
        return "index";
    }
}
```

2.通过超链接跳转到指定页面

在主页index.html中设置超链接

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
    <head>
        <meta charset="UTF-8">
        <title>首页</title>
    </head>
    <body>
        <h1>首页</h1>
        <a th:href="@{/target}">访问目标页面target.html</a>
    </body>
</html>
```

在请求控制器中创建处理请求的方法

```java
//当前注解value属性值要和当前的请求地址保持一致
@RequestMapping("/target")
public String target(){
    return "target";
}
```



#### 七.总结

浏览器发送请求，若请求地址符合前端控制器的url-pattern，该请求就会被前端控制器DispatcherServlet处理。前端控制器会读取SpringMVC的核心配置文件，通过扫描组件找到控制器，将请求地址和控制器中@RequestMapping注解的value属性值进行匹配，若匹配成功，该注解所标识的控制器方法就是处理请求的方法。处理请求的方法需要返回一个字符串类型的视图名称，该视图名称会被视图解析器解析，加上前缀和后缀组成视图的路径，通过Thymeleaf对视图进行渲染，最终转发到视图所对应页面





### @RequestMapping注解



#### 一.@RequestMapping注解的功能

​		从注解的名称上我们可以看到，@RequestMapping注解的作用就是将请求和处理请求的控制器关联起来，建立映射关系。
​		SpringMVC接收到指定的请求，就会来找到在映射关系中对应的控制器方法来处理这个请求

​		控制器中不能有多个方法响应同一个请求的情况



#### 二.@RequestMapping注解的位置

@RequestMapping标识一个类：设置映射请求的请求路径的初始信息

@RequestMapping标识一个方法：设置映射请求的请求路径的具体信息



#### 三.@RequestMapping注解的value属性

@RequestMapping注解的value属性通过请求的请求地址匹配请求映射

@RequestMapping注解的value属性是一个字符串类型的数组，表示该请求映射能够匹配多个请求地址所对应的请求

@RequestMapping注解的value属性必须设置，至少通过请求地址匹配请求映射

（注：若没有与value匹配，报404；如果两个请求的value值一样，那么它们的method一定不能一样）

```html
<a th:href="@{/hello/testRequestMapping}">测试RequestMapping注解的value属性</a><br>
<a th:href="@{/hello/test}">测试RequestMapping注解的value属性</a><br>
```

```java
@RequestMapping(value = {"/testRequestMapping" , "/test"})
public String success(){
    return "success";
}
```



#### 四.@RequestMapping注解的method属性

@RequestMapping注解的method属性通过请求的请求方式（get或post）匹配请求映射

@RequestMapping注解的method属性是一个RequestMethod类型的数组，表示该请求映射能够匹配多种请求方式的请求

若当前请求的请求地址满足请求映射的value属性，但是请求方式不满足method属性，则浏览器报错405：Request Method ‘post’ not supported

（注：若没有与method匹配，报405）

```html
<a th:href="@{/hello/test}">测试RequestMapping注解的mathod属性-->GET</a><br>
<form th:action="@{/hello/test}" method="post">
    <input type="submit" value="测试RequestMapping注解的method属性-->POST">
</form>
```

```java
@RequestMapping(value = {"/testRequestMapping" , "/test"},
                method = {RequestMethod.GET,RequestMethod.POST})
public String success(){
    return "success";
}
```

注：
		1.对于处理指定请求方式的控制器方法，SpringMVC中提供了@RequestMapping的派生注解
				处理get请求的映射-->@GetMapping
				处理post请求的映射-->@PostMapping
				处理put请求的映射-->@PutMapping
				处理delete请求的映射-->@DeleteMapping

​		2.常用的请求方式有get，post，put，delete
​		但是目前浏览器只支持get和post，若在form表单提交时，为method设置了其他请求方式的字符串（put或delete），则按照默认的请求方式get处理
​		若要发送put和delete请求，则需要通过spring提供的过滤器HiddenHttpMethodFilter，在restful部分会讲到



#### 五.@RequestMapping注解的params属性（了解）

@RequestMapping注解的params属性通过请求的参数匹配请求映射

@RequestMapping注解的params属性是一个字符串类型的数组，可以通过四种表达式设置请求参数和请求映射的匹配关系

"param"：要求请求映射所匹配的请求必须携带param请求参数
"!param"：要求请求映射所匹配的请求必须不能携带param请求参数
"param=value"：要求请求映射所匹配的请求必须携带param请求参数且param=value
"param!=value"：要求请求映射所匹配的请求必须携带param请求参数且param!=value

（注：value和method类型也是数组，设置多个值，只要满足一个就能找到其中的请求映射。但params和headers设置多个值，必须同时满足才行。若当前请求满足@RequestMapping注解的value和method属性，但是不满足params属性，此时页面回报错400）

```html
<a th:href="@{/hello/testParamsAndHeaders?(username=admin,password=123456)}">测试RequestMapping注解的params属性-->/testParamsAndHeaders</a><br>
```

```java
@RequestMapping(
        value = {"/testParamsAndHeaders" , "/test"},
        params = {"username","password!=123456"}
)
public String testParamsAndHeaders(){
    return "success";
}
```



#### 六.@RequestMapping注解的headers属性（了解）

@RequestMapping注解的headers属性通过请求的请求头匹配请求映射

@RequestMapping注解的headers属性是一个字符串类型的数组，可以通过四种表达式设置请求头信息和请求映射的匹配关系

"header"：要求请求映射所匹配的请求必须携带header请求头信息
"!header"：要求请求映射所匹配的请求必须不能携带header请求头信息
"header=value"：要求请求映射所匹配的请求必须携带header请求头信息且header=value
"header!=value"：要求请求映射所匹配的请求必须携带header请求头信息且header!=value

（注：value和method类型也是数组，设置多个值，只要满足一个就能找到其中的请求映射。但params和headers设置多个值，必须同时满足才行。若当前请求满足@RequestMapping注解的value和method属性，但是不满足headers属性，此时页面显示404）



#### 七.SpringMVC支持ant风格的路径

?：表示任意的单个字符（不能是空，必须有一个，有且只有一个。/和?关键字不能使用）
*：表示任意的0个或多个字符（/和?关键字不能使用）
**：表示任意的一层或多层目录

注意：在使用\**时，只能使用/**/xxx的方式

```html
<a th:href="@{/hello/a1a/testAnt}">测试@RequestMapping可以匹配ant风格的路径-->使用?</a><br>
<a th:href="@{/hello/a1a/testAnt}">测试@RequestMapping可以匹配ant风格的路径-->使用*</a><br>
<a th:href="@{/hello/a1a/testAnt}">测试@RequestMapping可以匹配ant风格的路径-->使用**</a><br>
```

```java
//    @RequestMapping("/a?a/testAnt")
//    @RequestMapping("/a*a/testAnt")
    @RequestMapping("/**/testAnt")
    public String testAnt(){
        return "success";
    }
```



#### 八.SpringMVC支持路径中的占位符（重点）

原始方式：/deleteUser?id=1
rest方式：/deleteUser/1

SpringMVC路径中的占位符常用于restful风格中，当请求路径中将某些数据通过路径的方式传输到服务器中，就可以在相应的@RequestMapping注解的value属性中通过占位符（xxx）表示传输的数据，在通过@PathVariable注解，将占位符所表示的数据赋值给控制器方法的形参

（注：路径中有占位符，那么匹配的请求地址中，也必须要有这一层路径，不能为空）

```html
<a th:href="@{/hello/testPath/1/admin}">测试@RequestMapping支持路径中的占位符-->/testPath</a><br>
```

```java
@RequestMapping("/testPath/{id}/{username}")
public String testPath(@PathVariable("id")Integer id,@PathVariable("username")String username){
    System.out.println("id:" + id + "，" + "username:" + username);
    return "success";
}

//最终输出的内容为-->id:1，username:admin
```





### SpringMVC获取请求参数



#### 一.通过ServletAPI获取

将HttpServletRequest作为控制器方法的形参，此时HttpServletRequest类型的参数表示封装了当前请求的请求报文的对象

```java
@RequestMapping("/testServletAPI")
//形参位置的request表示当前请求
public String testServletAPI(HttpServletRequest request){
    String username = request.getParameter("username");
    String password = request.getParameter("password");
    System.out.println("username:" + username + "," + "password:" + password);
    return "success";
}
```

 

#### 二.通过控制器方法的形参获取请求参数

在控制器方法的形参位置，设置和请求参数同名的形参，当浏览器发送请求，匹配到请求映射时，在DispatcherServlet中就会将请求参数赋值给相应的形参

```html
<a th:href="@{/testParam(username='admin',password=123456)}">测试获取请求参数-->/testParam</a><br>
```

```java
@RequestMapping("/testParam")
public String testParam(String username, String password){
    System.out.println("username:"+username+",password:"+password);
    return "success";
}
```

注：

若请求所传输的请求参数中有多个同名的请求参数，此时可以在控制器方法的形参中设置字符串数组或者字符串类型的形参接收此请求参数

若使用字符串数组类型的形参，此参数的数组中包含了每一个数据

若使用字符串类型的形参，此参数的值为每个数据中间使用逗号拼接的结果

```html
<form th:action="@{/testParam}" method="get">
    用户名：<input type="text" name="username"><br>
    密码：<input type="password" name="password"><br>
    爱好：<input type="checkbox" name="hobby" value="a">a
    <input type="checkbox" name="hobby" value="b">b
    <input type="checkbox" name="hobby" value="c">c<br>
    <input type="submit" value="测试使用控制器形参获取请求参数">
</form>
```

```java
@RequestMapping("/testParam")
//若请求参数中出现多个同名的请求参数，可以在控制器方法的形参位置设置字符串类型或字符串数组来接收此请求参数
//1.当使用字符串类型的形参，最终结果为请求参数的每一个值之间使用逗号进行拼接：
/*
public String testParam(String username,String password,String hobby){
    System.out.println("username:" + username + ",password:" + ",hobby:" + hobby);
    return "success";
}
* */
//2.当使用字符串数组的形参，最终结果为数组里边有当前请求参数所对应的值：
public String testParam(String username,String password,String[] hobby){
    System.out.println("username:" + username + ",password:" + ",hobby:" + Arrays.toString(hobby));
    return "success";
}
```



#### 三.@RequestParam

@RequestParam是将请求参数和控制器方法的形参创建映射关系

@RequestParam注解一共有三个属性：

1.value：指定为形参赋值的请求参数的参数名（当请求参数名和控制器形参的名不一致时，可以建立映射，来获取）

2.required：设置是否必须传输此请求参数，默认值为true
		若设置为true时，则当前请求必须传输value所指定的请求参数，若没有传输该请求参数，且没有设置defaultValue属性，则页面报错400：Required String parameter 'xxx' is not present；若设置为false，则当前请求不是必须传输value所指定的请求参数，若没有传输，则注解所标识的形参的值为null

3.defaultValue：不管required属性值为true或false，当value所指定的请求参数没有传输或传输的值为""（空字符串）时，则使用默认值为形参赋值

以下代码将请求参数username改成user_name

```html
<form th:action="@{/testParam}" method="get">
    用户名：<input type="text" name="user_name"><br>
    密码：<input type="password" name="password"><br>
    爱好：<input type="checkbox" name="hobby" value="a">a
    <input type="checkbox" name="hobby" value="b">b
    <input type="checkbox" name="hobby" value="c">c<br>
    <input type="submit" value="测试使用控制器形参获取请求参数">
</form>
```

```java
@RequestMapping("/testParam")
public String testParam(@RequestParam(value = "user_name",required = false,defaultValue = "hehe") String username,
                        String password,
                        String[] hobby){
    System.out.println("username:" + username + ",password:" + password + ",hobby:" + Arrays.toString(hobby));
    return "success";
}
```



#### 四.@RequestHeader

@RequestHeader是将请求头信息和控制器方法的形参创建映射关系

@RequestHeader注解一共有三个属性：value、required、defaultValue，用法同@RequestParam、



```java
@RequestMapping("/testParam")
public String testParam(@RequestParam(value = "user_name",required = false,defaultValue = "hehe") String username,
                        String password,
                        String[] hobby,
                        @RequestHeader(value = "Host111",required = false,defaultValue = "haha") String host){
    System.out.println("username:" + username + ",password:" + password + ",hobby:" + Arrays.toString(hobby));
    System.out.println("host:" + host);
    return "success";
}
```



#### 五.@CookieValue

@CookieValue是将cookie数据和控制器方法的形参创建映射关系

@CookieValue注解一共有三个属性：value、required、defaultValue，用法同@RequestParam



#### 六.通过实体类型的形参获取请求参数

可以在控制器方法的形参位置设置一个实体类类型的形参，此时若浏览器传输的请求参数的参数名和实体类中的属性名一致，那么请求参数就会为此属性赋值

```html
<form th:action="@{/testBean}" method="post">
    用户名：<input type="text" name="username"><br>
    密码：<input type="password" name="password"><br>
    性别：<input type="radio" name="sex" value="男">男<input type="radio" name="sex" value="女">女<br>
    年龄：<input type="text" name="age"><br>
    邮箱：<input type="text" name="email"><br>
    <input type="submit" value="使用实体类接收请求参数">
</form>
```

要创建个实体类：

```java
public class User {

    private Integer id;
    private String username;
    private String password;
    private String sex;
    private Integer age;
    private String email;

    public User() {
    }

    public User(Integer id, String username, String password, String sex, Integer age, String email) {
        this.id = id;
        this.username = username;
        this.password = password;
        this.sex = sex;
        this.age = age;
        this.email = email;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", password='" + password + '\'' +
                ", sex='" + sex + '\'' +
                ", age=" + age +
                ", email='" + email + '\'' +
                '}';
    }
}
```

```java
@RequestMapping("/testBean")
public String testBean(User user){
    System.out.println(user);
    return "success";
}
```



#### 七.解决获取请求参数的乱码问题

```xml
<!--配置springMVC的编码过滤器-->
<filter>
    <filter-name>CharacterEncodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </init-param>
    <init-param>
        <param-name>forceResponseEncoding</param-name>
        <param-value>true</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>CharacterEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```





### 域对象共享数据



一到六讲的是向request域对象共享数据的五种方法，第一种是servlet原生API提供的，建议使用后四种springMVC提供的



#### 一.使用servletAPI向request域对象共享数据

在控制器方法的形参设置httpservletrequest对象，这个request对象表示了当前的请求。有了request对象就可以使用最原始的方式往域对象中共享数据

注：html中：
		@{}：解析路径
		${}：解析键值

首页html中的跳转

```html
<a th:href="@{/testRequestByServletAPI}">通过servletAPI向request域对象共享数据</a><br>
```

控制器请求

```java
//使用servletAPI向request域对象共享数据
@RequestMapping("/testRequestByServletAPI")
public String testRequestByServletAPI(HttpServletRequest request){
    request.setAttribute("testRequestScope","hello,servletAPI");
    return "success";
}
```

success.html页面中访问域对象中的数据

```html
<p th:text="${testRequestScope}"></p>       <!--这个报错不影响-->
```



#### 二.使用ModelAndView向request域对象共享数据

```java
@RequestMapping("/testModelAndView")
public ModelAndView testModelAndView(){
    /**
     * ModelAndView有Model和View的功能
     * Model主要用于向请求域共享数据
     * View主要用于设置视图，实现页面跳转
     */
    ModelAndView mav = new ModelAndView();
    //处理模型数据，即请求域request共享数据
    mav.addObject("testRequestScope","hello,ModelAndView");
    //设置视图名称
    mav.setViewName("success");
    return mav;
}
```



#### 三.使用Model向request域对象共享数据

Model用的较多

![image-20220628073346202](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220628073346202.png)

```java
@RequestMapping("/testModel")
public String testModel(Model model){
    model.addAttribute("testRequestScope","hello,model");
    return "success";
}
```



#### 四.使用Map向request域对象共享数据

```java
@RequestMapping("/testMap")
public String testMap(Map<String,Object> map){
    map.put("testRequestScope","hello,map");
    return "success";
}
```



#### 五.使用ModelMap向request域对象共享数据

![image-20220628074306545](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220628074306545.png)

```java
@RequestMapping("/testModeMap")
public String testModeMap(ModelMap modelMap){
    modelMap.addAttribute("testRequestScope","hello,ModelMap");
    return "success";
}
```



#### 六.Model、Map、ModelMap之间的关系

Model、ModelMap、Map类型的参数其实本质上都是 BindingAwareModelMap 类型的

源码中的关系：

```java
public interface Model{}
public class ModelMap extends LinkedHashMap<String, Object> {}
public class ExtendedModelMap extends ModelMap implements Model {}
public class BindingAwareModelMap extends ExtendedModelMap {}
```



#### 七.通过servletAPI向session域共享数据

首页html中的跳转

```html
<a th:href="@{/testSession}">通过servletAPI向Session域对象共享数据</a><br>
```

控制器请求

```java
@RequestMapping("/testSession")
public String testSession(HttpSession session){
    session.setAttribute("testSessionScope","hello,session");
    return "success";
}
```

success.html页面中访问域对象中的数据

```html
<p th:text="${session.testSessionScope}"></p>
```



#### 八.通过servletAPI向application域共享数据

实际上就是servletcontext

首页html中的跳转

```html
<a th:href="@{/testApplication}">通过servletAPI向Application域对象共享数据</a><br>
```

控制器请求

```java
@RequestMapping("/testApplication")
public String testApplication(HttpSession session){
    ServletContext application = session.getServletContext();
    application.setAttribute("testApplicationScope","hello,application");
    return "success";
}
```

success.html页面中访问域对象中的数据

```html
<p th:text="${application.testApplication}"></p>
```





### SpringMVC的视图



SpringMVC中的视图时View接口，视图的作用渲染数据，将模型Model中的数据展示给用户

SpringMVC视图的种类很多，默认有转发视图和重定向试图

当工程引入jstl的依赖，转发视图会自动转换为JstlView

若使用的视图技术为Thymeleaf，在SpringMVC的配置文件中配置了Thymeleaf的视图解析器由此视图解析器解析之后所得到的时ThymeleafView



#### 一.ThymeleafView

当控制器方法中所设置的视图名称没有任何前缀时，此时的视图名称会被SpringMVC配置文件中所配置的视图解析器解析，视图名称拼接视图前缀和视图后缀所得到的最终路径，会通过转发的方式实现跳转

```java
    @RequestMapping("/testThymeleafView")
    public String testThymeleafView(){
        return "success";
    }
```

![img002](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/img002.png)



#### 二.转发试图：InternalResourceView

注：
1.控制器中方法的return返回值如果什么都不加，就会被thymeleaf视图解析器解析到，然后转发到相应的html页面
2.但如果在return返回的值的前边加上forword/:   那么就不会被视图解析器解析到，而是直接转发到相应的请求
3.但如果在return返回的值的前边加上redirect/:   那么就不会被视图解析器解析到，而是直接重定向跳转到相应的请求或网址
用了thymeleaf只能通过转发去访问webinf下的页面资源

SpringMVC中创建转发视图的情况：
		当控制器方法中所设置的视图名称以"forward:"为前缀时，创建InternalResourceView视图，此时的视图名称不会被SpringMVC配置文件中所配置的视图解析器解析，而是会将前缀"forward:"去掉，剩余部分作为最终路径通过转发的方式实现跳转

例如"forward:/"，"forward:/testThymeleafView"

```java
@RequestMapping("/testForward")
public String testForward(){
    return "forward:/testThymeleafView";
}
```

![image-20220630075849741](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220630075849741.png)



#### 三.重定向视图：RedirectView

SpringMVC中默认的重定向视图是RedirectView

当控制器方法中所设置的视图名称以"redirect:"为前缀时，创建RedirectView视图，此时的视图名称不会被SpringMVC配置文件中所配置的视图解析器解析，而是会将前缀"redirect:"去掉，剩余部分作为最终路径通过重定向的方式实现跳转

例如"redirect:/"，"redirect:/employee"

```java
@RequestMapping("/testRedirect")
public String testRedirect(){
    return"redirect:testThymeleafView";
}
```

![image-20220630080134636](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220630080134636.png)

注：
		转发能访问webinf下的资源，但是重定向不行。因为webinf下的资源具有安全性，隐藏性，只能通过服务器内部来访问，不能通过浏览器来访问。可以访问请求
		转发不能跨域，重定向可以。转发发生在服务器内部，那它就只能访问服务器内部的资源；而重定向是浏览器发送的两次请求，那通过浏览器可以访问任何资源，比如在项目里重定向到百度



#### 四.视图控制器view-controller

当控制器方法中，没有任何请求处理的过程，仅仅用来实现页面跳转，即只需要设置视图名称时，可以将处理器方法使用view-controller标签进行表示

```xml
   <!--
       path：设置处理的请求地址
view-name：设置请求地址所对应的视图名称
-->
   <mvc:view-controller path="/" view-name="index"></mvc:view-controller>
```

当SpringMVC中设置任何一个view-controller时，其他控制器中的请求映射将全部失效，此时需要在SpringMVC的核心配置文件中设置开启mvc注解驱动的标签：

```xml
<mvc:annotation-driven/>
```

或

```xml
<mvc:annotation-driven></mvc:annotation-driven>
```





### RESTful



#### 一.RESTful简介

REST：**Re**presentational **S**tate **T**ransfer，表现层资源状态转移。

1.资源：
		资源是一种看待服务器的方式，即，将服务器看作是由很多离散的资源组成。每个资源是服务器上一个可命名的抽象概念。因为资源是一个抽象的概念，所以它不仅仅能代表服务器文件系统中的一个文件、数据库中的一张表等等具体的东西，可以将资源设计的要多抽象有多抽象，只要想象力允许而且客户端应用开发者能够理解。与面向对象设计类似，资源是以名词为核心来组织的，首先关注的是名词。一个资源可以由一个或多个URI来标识。URI既是资源的名称，也是资源在Web上的地址。对某个资源感兴趣的客户端应用，可以通过资源的URI与其进行交互。

2.资源的表述：
		资源的表述是一段对于资源在某个特定时刻的状态的描述。可以在客户端-服务器端之间转移（交换）。资源的表述可以有多种格式，例如HTML/XML/JSON/纯文本/图片/视频/音频等等。资源的表述格式可以通过协商机制来确定。请求-响应方向的表述通常使用不同的格式。

3.状态转移：
		状态转移说的是：在客户端和服务器端之间转移（transfer）代表资源状态的表述。通过转移和操作资源的表述，来间接实现操作资源的目的。

注：
		1.表现层：视图层(前端视图页面)+控制层
		2.资源：可以理解为一种表现形式。可以是html、xml、jsp、json、纯文本、图片、视频、音频等等，万物皆资源
		3.操作资源的表述就是请求路径



#### 二.RESTful的实现

具体说，就是 HTTP 协议里面，四个表示操作方式的动词：GET、POST、PUT、DELETE。

它们分别对应四种基本操作：GET 用来获取资源，POST 用来新建资源，PUT 用来更新资源，DELETE 用来删除资源。

REST 风格提倡 URL 地址使用统一的风格设计，从前到后各个单词使用斜杠分开，不使用问号键值对方式携带请求参数，而是将要发送给服务器的数据作为 URL 地址的一部分，以保证整体风格的一致性。

| 操作     | 传统方式         | REST风格                |
| :------- | :--------------- | ----------------------- |
| 查询操作 | getUserById?id=1 | user/1-->get请求方式    |
| 保存操作 | saveUser         | user-->post请求方式     |
| 删除操作 | deleteUser?id=1  | user/1-->delete请求方式 |
| 更新操作 | updateUser       | user-->put请求方式      |



#### 三.HiddenHttpMethodFilter过滤器

1.概念：
		由于浏览器只支持发送get和post方式的请求，那么该如何发送put和delete请求呢？
		SpringMVC 提供了 **HiddenHttpMethodFilter** 帮助我们**将 POST 请求转换为 DELETE 或 PUT 请求**

​		HiddenHttpMethodFilter的父类是OncePerRequestFilter，它继承了父类的doFilterInternal方法，工作原理是将jsp页面的form表单的method属性值在doFilterInternal方法中转化为标准的Http方法，即GET,、POST、 HEAD、OPTIONS、PUT、DELETE、TRACE，然后到Controller中找到对应的方法。例如，在使用注解时我们可能会在Controller中用于@RequestMapping(value = "list", method = RequestMethod.PUT)，所以如果你的表单中使用的是<form method="put">，那么这个表单会被提交到标了Method="PUT"的方法中。

2.设置：
		**HiddenHttpMethodFilter** 处理put和delete请求的两个条件：
				(1).当前请求的请求方式必须为post
				(2).当前请求必须传输请求参数 _method
				满足以上条件，**HiddenHttpMethodFilter** 过滤器就会将当前请求的请求方式转换为请求参数 _method的值，因此请求参数 _method的值才是最终的请求方式

```html
<form action="..." method="post">
    <input type="hidden" name="_method" value="put" />
    ......
</form>
```

在web.xml中注册**HiddenHttpMethodFilter** :

```xml
<!--配置HiddenHTTPMethodFilter-->
<filter>
    <filter-name>HiddenHttpMethodFilter</filter-name>
    <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>HiddenHttpMethodFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

底层代码：

<img src="https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220703115605264.png" alt="image-20220703115605264"  />



#### 四.两个过滤器的配置顺序

目前为止，SpringMVC中提供了两个过滤器：CharacterEncodingFilter和HiddenHttpMethodFilter

在web.xml中注册时，必须先注册CharacterEncodingFilter，再注册HiddenHttpMethodFilter

原因：

- 在 CharacterEncodingFilter 中通过 request.setCharacterEncoding(encoding) 方法设置字符集的

- request.setCharacterEncoding(encoding) 方法要求前面不能有任何获取请求参数的操作

- 而 HiddenHttpMethodFilter 恰恰有一个获取请求方式的操作：

String paramValue = request.getParameter(this.methodParam);





### HttpMessageConverter

​		HttpMessageConverter：报文信息转换器，将请求报文转换为Java对象，或将Java对象转换为响应报文

​		HttpMessageConverter提供了两个注解和两个类型：@RequestBody，@ResponseBody，RequestEntity，ResponseEntity	（@RequestBody，@ResponseBody是注解；RequestEntity，ResponseEntity是类型）

注：请求报文由三部分组成，请求头，请求行，请求体。
				请求体只有在post请求的时候才有，get没有。因为请求体里放的就是请求参数。get把请求参数直接拼接在地址栏中，post把请求参数放在了请求体里



#### 一.@RequestBody

将当前的请求报文中的请求体转换为Java数据

@RequestBody可以获取请求体，需要在控制器方法设置一个形参，使用@RequestBody进行标识，当前请求的请求体就会为当前注解所标识的形参赋值

```html
<form th:action="@{/testRequestBody}" method="post">
    <input type="text" name="username">
    <input type="password" name="password">
    <input type="submit" value="测试@RequestBody">
</form>
```

```java
@RequestMapping("/testRequestBody")
public String testRequestBody(@RequestBody String requestBody){
    System.out.println("requestBody" + requestBody);
    return "success";
}
```

输出结果：requestBodyusername=admin&password=123456



#### 二.RequestEntity

RequestEntity封装请求报文的一种类型，需要在控制器方法的形参中设置该类型的形参，当前请求的请求报文就会赋值给该形参，可以通过getHeaders()获取请求头信息，通过getBody()获取请求体信息

```html
<form th:action="@{/testRequestEntity}" method="post">
    <input type="text" name="username">
    <input type="password" name="password">
    <input type="submit" value="测试RequestEntity">
</form>
```

```java
@RequestMapping("/testRequestEntity")
public String testRequestEntity(RequestEntity<String> requestEntity){
    //当前requestEntity表示整个请求报文的信息
    System.out.println("请求头：" + requestEntity.getHeaders());
    System.out.println("请求体：" + requestEntity.getBody());
    return "success";
}
```

输出结果：
请求头：[host:"localhost:8080", connection:"keep-alive", content-length:"30", cache-control:"max-age=0", sec-ch-ua:"" Not A;Brand";v="99", "Chromium";v="102", "Google Chrome";v="102"", sec-ch-ua-mobile:"?0", sec-ch-ua-platform:""Windows"", upgrade-insecure-requests:"1", origin:"http://localhost:8080", user-agent:"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/102.0.0.0 Safari/537.36", accept:"text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9", sec-fetch-site:"same-origin", sec-fetch-mode:"navigate", sec-fetch-user:"?1", sec-fetch-dest:"document", referer:"http://localhost:8080/springMVC/", accept-encoding:"gzip, deflate, br", accept-language:"zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7", cookie:"Hm_lvt_cd8218cd51f800ed2b73e5751cb3f4f9=1644640777,1644717225; Idea-8374e3b0=c67bec8c-7b13-4cb3-bc89-a5fe2d9dc14f", Content-Type:"application/x-www-form-urlencoded;charset=UTF-8"]
请求体：username=admin&password=123456



#### 三.通过HTTPServletResponse响应浏览器数据、

通过原生servletAPI的response对象响应浏览器数据（下边的@ResponseBody是springMVC提供的响应浏览器数据的方法）

```html
<a th:href="@{/testResponse}">通过servletAPI的response对象响应浏览器数据</a>
```

```java
@RequestMapping("/testResponse")
public void testResponse(HttpServletResponse response) throws IOException {
    response.getWriter().print("hello,response");
}
```

浏览器的页面中展示的结果：![image-20220703173938558](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220703173938558.png)

#### 四.@ResponseBody

将Java对象转换为响应体

@ResponseBody用于标识一个控制器方法，可以将该方法的返回值直接作为响应报文的响应体响应到浏览器

```java
@RequestMapping("/testResponseBody")
@ResponseBody
public String testResponseBody(){
    return "success";
}
```

浏览器的页面中展示的结果：![image-20220703175513150](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220703175513150.png)

（注：微服务哪里用到的非常多，微服务中控制器的每一个方法都要加@ResponseBody注解）



#### 五.SpringMVC处理json

如果响应回去的是一个对象呢？
		创建个User类，里边有id，username，password，age，sex属性，设置无参有参构造，设置get、set方法，先别设置toString，这样输出的显示更明显。
		发现报406，浏览器不知道后台使用的什么语言，需要将服务器的语言转换成json，即需要将java对象转换为json

浏览器能接收到服务器中的数据只能是字符串，再有就是json是JavaScript中的东西，不能在java中转换json对象，所以只能转换为json字符串

@ResponseBody处理json的步骤：
		1.导入jackson的依赖

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.13.3</version>
</dependency>
```

​		2.在SpringMVC的核心配置文件中开启mvc的注解驱动，此时在HandlerAdaptor中会自动装配一个消息转换器：MappingJackson2HttpMessageConverter，可以将响应到浏览器的Java对象转换为Json格式的字符串（第三次用了）

```xml
<mvc:annotation-driven />
```

​		3.在处理器方法上使用@ResponseBody注解进行标识
​		4.将Java对象直接作为控制器方法的返回值返回，就会自动转换为Json格式的字符串

```java
@RequestMapping("/testResponseUser")
@ResponseBody
public User testResponseUser(){
    return new User(1001,"admin","123456",23,"男");
}
```

浏览器的页面中展示的结果：![image-20220703181110990](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220703181110990.png)



#### 六.回顾json

json是JavaScript里的一种数据格式，是一种数据交互格式（xml也是，只不过xml更多的是配置文件，json更多的是数据交互，因为json数据结构比较简单，解析起来比较简单，生成的数据量比较少）

json有两种格式，一种是对象，一种是数组。
对象是放在大括号里边的以键值对的方式存储输出。而数组是放在方括号里边，存储的是一个一个数据
比如：
1.实体类对象转换为json是一个json对象。实体类中是属姓名和属性值，对应json对象中是键值对
2.map转换为json是json对象
3.list转换为json是json数组。list和数组的结构一样

如果不是将java对象响应到浏览器的话，是不需要加jackson的jar包



#### 七.@RestController注解

@RestController注解是springMVC提供的一个复合注解，标识在控制器的类上，就相当于为类添加了@Controller注解，并且为其中的每个方法添加了@ResponseBody注解

（俩注解合二为一了呗）



#### 八.ResponseEntity

ResponseEntity用于控制器方法的返回值类型，该控制器方法的返回值就是响应到浏览器的响应报文 





### 文件上传和下载



#### 一.文件下载

使用ResponseEntity实现下载文件的功能

```java
@RequestMapping("/testDown")
public ResponseEntity<byte[]> testResponseEntity(HttpSession session) throws IOException {
    //获取ServletContext对象
    ServletContext servletContext = session.getServletContext();
    //获取服务器中文件的真实路径
    String realPath = servletContext.getRealPath("/static/img/1.jpg");
    System.out.println(realPath);   //可以看看真实路径在哪里
    //创建输入流
    InputStream is = new FileInputStream(realPath);
    //创建字节数组
    byte[] bytes = new byte[is.available()];
    //将流读到字节数组中
    is.read(bytes);
    //创建HttpHeaders对象设置响应头信息
    MultiValueMap<String, String> headers = new HttpHeaders();
    //设置要下载方式以及下载文件的名字
    headers.add("Content-Disposition", "attachment;filename=1.jpg");
    //设置响应状态码
    HttpStatus statusCode = HttpStatus.OK;
    //创建ResponseEntity对象
    ResponseEntity<byte[]> responseEntity = new ResponseEntity<>(bytes, headers, statusCode);
    //关闭输入流
    is.close();
    return responseEntity;
}
```



#### 二.文件上传

文件上传要求form表单的请求方式必须为post，并且添加属性enctype="multipart/form-data"

SpringMVC中将上传的文件封装到MultipartFile对象中，通过此对象可以获取文件相关信息

上传步骤：
		1.添加依赖：

```xml
<dependency>
    <groupId>commons-fileupload</groupId>
    <artifactId>commons-fileupload</artifactId>
    <version>1.3.1</version>
</dependency>
```

​		2.在SpringMVC的配置文件中添加配置：

```xml
<!--配置文件上传解析器，将上传的文件封装为MultipartFile对象-->
<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver"></bean>
```

​		3.控制器方法：

```java
//文件上传
@RequestMapping("/testUp")
public String testUp(MultipartFile photo, HttpSession session) throws IOException {

    //先看看这两个什么意思
    System.out.println(photo.getName());    //获取表单元素的name属性值
    System.out.println(photo.getOriginalFilename());    //获取当前上传文件的名字

    //获取上传文件的文件名
    String fileName = photo.getOriginalFilename();

    //处理文件重名问题
    //获取上传的文件的后缀名
    String suffixName = fileName.substring(fileName.lastIndexOf("."));  //substring一个参数表示从该参数截取到末尾，且包前不包后，会包括这个.
    //将UUID作为文件名
    String uuid = UUID.randomUUID().toString();
    //将uuid和后缀名拼接后的结果作为最终的文件名
    fileName = uuid + suffixName;

    //通过ServletContext获取服务器中photo目录的路径（即想要获取服务器路径，先有session，通过session获得ServletContext对象，再通过ServletContext.getRealPath()）
    ServletContext servletContext = session.getServletContext();
    String photoPath = servletContext.getRealPath("photo");     //上传到服务器的路径

    //判断photoPath所对应路径是否存在
    File file = new File(photoPath);
    if (!file.exists()){
        //若不存在，则创建目录
        file.mkdir();
    }
    String finalPath = photoPath + File.separator + fileName;   //separator是文件的分隔符
    //实现上传功能
    photo.transferTo(new File(finalPath));     //上传到哪里
    return "success";
}
```





### 拦截器



#### 一.拦截器的配置

SpringMVC中的拦截器用于拦截控制器方法的执行

SpringMVC中的拦截器需要实现HandlerInterceptor

SpringMVC的拦截器必须在SpringMVC的配置文件中进行配置：

![image-20220705074058155](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220705074058155.png)



#### 二.拦截器的三个抽象方法

SpringMVC中的拦截器有三个抽象方法：

preHandle：控制器方法执行之前执行preHandle()，其boolean类型的返回值表示是否拦截或放行，返回true为放行，即调用控制器方法；返回false表示拦截，即不调用控制器方法

postHandle：控制器方法执行之后执行postHandle()

afterComplation：处理完视图和模型数据，渲染视图完毕之后执行afterComplation()



#### 三.创建并配置拦截器

创建一个用于放拦截器的包，包里创建拦截器类，让创建的类实现（implements）HandlerInterceptor类，类里重写三种拦截器方法。然后再springMVC.xml里配置拦截器

1.创建拦截器类：

```java
package com.yc.mvc.interceptors;

import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * @Description: 拦截器类
 * @Author: YC
 * @CreateTime: 2022/7/7 7:44
 */
public class FirstInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        return HandlerInterceptor.super.preHandle(request, response, handler);
//        return false;
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        HandlerInterceptor.super.postHandle(request, response, handler, modelAndView);
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        HandlerInterceptor.super.afterCompletion(request, response, handler, ex);
    }
}
```

2.在SpringMVC的配置文件中进行配置：

```xml
    <!--配置拦截器，三种方法：1.<bean/>    2.<ref/>    3.<mvc:interceptor/>-->
    <mvc:interceptors>
        <!-- 以下两种配置方式(bean标签、ref标签)都是对DispatcherServlet所处理的所有的请求进行拦截 -->
<!--        <bean class="com.yc.mvc.interceptors.FirstInterceptor"></bean>-->
<!--        <ref bean="firstInterceptor"></ref>   &lt;!&ndash;把拦截器交给IOC，通过标识组件的方式把拦截器标识为一个bean，再开启组件扫描&ndash;&gt;-->
        <!--自定义拦截。以下配置方式(mvc:interceptor标签)可以通过ref或bean标签设置拦截器，通过mvc:mapping设置需要拦截的请求，通过mvc:exclude-mapping设置需要排除的请求，即不需要拦截的请求-->
        <mvc:interceptor>
            <mvc:mapping path="/*"/>            <!--拦截所有页面-->	<!--拦截器里匹配所以请求：/**-->
            <mvc:exclude-mapping path="/"/>     <!--把主页面排除。即拦截除了主页面的所有页面-->
            <ref bean="firstInterceptor"></ref>
        </mvc:interceptor>
    </mvc:interceptors>
```



注：preHandle方法负责拦截，如果返回的是false，则表示被拦截



#### 四.多个拦截器的执行顺序

1.若每个拦截器的preHandle()都返回true
		此时多个拦截器的执行顺序和拦截器在SpringMVC的配置文件的配置顺序有关：
		preHandle()会按照配置的顺序执行，而postHandle()和afterComplation()会按照配置的反序执行

2.若某个拦截器的preHandle()返回了false
		preHandle()返回false和它之前的拦截器的preHandle()都会执行，postHandle()都不执行，返回false的拦截器之前的拦截器的afterComplation()会执行





### 异常处理器



SpringMVC提供了一个处理控制器方法执行过程中所出现的异常的接口：HandlerExceptionResolver

HandlerExceptionResolver接口的实现类有：DefaultHandlerExceptionResolver和SimpleMappingExceptionResolver

![image-20220710110212816](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220710110212816.png)

DefaultHandlerExceptionResolver返回的是ModelAndView，所以它是干什么的：如果在控制器方法执行的过程中出现了指定的异常，他就可以返回一个新的ModelAndView，来代替原来方法要返回的ModelAndView，跳转到指定的页面



#### 一.基于配置的异常处理

SpringMVC提供了自定义的异常处理器SimpleMappingExceptionResolver，使用方式：

```xml
<!--配置异常处理-->
<bean class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
    <!--properties的键表示处理器方法执行过程中出现的异常。properties的值表示若出现指定异常时，设置一个新的视图名称，跳转到指定页面-->
    <property name="exceptionMappings">     <!--类型是properties，properties继承了Hashtable，所以里边的结构应该是键值对-->
        <props>
            <prop key="java.lang.ArithmeticException">error</prop>    <!--key里写的是当前异常的全类名。后边的值就写要跳到的页面名称-->
        </props>
    </property>
    <!--exceptionAttribute属性设置一个属性名，将出现的异常信息在请求域中进行共享。即设置将异常信息共享在请求域中的键-->
    <property name="exceptionAttribute" value="ex"></property>      <!--可以设置一个键来存储当前的异常信息，默认存储到请求域中。value设置的是存储到请求域中异常信息的键。以设置的value值为键，以当前的异常为值-->
</bean>
```



#### 二.基于注解的异常处理

@ControllerAdvice是被@Component标识的，所以@ControllerAdvice也是组件的扩展注解。





### 注解配置SpringMVC

使用配置类和注解代替web.xml和SpringMVC配置文件的功能



#### 一.创建初始化类，代替web.xml

在Servlet3.0环境中，容器会在类路径中查找实现javax.servlet.ServletContainerInitializer接口的类，如果找到的话就用它来配置Servlet容器（也就是配置Tomcat服务器）。

Spring提供了这个接口的实现，名为SpringServletContainerInitializer，这个类反过来又会查找实现WebApplicationInitializer的类并将配置的任务交给它们来完成。Spring3.2引入了一个便利的WebApplicationInitializer基础实现，名为AbstractAnnotationConfigDispatcherServletInitializer，当我们的类扩展了AbstractAnnotationConfigDispatcherServletInitializer并将其部署到Servlet3.0容器的时候，容器会自动发现它，并用它来配置Servlet上下文。

```java
package com.yc.mvc.config;

import org.springframework.web.filter.CharacterEncodingFilter;
import org.springframework.web.filter.HiddenHttpMethodFilter;
import org.springframework.web.servlet.support.AbstractAnnotationConfigDispatcherServletInitializer;

import javax.servlet.Filter;

/**
 * @Description:
 * @Author: YC
 * @CreateTime: 2022/7/10 16:48
 */
//web工程的初始化类，用来代替web.xml
public class WebInit extends AbstractAnnotationConfigDispatcherServletInitializer {

    /*指定spring的配置类*/
    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class[]{SpringConfig.class};
    }

    /*指定SpringMVC的配置类*/
    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{WebConfig.class};
    }

    /*指定DispatcherServlet的映射规则，即url-pattern*/
    @Override
    protected String[] getServletMappings() {
        return new String[]{"/"};
    }

    /*注册过滤器*/
    @Override
    protected Filter[] getServletFilters() {
        CharacterEncodingFilter characterEncodingFilter = new CharacterEncodingFilter();
        characterEncodingFilter.setEncoding("UTF-8");
        characterEncodingFilter.setForceResponseEncoding(true);
        HiddenHttpMethodFilter hiddenHttpMethodFilter = new HiddenHttpMethodFilter();:
        return new Filter[]{characterEncodingFilter,hiddenHttpMethodFilter};
    }
}
```



#### 二.创建SpringConfig配置类，代替spring的配置文件

```java
@Configuration
public class SpringConfig {
    //ssm整合之后，spring的配置信息写在此类中
}
```



#### 三.创建WebConfig配置类，代替SpringMVC的配置文件

```java
/*
    代替SpringMVC的配置文件：
    1.扫描组件  2.视图解析器 3.view-controller   4.default-servlet-handler   5.mvc注解驱动   6.文件上传解析器   7.异常处理  8.拦截器
**/

//将当前类表示为一个配置类
@Configuration
//1.扫描组件
@ComponentScan("com.yc.mvc.controller")
//5.开启mvc注解驱动
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    //4.使用默认的servlet处理静态资源：default-servlet-handler
    @Override
    public void configureDefaultServletHandling(DefaultServletHandlerConfigurer configurer) {
        configurer.enable();
    }

    //8.拦截器
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        TestInterceptor testInterceptor = new TestInterceptor();
        registry.addInterceptor(testInterceptor).addPathPatterns("/**");
    }

    //3.view-controller
    @Override
    public void addViewControllers(ViewControllerRegistry registry) {
        registry.addViewController("/hello").setViewName("hello");
    }

    // 6.文件上传解析器
    @Bean
    public MultipartResolver multipartResolver(){
        CommonsMultipartResolver commonsMultipartResolver = new CommonsMultipartResolver();
        return commonsMultipartResolver;
    }

    //7.异常处理    注：Properties继承了Hashtable连泛型都没了，因为它在操作Properties文件的方面，它只能操作字符串类型的键和字符串类型的值
    @Override
    public void configureHandlerExceptionResolvers(List<HandlerExceptionResolver> resolvers) {
        SimpleMappingExceptionResolver exceptionResolver = new SimpleMappingExceptionResolver();
        Properties prop = new Properties();
        prop.setProperty("java.lang.ArithmeticException","error");
        //设置异常映射
        exceptionResolver.setExceptionMappings(prop);
        //设置共享异常信息的键
        exceptionResolver.setExceptionAttribute("exception");
        resolvers.add(exceptionResolver);
    }


    //2.视图解析器
    //以下的每个@Bean注解的方法都对应着之前项目里配置springMVC.xml里的前端控制器里的bean标签。springMVC.xml里的bean标签应该是先有最里层的，再有外层的
    
    //配置生成模板解析器
    @Bean
    public ITemplateResolver templateResolver() {
        WebApplicationContext webApplicationContext = ContextLoader.getCurrentWebApplicationContext();
        // ServletContextTemplateResolver需要一个ServletContext作为构造参数，可通过WebApplicationContext 的方法获得
        ServletContextTemplateResolver templateResolver = new ServletContextTemplateResolver(
                webApplicationContext.getServletContext());
        templateResolver.setPrefix("/WEB-INF/templates/");
        templateResolver.setSuffix(".html");
        templateResolver.setCharacterEncoding("UTF-8");
        templateResolver.setTemplateMode(TemplateMode.HTML);
        return templateResolver;
    }

    //生成模板引擎并为模板引擎注入模板解析器
    //在一个方法中所使用的参数，必须是符合自动装配的规则的。也就是说能够使用的参数，必须得是spring的IOC容器所拥有的bean，这个bean能为这个参数赋值
    @Bean
    public SpringTemplateEngine templateEngine(ITemplateResolver templateResolver) {
        SpringTemplateEngine templateEngine = new SpringTemplateEngine();
        templateEngine.setTemplateResolver(templateResolver);
        return templateEngine;
    }

    //生成视图解析器并未解析器注入模板引擎
    @Bean
    public ViewResolver viewResolver(SpringTemplateEngine templateEngine) {
        ThymeleafViewResolver viewResolver = new ThymeleafViewResolver();
        viewResolver.setCharacterEncoding("UTF-8");
        viewResolver.setTemplateEngine(templateEngine);
        return viewResolver;
    }


}
```





### SpringMVC执行流程



#### 一.SpringMVC常用组件

- DispatcherServlet：**前端控制器**，不需要工程师开发，由框架提供

作用：统一处理请求和响应，整个流程控制的中心，由它调用其它组件处理用户的请求

- HandlerMapping：**处理器映射器**，不需要工程师开发，由框架提供

作用：根据请求的url、method等信息查找Handler，即控制器方法。（将请求和控制器方法进行映射）

- Handler：**处理器**，需要工程师开发

作用：在DispatcherServlet的控制下Handler对具体的用户请求进行处理

- HandlerAdapter：**处理器适配器**，不需要工程师开发，由框架提供

作用：通过HandlerAdapter对处理器（控制器方法）进行执行。（找到控制器方法后要调用控制器方法，就用到HandlerAdapter，即源码的ha）

- ViewResolver：**视图解析器**，不需要工程师开发，由框架提供

作用：进行视图解析，得到相应的视图，例如：ThymeleafView、InternalResourceView、RedirectView

- View：**视图**

作用：将模型数据通过页面展示给用户



#### 二.DispatcherServlet初始化过程

DispatcherServlet 本质上是一个 Servlet，所以天然的遵循 Servlet 的生命周期。所以宏观上是 Servlet 生命周期来进行调度。

![img005](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/img005.png)

##### 1.初始化WebApplicationContext

所在类：org.springframework.web.servlet.FrameworkServlet

```java
protected WebApplicationContext initWebApplicationContext() {
    WebApplicationContext rootContext = WebApplicationContextUtils.getWebApplicationContext(this.getServletContext());
    WebApplicationContext wac = null;
    if (this.webApplicationContext != null) {
        wac = this.webApplicationContext;
        if (wac instanceof ConfigurableWebApplicationContext) {
            ConfigurableWebApplicationContext cwac = (ConfigurableWebApplicationContext)wac;
            if (!cwac.isActive()) {
                if (cwac.getParent() == null) {
                    cwac.setParent(rootContext);
                }

                this.configureAndRefreshWebApplicationContext(cwac);
            }
        }
    }

    if (wac == null) {
        wac = this.findWebApplicationContext();
    }

    if (wac == null) {
        // 创建WebApplicationContext
        wac = this.createWebApplicationContext(rootContext);
    }

    if (!this.refreshEventReceived) {
        synchronized(this.onRefreshMonitor) {
            // 刷新WebApplicationContext
            this.onRefresh(wac);
        }
    }

    if (this.publishContext) {
        // 将IOC容器在应用域共享
        String attrName = this.getServletContextAttributeName();
        this.getServletContext().setAttribute(attrName, wac);
    }

    return wac;
}
```



##### 2.创建WebApplicationContext

所在类：org.springframework.web.servlet.FrameworkServlet

```java
protected WebApplicationContext createWebApplicationContext(@Nullable ApplicationContext parent) {
    Class<?> contextClass = this.getContextClass();
    if (!ConfigurableWebApplicationContext.class.isAssignableFrom(contextClass)) {
        throw new ApplicationContextException("Fatal initialization error in servlet with name '" + this.getServletName() + "': custom WebApplicationContext class [" + contextClass.getName() + "] is not of type ConfigurableWebApplicationContext");
    } else {
        // 通过反射创建 IOC 容器对象
        ConfigurableWebApplicationContext wac = (ConfigurableWebApplicationContext)BeanUtils.instantiateClass(contextClass);
        wac.setEnvironment(this.getEnvironment());
        // 设置父容器
        wac.setParent(parent);
        String configLocation = this.getContextConfigLocation();
        if (configLocation != null) {
            wac.setConfigLocation(configLocation);
        }

        this.configureAndRefreshWebApplicationContext(wac);
        return wac;
    }
}
```



##### 3.DispatcherServlet初始化策略

FrameworkServlet创建WebApplicationContext后，刷新容器，调用onRefresh(wac)，此方法在DispatcherServlet中进行了重写，调用了initStrategies(context)方法，初始化策略，即初始化DispatcherServlet的各个组件

所在类：org.springframework.web.servlet.DispatcherServlet

```java
protected void initStrategies(ApplicationContext context) {
    this.initMultipartResolver(context);
    this.initLocaleResolver(context);
    this.initThemeResolver(context);
    this.initHandlerMappings(context);
    this.initHandlerAdapters(context);
    this.initHandlerExceptionResolvers(context);
    this.initRequestToViewNameTranslator(context);
    this.initViewResolvers(context);
    this.initFlashMapManager(context);
}
```



#### 三.DispatcherServlet调用组件处理请求



##### 1.processRequest()

FrameworkServlet重写HttpServlet中的service()和doXxx()，这些方法中调用了processRequest(request, response)

所在类：org.springframework.web.servlet.FrameworkServlet

```java
protected final void processRequest(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    long startTime = System.currentTimeMillis();
    Throwable failureCause = null;
    LocaleContext previousLocaleContext = LocaleContextHolder.getLocaleContext();
    LocaleContext localeContext = this.buildLocaleContext(request);
    RequestAttributes previousAttributes = RequestContextHolder.getRequestAttributes();
    ServletRequestAttributes requestAttributes = this.buildRequestAttributes(request, response, previousAttributes);
    WebAsyncManager asyncManager = WebAsyncUtils.getAsyncManager(request);
    asyncManager.registerCallableInterceptor(FrameworkServlet.class.getName(), new FrameworkServlet.RequestBindingInterceptor());
    this.initContextHolders(request, localeContext, requestAttributes);

    try {
        // 执行服务，doService()是一个抽象方法，在DispatcherServlet中进行了重写
        this.doService(request, response);
    } catch (IOException | ServletException var16) {
        failureCause = var16;
        throw var16;
    } catch (Throwable var17) {
        failureCause = var17;
        throw new NestedServletException("Request processing failed", var17);
    } finally {
        this.resetContextHolders(request, previousLocaleContext, previousAttributes);
        if (requestAttributes != null) {
            requestAttributes.requestCompleted();
        }

        this.logResult(request, response, (Throwable)failureCause, asyncManager);
        this.publishRequestHandledEvent(request, response, startTime, (Throwable)failureCause);
    }

}
```



##### 2.doService()

所在类：org.springframework.web.servlet.DispatcherServlet

```java
protected void doService(HttpServletRequest request, HttpServletResponse response) throws Exception {
    this.logRequest(request);
    Map<String, Object> attributesSnapshot = null;
    if (WebUtils.isIncludeRequest(request)) {
        attributesSnapshot = new HashMap();
        Enumeration attrNames = request.getAttributeNames();

        label116:
        while(true) {
            String attrName;
            do {
                if (!attrNames.hasMoreElements()) {
                    break label116;
                }

                attrName = (String)attrNames.nextElement();
            } while(!this.cleanupAfterInclude && !attrName.startsWith("org.springframework.web.servlet"));

            attributesSnapshot.put(attrName, request.getAttribute(attrName));
        }
    }

    request.setAttribute(WEB_APPLICATION_CONTEXT_ATTRIBUTE, this.getWebApplicationContext());
    request.setAttribute(LOCALE_RESOLVER_ATTRIBUTE, this.localeResolver);
    request.setAttribute(THEME_RESOLVER_ATTRIBUTE, this.themeResolver);
    request.setAttribute(THEME_SOURCE_ATTRIBUTE, this.getThemeSource());
    if (this.flashMapManager != null) {
        FlashMap inputFlashMap = this.flashMapManager.retrieveAndUpdate(request, response);
        if (inputFlashMap != null) {
            request.setAttribute(INPUT_FLASH_MAP_ATTRIBUTE, Collections.unmodifiableMap(inputFlashMap));
        }

        request.setAttribute(OUTPUT_FLASH_MAP_ATTRIBUTE, new FlashMap());
        request.setAttribute(FLASH_MAP_MANAGER_ATTRIBUTE, this.flashMapManager);
    }

    RequestPath previousRequestPath = null;
    if (this.parseRequestPath) {
        previousRequestPath = (RequestPath)request.getAttribute(ServletRequestPathUtils.PATH_ATTRIBUTE);
        ServletRequestPathUtils.parseAndCache(request);
    }

    try {
        // 处理请求和响应
        this.doDispatch(request, response);
    } finally {
        if (!WebAsyncUtils.getAsyncManager(request).isConcurrentHandlingStarted() && attributesSnapshot != null) {
            this.restoreAttributesAfterInclude(request, attributesSnapshot);
        }

        if (this.parseRequestPath) {
            ServletRequestPathUtils.setParsedRequestPath(previousRequestPath, request);
        }

    }

}
```



##### 3.doDispatch()

所在类：org.springframework.web.servlet.DispatcherServlet

```java
protected void doDispatch(HttpServletRequest request, HttpServletResponse response) throws Exception {
    HttpServletRequest processedRequest = request;
    HandlerExecutionChain mappedHandler = null;
    boolean multipartRequestParsed = false;
    WebAsyncManager asyncManager = WebAsyncUtils.getAsyncManager(request);

    try {
        try {
            ModelAndView mv = null;
            Object dispatchException = null;

            try {
                processedRequest = this.checkMultipart(request);
                multipartRequestParsed = processedRequest != request;
                /*
            	mappedHandler：调用链
                包含handler、interceptorList、interceptorIndex
            	handler：浏览器发送的请求所匹配的控制器方法
            	interceptorList：处理控制器方法的所有拦截器集合
            	interceptorIndex：拦截器索引，控制拦截器afterCompletion()的执行
           		*/
                mappedHandler = this.getHandler(processedRequest);
                if (mappedHandler == null) {
                    this.noHandlerFound(processedRequest, response);
                    return;
                }

                // 通过控制器方法创建相应的处理器适配器，调用所对应的控制器方法
                HandlerAdapter ha = this.getHandlerAdapter(mappedHandler.getHandler());
                String method = request.getMethod();
                boolean isGet = HttpMethod.GET.matches(method);
                if (isGet || HttpMethod.HEAD.matches(method)) {
                    long lastModified = ha.getLastModified(request, mappedHandler.getHandler());
                    if ((new ServletWebRequest(request, response)).checkNotModified(lastModified) && isGet) {
                        return;
                    }
                }

                // 调用拦截器的preHandle()
                if (!mappedHandler.applyPreHandle(processedRequest, response)) {
                    return;
                }

                // 由处理器适配器调用具体的控制器方法，最终获得ModelAndView对象
                mv = ha.handle(processedRequest, response, mappedHandler.getHandler());
                if (asyncManager.isConcurrentHandlingStarted()) {
                    return;
                }

                this.applyDefaultViewName(processedRequest, mv);
                // 调用拦截器的postHandle()
                mappedHandler.applyPostHandle(processedRequest, response, mv);
            } catch (Exception var20) {
                dispatchException = var20;
            } catch (Throwable var21) {
                dispatchException = new NestedServletException("Handler dispatch failed", var21);
            }

            // 后续处理：处理模型数据和渲染视图
            this.processDispatchResult(processedRequest, response, mappedHandler, mv, (Exception)dispatchException);
        } catch (Exception var22) {
            this.triggerAfterCompletion(processedRequest, response, mappedHandler, var22);
        } catch (Throwable var23) {
            this.triggerAfterCompletion(processedRequest, response, mappedHandler, new NestedServletException("Handler processing failed", var23));
        }

    } finally {
        if (asyncManager.isConcurrentHandlingStarted()) {
            if (mappedHandler != null) {
                mappedHandler.applyAfterConcurrentHandlingStarted(processedRequest, response);
            }
        } else if (multipartRequestParsed) {
            this.cleanupMultipart(processedRequest);
        }

    }
}
```



##### 4.processDispatchResult()

```java
private void processDispatchResult(HttpServletRequest request, HttpServletResponse response, @Nullable HandlerExecutionChain mappedHandler, @Nullable ModelAndView mv, @Nullable Exception exception) throws Exception {
    boolean errorView = false;
    if (exception != null) {
        if (exception instanceof ModelAndViewDefiningException) {
            this.logger.debug("ModelAndViewDefiningException encountered", exception);
            mv = ((ModelAndViewDefiningException)exception).getModelAndView();
        } else {
            Object handler = mappedHandler != null ? mappedHandler.getHandler() : null;
            mv = this.processHandlerException(request, response, handler, exception);
            errorView = mv != null;
        }
    }

    if (mv != null && !mv.wasCleared()) {
        // 处理模型数据和渲染视图
        this.render(mv, request, response);
        if (errorView) {
            WebUtils.clearErrorRequestAttributes(request);
        }
    } else if (this.logger.isTraceEnabled()) {
        this.logger.trace("No view rendering, null ModelAndView returned.");
    }

    if (!WebAsyncUtils.getAsyncManager(request).isConcurrentHandlingStarted()) {
        if (mappedHandler != null) {
            // 调用拦截器的afterCompletion()
            mappedHandler.triggerAfterCompletion(request, response, (Exception)null);
        }

    }
}
```



#### 四.SpringMVC的执行流程

1.用户向服务器发送请求，请求被SpringMVC 前端控制器 DispatcherServlet捕获。

2.DispatcherServlet对请求URL进行解析，得到请求资源标识符（URI），判断请求URI对应的映射：

a) 不存在
		i. 再判断是否配置了mvc:default-servlet-handler
		ii. 如果没配置，则控制台报映射查找不到，客户端展示404错误

![img006](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/img006.png)

![img007](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/img007.png)

​		iii. 如果有配置，则访问目标资源（一般为静态资源，如：JS,CSS,HTML），找不到客户端也会展示404错误

![img008](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/img008.png)

![img009](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/img009.png)

b) 存在则执行下面的流程

3.根据该URI，调用HandlerMapping获得该Handler配置的所有相关的对象（包括Handler对象以及Handler对象对应的拦截器），最后以HandlerExecutionChain执行链对象的形式返回。

4.DispatcherServlet 根据获得的Handler，选择一个合适的HandlerAdapter。

5.如果成功获得HandlerAdapter，此时将开始执行拦截器的preHandler(…)方法【正向】

6.提取Request中的模型数据，填充Handler入参，开始执行Handler（Controller)方法，处理请求。在填充Handler的入参过程中，根据你的配置，Spring将帮你做一些额外的工作：
		a) HttpMessageConveter： 将请求消息（如Json、xml等数据）转换成一个对象，将对象转换为指定的响应信息
		b) 数据转换：对请求消息进行数据转换。如String转换成Integer、Double等
		c) 数据格式化：对请求消息进行数据格式化。 如将字符串转换成格式化数字或格式化日期等
		d) 数据验证： 验证数据的有效性（长度、格式等），验证结果存储到BindingResult或Error中

7.Handler执行完成后，向DispatcherServlet 返回一个ModelAndView对象。

8.此时将开始执行拦截器的postHandle(...)方法【逆向】。

9.根据返回的ModelAndView（此时会判断是否存在异常：如果存在异常，则执行HandlerExceptionResolver进行异常处理）选择一个适合的ViewResolver进行视图解析，根据Model和View，来渲染视图。

10渲染视图完毕执行拦截器的afterCompletion(…)方法【逆向】。

11.将渲染结果返回给客户端。











### 补充



#### 一.基于配置的mvc创建过程

1.引入依赖 

```xml
<packaging>war</packaging>

<dependencies>

    <!--SpringMVC-->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.3.15</version>
    </dependency>

    <!--日志-->
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>1.2.10</version>
    </dependency>

    <!--ServletAPI-->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>4.0.1</version>
        <scope>provided</scope>
    </dependency>

    <!--Spring5和Thymeleaf整合包-->
    <dependency>
        <groupId>org.thymeleaf</groupId>
        <artifactId>thymeleaf-spring5</artifactId>
        <version>3.0.15.RELEASE</version>
    </dependency>

</dependencies>
```

2.添加webapp，在项目结构里添加项目描述符（webapp没有那个小蓝点的话，点一下代码区右上方的maven小图标，或者刷新一下maven）

![image-20220627202915386](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220627202915386.png)

![image-20220627203009102](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220627203009102.png)

![image-20220627203040818](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220627203040818.png)

3.web.xml里配置编码过滤器，配置HiddenHTTPMethodFilter过滤器，配置springMVC的前端控制器

```xml
<!--配置编码过滤器-->
<filter>
    <filter-name>CharacterEncodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </init-param>
    <init-param>
        <param-name>forceResponseEncoding</param-name>
        <param-value>true</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>CharacterEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>

<!--配置HiddenHTTPMethodFilter-->
<filter>
    <filter-name>HiddenHttpMethodFilter</filter-name>
    <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>HiddenHttpMethodFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>

<!--配置springMVC的前端控制器-->
<servlet>
    <servlet-name>DispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:springMVC.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>
    <servlet-name>DispatcherServlet</servlet-name>
    <url-pattern>/</url-pattern>
</servlet-mapping>
```

4.在resources里创建springMVC.xml，然后启动扫描组件，并配置视图解析器，创建templates文件夹（创建templates文件夹是因为视图解析器的视图前缀），html都放在templates文件夹里边

![image-20220627204712970](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220627204712970.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
                           http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <!--扫描组件-->
    <context:component-scan base-package="com.yc.mvc.controller"></context:component-scan>

    <!--配置视图解析器-->
    <bean id="viewResolver" class="org.thymeleaf.spring5.view.ThymeleafViewResolver">
        <property name="order" value="1"/>
        <property name="characterEncoding" value="UTF-8"/>
        <property name="templateEngine">
            <bean class="org.thymeleaf.spring5.SpringTemplateEngine">
                <property name="templateResolver">
                    <bean class="org.thymeleaf.spring5.templateresolver.SpringResourceTemplateResolver">

                        <!-- 视图前缀 -->
                        <property name="prefix" value="/WEB-INF/templates/"/>

                        <!-- 视图后缀 -->
                        <property name="suffix" value=".html"/>

                        <property name="templateMode" value="HTML5"/>
                        <property name="characterEncoding" value="UTF-8"/>
                    </bean>
                </property>
            </bean>
        </property>
    </bean>

    <!--视图控制器view-controller （必须要搭配mvc注解驱动使用，否则其他请求映射都会失效）
       path：设置处理的请求地址
       view-name：设置请求地址所对应的视图名称
   -->
    <mvc:view-controller path="/" view-name="index"></mvc:view-controller>  <!--这是进入首页-->

    <!--开放对静态资源的访问 （必须要搭配mvc注解驱动使用，否则其他请求映射都会失效）-->
    <mvc:default-servlet-handler />
<!--    <mvc:default-servlet-handler></mvc:default-servlet-handler>-->

    <!--开启mvc注解驱动-->
    <mvc:annotation-driven/>
<!--    <mvc:annotation-driven></mvc:annotation-driven>-->


</beans>
```

![image-20220627204857410](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220627204857410.png)

5.搭建tomcat。在Deployment里把原来的删除，点加号创建一个新的，可以改一下上下文路径

![image-20220627205328125](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220627205328125.png)

![image-20220627205342650](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220627205342650.png)

![image-20220703164626220](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220703164626220.png)

6.就可以创建控制层了，搭建完成





#### 二.小问题

1.如果两个请求的value值一样，那么它们的method一定不能一样

2.服务器的部署路径：
		如果是web工程，是放在out下，也可以在Project Structure下的Project 的project compiler output设置
				Idea项目下的out目录是用来存放.java文件编译后的字节码文件的

![image-20220704110926326](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220704110926326.png)

​		如果是maven工程，放在target下

![image-20220704111007682](https://raw.githubusercontent.com/chocman99/Image/main/SpringMVC/image-20220704111007682.png)



