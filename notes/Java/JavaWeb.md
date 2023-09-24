### HTML

#### 一.HTML中的基础标签

HTML能决定页面上展示哪些内容

html语言是解释型语言，不是编译型
浏览器是容错的

##### 1）`<html></html>`

html页面中由一对标签组成：`<html></html>`

`<html>`  称之为开始标签 
`</html>`称之为结束标签

##### 2）`<title></title>`

`<title></title>`表示网页的标题 

![image-20220417151137976](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417151137976.png)

![image-20220417151150384](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417151150384.png)

##### 3）`<meta>`

可以在`<meta>`标签中设置编码格式 

![image-20220417172745339](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417172745339.png)

##### 4）`<br/>`

`<br/>`表示换行。br标签是一个单标签。单标签：开始标签和结束标签是同一个，斜杠放在 单词 后面

![image-20220417151104791](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417151104791.png)

![image-20220417151115501](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417151115501.png)

##### 5）`<p></p>`

`<p></p>`表示段落标签

##### 6）`<img/>`

`<img/>`图片标签 
         src属性表示图片的文件路径
         width和height表示图片大小
         alt表示图片的提示

![image-20220417151006617](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417151006617.png)

##### 7）路径问题：

​     1.相对路径
​     2.绝对路径

##### 8）h1~h6

h1~h6：标题标签（标题一到标题六 ） 
`<h1></h1>`：标题一
`<h2></h2>`：标题二
...

![image-20220417150747646](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417150747646.png)![image-20220417150821636](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417150821636.png)

##### 9）`<ol></ol>` `<ul></ul>`

列表标签：
         `<ol></ol>`：有序列表
                 start 表示从几开始，type显示的类型：A ， a ， I ， i ，1
          `<ul></ul>`：无序列表
                 type显示类型：disc（default），   circle  ， square

![image-20220417150512835](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417150512835.png)![](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417150522518.png)



![image-20220417150634895](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417150634895.png)![image-20220417150642866](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417150642866.png)



##### 10）字体标签ubi

​         u：下划线 
​         b：加粗  
​         i：斜体

![image-20220411100638642](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220411100638642.png)

![image-20220417150426224](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417150426224.png)

##### 11）`<sup></sup>`和`<sub></sub>`

上标`<sup></sup>`
下标`<sub></sub>`

![image-20220417144122436](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417144122436.png)

![image-20220417144139032](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417144139032.png)

##### 12）字符实体

html中的字符实体（等等很多字符实体标签去网上搜就行）

​             小于号：`&lt;`  
​             大于等于号：`&ge;`
​             版权：`&copy`

![image-20220417144236721](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417144236721.png)

![image-20220417144300173](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417144300173.png)

##### 13）`<span></span>`

不换行的块标记
`<span></span>`

##### 14）超链接a

   a表示超链接
           href：链接的地址
           target：
                    _self：在本窗口打开
                    _blank：在一个新窗口的打开
                    _parent：在父窗口打开
                    _top：在顶层窗口打开

![image-20220417150016346](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417150016346.png)

##### 15）div层

先了解，就是一层一层的



#### 二.HTML中的table标签

表格     `<table></table>`
      行         `<tr></tr>`
      列         `<td></td>`
      表头列   `<th></th>`

​      table中有如下属性（虽然已经淘汰，但是最好了解一下）
​          border：表格边框的粗细（如果不写的话就是无表格）
​          width：表格的宽度
​          cellspacing：单元格间距
​          cellpadding：单元格填充

​      tr中有一个属性：align（对齐方式）：left（左对齐，默认），center（居中），right（右对齐）

![image-20220417174956388](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417174956388.png)

![image-20220417175018563](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417175018563.png)

rowspan：行合并
colspan：列合并

​                （在苹果的第二个标签处写上rowspan="2"，代表着两行合并）

![image-20220417182543353](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417182543353.png)

![image-20220417182732097](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417182732097.png)

​              （在最后加上一行标签写上colspan="4"，代表着四列合并）

![image-20220417182920498](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417182920498.png)

![image-20220417183104378](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220417183104378.png)



#### 三.HTML-表单标签

表单就是一个容器，他能够承载我们要发送给服务器的数据

`<form></form>`
action 表示发送的目的地。发送到哪个页面
method 表示发送方式。get方式都堆在地址栏了，不安全，且有大小限制。
                                      post方式就不会

input type="text"  表示文本框。其中name属性必须要指定(自己指定)，否则这个文本框的数据将来是不会发送给服务器的。文本框中可以有value值，文本框中输入的是什么，将来value就是什么
input type="password"  表示密码框。输入密码时是看不到的
input type="radio"  表示单选按钮。需要注意，name属性值保持一致，这样才会有互斥的效果。要加value值，因为单选按钮没法输入，所以要指定好当选中一个选项时，value值是什么。可以通过checked属性 设置成默认选中的项（实际上是checked="checked"   但当属性名和属性值相同时，可以省略属性值，直接写个属性名就行）
input type="checkbox"  表示复选框。name属性建议保持一致，这样将来我们服务器端获取值的时候获取的是一个数组
`<select></select>`表示下拉列表。每一个选项是`<option></option>`，其中value属性是发送给服务器的值，selected表示默认选中的项
`<textarea></textarea>`  表示多行文本框（或者称之为文本域）。rows是让他显示多少行(默认两行)，cols是一行多少 个字。他的value值就是开始结束标签之间的内容
input type="submit" 表示提交按钮
input type="radio" 表示重置按钮
input type="radio" 表示普通按钮

![image-20220418110759349](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220418110759349.png)

![image-20220418125353453](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220418125353453.png)



#### 四.frameset-iframe

frameset 表示页面框架，这个标签已经淘汰，了解即可
frame表示框架中的具体页面引用

![image-20220418125114791](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220418125114791.png)

![image-20220418125144625](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220418125144625.png)

iframe 在一个页面嵌入一个子页面

![image-20220418125231180](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220418125231180.png)

![image-20220418125250969](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220418125250969.png)







### CSS

#### 一.CSS语法

CSS能决定页面的美观程度

CSS英文全称为Cascading　Style　Sheet，中文译为“层叠样式表”。CSS主要是对HTML标记的内容进行更加丰富的装饰，并将网页表现样式与网页结构分离的一种样式设计语言。可以使用CSS控制HTM页面中的文本内容、图片外形以及版面布局等外观的显示样式。

1.为什么需要CSS

2.CSS最基本的分类：标签样式表、类样式表、ID样式表

![image-20220425165527487](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220425165527487.png)

3.CSS从位置上的分类：嵌入式样式表（行内样式）、内部样式表、外部样式表
               嵌入式样式表：写在一个标签的内部

![image-20220419211147639](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220419211147639.png)

​               内部样式表：

![image-20220419211205631](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220419211205631.png)

​               外部样式表：把CSS代码专门用一个文件去管理，然后再HTML页面导入这个CSS文件
​                                     在head标签中写link标签`<link>`,rel="stylesheet"是固定写法

![image-20220419211218290](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220419211218290.png)



#### 二.CSS盒子模型

1.border：边框样式
          border-width：边框粗细
          border-style：边框样式：solid（实线），dotted（点状线），...
          border-color：边框颜色
可以直接写在一起：`border:4px double blue;`

![image-20220425190322310](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220425190322310.png)

在div中可以嵌入一个div

![image-20220425190117713](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220425190117713.png)

![image-20220425190143696](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220425190143696.png)

2.margin：间距

可以设置内div在外div（父容器）中的位置
margin-top:100px;  据上边100px
margin-left:100px;  据左边100px
也可以写成一个：margin:100px;  代表着据上下左右都是100px

CSS文档中属性里外补丁里的margin有说明：
如果提供全部四个参数值，将按上－右－下－左的顺序作用于四边。
如果只提供一个，将用于全部的四边。
如果提供两个，第一个用于上－下，第二个用于左－右。
如果提供三个，第一个用于上，第二个用于左－右，第三个用于下。

![image-20220425190454443](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220425190454443.png)

![image-20220425190651513](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220425190651513.png)

3.padding：填充

也可用填充来调整内div的位置（给父容器进行填充来调整）
padding-top:50px;  上边填充50px
padding-left:50px;  左边填充50px

![image-20220425191303373](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220425191303373.png)

![image-20220425191316086](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220425191316086.png)

IE浏览器：实际尺寸+width
google浏览器：实际尺寸=width+左右border-width+padding

div在页面上布局总是上边和左边有一小块空白，可以加个body，里面设置margin:0;和padding:0;

![image-20220425185800201](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220425185800201.png)

![image-20220425185844571](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220425185844571.png)





#### 三.CSS布局

position:absolute：绝对定位，需要配合使用left，top，代表横坐标和纵坐标的像素
position:relative：相对定位，一般会和float，margin，padding....一起使用







### Javascript

#### 一.js语法快速学习

Javascript用来修饰页面的特效的（简称JS）

Javascript：客户端的一个脚本语言
js是一门弱类型的语言，变量的数据类型由后面赋的值的类型决定

alert(typeof str);
		alert()：警告框，对话框
		typeof：返回类型

Javascript大小写敏感



//当鼠标悬浮时，显示背景颜色
funtion showBGColor(){
		//event：当前发生的事件
		//event.srcElement：事件源
		alert(event.srcElement);
		alert(event.srcElement.tagName);
		if(event && event.srcElement && event.srcElement.tagName == "TD"){
				var td = event.srcElement;
				//td.parentElement 表示获取td的父元素 -> TR
				var tr = td.parentElement;
				//如果想要通过js代码设置某节点的样式，则需要加上.style
				tr.style.backgroundColor = "navy";

​				//tr.cells表示获取这个tr中的所有单元格
​				var tds = tr。cells；
​				for(var i = 0 ; i < tds.length ; i++){
​						tds[i].style.color = "white";
​				}
​		}
}

//当鼠标离开时，恢复原始样式
funtion clearBGColor(){
		if(event && event.srcElement && event.srcElement.tagName == "TD"){
				var td = event.srcElement;
				var tr = td.parentElement;
				tr.style.backgroundColor = "transparent";
				var tds = tr。cells；
				for(var i = 0 ; i < tds.length ; i++){
						tds[i].style.color = "threeddarkshadow";
				}
		}
}

//当鼠标悬浮在单价单元格时，显示手势
function showHand(){
		if(event && event.srcElement && event.srcElement.tagName == "TD"){
				var td = event.srcElement;
				//cursor：光标
				td.style.cursor = “hand”;
		}
}

//当鼠标点击单价单元格时进行价格编辑
function editPrice(){
		if(event && event.srcElement && event.srcElement.tagName == "TD"){
				var priceTD = event.srcElement;
				//目的是判断当前priceTD有子节点，而且第一个子节点是文本节点，TextNode对应的是3，ElementNode对应的是1
				if(priceTD.firstChild && priceTD.firstChild.noteType == 3){
						//innerText 表示设置或者获取当前节点的内部文本
						var oldPrice = priceTD.innerText;
						//innerHTML 表示设置当前节点的内部HTML，size设置文本框大小
						priceTD.innerHML = "<input type = 'text' size = '4'/>";
						var input  = priceTD.firstChils;
						if(input.tagName == "INPUT"){
								input.value = oldPrice;
								//选中输入框内部的文本
								input.select();
								//4.绑定输入框失去焦点事件，失去焦点，更新单价
								input.onblur = updatePrice;

​								//在输入框上绑定键盘摁下的事件，此处我需要保证用户输入的是数字

​						}
​				}
​		}
}

//检验键盘摁下的值的方法
function ckInput(){
		var kc = event.keyCode;
		//0~9的ASCII码：48~57
		//backspace的ASCII码：8
		//enter的ASCII码：13
		console.log(kc);    //从控制台看到对应的ASCII码
		
		if(!((kc>=48 && kc<=57) || kc==8 || kc==13)){
				event.returnValue = false;
		}

​		if(kc==13){
​				event.srcElement.blur();
​		}
}



//更新单价的方法
funtion updatePrice(){
		if(event && event.srcElement && event.srcElement.tagName == "INPUT"){
				var input = event.srcElement;
				var newPrice = input.value;
				//input节点的父节点是td
				var priceTD = input.parentElement;
				priceTD.innerText = newPrice;

​				//更新当前行的小计这一个格子的值
​				updateXJ(priceTD.parentElement);
​		}
}

//更新指定行的小计
function updateXJ(tr){
		if(tr && tr.tagName == ""TR){
				var tds = tr.cells;
				var priceTD = Tds[1].innerText;
				var countTD = Tds[2].innerText;

​				//innerText获取到的值的类型是字符串类型，因此需要类型转换，才能进行数学运算				parseInt(price) * parseInt(count);	
​				tds[3].innerText = Xj;

​				//更新总计
​				updateZJ();
​		}
}

//更新总计
function updateZJ(){
		var fruitbl = document.getElementById("tbl_fruit");
		var rows = fruitTbl.rows;
		var sum = 0;
		for(var i = 1; i < rows.length-1 ; i++){
				var tr = rows[i];
				var xj = parseInt(tr.cells[3].innerText);     //NaN：not a number，不是一个数字
				sum = sum + xj;
		}
		rows[rows.length - 1].cells[1].innerText = sum;
}

//绑定删除小图标的点击事件
var img = cells[4].firstChild;
if(img && img.tagName == "IMG"){
		//绑定单击事件
		img.onclick = delFruit;
}

function delFruit(){
		if(event && event.srcElement && event.srcElement.tagName == "IMG"){
				//alert表示弹出一个对话框，只有确认按钮
				//confire表示弹出一个对话框，有确定和取消按钮。当点击确认，返回true，否则返回false
				if(windows.confire("是否确认删除当前库存记录")){
						var img = event.srcElement;
						var tr = img.parentElement.parentElement;
						var fruitTbl = document.getElementById("tbl_fruit");
						fruitTbl = document.getElementById("tbl_fruit");

​						updateZJ();
​				}
​		}
}





onmouseover="showBGColor"：当鼠标悬浮时，显示背景颜色。
		onmouseover：当鼠标悬浮的时候。on表示当什么时候，mouse表示鼠标，over表示悬浮。
onmouseout="clearBGColor()"：当鼠标离开的时候。

onclick：当点击的时候



### Web，Tomcat

#### 一.BS和CS异同点

CS：客户端服务器架构模式
		优点：充分利用客户端机器的资源，减轻服务器的负荷
					（一部分安全要求不高的计算任务存储任务放在客户端执行，不需要把所有的计算和存储都在服务器端执行，从而能够减轻服务器的压力，也能够减轻网络负荷）
		缺点：需要安装；升级维护成本较高

BS：浏览器服务器架构模式
		优点：客户端不需要安装；维护成本较低
		缺点：所有的计算和存储任务都是放在服务器端的，服务器的负荷较重；在服务端计算完成后把结果再传输给客户端，因此客户端和服务器端会进行非常频繁的数据通信，从而网络负荷较重。



#### 二.Tomcat

1.Tomcat的安装和配置
		1）.解压：不要有中文不要有空格
		2）.目录结构说明：
				bin：可执行文件目录
				con：配置文件目录
				lib：存放lib的目录
				logs：日志文件目录
				webapps：项目部署的目录
				work：工作目录
				temp：临时目录 
		3）.配置环境变量，让tomcat能够运行
				因为tomcat也是用java和C写的，因此需要JRE，所以需要配置JAVA_HOME
		4）.启动tomcat，然后访问主页

2.新建Web项目，并在tomcat中部署，最后再访问



可以在idea里配置tomcat



### Servlet

#### 一.servlet入门：获取参数

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
        <form action="add" method="post">
            名称：<input type="text" name="fname"/><br/>
            价格：<input type="text" name="price"/><br/>
            库存：<input type="text" name="fcount"/><br/>
            备注：<input type="text" name="remark"/><br/>
            <input type="submit" value="添加"/>
        </form>
    </body>
</html>
```



```java
public class AddServlet extends HttpServlet {
    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        String fname = request.getParameter("fname");
        String priceStr = request.getParameter("price");
        Integer price = Integer.parseInt(priceStr);
        String fcountStr = request.getParameter("fcount");
        Integer fcount = Integer.parseInt(fcountStr);
        String remark = request.getParameter("remark");

        System.out.println("fname = " + fname);
        System.out.println("price = " + price);
        System.out.println("fcount = " + fcount);
        System.out.println("remark = " + remark);

    }
}
```

将两个连接起来

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <servlet>
        <servlet-name>AddServlet</servlet-name>
        <servlet-class>com.yc.servlets.AddServlet</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>AddServlet</servlet-name>
        <url-pattern>/add</url-pattern>
    </servlet-mapping>

    <!--
    1.用户发请求，action = add
    2.项目中，web.xml中找到url-pattern = /add
    3.找servlet-name = AddServlet
    4.找和servlet-mapping中servlet-name一致的servlet
    5.找到servlet-class对应的com.yc.servlets.AddServlet
    6.用户发送的是post请求（method="post），因此tomcat会执行AddServlet中的dopost方法
    -->

</web-app>
```

（xml配置可以通过注解搞定，以后再说）



#### 二.中文乱码，设置编码

​		1）.post请求方式
​				post方式下，设置编码，防止中文乱码
​				request.setCharacterEncoding("UTF-8");
​				需要注意的是，设置编码这一句代码必须在所有的获取参数动作之前

​		2）.get请求方式
​				tomcat8及之后，get方式目前不需要设置编码
​				tomcat8之前的话，如果是get请求发送的中文数据，转码稍微有点麻烦
​						String fname = request.getParameter("fname");
​						1.将字符串打散成字节数据
​						byte[] bytes = fname.getBytes("ISO-8859-1");
​						2.将字节数组按照设定的编码重新组成字符串
​						fname = new String(bytes,"UTF-8");



#### 三.继承关系以及servlet方法

servlet的继承关系  ——重点查看的是服务方法  servlet()

1.继承关系
		Servlet 接口
				GenericServlet 抽象类
							HttpServlet 抽象子类

2.相关方法
		Servlet 接口：
				void init(config)    ——初始化方法
				void service(request,response)    ——服务方法
				void destory()    ——销毁方法

​		GenericServlet 抽象类：
​				void service(request,response)  ：仍然是抽象的

​		HttpServlet 抽象子类：
​				void service(request,response)  ：不是抽象的
​				1.String method = req.getMethod();  获取请求的方式
​				2.各种if判断，根据请求方式不同，决定去调用不同的do方法
​				3.在HttpServlet这个抽象类中，do方法都差不多

3.小结：
		1）.继承关系：HttpServlet -> GenericServlet -> Servlet
		2）.Servlet中的核心方法：init()，service()，destroy()
		3）.服务方法：当有请求过来时，service方法会自动相应（其实是tomcat容器调用的）
				在HttpServlet中我们会去分析请求的方式：到底是get，post，head还是delete等等
				然后再决定调用哪个do开头的方法
				那么在HttpServlet中这些do方法默认都是405的实现风格，要我们子类去实现对应的方法，否则默认会报405错误
		4）.因此，我们在新建servlet时，我们才会去考虑请求方法，从而决定重写哪个do方法

（要重写do方法，否则执行父类的do方法，那就是报405错误）





#### 四.Servlet的生命周期

1）.生命周期：从出生到死亡的过程就是生命周期。对应着Servlet中的三个方法：init()，service()，destroy()
2）.默认情况下：
		第一次接收请求时，这个Servlet会进行实例化（调用构造方法）、初始化（调用init()）、然后服务（调用service()）
		从第二次请求开始，每一次都是服务
		当容器关闭时，其中的所有的servlet实例会被销毁，调用销毁方法
3）.通过案例我们发现：
		Servlet实例tomcat只会创建一次，所有的请求都是这个实例去响应。
		默认情况下，第一次请求时，tomcat才会去实例化，初始化，然后再服务。
				好处：提高系统的启动速度。
				缺点：第一次请求时耗时较长：
		因此得出结论：
				如果需要提高系统的启动速度，当前默认情况就是这样。
				如果需要提高响应速度，我们应该设置Servlet的初始化时机。

4）.Servlet的初始化时机：
		默认时第一次接收请求时，实例化，初始化
		我们可以在web.xml里通过<load-on-startup>来设置servlet启动的先后顺序，数字越小，启动越靠前，最小值0

5）.Servlet在容器中是：单例的，线程不安全的
		单例：所有的请求都是同一个实例去响应
		线程不安全：一个线程需要根据这个实例中的某个成员变量值去做逻辑判断。但在中间某个时机，另一个线程改变了这个成员变量的值，从而导致第一个线程的执行路径发生了变化
		我们已经知道了servlet是线程不安全的，给我们的启发是：尽量不要在servlet中定义成员变量。如果不得不定义成员变量，那么不要去：①不要去修改成员变量的值  ②不要去根据成员变量的值做一些逻辑判断



#### 五.HTTP协议

1）.Http 称之为 超文本传输协议
2）.Http是无状态的
3）.Http请求响应包含两个部分：请求和响应
		请求：请求包含三部分：1.请求行 ； 2.请求消息头 ； 3.请求主体
				1.请求行包含三个信息：1.请求的方式 ； 2.请求的URL ； 3.请求的协议（一般是HTTP1.1）
				2.请求消息头中包含了很多客户端需要告诉服务器的信息。比如：我的浏览器型号、版本，我能接收的内容的类型，我给你发的内容的类型，内容的长度...
				3.请求体：三种情况（目前先记住，只要不是form表单，即method=post的形式，都是get请求）
						get方式，没有请求体，但是有一个queryString
						post方式，有请求体，form data
						json格式，有请求体，request payload
		响应：响应也包含三部分：1.响应行 ； 2.响应头 ； 3.响应体
				1.响应行包含三个信息：1.协议   2.响应状态码（200）   3.响应状态（ok）
				2.响应头：包含了服务器的信息；服务器发送给浏览器的信息（内容的媒体类型、编码、内容长度等）
				3.响应体：响应的实际内容（比如请求add.html页面时，相应的内容就是<html><head><body><form...）



#### 六.会话

1.Http是无状态的
		Http是无状态：服务器无法判断这两次请求是同一个客户端发过来的，还是不同的客户端发送过来的
		无状态带来的现实问题：第一次请求是添加商品到购物车，第二次请求是结账；如果这两次请求服务器无法区分是同一个用户的，那么就会导致混乱
		通过会话跟踪技术来解决无状态的问题。		

![image-20220519172906365](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220519172906365.png)



2.会话跟踪技术
		客户端第一次发送请求给服务器，服务器获取session，获取不到，则创建新的，然后响应给客户端
		下次客户端给服务器发送请求时，会把sessionID带给服务器，那么服务器就能获取到了，那么服务器就判断这一次请求和上次某次请求是同一个客户端，从而能够区分开客户端
		常用的API：
				request.getSession()  ->  获取当前的会话，没有则创建一个新的会话
				request.getSession(true)  ->  效果和不带参数相同
				request.getSession(false)  ->  获取当前的会话，没有则返回null，不会创建新的

​				session.getId()  ->  获取sessionID
​				session.isNew()  ->  判断当前session是否是新的
​				session.getMaxInactiveInterval()  ->  session的非激活间隔时长，默认1800秒
​				session.setMaxInactiveInterval()
​				session.invalidate()  ->  强制性让会话立即失效
​				...

```java
public class Demo03Servlet extends HttpServlet {

    @Override
    protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //获取session，如果获取不到，则创建一个新的
        HttpSession session = request.getSession();
        System.out.println("session ID："+session.getId());
    }
}
```

```xml
<servlet>
    <servlet-name>Demo03Servlet</servlet-name>
    <servlet-class>com.yc.servlet.Demo03Servlet</servlet-class>
</servlet>

<servlet-mapping>
    <servlet-name>Demo03Servlet</servlet-name>
    <url-pattern>/demo03</url-pattern>
</servlet-mapping>
```

（继承Httpservlet时要导入Tomcat依赖）

3.session保存作用域
		session保存作用域是和具体的某一个session对应的
		常用的API：
				void session.setAttribute(k,v)
				Object session.getAttribute(k)
				void removeAttribute(k)

```java
public class Demo04Servlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        req.getSession().setAttribute("uname","yc1");
    }
}
```

```java
public class Demo05Servlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        Object unameobj = req.getSession().getAttribute("uname");
        System.out.println(unameobj);
    }
}
```

```xml
<servlet>
    <servlet-name>Demo04Servlet</servlet-name>
    <servlet-class>com.yc.servlet.Demo04Servlet</servlet-class>
</servlet>

<servlet-mapping>
    <servlet-name>Demo04Servlet</servlet-name>
    <url-pattern>/demo04</url-pattern>
</servlet-mapping>

<servlet>
    <servlet-name>Demo05Servlet</servlet-name>
    <servlet-class>com.yc.servlet.Demo05Servlet</servlet-class>
</servlet>

<servlet-mapping>
    <servlet-name>Demo05Servlet</servlet-name>
    <url-pattern>/demo05</url-pattern>
</servlet-mapping>
```

通过一个浏览器set后再get可以访问该key的value，但换个浏览器就不能再被访问，一个会话对应一个sessionID



#### 七.服务器内部转发以及客户端重定向

1.服务器内部转发：request.getRequestDispatcher("...").forward(request,response);
		*一次请求响应的过程，对于客户端而言，内部经过了多少次转发，客户端是不知道
		*浏览器地址栏没有变化

```java
public class Demo06Servlet extends HttpServlet {

    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("demo06...");
        //服务器内部转发
        req.getRequestDispatcher("demo07").forward(req,resp);
    }
}
```

```java
public class Demo07Servlet extends HttpServlet {

    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("demo07...");
    }
}
```

再把xml配置一下。

![image-20220520105537028](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220520105537028.png)

2.客户端重定向：response.sendRedirect("...");
		*两次请求响应的过程。客户端肯定知道请求URL有变化
		*浏览器地址栏有变化

```java
public class Demo06Servlet extends HttpServlet {

    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("demo06...");
        //服务器内部转发
//        req.getRequestDispatcher("demo07").forward(req,resp);
        //客户端重定向
        resp.sendRedirect("demo07");
    }
}
```

```java
public class Demo07Servlet extends HttpServlet {

    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("demo07...");
    }
}
```

再把xml配置一下。

![image-20220520105857684](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220520105857684.png)





#### 八.Thymeleaf——视图模板技术

1.添加thymeleaf的jar包

2.新建一个Servlet类ViewBaseServlet

3.在web.xml文件中添加配置
		配置前缀：view-prefix
		配置后缀：view-suffix

4.使得我们的Servlet继承ViewBaseServlet

5.根据逻辑视图名称得到物理视图名称
		//此处的视图名称是index
		//那么thymeleaf会将这个逻辑视图名称对应到物理视图名称上去
		//逻辑视图名称：index
		//物理视图名称：view-prefix + 逻辑视图名称 + view-suffix
		//所以真实的视图名称是：   /    index       .html
		super.processTemplate("index" , request , response)

6.使用thymeleaf的标签
		th:if       ;       th:unless       ;       th:each       ;       th:text



#### 九.保存作用域

​		原始情况下，保存作用域我们可以认为有4个：page（页面级别，现在几乎不用），request（一次请求响应范围），session（一次会话范围），application（整个应用程序范围）

1.request：一次请求响应范围
		客户端重定向的请求改变了，自然访问不到。请求2里想获取请求1的数据，取不到
		浏览器内部转发属于一次请求响应，所以可以访问的到。内部转几次没有关系，最终就是一次请求响应

```java
@WebServlet("/demo01")
public class Demo01Servlet extends HttpServlet{
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //1.向request保存作用域保存数据
        req.setAttribute("uname","zhangsan");
        //2.客户端重定向
//        resp.sendRedirect("demo02");

        //3.服务器内部转发
        req.getRequestDispatcher("demo02").forward(req,resp);

    }
}
```

```java
@WebServlet("/demo02")
public class Demo02Servlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //1.获取request保存作用域保存的数据，key为uname
        Object unameObj = req.getAttribute("uname");
        System.out.println("unameObj = " + unameObj);
    }
}
```

![image-20220520162750843](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220520162750843.png)

2.session：一次会话范围有效
		一个客户端进程没断，属于同一sessionID，一次会话，所以只要没过期，是可以访问得到的

```java
@WebServlet("/demo03")
public class Demo03Servlet extends HttpServlet{
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //1.向session保存作用域保存数据
        req.getSession().setAttribute("uname","zhangsan");
        //2.客户端重定向
        resp.sendRedirect("demo04");

        //3.服务器内部转发
//        req.getRequestDispatcher("demo04").forward(req,resp);

    }
}
```

```java
@WebServlet("/demo04")
public class Demo04Servlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //1.获取session保存作用域保存的数据，key为uname
        Object unameObj = req.getSession().getAttribute("uname");
        System.out.println("unameObj = " + unameObj);
    }
}
```

![image-20220520162504354](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220520162504354.png)

3.application：一次应用程序范围有效
		应用程序里相当于是公共的 ，所有的客户端去请求都能请求的到。当Tomcat停止了就请求不到了

```java
@WebServlet("/demo05")
public class Demo05Servlet extends HttpServlet{
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //1.向application保存作用域保存数据
        //ServletContext：Servlet上下文
        ServletContext application = req.getServletContext();
        application.setAttribute("uname","zhangsan");
        //2.客户端重定向
        resp.sendRedirect("demo06");

        //3.服务器内部转发
//        req.getRequestDispatcher("demo04").forward(req,resp);

    }
}
```

```java
@WebServlet("/demo06")
public class Demo06Servlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //1.获取application保存作用域保存的数据，key为uname
        ServletContext application = req.getServletContext();
        Object unameObj = application.getAttribute("uname");
//合成一句是        Object unameObj = req.getServletContext().getAttribute("uname");
        System.out.println("unameObj = " + unameObj);
    }
}
```

![image-20220520162611767](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220520162611767.png)





#### 十.路径问题

1.相对路径
		../  代表到上一级目录 
		比如user下的login.html要引用css下的login.css文件，那么在login.html里引用路径为 ../css/login.css
		或者user下的member下的shopping.html要引用css下的shopping.css，那么路径应该为 ../../css/shopping.css
2.绝对路径
		协议+IP地址+端口号+context root（项目名，项目根目录）+该文件路径
		比如user下的login.html的绝对路径为http://localhost:8080/pro10/css/login.css

![image-20220520170626030](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220520170626030.png)







P40











### Servlet



#### 一.Servlet技术

##### 1.什么是Servlet

​		1）.Servlet是JavaEE规范之一。规范就是接口
​		2）.Servlet是JavaWeb三大组件之一。三大组件分别是：Servlet程序、Filter过滤器、Listener监听器
​		3）.Servlet是运行在服务器上的一个java小程序，他可以接收客户端发送过来的请求，并响应数据给客户端。

##### 2.手动实现Servlet程序

​		1）.编写一个类去实现Servlet接口
​		2）.实现service方法，处理请求，并响应数据
​		3）.到web.xml中去配置servlet程序的访问地址

```java
public class HelloServlet  implements Servlet {

    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
    }

    @Override
    public ServletConfig getServletConfig() {
        return null;
    }

    //service方法是专门用来处理请求和响应的
    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("Hello Servlet 被访问了");
    }

    @Override
    public String getServletInfo() {
        return null;
    }

    @Override
    public void destroy() {

    }
}
```

```xml
    <!--servlet标签给Tomcat配置Servlet程序-->
    <servlet>
        <!--servlet-name标签：给Servlet程序起一个别名（一般是类名）-->
        <servlet-name>HelloServlet</servlet-name>
        <!--servlet-class标签：是Servlet程序的全类名-->
        <servlet-class>com.yc.servlet.HelloServlet</servlet-class>
    </servlet>

    <!--servlet-mapping标签给servlet程序配置访问地址-->
    <servlet-mapping>
        <!--servlet-name标签：是告诉服务器，我当前配置的地址给哪个Servlet程序使用-->
        <servlet-name>HelloServlet</servlet-name>
        <!--url-pattern标签：配置访问地址
            /：斜杠在服务器解析的时候，表示地址为http://ip:port/工程路径（工程路径就是Tomcat配置里的URL）
            /hello：表示地址为：http://ip:port/工程路径/hello
        -->
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>

</web-app>
```



##### 3.url地址到Servlet程序的访问

![image-20220526145723702](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220526145723702.png)



##### 4.Servlet的生命周期

​		1）.执行Servlet构造方法
​		2）.执行init初始化方法
​		3）.执行service方法
​		4）.执行destroy销毁方法

​		第一、二步是在第一次访问的时候创建Servlet程序会调用。
​		第三步，每次访问都会调用
​		第四步，在web工程停止的时候调用

##### 5.通过继承HttpServlet实现Servlet程序

​		1）.一般在实际项目开发中，都是使用继承HttpServlet类的方式去实现Servlet程序
​		2）.根据业务需要重写doGet或doPost方法
​		3）.到web.xml中的配置Servlet程序的访问地址



##### 6.使用IDEA创建Servlet程序

​		配置Servlet信息：
​				右击包名 -> new -> Servlet		（注解先不勾选，先学习xml配置）

![image-20220526164130916](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220526164130916.png)

​				创建好的类下自动生成doget、dopost方法。自动生成配置Servlet程序的xml，servlet程序的访问地址需要自己配

##### 7..Servlet类的继承

![image-20220526172533207](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220526172533207.png)



#### 二.ServletConfig类

ServletConfig类从类名上来看，就知道是Servlet程序的配置信息

Servlet程序和ServletConfig对象都是由Tomcat负责创建，我们负责使用
Servlet程序默认是第一次访问的时候创建，ServletConfig是每个Servlet程序创建时，就创建一个对应的ServletConfig对象。每一个ServletConfig对应的是他自己的Servlet程序的，不能在一个Servlet里得到别的Servlet信息。

##### 1.ServletConfig类的三大作用

​		1）.可以获取Servlet程序的别名servlet-name的值
​				就是xml里配置的servlet-name标签里的名字
​		2）.获取初始化参数init-param
​				在xml配置初始化参数，servlet程序里init方法里可以输出对应的参数名的参数值
​		3）.获取ServletContext对象

web.xml中的代码：

```xml
<!--servlet标签给Tomcat配置Servlet程序-->
<servlet>
    <!--servlet-name标签：给Servlet程序起一个别名（一般是类名）-->
    <servlet-name>HelloServlet</servlet-name>
    <!--servlet-class标签：是Servlet程序的全类名-->
    <servlet-class>com.yc.servlet.HelloServlet</servlet-class>

    <!--init-param是初始化参数（键值对）可以不止一对-->
    <init-param>
        <!--参数名-->
        <param-name>username</param-name>
        <!--参数值-->
        <param-value>root</param-value>
    </init-param>
    <init-param>
        <!--参数名-->
        <param-name>url</param-name>
        <!--参数值-->
        <param-value>jdbc:mysql://localhost:3306/test</param-value>
    </init-param>

</servlet>

<!--servlet-mapping标签给servlet程序配置访问地址-->
<servlet-mapping>
    <!--servlet-name标签：是告诉服务器，我当前配置的地址给哪个Servlet程序使用-->
    <servlet-name>HelloServlet</servlet-name>
    <!--url-pattern标签：配置访问地址
        /：斜杠在服务器解析的时候，表示地址为http://ip:port/工程路径（工程路径就是Tomcat配置里的URL）
        /hello：表示地址为：http://ip:port/工程路径/hello
    -->
    <url-pattern>/hello</url-pattern>
</servlet-mapping>
```

Servlet中的代码：

```java
    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
        System.out.println("2.init初始化方法");

//        1）.可以获取Servlet程序的别名servlet-name的值
        System.out.println("HelloServlet程序的别名是：" + servletConfig.getServletName());
//        2）.获取初始化参数init-param
        System.out.println("初始化参数username的值是：" + servletConfig.getInitParameter("username"));
        System.out.println("初始化参数url的值是：" + servletConfig.getInitParameter("url"));
//        3）.获取ServletContext对象
        System.out.println(servletConfig.getServletContext());
    }
```



补充：
		1.在do方法里还可以得到某些信息，但只能得到该Servlet程序里的信息

```java
//也可以使用。但每一个ServletConfig对应的是他自己的Servlet程序的，不能在一个Servlet程序里得到别的Servlet信息。
ServletConfig servletConfig = getServletConfig();
System.out.println(servletConfig);
```

​		2.重写init方法要加上super.init(config)，因为父类GenericServlet类里init把config保存起来了，不写super，调用的时候就调用子类了，保存操作就会丢失。

```java
@Override
public void init(ServletConfig config) throws ServletException {
    super.init(config);
    System.out.println("重写了init初始化方法，做了一些工作");
}
```



#### 三.ServletContext类

##### 1.什么是ServletContext？

​		1）.ServletContext是一个接口，他表示Servlet上下文对象。
​		2）.一个web工程，只有一个ServletContext对象实例。
​		3）.ServletContext对象是一个域对象。
​		4）.ServletContext是在web工程部署启动的时候创建。在web工程停止的时候销毁。
​				什么 是域对象？
​						域对象，是可以像Map一样存取数据的对象，叫域对象
​						这里的域指的是存取数据的操作范围，整个web项目工程

​										存数据						取数据							删除数据
​		Map						   put()						   get()							  remove()
​		域对象					setAttribute()			getAttribute()				removeAttribute()

##### 2.ServletContext类的四个作用

​		1）.获取web.xml中配置的上下文参数context-param
​		2）.获取当前的工程路径，格式：/工程路径
​		3）.获取工程部署后在服务器硬盘上的绝对路径
​		4）.像Map一样存取数据

​		1）2）3）.

```xml
<!--context-param是上下文参数
它属于整个web工程。也就是说，但凡是在这个web工程里创建的Servlet程序、Filter过滤器、Listener监听器等都可以得到这些参数
 可以配置多组
-->
<context-param>
    <param-name>username</param-name>
    <param-value>context</param-value>
</context-param>
<context-param>
    <param-name>password</param-name>
    <param-value>1234</param-value>
</context-param>
```

```java
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
//
//        1）.获取web.xml中配置的上下文参数context-param（不能获取init-param参数的值，init-param只能是ServletConfig获取的，context-param只能是ServletContext对象获取的）
        ServletContext context = getServletConfig().getServletContext();

        String username = context.getInitParameter("username");
        System.out.println("context-param参数username的值是"+ username);
        System.out.println("context-param参数password的值是"+ context.getInitParameter("password"));
//        2）.获取当前的工程路径，格式：/工程路径
        System.out.println("获取当前工程路径" + context.getContextPath());
//        3）.获取工程部署后在服务器硬盘上的绝对路径
        //斜杠被服务器解析地址为http://ip:port/工程名/       映射到IDEA代码的web目录
        System.out.println("工程部署的路径是：" + context.getRealPath("/"));
        System.out.println("工程下css目录的绝对路径是：" + context.getRealPath("/css"));
//        4）.像Map一样存取数据
    }
```

​		4）.像Map一样存取数据（创建一个servlet程序，可以往里面存数据，还可以获取到）

```java
public class ContextServlet1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //获取ServletContext对象，可以简单些
//        ServletContext servletContext = getServletConfig().getServletContext();
        ServletContext servletContext = getServletContext();
        System.out.println(servletContext);

        System.out.println("保存之前：context1获取key1的值是：" + servletContext.getAttribute("key1"));

        servletContext.setAttribute("key1","value1");

        System.out.println("context1中获取域数据key1的值是：" + servletContext.getAttribute("key1"));
    }
}
```

​				再创建一个servlet2，发现可以取到刚才servlet1里的值。但如果重启项目或重新部署就不行了，除非再访问servlet1，再存一遍数据，那servlet2就可以获取了

```java
public class ContextServlet2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        ServletContext servletContext = getServletContext();
        System.out.println(servletContext);

        //会发现这个servler里也可以获取key1的值。如果重启服务或重新部署就不行了，除非再往里存数据
        System.out.println("context1中获取域数据key1的值是：" + servletContext.getAttribute("key1"));
    }
}
```



#### 四.Http协议

##### 1.什么是HTTP协议？

什么是协议？
		协议是指双方，或多方，相互约定好，大家都需要遵守的规则，叫协议

所谓HTTP协议，就是指，客户端和服务器之间通信时，发送的数据，需要遵守的规则，叫HTTP协议

HTTP协议中的数据又叫报文

##### 2.请求的HTTP协议格式

客户端给服务器发送数据叫请求
服务器给客户端回传数据叫响应

请求又分为GET请求，和POST请求

1）.GET请求
		(1).请求行
				a）.请求的方式				GET
				b）.请求的资源路径		[+?+请求参数]
				c）.请求的协议的版本号		HTTP/1.1

​		(2).请求头
​				a）.key：value组成		不同的键值对，表示不同的含义

![image-20220527153351957](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220527153351957.png)



2）.POST请求
		(1).请求行
				a）.请求的方式				POST
				b）.请求的资源路径		[+?+请求参数]
				c）.请求的协议的版本号		HTTP/1.1

​		(2).请求头
​				a）.key：value组成		不同的键值对，表示不同的含义

​		空行隔开

​		(3).请求体	==>>	就是发送给服务器的数据

![image-20220527155519060](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220527155519060.png)



3）.常用的请求头说明
		Accept：表示客户端可以接收的数据类型
		Accept-Languege：表示客户端可以接收的语言类型
		User-Agent：表示客户端浏览器的信息
		host：表示请求时的服务器ip和端口号

4）.哪些是GET请求，哪些是POST请求
		GET请求有哪些：
				(1).form标签	method=get
				(2).a标签
				(3).link标签引入css
				(4).Script标签引入js文件
				(5).img标签引入图片
				(6).iframe引入html页面
				(7).在浏览器地址栏中输入地址后敲回车

​		POST请求有哪些：
​				(1).form标签	method=post

##### 3.响应的HTTP协议格式

​		1）.响应行
​				(1).响应的协议和版本号				HTTP/1.1
​				(2).响应状态码							  200
​				(3).响应状态描述符					   ok
​		2）.响应头
​				(1).key：value		不同的响应头，有其不同的含义
​		空行
​		3）.响应体	->	就是回传给客户端的数据

![image-20220527162734914](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220527162734914.png)



##### 4.常用的响应码说明

​		200：表示请求成功
​		302：表示请求重定向
​		404：表示请求服务器已经收到了，但是你要的数据不存在（请求地址错误）
​		500：表示服务器已经收到请求，但是服务器内部错误（代码错误）

##### 5.MIME类型说明

MIME是HTTP协议中的数据类型
MIME的英文全称是"Multipurpose Internet Mail Extensions"，多功能Internet邮件扩充服务。MIME类型的格式是“大类型/小类型”，并于某一种文件的拓展名相对应。

常见的MIME类型：

| 文本              | MIME类型    |                          |
| :---------------- | :---------- | ------------------------ |
| 超文本标记语言    | .html，.htm | text/html                |
| 普通文本          | .txt        | text/plain               |
| RTF文本           | .rtf        | application/rtf          |
| GIF图形           | .gif        | image/gif                |
| JPEG图形          | .jpeg，.jpg | image/jpeg               |
| au声音文件        | .au         | audio/basic              |
| MIDI音乐文件      | mid，.midi  | audio/midi，audio/x-midi |
| RealAudio音乐文件 | .ra，.ram   | audio/x-pn-realaudio     |
| MPEG文件          | .mpg，.mpeg | video/mpeg               |
| AVI文件           | .avi        | video/x-msvideo          |
| GZIP文件          | .gz         | application/x-gzip       |
| TAR文件           | .tar        | application/x-tar        |
|                   |             |                          |



谷歌浏览器如何查看HTTP协议：

![image-20220527170147670](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220527170147670.png)





#### 五.HttpServletRequest类

##### 1.HttpServletRequest类有什么作用

​		每次只要有请求进入Tomcat服务器，Tomcat服务器就会把请求过来的HTTP协议信息解析好封装到Request对象中。然后传递到service方法中（或doGet和doPost）中给我们使用。我们可以通过HttpServletRequest对象，获取到所有请求的信息。



##### 2.HttpServletRequest类的常用方法

​		1）.getRequestURI()						获取请求的资源路径（URI地址）
​		2）.getRequestURL()					   获取请求的统一资源定位符（绝对路径）
​		3）.getRemoteHost()					    获取客户端的ip地址
​		4）.getHeader()								获取请求头
​		5）.getParameter()						   获取请求的参数
​		6）.getParameterValues()				获取请求的参数（多个值的时候使用）
​		7）.getMethod()								获取请求的方式（GET或POST）
​		8）.setAttribute(key,value)				设置域数据
​		9）.getAttribute(key)						  获取域数据
​		10）.getRequestDispatcher()		    获取请求转发对象



##### 3.如何获取请求参数

前端页面：

```html
<!DOCTYPE html>
<html lang="zh_CN">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
        <!--action里端口号后边的地址要和Tomcat配置的URL一致，之后再往后写xml里的url-pattern标签里的值-->
        <form action="http://localhost:8080/javawebhahaha/parameterServlet" method="post">
            用户名：<input type="text" name="username"><br/>
            密码：<input type="password" name="password"><br/>
            兴趣爱好：<input type="checkbox" name="hobby" value="cpp">c++
            <input type="checkbox" name="hobby" value="java">Java
            <input type="checkbox" name="hobby" value="js">JavaScript<br/>
            <input type="submit">
        </form>

    </body>
</html>

<!--如何获取请求参数-->
```

后端：

```java
package com.yc.servlet;

import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import java.io.IOException;
import java.util.Arrays;

/**
 * @Description: 如何获取请求参数
 * @Author: YC
 * @CreateTime: 2022/05/27 17:52
 */
public class ParameterServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("-------doGet--------");
        //获取请求参数
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        String[] hobby = req.getParameterValues("hobby");

        System.out.println("用户名：" + username);
        System.out.println("密码：" + password);
        System.out.println("兴趣爱好：" + Arrays.asList(hobby));
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //设置请求体的字符集为UTF-8，从而解决post请求的中文乱码问题。并且要在获取请求参数之前调用才有效
        req.setCharacterEncoding("UTF-8");
        System.out.println("-------doPost--------");
        //获取请求参数
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        String[] hobby = req.getParameterValues("hobby");

        System.out.println("用户名：" + username);
        System.out.println("密码：" + password);
        System.out.println("兴趣爱好：" + Arrays.asList(hobby));
    }
}
```

xml配置文件将前后端连接：

```xml
<servlet>
    <servlet-name>ParameterServlet</servlet-name>
    <servlet-class>com.yc.servlet.ParameterServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>ParameterServlet</servlet-name>
    <url-pattern>/parameterServlet</url-pattern>
</servlet-mapping>
```



##### 4.POST请求中文乱码问题

在doPost方法里首先添加：

```java
    //设置请求体的字符集为UTF-8，从而解决post请求的中文乱码问题。并且要在获取请求参数之前调用才有效
    req.setCharacterEncoding("UTF-8");
```



##### 5.请求的转发

什么是请求的转发？
		请求转发是指，服务器收到请求后，从一个资源跳转到另一个资源的操作叫请求转发

请求转发的特点：
		1.浏览器地址栏没有变化
		2.它们是一次请求
		3.它们共享Request域中的数据
		4.可以转发到WEB-INF目录下
		5.不可以访问工程以外的资源

第一个servlet：

```java
public class Servlet1 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //获取请求的参数（办事的材料）
        String username = req.getParameter("username");
        System.out.println("在Servlet1（柜台1）中查看参数（材料）：" + username);

        //给材料盖一个章，并传递到Servlet2（柜台2）去查看
        req.setAttribute("key1","柜台1的章");
        //问路：Servlet2（柜台2）怎么走
        /*
        *请求转发必须要以斜杠打头，斜杠表示地址为：http://ip:port/工程名/，映射到IDEA代码的web目录
         */
        RequestDispatcher requestDispatcher = req.getRequestDispatcher("/servlet2");

        //走向Servlet2（柜台）
        requestDispatcher.forward(req,resp);
    }
}
```

第二个servlet：

```java
public class Servlet2 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //获取请求的参数（办事的材料）
        String username = req.getParameter("username");
        System.out.println("在Servlet2（柜台2）中查看参数（材料）：" + username);

        //查看柜台1是否有盖章
        Object key1 = req.getAttribute("key1");
        System.out.println("柜台1是否有章："+ key1);

        //处理自己的业务
        System.out.println("Servlet2处理自己的业务");
    }
}
```

xml配置：

```xml
<servlet>
    <servlet-name>Servlet1</servlet-name>
    <servlet-class>com.yc.servlet.Servlet1</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>Servlet1</servlet-name>
    <url-pattern>/servlet1</url-pattern>
</servlet-mapping>

<servlet>
    <servlet-name>Servlet2</servlet-name>
    <servlet-class>com.yc.servlet.Servlet2</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>Servlet2</servlet-name>
    <url-pattern>/servlet2</url-pattern>
</servlet-mapping>
```



![image-20220531113145267](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220531113145267.png)



##### 6.base标签的作用

base标签设置页面相对路径工作时参照的地址
		href属性就是参数的地址值，c.html可以省略的，但最后的斜杠不能省略

```java
<base href="http://localhost:8080/javawebhahaha/a/b/c.html">
```

a标签进行跳转时：
		首先c.html不是路径，不用管，一个../返回上一级目录，两个../就返回两级目录
				http://localhost:8080/javawebhaahaha/a/b/c.html../../index.html
				http://localhost:8080/javawebhaahaha/a/../index.html
				http://localhost:8080/javawebhaahaha/index.html

请求转发进行跳转时：
		首先forwardC不是路径，不用管，一个../返回上一级目录，两个../就返回两级目录。但去掉一个目录后前边就是端口了，没有可去的了，最终就不管了，所以最终的路径是个错误的路径，报404.
								http://localhost:8080/javawebhaahaha/forwardC../../index.html
								http://localhost:8080/../index.html
								http://localhost:8080/index.html

![image-20220531113306896](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220531113306896.png)



##### 7.web中的相对路径和 绝对路径

在javaWeb中，路径分为相对路径和绝对路径两种：
		相对路径：
				.				  表示当前目录
				..				 表示上一级目录
				资源名		表示当前目录/资源名

​		绝对路径：
​				http://ip:port/工程路径 /资源路径



##### 8.web中 / 斜杠的不同意义

在web中 / 斜杠是一种绝对路径

​		/斜杠 如果被浏览器解析，得到的地址是：http://ip:port           
​				`<a href="/">斜杠</a>`

​		/斜杠 如果被服务器解析，得到的地址是：http://ip:port/工程路径
​				1.xml配置里的<url-pattern>/servlet1</url-pattern>
​				2.servletContext.getRealPath("/");
​				3.request.getRequestDispatcher("/");

特殊情况：response.sendReadiect("/");	把斜杠发送给浏览器解析。得到http://ip:port



#### 六.HttpservletResponse类



##### 1.HttpServletResponse类的作用

​		HttpServletResponse类和HttpServletRequest类一样。每次请求进来，Tomcat服务器都会创建一个Response对象传递给Servlet程序去使用。HttpServletRequest表示请求过来的信息，HttpServletResponse表示所有响应的信息，我们如果需要设置返回给客户端的信息，都可以通过HttpServletResponse对象来进行设置。



##### 2.两个输出流的说明

字节流		getOutputStream();		常用于下载（传递二进制数据）
字符流		getWriter();					 常用于回传字符串（常用）

两个流只能使用一个。
使用了字节流，就不能再使用字符流，反之亦然，否则就会报错。

![image-20220531140909350](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220531140909350.png)



##### 3.如何往客户端回传数据

要求：往客户端回传字符流数据

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    //要求：往客户端回传字符流数据
    PrintWriter writer = resp.getWriter();
    writer.println("response's context!!!");
}
```

注：数据是中文时出现乱码

```java
//查看响应的字符集
System.out.println(resp.getCharacterEncoding());
```

```java
//设置服务器字符集为UTF-8
resp.setCharacterEncoding("UTF-8");
```

浏览器也会出现编码错误，以下设置浏览器编码

```java
//通过响应头，设置浏览器也是用UTF-8，以下两种方式都可以
resp.setHeader("Content-Type","text/html;charset=UTF-8");
//下面的方法会同时设置服务器和客户端都使用UTF-8字符集，还设置了响应头。不过此方法一定要在获取流对象之前调用才有效
resp.setContentType("text/html；charset=UTF-8");
```



##### 4.请求重定向

请求重定向，是指客户端给服务器发请求，然后服务器告诉客户端说，我给你一些地址，你去新地址访问。叫请求重定向（因为之前的地址可能已经被废弃）

重定向的特点：
		1.浏览器地址栏会发生变化
		2.两次请求
		3.不共享Request域中的数据
		4.不能访问WEB-INF下的资源
		5.可以访问工程外的资源

1）.请求重定向的第一种方案（推荐第二种）

第一个资源：

```java
public class Response1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("到此一游 Response1");
        req.setAttribute("key1","value1");
        //设置想响应状态码302，表示重定向
        resp.setStatus(302);
        //设置响应头，说明新的地址在哪里
        resp.setHeader("Location","http://localhost:8080/javawebhahaha/response2");
    }
}
```

第二个资源：

```java
public class Response2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.getWriter().write("response2's result!!!");
        System.out.println(req.getAttribute("key1"));//得不到请求一的数据
    }
}
```

xml配置：

```xml
<servlet>
    <servlet-name>Response1</servlet-name>
    <servlet-class>com.yc.servlet.Response1</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>Response1</servlet-name>
    <url-pattern>/response1</url-pattern>
</servlet-mapping>

<servlet>
    <servlet-name>Response2</servlet-name>
    <servlet-class>com.yc.servlet.Response2</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>Response2</servlet-name>
    <url-pattern>/response2</url-pattern>
</servlet-mapping>
```



2）.请求重定向的第二种方案（推荐使用）

```java
public class Response1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("到此一游 Response1");
        req.setAttribute("key1","value1");
	   //请求重定向的第二种方案：
	   resp.sendRedirect("http://localhost:8080/javawebhahaha/response2");
	   //resp.sendRedirect("http://baidu.com");//可以访问工程以外的资源
    }
}
```



![image-20220531155245788](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220531155245788.png)







### Cookie



#### 一.什么是Cookie？

1.Cookie翻译过来就是饼干的意思
2.Cookie是服务器通知客户端保存键值对的一种技术
3.客户端有了Cookie以后，每次请求都发送给服务器
4.每个Cookie的大小不能超过4kb



#### 二.如何创建Cookie



![image-20220531172925829](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220531172925829.png)

![image-20220531172753446](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220531172753446.png)







### Filter

#### 一.什么是过滤器

1.Filter是JavaWeb三大组件之一。三大组件分别是：Servlet程序、Listener监听器、Filter过滤器
2.Filter过滤器它是JavaEE的规范。也就是接口
3.Filter过滤器它的作用是：**拦截请求**，过滤响应

拦截请求常见的应用场景：
		1.权限检查
		2.日记操作
		3.事务管理
		......等等



#### 二.Filter初体验

要求在你的web工程下，有一个admin目录。这个admin目录下的所有资源（html页面、jpg图片、jsp文件、等等）都必须是用户登录之后才允许访问。

思考：根据之前学过的内容，我们知道，用户登录之后都会把用户登陆的信息保存在Session域中。所以要检查用户是否登录，可以判断Session中是否包含有用户登录的信息即可！！！

![image-20220619101237788](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220619101237788.png)



添加过滤器类

```java
public class AdminFilter implements Filter {

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    /*doFilter方法，专门用于拦截请求。可以做权限检查
     */
    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        HttpServletRequest httpServletRequest = (HttpServletRequest) servletRequest;
        HttpSession session = httpServletRequest.getSession();
        Object user = session.getAttribute("");
        //如果等于null，说明还没有登陆
        if (user == null){
            servletRequest.getRequestDispatcher("/login.jsp").forward(servletRequest,servletResponse);
            return;
        }else {
            //让程序继续往下访问用户的目标资源
            filterChain.doFilter(servletRequest,servletResponse);
        }
    }

    @Override
    public void destroy() {

    }
}
```

web.xml中配置filter过滤器

```xml
<!--filter标签用于配置一个Filter过滤器-->
<filter>
    <!--给filter起一个别名-->
    <filter-name>AdminFilter</filter-name>
    <!--配置filter的全类名-->
    <filter-class>com.yc.filter.AdminFilter</filter-class>
</filter>
<!--filter-mapping配置Filter过滤器的拦截路径-->
<filter-mapping>
    <!--filter-name表示当前的拦截路径给哪个filter使用-->
    <filter-name>AdminFilter</filter-name>
    <!--url-pattern配置拦截路径
        / 表示请求地址为：http://ip:port/工程路径/     映射到IDEA的web路径
        /admin/*  表示请求地址为：http://ip:port/工程路径/admin/*
    -->
    <url-pattern>/admin/*</url-pattern>
</filter-mapping>
```



Filter过滤器的使用步骤：
		1.编写一个类去实现Filter接口
		2.实现过滤方法doFilter()
		3.到web.xml中去配置Filter的拦截路径



#### 三.Filter的生命周期

Filter的生命周期包含几个方法
		1.构造器方法
		2.init初始化方法
				第1，2步在web工程启动的时候执行（Filter已经创建）
		3.doFilter过滤方法
				第3步，每次拦截到请求，就会执行
		4.destroy销毁
				第4步，停止web工程的时候，就会执行（停止web工程，也会销毁Filter过滤器）



#### 四.FilterConfig类

FilterConfig类见名知义，它是Filter过滤器的配置文件类。
Tomcat每次创建Filter的时候，也会同时创建一个FilterConfig类，这里包含了Filter配置文件的配置信息。

FilterConfig类的作用是获取filter过滤器的配置内容
		1.获取Filter的名称filter-name的内容
		2.获取在Filter中配置的init-param初始化参数
		3.获取ServletContext对象



#### 五.FilterChain过滤器链

Filter				过滤器
Chain	   		链条
FilterChain	   就是过滤器链（多个过滤器如何一起工作）

FilterChain.doFilter()方法的作用
		1.执行下一个Filter过滤器（如果有Filter）
		2.执行目标资源（没有Filter）

在多个Filter过滤器执行的时候，它们执行的优先顺序是由它们在web.xml中Filter过滤器标签从上到下配置的顺序决定的

多个Filter过滤器执行的特点：
		1.所有filter和目标资源默认都执行在同一个线程中
		2.多个Filter共同执行的时候，它们都使用同一个Request对象

若其中一个过滤器的chain.doFilter()方法没有执行，那么不会再往下执行后面的过滤器和目标资源，而是直接到后置代码，知道走完后置代码。比如下图的Filter2的chain.doFilter()方法被删除，那么不会执行后边的目标资源，而是直接执行Filter2的后置代码2，再执行后置代码1，最后返回客户端。如果Filter2的chain.doFilter()方法和后置代码2都被删除，那么前置代码2走完直接到后置代码1。

![image-20220625180808952](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220625180808952.png)



#### 六.Filter的拦截路径

Filter过滤器的拦截路径有三种匹配方法
		精确匹配、目录匹配、后缀名匹配

##### 1.精确匹配：

```xml
        <url-pattern>/target.jsp</url-pattern>
```

以上配置的路径，表示请求地址必须为：http://ip:port/工程路径/target.jsp

##### 2.目录匹配

```xml
        <url-pattern>/admin/*</url-pattern>
```

以上配置的路径，表示请求地址必须为：http://ip:port/工程路径/admin/*

##### 3.后缀名匹配

```xml
        <url-pattern>*.html</url-pattern>
```

以上配置的路径，表示请求地址必须以.html结尾才会拦截 



Filter过滤器它只关心请求的地址是否匹配，不关心请求的资源是否存在！！！









### JSON



JSON（JavaScript Object Notation）是一种轻量级的数据交换格式。易于人阅读和编写，同时也易于机器解析和生成。JSON采用完全独立于编程语言的文本格式来存储和表示数据，而且很多语言都提供了对json的支持（包括C,C++,C#,Java,JavaScript,Perl,Python等）。这样就使得JSON成为

P305	1：25













### 补充



#### 一.部署包问题

File -> Project Structure - >Artifacts -> 点加号+ -> Web Application Exploded -> From Modules -> 选择要添加的模块 -> Apply -> ok

![image-20220526143021906](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220526143021906.png)

打开tomcat配置 -> Deployment -> 点击加号+ -> Artifact（可以把红色的启动部署删掉） -> 可以设置一下工程路径 -> Apply -> ok

![image-20220526143613618](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220526143613618.png)

![image-20220526143930790](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220526143930790.png)

![image-20220526144416848](https://raw.githubusercontent.com/chocman99/Image/main/JavaWeb/image-20220526144416848.png)



#### 二.Http状态码

```txt
200：正常响应
302：重定向
400：Bad Request 客户端请求的语法错误，服务器无法理解
404：找不到对应的资源
405：当前请求的方法不支持。比如我们表单method=post，那么servlet必须对应dopost。如果用其他的，则会报405错误。或者没有重写doget或dopost方法，调用父类的了。请求方式不满足methods
406：表示无法使用请求的内容特性来响应请求的网页。说白了就是后台的返回结果前台无法解析就报406错误。j请求头（Request Headers）中看到请求信息是json格式，响应头（Response Hraders）中却发现返回信息的格式是“text/html”，前台无法解析，需将结果转换成json格式返回给前台。
500：服务器内部错误
```



#### 三.请求方式：get和post

get：
		1）.请求参数会拼接在请求地址后，？（问号）进行拼接，后边是 请求参数名=请求参数值 and ...	：http:ip:port/项目名?name=value and ...
		2）.相对不是很安全
		3）既然不安全，那get传输速度比较快，它是伴随着请求地址传过去的
		4）.传输的数据量有限
		5）.不能文件上传

post：
		1）.请求参数会放在请求体里，所以个体方式没有请求体，post的方式有。但请求体里的请求参数和get一样
		2）.相对安全
		3）.传输速度相对较慢
		4）.传输的数据量大，无限制
		5）.可以文件上传



#### 四.小问题

1.获取服务器路径，先有session，通过session获得ServletContext对象，再通过ServletContext.getRealPath()











