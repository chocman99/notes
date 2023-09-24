

### 方法



#### 一.方法定义

返回值类型：也就是方法最终产生的数据结果是什么类型
方法名称：方法的名字，规则和变量一样，小驼峰
参数类型：进入方法的数据是什么类型
参数名称：进入方法的数据对应的变量名称
ps：参数如果有多个，使用逗号分隔
方法体：方法需要做的事情，若干代码行
return：两个作用，第一是停止当前方法，第二是将后面的返回值类型还给调用处
返回值：也就是方法执行后最终产生的数据结果
注意：return后面的“返回值”，必须和方法名称前面的“返回值类型”，保持对应

#### 二.方法调用

方法的三种调用格式：
1.单独调用：方法名(参数);

![image-20220305193523738](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220305193523738.png)

2.打印调用：System.out.println(方法名称(参数));

![image-20220305194210118](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220305194210118.png)

3.赋值调用：数据类型 变量名称=方法名称(参数);

![image-20220305195603246](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220305195603246.png)

#### 三.方法的有参和无参

1.有参数：小括号当中有内容，当一个方法需要一些数据条件，才能完成任务的时候，就有参数。例如两个数字相加，必须知道两个数字是各自多少，才能相加。

![image-20220305220940094](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220305220940094.png)

2.无参数：小括号当中留空。一个方法不需要任何数据条件，自己就能独立完成任务，就是无参数。例如定义一个方法，打印固定10次HelloWorld。

![](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220305221037590.png)

![image-20220305221056179](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220305221056179.png)

#### 四.方法的有返回值和无返回值

1.题目要求：定义一个方法，用来【求出】两个数之和。(你帮我算，算完之后把结果告诉我)

![image-20220305221450781](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220305221450781.png)

2.定义一个方法，用来【打印】两个数之和。(你来计算，算完之后你自己负责显示结果，不用告诉我)

![image-20220305221652388](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220305221652388.png)

![image-20220305221741242](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220305221741242.png)

注意事项：对于有返回值的方法，可以使用单独调用，打印调用或赋值调用
                  对于无返回值的方法，只能使用单独调用，不能使用打印和赋值调用

#### 五.方法的重载

对于功能类似的方法来说，因为参数列表不一样，却需要记住那么多不同的方法名称，太麻烦。

方法的重载(Overload)：多个方法的名称一样，但是参数列表不一样。
好处：只需要记住唯一一个方法名称，就可以实现类似的多个功能

![image-20220305222859896](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220305222859896.png)

方法重载与下列因素相关：
1.参数个数不同
2.参数类型不同
3.参数的多类型顺序不同

方法重载与下列因素无关：
1.与参数的名称无关
2.与方法的返回值类型无关

### 类和对象

#### 一.什么是类

类：是一组相关属性和行为的集合。可以看成是一类事物的模板，使用事物的属性特性和行为特征来描述该类事物。

现实中，描述这一类：
属性：就是该事物的状态信息。
行为：就是该事物能够做什么。

举例：小猫
属性：名字，体重，年龄，颜色
行为：走，跑，叫

#### 二.什么是对象

对象：是一类事物的具体体现，对象是类的一个实例，必然具备该类事物的属性和行为。

#### 三.类与对象的关系：

类是对一类事物的描述，是抽象的。
对象是一类事物的实例，是具体的。
类是对象的模板，对象是类的实体。

#### 四.对象的创建及使用

通常情况下，一个类不能直接使用，需要根据类创建一个对象，才能使用。

1.导包：也就是指出需要使用的类，在什么位置。
import  包名称.类名称
对于和当前类属于同一个包的情况，可以省略导包语句不写。

2.创建，格式：
类名称 对象名=new 类名称()；
Student stu = new Student;

3.使用，分为两种情况：
使用成员变量：对象名.成员变量名
使用成员方法：对象名.成员方法名(参数)
（也就是，想用谁，就用对象点谁）

注意事项：
如果成员变量没有进行赋值，那么将会有一个默认值，规则和数组一样。

#### 五.面向对象三大特征之封装性

面向对象三大特征：封装，继承，多态

封装性在java中的体现：
1.方法就是一种封装
2.关键字private也是一种封装

封装就是将一些细节信息隐藏起来，对于外界不可见

#### 六.this的作用

当方法的局部变量和类的成员变量重名的时候，根据“就近原则”，优先使用局部变量。
如果需要访问本类中的成员变量，需要使用格式：this.成员变量

通过谁调用的方法，谁就是this。

![image-20220307101323520](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220307101323520.png)

![image-20220307101407446](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220307101407446.png)

#### 七.构造方法

构造方法是专门用来创建对象的方法，当我们通过关键字new来创建对象时，其实就是在调用构造方法。
格式：
public 类名称(参数类型 参数名称){
          方法体
}

注意事项：
1.构造方法的名称必须和所在的类名称完全一样，就连大小写也要一样
2.构造方法不要写返回值类型，连void都不写
3.构造方法不能return一个具体的返回值
4.如果没有编写任何构造方法，那么编译器将会默认赠送一个构造方法，没有参数、方法体，什么事情都不做。
public Student(){}
5.一旦编写了至少一个构造方法，那么编译器将不再赠送。
6.构造方法也是可以进行重载的。

#### 八.定义一个标准的类

一个标准的类通常拥有下面四个组成部分：
1.所有的成员变量都要使用private关键字修饰
2.为每一个成员变量编写一对Getter/Setter方法
3.编写一个无参构造方法
3.编写一个全参构造方法

这样标准的类也叫做Java Bean
快捷键：alt+insert

#### 九.Scanner类

Scanner类的功能：可以实现键盘输入数据，到程序当中。

引用类型的一般使用步骤：
1.导包
import 包路径.类名称；
如果需要使用的目标类，和当前类位于同一个包下，则可以省略导包语句不写。
只有java.lang包下的内容不需要导包，其他的包都需要import语句。
2.创建
类名称 对象名 = new 类名称（）；
3.使用
对象名.成员方法名（）

获取键盘输入的一个int数字：int num = sc.nextInt();
获取键盘输入的一个字符串：String str = sc.next();

![image-20220307104312945](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220307104312945.png)

![image-20220307104630793](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220307104630793.png)

#### 十.Random类

Random类用来生成随机数字。使用起来也是三个步骤：
1.导包
import java.util.Random
2.创建
Random r = new Random();（小括号中留空即可）
3.使用
获取一个随机的int数字（范围是int所有范围，有正负两种）：int num = r.nextInt()
获取一个随机的int数字（参数代表了范围，左闭右开区间）：int num = r.nextInt(3)

无参：

![image-20220307110447440](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220307110447440.png)

有参：（注意：参数是多少，范围就是0~多少-1）

![image-20220307110425108](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220307110425108.png)



#### 十一.数组

##### 1.数组的概念及初始化

1.数组的概念：
数组是一种容器，可以同时存放多个数据值

2.数组的特点：
(1)).数组是一种引用数据类型
(2).数组当中的多个数据，类型必须统一
(3).数组的长度在程序运行期间不可改变

3.数组的初始化：在内存当中创建一个数组，并且向其中赋予一些默认值

两种常见的初始化方式：
(1).动态初始化（指定长度）：在创建数组的时候，直接指定数组当中的数据元素个数
(2).静态初始化（指定内容）：在创建数组的时候，不直接指定数据个数多少，而是直接将具体的数据内容进行指定

(1).动态初始化数组的格式：
数据类型[ ] 数组名称 = new 数据类型[数组长度];

解析含义：
左侧数据类型数据：也就是数组当中保存的数据，全都是统一的什么类型
左侧的中括号：代表我是一个数组
左侧数组名称：给数组取一个名字
右侧的new：代表创建数组的动作
右侧数据类型：必须和左边的数据类型保持一致
右侧中括号的长度：也就是数组当中，到底可以保存多少个数据，是一个int数字

(2).静态初始化基本格式：

标准格式：
数据类型[ ] 数组名称 = new 数据类型[ ] {元素1,元素2,...};

省略格式：使用静态初始化数组的时候，格式可以省略一下：
数据类型[ ] 数组名称 = {元素1,元素2,...};

注意事项：
(1).虽然静态初始化没有直接告诉长度，但是根据大括号里面的元素具体内容，也可以自动推算出来长度。
(2).静态初始化标准格式可以拆分成为两个步骤。
(3).动态初始化也可以拆分成为两个步骤。
(4).静态初始化一旦使用省略格式，就不能拆分成为两个步骤了。

使用建议：如果不确定数组当中的内容，用动态初始化；否则，已经确定了内容，用静态初始化。

##### 2.访问数组元素进行获取

直接打印数组名称：得到的是数组对应的：内存地址哈希值。

访问数组元素的格式：数组名称[索引值]
索引值：就是一个int数字，代表数组当中元素的编号。
注意：索引值从0开始，一直到”数组的长度-1“为止。

##### 3.访问数组元素进行赋值

使用动态初始化数组的时候，其中的元素将会自动拥有一个默认值。规则如下：
如果是整数类型，那么默认值为0；
如果是浮点类型，那么默认值为0.0；
如果是字符类型，那么默认值为‘\u0000’；
如果是布尔类型，那么默认值为false；
如果是引用类型，那么默认值为null；

注意事项：静态初始化其实也有默认值的过程，只不过系统自动马上将默认值替换成为了大括号当中的具体数值。

##### 4.常见问题

1.数组索引越界异常

数组的索引编号从0开始，一直到”数组的长度-1“为止。

如果访问数组元素的时候，索引编号并不存在，那么将会发生数组引越界异常（ArrayIndexOutOfBoundException）

原因：索引编号写错了
解决：修改成为存在的正确索引编号。

2.空指针异常

所有的引用类型变量，都可以赋值为一个null值；但是代表其中什么都没有。

数组必须进行new初始化才能使用其中的元素。
如果只是赋值了一个null，没有进行new创建，那么将会发生：空指针异常（NullPointerException）

原因：忘了new
解决：补上new

##### 5.获取数组的长度

获取数组的长度，格式：
数组名称.length

这将会得到一个int数字，代表数组的长度。

数组一旦创建，程序运行期间，长度不可改变。

##### 6.数组的遍历输出

遍历数组：说的就是对数组当中的每一个元素进行逐一，挨个处理。默认的处理方式就是打印输出。
for循环

![image-20220308105934026](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220308105934026.png)

##### 7.数组作为方法返回值

一个方法可以有0、1、多个参数；但是只能有0或者1个返回值，不能有多个返回值。
如果希望一个方法当中产生了多个结果数据进行返回，怎么办？
解决办法 ：使用一个数组作为返回值类型即可。

任何数据类型都能作为方法的参数类型，或者返回值类型。

数组作为方法的参数，传递进去的其实是数组的地址值。
数组作为方法的返回值，返回的其实也是数组的地址值。

![image-20220308112201472](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220308112201472.png)



#### 十二.ArrayList集合

数组的长度不可以发生改变。
但是ArrayList集合的长度是可以随意变化的。

对于 ArrayList来说，有一个尖括号<E>代表泛型。
泛型：也就是装在集合当中的所有元素，全都是统一的什么类型。
注意：泛型只能是引用类型，不能是基本类型。

注意事项：
对于ArrayList集合来说，直接打印得到的不是地址值，而是内容。
如果内容是空，得到的是空洞的中括号：[ ]

![image-20220307190609169](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220307190609169.png)

ArrayList当中的常用方法有：
public boolean add(E e)：向集合当中添加元素，参数的类型和泛型一致。返回值代表添加是否成功。
                                          备注：对于ArrayList集合来说，add添加动作一定是成功的，所以返回值可用可不用。
                                          但是对于其他集合来说，add添加动作不一定成功
public E get(int index)：从集合当中获取元素，参数是索引编号，返回值就是对应位置的元素
public E remove(int index)：从集合中删除元素，参数是索引编号，返回值就是被删除掉的元素
public int size()：获取集合的尺寸长度，返回值就是集合中包含的元素个数

![image-20220307220849078](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220307220849078.png)

![image-20220307192229624](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220307192229624.png)

![image-20220307220744187](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220307220744187.png)

![image-20220307220817988](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220307220817988.png)

遍历集合：

![image-20220307221052079](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220307221052079.png)

如果希望向集合ArrayList当中存储基本类型数据，必须使用基本类型对应的“包装类”。

基本类型                 包装类（引用类型，包装类都位于java.lang包下）
byte                         Byte
short                        Short
int                            Integer
long                         Long
float                         Float
double                     Double
char                         Character
boolean                    Boolean

从JDK1.5+开始，支持自动装箱，自动拆箱
自动装箱：基本类型-->包装类型
自动拆箱：包装类型-->基本类型

#### 十三.静态static

一旦使用了static关键字，那么这样的内容不再属于对象自己，而是属于类的，所以凡是本类的对象，都共享同一份。

一旦使用了static修饰成员方法，那么这就成为了静态方法。静态方法不属于对象，而是属于类的。

如果没有static关键字，那么必须首先创建对象，然后通过对象下能使用它。
如果有了static关键字，那么不需要创建对象，直接就能通过类名称来使用它。

无论是成员变量，还是成员方法，如果有了static，都推荐使用类名称进行调用。
静态变量：类名称.静态变量
静态方法：类名称.静态方法

注意事项：
1.静态只能直接访问静态，不能直接访问非静态。
原因：因为在内存当中是先有的静态内容，后有的非静态内容。
2.静态方法中不能使用this。
原因：this代表当前对象，通过谁调用的方法，谁就是当前对象。

![image-20220312112206575](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220312112206575.png)

静态static的内存图：

![image-20220312112745364](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220312112745364.png)

静态代码块：

静态代码块的格式是：
public class 类名称{
static{
             //静态代码块
    }
}

特点：当第一次用到本类时，静态代码块执行唯一的一次。
静态内容总是优先于非静态，所以静态代码块比构造方法先执行。

静态代码块的典型用途：
用来一次性的对静态成员变量进行赋值。

#### 十四.Math类

java.util.Math类是数学相关的工具类，里面提供了大量的静态方法，完成与数学运算相关的操作。

public static double abs(double num)：获取绝对值。

![image-20220312114635162](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220312114635162.png)

public static double ceil(double num)：向上取整。

![image-20220312114715065](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220312114715065.png)

public static double floor(double num)：向下取整。

![image-20220312114743668](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220312114743668.png)

public static long round(double num)：四舍五入。

![image-20220312114836459](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220312114836459.png)

Math.PI代表近似的圆周率常量。

#### 十五.匿名对象类

创建对象的标准格式：
类名称 对象名 = new 类名称();

匿名对象就是只有右边的对象，没有左边的名字和赋值运算符
new 类名称();

注意事项：匿名对象只能使用唯一的一次，下次再用不得不再创建一个对象。
使用建议：如果确定有一个对象只需要使用唯一一次，就可以用匿名对象。

![image-20220403185708139](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220403185708139.png)

匿名对象作为方法的参数和返回值：

![image-20220403190532105](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220403190532105.png)

![image-20220403191320627](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220403191320627.png)



### 继承

#### 一.继承的概述

继承是多态的前提，如果没有继承，就没有多态。

继承主要解决的问题就是：共性抽取。

继承关系当中的特点：
1.子类可以拥有父类的“内容”
2.子类还可以拥有自己专属的内容

#### 二.继承的格式

在继承的关系中，“子类就是一个父类”。也就是说，子类可以被当作父类看待。
例如父类是员工，子类是讲师，那么“讲师就是一个员工”。关系：is-a

定义父类的格式：（就是一个普通的类定义）
public class 父类名称{
          //...
}

定义子类的格式：
public class 子类名称 extends 父类名称{
         //...
}

#### 三.继承中成员变量的访问特点

在父子类的继承关系当中，如果成员变量重名，则创建子类对象时，访问有两种方式：
1.直接通过子类对象访问成员变量
   等号左边是谁，就优先用谁，没有则向上找。
2.间接通过成员方法访问成员变量
   该方法属于谁，就优先用谁，没有则向上找

![image-20220318160653625](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220318160653625.png)

#### 四.子类方法中重名的三种变量

局部变量：                   直接写成员变量名
本类的成员变量：        this.成员变量名
父类的成员变量：        super.成员变量名

![image-20220318161235976](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220318161235976.png)

#### 五.继承中成员方法的访问特点

在父子类的继承关系当中，创建子类对象，访问成员方法的规则：
        创建的对象是谁，就优先用谁，如果没有则向上找。（new的谁，运行的就是谁。也就是看右侧是谁）

注意事项：
无论是成员方法还是成员变量，如果没有都是向上找父类，绝不会向下找子类的。

#### 六.继承中方法的覆盖重写

重写（Override）

概念：在继承关系中，方法的名称一样，参数列表也一样

重写（Override）：方法的名称一样，参数列表【也一样】。也叫覆盖、覆写
重载（Overload）：方法的名称一样，参数列表【不一样】。

方法的覆盖重写特点：创建的是子类对象，则优先用这类方法。

方法覆盖重写的注意事项：
1.必须保证父子类之间方法的名称相同，参数列表也相同。
@Override：写在方法前面，用来检测是不是有效的正确覆盖重写。
这个注解就算不写，只要满足 要求，也是正确的方法覆盖重写。

2.子类方法的返回值必须【小于等于】父类方法的返回值范围。
java.lang.Object类是所有类的公共最高父类（祖宗类），java.lang.String就是Object的子类。

3.子类方法的权限必须【大于等于】父类方法的权限修饰符。
小扩展提示：public>protected>(default)>private
备注：（default）不是关键字default，而是什么都不写，留空。

#### 七.继承中构造方法的访问特点

继承关系中，父子类构造方法的访问特点：
1.子类构造方法当中有一个默认隐含的“super()”调用，所以一定是先调用的父类构造，后执行的子类构造

![image-20220318165141272](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220318165141272.png)

2.子类构造可以通过super关键字来调用父类重载构造

![image-20220318165517421](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220318165517421.png)

![image-20220318165550995](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220318165550995.png)

3.super的父类构造调用，必须是子类构造方法的第一个语句。不能一个子类构造调用多次super构造。

![image-20220318165948000](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220318165948000.png)

![image-20220318172517957](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220318172517957.png)

总结：“
子类必须调用父类构造方法，不写则赠送super()；写了则用写的指定的super调用，super只能有一个，还必须是第一个。

#### 八.super关键字的三种用法

super关键字的用法有三种：
1.在子类的成员方法中，访问父类的成员变量。
2.在子类的成员方法中，访问父类的成员方法。
3.在子类的构造方法中，访问父类的构造方法。

#### 九.this关键字的三种用法

super关键字用来访问父类内容，而this关键字用来访问本类内容。用法也有三种：

1.在本类的成员方法中，访问本类的成员变量。
2.在本类的成员方法中，访问本类的另一个成员方法。（强调作用）
3.在本类的构造方法中，访问本类的另一个构造方法。
在第三种用法当中要注意：
1).this(...)调用也必须是构造方法的第一个语句，唯一一个。
2).super和this两种构造调用，不能同时使用。

![image-20220318201239800](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220318201239800.png)

#### 十.Java继承的三个特点

Java语言是单继承的，一个类的直接父类只能有唯一一个。

Java语言可以多级继承。如：我有一个父亲，我父亲还有一个父亲，也就是爷爷。

一个子类的直接父类是唯一的，但是一个父类可以拥有很多个子类。如：可以有很多兄弟姐妹



### 抽象

如果父类当中的方法不确定如何进行{}方法体实现，那么这就应该十一个抽象方法。

#### 一.抽象方法和抽象类的格式

抽象方法：就是加上abstract关键字，然后去掉大括号，直接分号结束。
抽象类：抽象方法所在的类，必须是抽象类才行，在class之前写上abstract即可。

![image-20220318202545405](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220318202545405.png)

#### 二.抽象方法和抽象类的使用

如何使用抽象类和抽象方法；
1.不能直接创建new抽象类对象。
2.必须用一个子类来继承抽象父类。
3.子类必须覆盖重写抽象父类当中所有的抽象方法。
   覆盖重写（实现）：子类去掉抽象方法的abstract关键字，然后补上方法体大括号。
4.创建子类对象进行使用。

#### 三.抽象方法和抽象类的注意事项

1.抽象类不能创建对象，如果创建，编译将无法通过而报错。只能创建其非抽象子类的对象

2.抽象类中，可以有构造方法，是供子类创建对象时，初始化父类成员使用的。

3.抽象类中，不一定包含抽象方法，但是有抽象方法的类必定是抽象类。
   这样，没有抽象方法的抽象类，也不能直接创建对象，在一些特殊场景下有用途。

4.抽象类的子类，必须重写抽象父类中所有的抽象方法，否则编译无法通过而报错，除非该子类也是抽象类。



### 接口

接口就是一种公共的规范标准。

#### 一.接口的定义基本格式

接口就是多个类的公共规范。
接口是一种引用数据类型，最重要的内容就是其中的：抽象方法。

如何定义一个接口的格式：
public interface 接口名称{
          ///接口内容
}

备注：换成了关键字 interface之后，编译生成的字节码文件仍然是：java -->.class

如果是Java7，那么接口中可包含的内容有：
1.常量
2.抽象方法

如果是Java8，还可以额外包含有：
3.默认方法
4.静态方法

如果是Java9，还可以额外包含有：
5.私有方法

#### 二.接口的抽象方法定义

在任何版本的Java中，接口都能定义抽象方法。

格式：
public abstract 返回值类型 方法名称(参数列表);

注意事项：
1.接口当中的抽象方法，修饰符必须是两个固定的关键字：public abstract
2.这两个关键字修饰符，可以选择性的省略。
3.方法的三要素，可以随意定义。

#### 三.接口的抽象方法使用

接口使用步骤：
1.接口不能直接使用，必须有一个“实现类”来“实现”该接口。

格式：
public class 实现类名称 implements 接口名称 {
           //...
}
2.接口的实现类必须覆盖重写（实现）接口中所有的抽象方法。
实现：去掉abstract关键字，加上方法体大括号。
3.创建实现类的对象，进行使用。

注意事项：
如果实现类并没有覆盖重写接口中所有的抽象方法，那么这个实现类自己就必须是抽象类。

#### 四.接口的默认方法定义与使用

##### 1.定义：

从Java8开始，接口里允许定义默认方法。

格式：
public default 返回值类型 方法名称(参数列表){
        方法体
}

备注：接口当中的默认方法，可以解决接口升级的问题。

##### 2.使用：

1.接口的默认方法，可以通过接口实现类对象，直接调用。
2.接口的默认方法，也可以被接口实现类进行覆盖重写。

![image-20220319105609339](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220319105609339.png)

#### 五.接口的静态方法定义与使用

##### 1.定义

从Java8开始，接口里允许定义静态方法。

格式：
public static 返回值类型 方法名称(参数列表){
        方法体
}
提示：就是将abstract或者default换成static即可，带上方法体。

##### 2.使用

注意事项：不能通过接口实现类的对象来调用接口当中的静态方法
正确用法：通过接口名称，直接调用其中的静态方法。

格式：
接口名称.静态方法名(参数);

![image-20220319113612801](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220319113612801.png)

#### 六.接口的私有方法定义与使用

问题描述:
我们需要抽取一个共有方法，用来解决两个默认方法之间重复代码的问题。
但是这个共有方法不应该让实现类使用，应该是私有化的。

解决方案：
从Java9开始，接口当中允许定义私有。
1.普通私有方法，解决多个默认方法之间重复代码问题
格式：
private 返回值类型 方法名称(参数列表){
            方法体
}

2.静态私有方法，解决多个静态方法之间重复代码问题
格式：
private static 返回值类型 方法名称(参数列表){
            方法体
}

![image-20220319121347161](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220319121347161.png)

![image-20220319121406945](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220319121406945.png)

#### 七.接口的常量定义与使用

##### 1.定义

接口当中也可以定义“成员变量”，但必须使用public static final三个关键字进行修饰
从效果上看，这其实就是接口的【常量】。

格式：
public static final 数据类型 常量名称 = 数据值
备注：
一旦使用final关键字进行修饰，说明不可改变。

注意事项：
1.接口当中的常量，可以省略public static final，注意：不写也照样是这样。
2.接口当中的常量，必须进行赋值，不能不赋值。
3.接口中常量的名称，使用完全大写的字母，多个单词用下划线进行分隔。（推荐命名规则）

##### 2.使用

格式：
接口名称.常量名称

![image-20220319121226197](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220319121226197.png)

#### 八.继承父类并实现多个接口

使用接口的时候，需要注意：
1.接口时没有静态代码块或者构造方法的。
2.一个类的直接父类是唯一的，但是一个类可以同时实现多个接口。
格式：
public class MyInterfaceImpl implements MyInterfaceA,MyInterfaceB{
          //覆盖重写所有抽象方法
}
3.如果实现类所实现的多个接口当中，存在重复的抽象方法，那么只需要覆盖重写一次即可。
4.如果实现类没有覆盖重写所有接口当中的所有抽象方法，那么实现类就必须是一个抽象类。
5.如果实现类所实现的多个接口当中，存在重复的默认方法，那么实现类一定要对冲突的默认方法进行覆盖重写。
6.一个类如果直接父类当中的方法，和接口当中的默认方法产生了冲突，优先用父类当中的方法。（优先级是父类高于接口）

#### 九.接口之间的多继承

1.类与类之间是单继承的。直接父类只有一个。
2.类与接口之间是多实现的。一个类可以实现多个接口。
3.接口与接口之间是多继承的。

注意事项：
1.多个父接口当中的抽象方法如果重复，没关系。
2.多个父接口当中的默认方法如果重复，哪门子接口必须进行默认方法的覆盖重写，【而且带着default关键字】





### 多态

一个对象拥有多种形态，这就是：对象的多态性

extends继承或者implements实现，是多态性的前提。

#### 一.多态的格式与使用

代码当中体现多态性，其实就是一句话：父类引用指向子类对象。

格式：             （左父右子）
父类名称 对象名 = new 子类名称();
或者：
接口名称 对象名 = new 实现类名称();

#### 二.多态中<u>成员变量</u>的使用特点

访问成员变量的两种方式：
1.直接通过对象名称访问成员变量：看等号左边是谁，优先用谁，没有则向上找。
2.间接通过成员方法访问成员变量：看该方法属于谁，优先用谁，没有则向上找。

![image-20220320192009088](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220320192009088.png)

![image-20220320192031191](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220320192031191.png)

![image-20220320191904883](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220320191904883.png)

#### 三.多态中<u>成员方法</u>的使用特点

在多态的代码中，成员方法的访问规则是：
          看new的是谁，就优先用谁，没有则向上找。

![image-20220320192658351](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220320192658351.png)

口诀：编译看左边，运行看右边。

对比一下：
成员变量：编译看左边，运行还看左边。
成员方法：编译看左边，运行看右边。

![image-20220320192831220](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220320192831220.png)

#### 四.使用多态的好处

![image-20220320193100746](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220320193100746.png)



#### 五.对象的向上转型 

对象的向上转型，就是：父类引用指向子类对象。
向上转型一定是安全的，没有问题。但也有一个弊端：对象一旦向上转型为父类，那么就无法调用子类原本特有的内容。

解决方案：用对象的向下转型【还原】。

![image-20220321095032725](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220321095032725.png)

![image-20220321095118340](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220321095118340.png)

#### 六.对象的向下转型 

![image-20220321100434641](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220321100434641.png)

![image-20220321100505007](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220321100505007.png)

#### 七.向下转型用instanceof关键字进行类型判断

向下转型时如何才能知道一个父类引用对象，本来是什么子类？

格式：
对象 instanceof 类名称
这将会得到一个boolean值结果，也就是判断前面的对象能不能当做后面的类型的实例。

![image-20220321102214681](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220321102214681.png)

![image-20220321102302569](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220321102302569.png)

### 其他

#### 一.final关键字

final关键字代表最终的、不可改变的。

##### 1.final关键字的概念与四种用法

常见的四种用法：
1.可以用来修饰一个类
2.可以用来修饰一个方法
3.可以用来修饰一个局部变量
4.可以用来修饰一个成员变量

##### 2.final关键字用来修饰类

当final关键字用来修饰一个类的时候，格式：
public final class 类名称 {
           //...
}

含义：当前这个类不能有任何的子类。（太监类：有父类无子类）
注意：一个类如果是final的，那么其中所有的成员方法都无法进行覆盖重写（因为没儿子）。
           一个final类可以对自己父类的方法进行覆盖重写。

##### 3.final关键字用来修饰成员方法

当final关键字用来修饰一个方法的时候，这个方法就是最终方法，也就是不能被覆盖重写。

格式：
修饰符 final 返回值类型 方法名称 (参数列表){
           // 方法体
}

对于类、方法来说，abstract关键字和final关键字不能同时使用，因为矛盾。

##### 4.final关键字用来修饰局部变量

一旦使用final用来修饰局部变量，那么这个变量就不能进行更改 。
”一次赋值，终生不变“

![image-20220321105215494](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220321105215494.png)

对于基本类型来说，不可变说的是变量当中的数据不可改变
对于引用类型来说，不可变说的是变量当中的地址值不可改变

![image-20220321105344453](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220321105344453.png)

##### 5.final关键字用来修饰成员变量

对于成员变量来说，如果使用final关键字修饰，那么这个变量也照样是不可变。

1.由于成员变量具有默认值，所以用了final之后必须手动赋值，不会再给默认值了。
2.对于final的成员变量，要么使用直接赋值，要么通过构造方法赋值。二者选其一。
3.必须保证类当中所有重载的构造方法，都最终会对final的成员变量进行赋值。

#### 二.四种权限修饰符

Java中有四种发权限修饰符：
                                  public   >    protected    >     (default)      >      private
同一个类                    yes             yes                     yes                    yes
同一个包                    yes             yes                     yes                    no
不同包子类                yes             yes                     no                      no
不同包非子类             yes            no                       no                      no   

注意事项：（default）并不是关键字，而是什么都不写

#### 三.内部类

如果一个事物的内部包含另一个事物，那么这就是一个类内部包含一个类。
例如：身体和心脏的关系。又如：汽车和发动机的关系。

分类：
1.成员内部类
2.局部内部类（包含匿名内部类）

##### 1.成员内部类的定义

格式：
修饰符 class 类名称{
         修饰符 class 内部类名称{
                  // ...
          }
          // ...
}

注意：内用外，随意访问；外用内，需要内部类对象。

##### 2.成员内部类的使用

1.间接方式：在外部类的方法当中，使用内部类，然后main只调用外部类方法。
2.直接方式，公式：
平时创建对象是：类名称 对象名 = new 类名称
而内部类是【外部类名称.内部类名称 对象名 = new 外部类名称().new 内部类名称();】

##### 3.内部类的同名变量访问

如果出现了重名现象，那么格式是：外部类名称.this.外部类成员变量

![image-20220330203930591](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220330203930591.png)

##### 4.局部内部类的定义

如果一个类是定义在一个方法内部的，那么这就是一个局部内部类
"局部"：只有当前所属的方法才能使用他，出了这个方法外面就不能用了

定义格式：
修饰符 class 外部类名称{
          修饰符  返回值类型  外部类方法名称(参数列表){
                     class 局部内部类名称{
                            //...
                     }
          }
}

类的权限修饰符：
public > protected  > (default) > private
定义一个类的时候，权限修饰符规则：
1.外部类：public / （default）
2..成员内部类：public / protected / （default） / private
3.局部内部类：什么都不能写

##### 5.局部内部类的final问题

局部内部类，如果希望访问所在方法的局部变量，那么这个局部变量必须是【有效final的】

备注：从java8+开始，只要局部变量不变，那么final关键字可以省略。

原因：
1.new出来的对象在堆内存当中。
2.局部变量是跟着方法走的，在栈内存当中。
3.方法运行结束之后，立刻出栈，局部变量就会立刻消失
4.但是new出来的对象会在堆当中持续存在，直到垃圾回收消失

##### 6.匿名内部类

如果接口的实现类（或者是父类的子类）只需要使用唯一一次，那么这种情况下就可以省略掉该类的定义，而改为使用【匿名内部类】

匿名内部类的定义格式：
接口名称 对象名 = new 接口名称(){
        //覆盖重写所有抽象方法
};

使用匿名内部类，都不用实现类了，最后别忘了大括号结尾有分号。

![image-20220330213035284](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220330213035284.png)

##### 7.匿名内部类的注意事项：

对格式 “new 接口名称(){...}” 进行解析：
1.new代表创建对象的动作	
2.接口名称就是匿名内部类需要实现哪个接口
3.{...}这才是匿名内部类的内容

另外还要注意几点问题：
1.匿名内部类，在【创建对象】的时候，只能使用唯一一次。
   如果希望多次创建对象，而且类的内容一样的话，那么就必须使用单独定义的实现类了。
2.匿名对象，在【调用方法】的时候，只能调用唯一一次。
   如果希望同一个对象，调用多次方法，那么必须给对象起个名字
3.匿名内部类是省略了【实现类/子类】，但是匿名对象是省略了【对象名称】
   强调：匿名内部类和匿名对象不是一回事！！！

![image-20220330214842968](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220330214842968.png)

![image-20220330215436259](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220330215436259.png)



##### 8.类作为成员变量类型

成员变量不光能用基本类型，还可以用任何一种类class



#### 四.object类的方法

java.lang.Object

类 `Object` 是类层次结构的根类(最顶层的类)。每个类都使用 `Object`  作为超类(父类)。所有对象（包括数组）都实现这个类的方法。 

##### 1.toString方法

创建的类默认继承了Object类，所以可以使用Object类中的toString方法
String toString()    返回该对象的字符串表示。

直接打印对象的名字，其实就是调用对象的toString方法 p = p.toString();
打印出来的是对象的地址值
直接打印对象的地址值没有意义，需要重写Object类中的toString方法

看一个类是否重写了toString方法，直接打印这个类对应对象的名字即可
如果没有重写，那么打印的就是对象的地址值（默认）
如果重写了，纳闷就按照重写的方式打印



##### 2.equals方法

###### 1）.定义

创建的类默认继承了Object类，所以可以使用Object类中的equals方法
boolean equals(Object obj)   指示其他某个对象是否与此对象"相等"。

Object类equals方法的源码：
public boolean equals(Object obj){
        return (this == obj);
}

![image-20220331222658425](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220331222658425.png)

###### 2）.重写equals方法

Object类的equals方法默认比较的是两个对象的地址值，没有意义
所以需要重写equals方法，比较两个对象的属性值
对象的属性值一样，返回true ，否则返回false

问题：
隐含着一个多态
Object obj = p2 = new person(张三,18)       //姓名张三，年龄18
多态弊端：无法使用子类特有的内容（属性，方法）
解决：可以使用向下转型（强转）把Object类型装换为Person

null是不能调用方法的，会抛出空指针异常



#### 五.StringBuilder

1.原理 ：

String类：
字符串是常量，他们的值在创建后不能更改 。
字符串的底层是一个被final修饰的数组，不能改变，是一个常量

StringBuilder类：
字符串缓冲区，可以提高字符串的操作效率（看成一个长度可以变化的字符串）
底层也是一个数组，但是没有被final修饰，可以改变长度
byte[]  value = new byte[16];

StringBuilder在内存中始终是一个数组，占用空间少，效率高 
如果超出了StringBuilder的容量，会自动扩容 

2.StringBuilder的构造方法

构造方法：
Public StringBuilder()：构造一个空的StringBuilder容器。
Public StringBuilder(String  str)：构造一个StringBuilder容器，并将字符串添加进去。

3.StringBuilder类的append方法 

StringBuilder类的成员方法：
public StringBuilder append(...)：添加任意类型数据的字符串形式，并返回当前对象自身。
参数：可以是任意的数据类型

使用append方法往StringBuilder中添加数据
append方法返回的是this

![image-20220404101242444](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220404101242444.png)

简单写法：链式编程：方法的返回值是一个对象，可以根据对象继续调用方法

![image-20220404101430919](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220404101430919.png)

4.StringBuilder类的toString方法

StringBuilder和String可以互相转换：
      String -> StringBuilder：可以使用StringBuilder的构造方法
                 StringBuilder(String  str)：构造一个字符串生成器，并初始化为指定的字符串内容
      StringBuilder -> String：可以使用StringBuilder中的toString方法
                  public String toString()：将当前 StringBuildr对象转换为String对象

#### 六.包装类

基本数据类型的数据，使用起来非常的方便，但是没有对应的方法来操作这些数据
所以我们可以使用一个类，把基本类型的数据包装起来，这个类就叫包装类 
在包装类中可以定义一些方法，用来操作基本类型的数据

1.装箱与拆箱

装箱：把基本类型的数据，包装到包装类中（基本类型的数据 - > 包装类）
           构造方法：
                      Integer(int value)：构造一个新分配的 `Integer` 对象，它表示指定的 `int` 值。
                      Integer(String s)：构造一个新分配的 `Integer` 对象，它表示 `String` 参数所指示的 `int`  值。
                           第二个构造方法传递的是字符串，必须是基本类型的字符串，否则会抛出异常。”100“正确， ”a“抛异常
           静态方法：
                      Static Integer valueOf(int i)：返回一个表示指定的 `int` 值的 `Integer` 实例。
                      Static Integer valueOf(String s)：返回保存指定的 `String` 的值的 `Integer` 对象。

拆箱：在包装类中取出基本类型的数据（包装类 - >  基本类型的数据 ）
           成员方法：int intValue()：以 `int` 类型返回该 `Integer` 的值。

2.自动装箱与自动拆箱

基本类型的数据和包装类之间可以自动的相互转换
JDK1.5之后出现的新特性

自动装箱：直接把int类型的整数型赋值给包装类
                  Integer in = 1   ：就相当于Integer in = new Integer(1):

自动拆箱：in是包装类，无法直接参与运算，可以自动转换为基本类型的数据，在参与计算
                  in + 2 ：就相当于in.intvalue() + 3 = 3;
                  in = in + 2 ：就相当于in = new Integer(3) 自动装箱

3.基本类型与字符串类型之间的相互转换

基本类型 -> 字符串
         1.基本类型数据的值+" "      （直接加空字符串），最简单的方式（工作中常用）
         2.使用包装类中的静态方法
                     static String toString(int i) 返回一个表示指定整数的String对象。
         3.使用String类中的静态方法
                     static String valueOf(int i) 返回int参数的字符串表示形式。
字符串 -> 基本类型
         使用包装类的静态方法parseXX( "字符串")
                     Integer类：static int parseInt(String s)
                     Double类：static double parseDouble(String s)
                     ...



#### 七.Junit单元测试

测试分类：
        1.黑盒测试：不需要写代码，给输入值期望的值
        2.白盒测试：需要写代码。关注程序具体的执行流程

Junit使用：白盒测试
           步骤：
                    1.定义一个测试类（测试用例）
                                  建议：-测试类名：被测试的类名Test          如CalculatorTest
                                             -包名：xxx.xxx.xx.test              如com.yc.test
                    2.定义测试方法：可以独立运行
                                  建议：-方法名：test测试的方法名           如testAdd()
                                             -返回值：void
                                             -参数列表 ：空参
                    3.给方法加@Test
                    4.导入junit依赖环境

判定结果：（看运行结果的颜色）
        红色：失败
        绿色：成功
        一般我们使用断言操作来处理结果
                   Assert.assertEquals（期望的结果，运行的结果）;

![image-20220506105447363](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220506105447363.png)

![image-20220506105530107](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220506105530107.png)



  补充：
          @Before：
                    修饰的方法会在测试方法之前被自动执行
          @After：
                    修饰的方法会在测试方法执行之后自动被执行（即使方法出现异常，该方法依然会被执行）

![image-20220506113556012](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220506113556012.png)

![image-20220506113702209](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220506113702209.png)





### 反射

#### 一.概述

反射：框架设计的灵魂
           框架：半成品软件。可以在框架的基础上进行软件的开发，简化编码
           概念：将类的各个组成部分封装成其他对象，这就是反射机制
                    好处：
                                 1.可以在程序运行过程中，操作这些对象。
                                 2.可以解耦，提高程序的可扩展性。

<img src="https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220506115549597.png" alt="image-20220506115549597"  />



#### 二.Class对象功能

##### 1.获取Class对象的方式：      

​         三种方式对应着上图中的三个阶段

​         1.Class.forName（“全类名”）：将字节码文件加载进内存，返回Class对象
​                    多用于配置文件，将类名定义在配置文件中。读取文件，加载类

​         2.类名.class：通过类名的属性class获取
​                    多用于参数的传递

​         3.对象.getClass（）：getClass（）方法在object类中定义着
​                    多用于对象的获取字节码的方式

用==比较三个对象，都是ture
结论：同一字节码文件（*.class）在一次程序运行过程中，只会被加载一次，不论通过哪一种方式获取的Class对象都是同一个。

##### 2.Class对象功能

获取功能：（以下方法中：不带Declared只能获取公共的； 带Declared不考虑修饰符，什么都能获取到，若要获取私有的，需要暴力反射）
         1.获取成员变量们
                Field[] getFields()：获取所有public修饰的成员变量
                Field getField(String name)：获取指定名称的 public修饰的成员变量

​                Field[] getDeclaredFields()：获取所有的成员变量，不考虑修饰符
​                Field getDeclaredFields(String name)

​         2.获取构造方法们
​                Constructor<?>[] getConstructors()
​                Constructor<T> getConstructor(Class<?>... parameterTypes)

​                Constructor<T> getDeclaredConstructor(Class<?>... parameterTypes) 
​                Constructor<?>[] getDeclaredConstructors() 

​         3.获取成员方法们
​                Method[] getMethods()  
​                Method getMethod(String name, Class<?>... parameterTypes)  

​                Method[] getDeclaredMethods() 
​                Method getDeclaredMethod(String name, Class<?>... parameterTypes) 

​         4.获取类名
​                String getName()  



1.Field：成员变量
         操作：
                  1.设置值
                            void set(Object obj, Object value)
                  2.获取值
                            object get(Object obj)
                  3.忽略访问权限修饰符的安全检查（因为私有的是不能被访问的）
                            setAccessible(true);  ：暴力反射

2.Constructor：构造方法
         创建对象：
                   T newInstance(Object... initargs)
                   如果使用空参数构造方法创建对象，操作可以简化：Class对象的newInstance方法

3.Method：方法对象
         执行方法：
                   Object invoke(Object obj, Object... args)
         获取方法名称：
                   String getName：获取方法名



#### 三.案例

需求：写一个”框架“，不能改变该类的任何代码的前提下，可以帮我们创建任意类的对象，并且执行其中任意方法
          实现：
                    1.配置文件
                    2.反射
          步骤：
                    1.将需要创建的对象的全类名和需要执行的方法定义在配置文件中
                    2.在程序中加载读取配置文件
                    3.使用反射技术来加载类文件进内存
               	 4.创建对象
                    5.执行方法

以后看到配置文件里边有的地方使用了全类名，第一时间应该知道 用的是反射





### 注解

#### 一.概念

注释概念：用文字描述程序的。给程序员看的
注解概念：说明程序的。给计算机看的

定义：注解（Annotation），也叫元数据。一种代码级别的说明。它是JDK1.5及以后版本引入的一个特性，与类、接口、枚举是在同一个层次。它可以声明在包、类、字段、方法、局部变量、方法参数等的前面，用来对这些元素进行说明，注释。

概念描述：
JDK1.5之后的新特性
说明程序的

作用分类：
1.编写文档：通过代码里标识的注解生成为文档【生成文档doc文档】
2.代码分析：通过代码里标识的注解对代码进行分析【使用反射】
3.编译检查：通过代码里标识的注解让编译器能够实现基本的编译检查【Override】

#### 二.JDK内置注解

JDK中预定义的一些注解
@Override：检测被该注解标注的方法是否是继承自父类（接口）的
@Deprecated：该注解标注的内容，表示已过时
@SuppressWarnings：压制警告        *一般传递参数all    @SuppressWarnings("all")

#### 三.自定义注解

1.格式：
             元注解
             public @interface 注解名称{
                          属性列表;
             }

2.本质：注解本质上就是一个接口，该接口默认继承Annotation接口
              public interface MyAnno extends java.lang.annotation.Annotation{}    //MyAnno是自己定义的注解名称

3.属性：接口中的抽象方法
          要求：
                    1.属性的返回值类型有下列取值
                               基本数据类型
                               String
                               枚举
                               注解
                               以上类型的数组

​                    2.定义了属性，在使用时需要给属性赋值
​                              1）.如果定义属性时，使用default关键字给属性默认初始值，则使用注解时，可以不进行属性的赋值
​                              2）.如果只有一个属性需要赋值，并且属性的名称是value，则value可以省略，直接定义值即可
​                              3）.数组赋值时，值使用{}包裹。如果数组中只有一个值，则{}省略

4.元注解：用于描述注解的注解
		*@Target：描述注解能够作用的位置
				*ElementType取值：
						*TYPE：可以作用于类上
						*METHOH：可以作用于方法上
						*FIELD：可以作用于成员变量上*
		*@Retention：描述注解被保留的阶段
				*@Retention(RetentionPolicy.RUNTIME)：当前被描述的注解，会保留到class字节码文件中，并被JVM读取到
		*@Documented：描述注解是否被抽取到api文档中
		*@Inherited：描述注解是否被子类继承

#### 四.注解解析

在程序使用（解析）注解：获取注解中定义的属性值
		1.获取注解定义的位置的对象（Class，Method，Field）
		2.获取指定的注解
				*getAnnotation（Class）

```java
//其实就是在内存中生成了一个该注解接口的子类实现对象
public class ProImpl implements Pro{
		public String className(){
				return "cn.yc.annotation.Demo1";
		}
		public String methodName(){
				return "show";
		}
}
```

​		3.调用注解中的抽象方法获取配置的属性值

小结：
		1.以后大多数时候，我们会使用注解，而不是自定义注解
		2.注解给谁用？
				1）.编译器
				2）.解析程序
		3.注解不是程序的一部分，可以理解为注解就是一个标签





### XML

1.概念
2.语法
3.解析

#### 一.概念

1.概念：Extensible Markup Language可扩展标记语言
         *可扩展：标签都是自定义的。

2.功能
         *存储数据
                  1.配置文件
                  2.在网络中传输 

3.xml与html的区别
        1.xml标签都是自定义的，html标签是预定义的
        2.xml的语法严格，html语法松散的
        3.xml是存储数据的，html是展示数据

*注：w3c：万维网联盟（xml和html的父亲）

#### 二.语法

1.基本语法：
       1）.xml文档的后缀名   .xml
       2）.xml第一行必须定义为文档声明
       3）.xml文档中有且只有一个根标签
       4）.属性值必须使用引号（单双都可）引起来    （html不用引号）
       5）.标签必须正确关闭
       6）.xml标签名称区分大小写     （html不区分）

2.快速入门：
<?xml version='1.0' ?>

<users>

```xml
       <user id='1'>
               <name>zhangsan</name>
               <age>23</age>
               <gender>male</gender>
       </user>

       <user id='2'>
               <name>lisi</name>
               <age>24</age>
               <gender>female</gender>
       </user>
```

</users>

3.组成部分：
          1）.文档声明
                      (1).格式：<?xml 属性列表 ？>
                      (2).属性列表：
                                  *version：版本号
                                  *encoding：编码方式。告知解析引擎当前文档使用的字符集，默认值：ISO-8859-1
                                  *standalone：是否独立。取值有两个：yes：不依赖其他文件；no：以来其他文件

​          2）.指令（了解）：结合CSS的
​          3）.标签：标签名称自定义的
​                           规则：*名称可以含字母、数字以及其他的字符
​                                    *名称不能以数字或者标点符号开始
​                                    *名称不能以字符 “xml”（或者 XML、Xml）开始
​                                    *名称不能包含空格

​          4）.属性：id属性值唯一
​          5）.文本：
​                           CDATA区：在该区域中的数据会被原样展示
​                                     格式：`<![CDATA[ 数据 ]]>`

![image-20220505112251513](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220505112251513.png)



#### 三.约束

1.约束：规定xml文档的书写规则
              作为框架的使用者（程序员）：
                    1.能够在xml中引入约束文档
                    2.能够简单的读懂约束文档

![image-20220505113340228](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220505113340228.png)



2.分类：
         1.DTD：一种简单的约束技术
         2.Schema：一种复杂的约束技术

DTD：
       引入dtd文档到xml文档中
               内部dtd：将约束规则定义在xml文档中
               外部dtd：将约束规则定义在外部 的dtd文件中
                         本地：`<!DOCTYPE 根标签名 SYSTEM "dtd文件位置">`
                         网络：`<!DOCTYPE 根标签名 PUBLIC "dtd文件名字" "dtd文件的位置URL">`

Schema：
         1.填写xml文档的根元素
         2.引入xsi前缀（好多取值）      
                    xmlns:xsi=http://www.w3.org/2001/XMLSchema-instance
         3.引入xsd文件命名空间（后边的是schema文档的路径，前边的是给这个路径起了个名字，称为命名空间） 
                    xsi:schemaLocation="http://www.itcast.cn/xml   student.xsd"
         4.为每一个xsd约束声明一个前缀，作为标识       xmls="http://www.itcast.cn/xml"

![image-20220505141308165](https://raw.githubusercontent.com/chocman99/Image/main/JavaSE/image-20220505141308165.png)





#### 四.解析



解析：操作xml文档，将文档中的数据读取到内存中
        *操作xml文档
                 1.解析（读取）：将文档中的数据读取到内存中
                 2.写入：将内存中的数据保存到xml文档中。持久化的存储

​        *解析xml的方式：
​                 1.DOM：将标记语言文档一次性加载进内存，在内存中形成一颗dom树
​                           优点：操作方便，可以对文档进行CRUD（增删改查）的所有操作
​                           缺点：占内存
​                 2.SAX：逐行读取，基于事件驱动的
​                           优点：不占内存
​                           缺点：只能读取，不能增删改

​        *xml常见的解析器：
​                 1.JAXP：sun公司提供的解析器，支持dom和sax两种思想
​                 2.DOM4J：一款非常优秀的解析器
​                 3.Jsoup：jsoup 是一款Java 的HTML解析器，可直接解析某个URL地址、HTML文本内容。它提供了一套非常省力的API，可通过DOM，CSS以及类似于jQuery的操作方法来取出和操作数据。
​                 4.PULL：Android操作系统内置的解析器，sax方式的



Jsoup快速入门：
         步骤：
                 1.导入jar包
                 2.获取Document对象
                 3.获取对应的标签Element对象
                 4.获取数据

​         代码：

```java
public static void main(String[] args) throws IOException {
    //2.获取Document对象，根据xml文档获取
    //2.1获取student.xml的path
    String path = JsoupDemo1.class.getClassLoader().getResource("student.xml").getPath();
    //2.2解析xml文档，加载文档进内存，获取dom树---->Document
    Document document = Jsoup.parse(new File(path), "utf-8");
    //3.获取元素对象Element
    Elements elements = document.getElementsByTag("name");

    //查看长度
    System.out.println(elements.size());
    //3.1获取第一个name的Element对象
    Element element = elements.get(0);
    //3.2获取数据
    String name = element.text();
    System.out.println(name);

}
```

代码中对象的使用：
         1.Jsoup：工具类，可以理解html或xml文档，返回Document
                   *parse：解析html或xml文档，返回Document
                             *parse(File in,String charseName)：解析xml或html文件的
                             *parse(String html)：解析xml或html字符串
                             *parse(URL url,int timeoutMillis)：通过网络路径获取指定的html或xml的文档对象

​         2.Document：文档对象。代表内存中的dom树
​                   *获取Element对象
​                             *getElementsById(String id)：根据id属性值获取唯一的element对象
​                             *getElementsByTag(String tagName)：根据标签名称获取元素对象集合
​                             *getElementsByAttribute(String key)：根据属性名称获取元素对象集合
​                             *getElementsByAttributeValue(String key,String value)：根据对应的属性名和属性值获取元素对象的集合

​         3.Elements：元素Element对象的集合。可以当作ArrayList<Element>来使用

​         4.Element：元素对象
​                   *获取子元素标签
​                             *getElementsById(String id)：根据id属性值获取唯一的element对象
​                             *getElementsByTag(String tagName)：根据标签名称获取元素对象集合
​                             *getElementsByAttribute(String key)：根据属性名称获取元素对象集合
​                             *getElementsByAttributeValue(String key,String value)：根据对应的属性名和属性值获取元素对象的集合
​                   *获取属性值
​                             *String attr(String key)：根据属性名称获取属性值
​                   *获取文本内容
​                             *String text()：获取所有子标签的纯文本内容
​                             *String html()：获取标签体的所有内容（包括子标签的标签和文本内容）

​         5.node：节点对象 
​                   *是Document和 Element的父类



快捷查询方式：
           1.selector：选择器
                  使用方法：Elements         select(String cssQuery)
                             语法：参考Selector类中定义的语法

​           2.XPath：XPath即为XML路径语言（XML Path Language），它是一种用来确定XML（标准通用标记语言的子集）文档中某部分位置的语言。
​                  使用Jsoup的Xpath需要额外导入jar包
​                  使用w3cschool参考手册，使用xpath的语法完成查询







