### postman接口测试

一.接口测试基础：
		后端测试
		功能黑盒测试
		协议：
				http（https）
				RPC：dubbo
				websockets
				webservies

二.接口测试之前的准备：

接口测试工具：
		postman，jmeter
		接口自动化：
				requests，httpx，httprunner

接口的信息获取方式：

​		1.接口需求文档：
​				接口的功能说明
​				接口的名称：login
​				接口的url前缀：http://127.0.0.1:8080/api/yc
​				接口的请求头信息：headers
​				接口的参数类型：json，text，form-data
​				接口的参数：
​						参数的说明，参数的类型，参数是否必填
​				接口的响应值：返回的字段

​		2.fiddle抓包

​		3.数据库表结构，日志，代码（经验）





三.postman接口测试：



​		get：可以直接在浏览器里发送请求
​				请求成功的状态码：200
​				参数：不同的参数，后端会返回不同的数据
​				参数格式：接口url前缀+接口名称？参数名称1=参数值1&参数名称2=参数值2
​						如：http://127.0.0.1/api/yinuo/demo?参数名称1=参数值1&参数名称2=参数值2



json语法规范：
		{
				“名称”:"值1",         #必须是双引号括起来的
				"名称2":"值2"        #最后一条数据不能加逗号
		}

404 Not Found：





