# DAY09:Fiddler基础和综合使用

## 一、Fiddler基本应用

### 1、含义：Fiddler是一款Web调试代理工具

​						Web Debugging Proxy Tool

原先：
		客户端——网络——服务器（Web服务器、数据库服务器）

浏览器（UI测试）http协议  web服务器

Postman（接口测试）

http请求----> 接受并处理 接口程序SQL访问数据库

HTTP响应——————提供结果返回

今天：通过FIddler代理，进行Web请求和响应包的调试

浏览器——fiddler——Web服务器

HTTP请求———>拦截、抓包——>处理方式和之前一样

HTTP响应——>拦截、抓包——响应

作用：为浏览器等客户端提供代理，和Web服务器交互，主要支持HTTP、HTTPS、FTP协议，并且可以代理远程技巧（手机），进行抓包和处理（对数据包进行篡改、重发，可以设置断点、弱网测试、流量监控）

​	经常作为接口测试的辅助工具，进行日常的抓包分析、调试；

​	抓包、捉包：补货数据包（网络协议中的  数据报文）
​														请求包request	响应包response

同类工具：Sniffer 嗅探器、WireShark 网络鲨鱼、Charles 青花瓷

Fiddler支持广泛：三多
						多浏览器：可以对各种浏览器进行代理
						多系统支持：不同操作系统都可使用Fiddler
						多开发平台：java、.net、PHP、python、Ruby等
										采用Web协议都一样，比如 ：HTTP、HTTPS

Fiddler之父：艾瑞克·劳伦斯	互联网 96后

二进制之父：莱布尼茨	0 1  康熙年间	伏羲

计算机科学之父、人工智能之父：艾伦·图灵	二战	图灵奖	

Python之父：Python	89后	吉多·范	Guido van Rossum

java之父：java 95后	詹姆斯·高斯林	James Gosling

### 2、Fiddler的界面基本布局（思路：先整体，后局部）

#### 1）菜单栏、工具条

![image-20220523110848523](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523110848523.png)

#### 3）Web会话列表		4）监控面板

​	任选一条会话												选择：审查员Inspectors	选项卡
​													上面：请求包	Raw	原始的数据包内容
​													下面：响应包	Raw

#### 2）状态栏

界面基本布局

![image-20220523114359040](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523114359040.png)

### 3、开始和停止捕获

#### 方法1:File菜单->Capture Traffic	打勾或取消

​			文件					捕获				信息流

![image-20220523115137813](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523115137813.png)

方法2:F12

方法3:状态栏Capturing	单击 （有、没有）

​								正在捕获中	如果消失表示停止捕获，既是开关，又是刷新

![image-20220523115358793](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523115358793.png)

​	

### 4、清空Web会话列表：工具栏x->Remove All 移除所有

![image-20220523115719128](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523115719128.png)

### 5、为Web会话列表添加列，自定义列

比如：Request Method 	请求方法

技巧：右击列名->选择自定义列-》选择杂项-〉RequestMethon请求

![image-20220523120105109](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523120105109.png)

![image-20220523120146584](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523120146584.png)

![image-20220523220138947](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523220138947.png)

### 6、恢复Fiddler默认设置：按住Shift启动Fiddler

![image-20220523140755845](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523140755845.png)

### 7、常用设置：默认端口、是否代理FTP协议，是否代理远程计算机

步骤：Tools工具-》Options选项-〉Connections选项卡	连接配置

![image-20220523141208946](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523141208946.png)

![image-20220523141414168](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523141414168.png)

点击OK确认配置

### 8、如何捕获HTTPS请求？默认不捕获

默认不捕获HTTPS，为了考虑安全问题

配置位置：Tools-》Options-〉HTTPS选项卡

默认已经选择了：Capture HTTPS CONNETs
								捕获		HTTPS	连接
		进行HTTPS通信前，需要建立安全的连接通道；（为了安全）
		请求方法：Connect

![image-20220523220222248](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523220222248.png)

要求再选择：Decrypt	HTTPS traffic
						解密		HTTPS	数据流
		弹出提示框：是否生成一个唯一的根证书？Yes 是
			HTTPS= HTTP + SSL 安全的套接字层	（安全的加密步骤）

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523142516129.png" alt="image-20220523142516129" style="zoom:50%;" />

弹出提示框，提示：为了拦截HTTPS数据流，Fiddler 要生

成一个唯一的根证书，是否生成？

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523142717992.png" alt="image-20220523142717992" style="zoom:50%;" />

弹出安全警告提示，点击“是”

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523142803549.png" alt="image-20220523142803549" style="zoom:50%;" />

勾选“Decrypt HTTPS traffic”成功

![image-20220523142839762](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523142839762.png)



![image-20220523143012748](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523143012748.png)

最后效果：后续可以捕获到HTTPS的请求

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523143413523.png" alt="image-20220523143413523" style="zoom:50%;" />

经过解码后：

![image-20220523220342228](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523220342228.png)

### 9、查看请求参数技巧：WebForms视图

对于Get方法：QueryString 查询字符串

对于Post方法：Body  主体

![image-20220523145044973](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523145044973.png)

### 10、对客户端的选择

![image-20220523145545281](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523145545281.png)



## 二、Fiddler抓包练习



### 1、**分析数据包结构**

#### 1）以Postman的某请求为例

![image-20220523152046026](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523152046026.png)



结果分析

![image-20220523152601401](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523152601401.png)

#### 2）用Postman发送一个Post请求，在Body部分携带JSON文本

![image-20220523220544806](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523220544806.png)

抓包结果分析：

![image-20220523220606830](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523220606830.png)

#### 3）使用Postman发送一个Post请求，采用**x-www-form-urlencoded** 表单

![image-20220523220631152](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523220631152.png)

抓包结果分析：

![image-20220523220656428](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523220656428.png)

#### 4）使用Postman发送一个Post请求，使用form-data类型

特点：既能提交普通文本，又能够提交1个或多个文件，使用边界符号分隔！（好比：打隔断）

![image-20220523220740675](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523220740675.png)

抓包结果分析：

![image-20220523220803483](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523220803483.png)

观察请求参数：**WebForms**视图

![image-20220523220825735](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523220825735.png)

请求包（请求报文）：

```json
POST http://192.168.198.133/apitest/upload-file/upfiles/?id=123 HTTP/1.1 User-Agent: PostmanRuntime/7.29.0
Accept: */*
Cache-Control: no-cache 
Postman-Token: 76442797-ac61-4847-858d-674bd0ff5ec9
Host: 192.168.198.133 Accept-Encoding: gzip, deflate, br Connection: keep-alive Content-Type: multipart/form-data; boundary=------------------------- -511558446301412780406307 Content-Length: 590

----------------------------511558446301412780406307 Content-Disposition: form-data; name="name" Tom ----------------------------511558446301412780406307 Content-Disposition: form-data; name="age" 23----------------------------511558446301412780406307 Content-Disposition: form-data; name="f1"; filename="hello1.txt" Content-Type: text/plain Hello1 hehe ----------------------------511558446301412780406307 Content-Disposition: form-data; name="f2"; filename="hello2.txt" Content-Type: text/plain Hello2 haha ----------------------------511558446301412780406307--
```

响应包（响应报文）：

```json
HTTP/1.1 200 OK 
Date: Mon, 23 May 2022 07:55:28 GMT 
Server: Apache/2.4.6 (CentOS) PHP/5.6.40 
X-Powered-By: PHP/5.6.40 
Content-Length: 54 
Keep-Alive: timeout=5, max=100 
Connection: Keep-Alive 
Content-Type: text/html;charset=utf-8 
hello1.txt上传成功<br/>hello2.txt上传成功<br/>
```



### 2、通过抓包设计接口测试用例

#### 1）需求：针对百度搜索的词条提示功能，进行接口测试；

搜索栏中改变文本，就会向百度的服务器发送请求，返普通文本，含有JSON文本，就是词条列表信息；

![image-20220523163631073](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523163631073.png)

#### 2）问题：没有接口文档，但是功能可以通过浏览器直接访问；

#### 3）如何解决：通过Fiddler抓包，获取协议的重要信息，还原成接口文档，设计用例并执行；要么直接问百度的开发工程师（目前不现实）

配置Fiddler：

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523163244340.png" alt="image-20220523163244340" style="zoom: 25%;" />

#### 4）打开捕获开关，直接填入：Jmeter	触发搜索和抓包

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523164756463.png" alt="image-20220523164756463" style="zoom:50%;" />

![image-20220523165043151](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523165043151.png)

切换到Row格式，查看数据包：

![image-20220523221303089](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523221303089.png)

请求报文：

```http
GET https://www.baidu.com/sugrec?pre=1&p=3&ie=utf-8&json=1&prod=pc&from=pc_web&sugsid=36455,31254,35912,36166,35978,36055,36232,26350,36301,36468,36312,36447&wd=jmter&req=2&csor=5&pwd=jmte&cb=jQuery110208964885299844363_1653294831845&_=1653294831856 HTTP/1.1
Host: www.baidu.com

```

响应结果：

```
jQuery110208964885299844363_1653294831845({"q":"jmter","p":false,"g":[{"type":"sug","sa":"s_1","q":"Jmeter"},{"type":"sug","sa":"s_2","q":"jmeter性能测试步骤"},{"type":"sug","sa":"s_3","q":"jmeter压力测试怎么测"},{"type":"sug","sa":"s_4","q":"jmeter接口测试步骤"},{"type":"sug","sa":"s_5","q":"jmeter怎么做接口测试"},{"type":"sug","sa":"s_6","q":"jmeter性能测试"},{"type":"sug","sa":"s_7","q":"jmeter参数化"},{"type":"sug","sa":"s_8","q":"jmeter事务控制器"},{"type":"sug","sa":"s_9","q":"jmeter返回中文乱码"},{"type":"sug","sa":"s_10","q":"jmeter压测"}],"slid":"94605287493951","queryid":"0x161560b028e113f"})
```

其中的json文本：

```json
{"q":"jmter","p":false,"g":[{"type":"sug","sa":"s_1","q":"Jmeter"},{"type":"sug","sa":"s_2","q":"jmeter性能测试步骤"},
{"type":"sug","sa":"s_3","q":"jmeter压力测试怎么测"},
                            {"type":"sug","sa":"s_4","q":"jmeter接口测试步骤"},{"type":"sug","sa":"s_5","q":"jmeter怎么做接口测试"},
                            {"type":"sug","sa":"s_6","q":"jmeter性能测试"},{"type":"sug","sa":"s_7","q":"jmeter参数化"},
                            {"type":"sug","sa":"s_8","q":"jmeter事务控制器"},{"type":"sug","sa":"s_9","q":"jmeter返回中文乱码"},
                            {"type":"sug","sa":"s_10","q":"jmeter压测"}],"slid":"94605287493951","queryid":"0x161560b028e113f"}
```

#### 5）使用Postman，新建请求，发送并测试结果是否合理

在新建的day09用例集下，新建请求：test_百度搜索

![image-20220523221325378](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523221325378.png)

改为搜索Postman：

![image-20220523170958880](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523170958880.png)

## 三、Fiddler实际应用技巧、面试题

### 1、面试题：如何使用Fillder进行断点调试？（重要）

#### 1）断点：程序执行过程中，可以设置中断，中断的位置就是断点；

​				源自于编程的调试方法

#### 2）目的：设置断点是为了调试细节，进行对比

​		观察执行过程中的状态，查看和预期是否一致；
​		请求发送时，可以中断，可以修改请求包数据，观察变化；
​		返回响应时，也可中断，可以修改响应包数据，观察变化；
​				比如模拟一些错误提示，交给前端使用，观察前端的反应；
​		（类似Mock模拟任何结果返回，可以测试是否为前端的问题）

如果结果是按照接口文档是合理的，前端显示出现问题，说明是前端的问题！

#### 3）何时使用？

Python、Java等程序执行过程中，可以设置断点，观察中途数据的变化；（编程角度）

目前：Fiddler设置断点
		在发送请求时，观察并修改数据包内容，试探后端的反应；
		在返回响应时，也可以观察并修改数据包内容，试探前端的反应；
		便于调试、发现前端还是后端的问题。

#### 4）分类：断点 BreakPoint		break打断	Point点

##### <1>请求头断点	Before	Requests

​	Fiddler在收到客户端的请求，准备发给服务器之前，设置断点；
​	可以观察数据包细节，修改数据包，再发送

##### <2>请求后断点	After 	Responses

​	Fiddler在收到服务器响应后，准备发给客户端之前，设置断点；
​		可以观察数据包细节，修改数据包，再返回；

原理效果图：

​		客户端————————Fiddler——————Web服务器
​		请求———————>求头断点——————>访问接口程序、后台数据库
​		响应<————————响应后断<———————响应包

#### 5）使用方法：

方法1:Rules菜单	规则

​		Automatic Breakpoints	自动断点

三种选择：

请求头断点	：Before	Requests
响应后断点：After Requests
取消断点：DIsabled	（默认，平时不设置）

![image-20220523175639451](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523175639451.png)

方法2：状态栏 第3个方块按钮 单击可切换

请求头断点：表示正在上传时被暂停了

![image-20220523221427735](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523221427735.png)

响应后断点：表示正在下载时被暂停了

![image-20220523221449448](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523221449448.png)

取消断点：显示空白

![image-20220523221514756](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523221514756.png)

在请求头断点时：

 可以在“审查员”**Inspectors**中，在请求包中查看并修改数据：

 常用**Raw**视图，直接对请求包的源代码修改，最准确、最完整；

 也可用**WebForms**视图，更直观看到请求参数，缺点：可能不是源代码，有误差！

![image-20220523221540850](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523221540850.png)

![image-20220523221556231](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523221556231.png)

前端效果：因为请求参数被篡改了，返回的结果也改变了

![image-20220523221616138](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523221616138.png)

在响应后断点时：

 可以在“审查员”的响应包的Raw视图中，查看并修改数据，再发送；

都可以通过：**Run to Completion** 断点继续，运行直到完成

![image-20220523221636915](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523221636915.png)

前端效果：

![image-20220523221654886](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523221654886.png)

比如：分别使用请求头断点、响应后断点

![image-20220523221714759](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523221714759.png)

前端效果：

![image-20220523221736846](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523221736846.png)

### 2、接口测试笔试题

需求：根据以下接口描述，编写接口测试用例

```
请根据接口信息，编写测试用例 
此接口作用：新增域名，对已有域名进行修改，删除。 
请求方式：POST（请使用HTTPS协议） https://api.weixin.qq.com/wxa/setwebviewdomain 1)
增加域名，数据实例：
{ 
	"action": "add"， 
	"webviewdomain": "www.qq.com" 
	}
```

参数说明：

| 参数             | 是否必填 | 说明                                                         |
| ---------------- | -------- | ------------------------------------------------------------ |
| action           | 必填     | 参数值可为add，delete，set<br />add：添加，delete：删除，set：修改<br />当参数为set时需要填写newwebviewdomain字段，用于新域名名字 |
| webviewdomain    | 必填     | 域名URL，用于指定对哪个域名进行操作，当操作为set时，此值代表久的域名 |
| newwebviewdomain |          | 当参数是set时需要填newwebviewdomain用于指定新域名名字        |

设计用例：

总体说明：采用Post方法，填写URL地址，设置请求参数，不同用例就是参数值不同；目前提交的是

JSON格式文本，将所有参数都“封装”在JSON中提交，采用Body中的Raw格式，提交JSON源代码！

使用Postman:

![image-20220523221944494](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523221944494.png)

```json
用例1:增加一个域名 www.qq.com
{
	"action":"add",
	"webviewdomain":"www.qq.com"
}
用例2:添加重复的域名，判断是否有错误提示
{
  "action":"add",
  "webviewdomain":"www.qq.com"
}
用例3:修改域名www.qq.com为www.qq.com
{
  "action":"set",
  "webviewaomain":"www.qq.com",
  "newwebviewdomain":"www.qqq.com"
}
用例4:删除域名www.qq.com
{
  "action":"delete",
  "webviewdomain":"www.qqq.com"
}

```

### 3、使用fiddler弱网调试（重要面试题）

#### 1）弱网调试：通过模拟低速的网络，观察被测系统是否出现异常；

#### 2）在何处需要使用？

平时，访问互联网时，会遇到网速的不稳定，甚至是低速网络；
比如：移动端，采用无线信号
		移动运营商：2G、3G、4G、5G	从5G->3G->2G降速，对App有何影响
		无线路由：Wifi	局域网

#### 3）如何设置？

对比：Charles比较简单，只需要指定网络带宽（网速）、丢包率等数据；

![image-20220523195225035](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523195225035.png)

​		配置

![image-20220523195344174](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523195344174.png)

​	对比：Fiddler配置稍微麻烦，需要计算出网络的延迟时间，作为配置参数！

##### <1>设置模拟调试参数

Fiddler的Rules菜单->CUstomize Rules自定义规则

修改CustomRules.js脚本	File->Open打开编辑

搜索关键词：m_SimulateModem 	模拟调制   调制：调节和控制

![image-20220523195940527](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523195940527.png)

观察脚本：

![image-20220523200153748](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523200153748.png)

代码分析：延迟时间越长，意味着网速越拖拉，网络越慢

```javascript
if (m_SimulateModem) {
            // Delay sends by 300ms per KB uploaded.
  				//上传每1kb数据包需要延迟300毫秒	发送	1KB=1024B
            oSession["request-trickle-delay"] = "300"; 
            // Delay receives by 150ms per KB downloaded.
  				//下载每1KB数据包需要延迟150毫米	接收	1KB=1024B
            oSession["response-trickle-delay"] = "150"; 
        }
1Byte=8bit
1字节=8个比特（二进制位	00000000～11111111）
1Byte	简称为 1B 
1KB  1024B
1MB	 1024*1024b
1GB	 1024*1024*1024B
1TB	 1024*1024*1024*1024B
行业规律：
		文件、硬盘、内存数据的存储的基本单位：字节 Byte
    16.5KB	1TB		16GB
    网速：带宽bandwidth	单位：bps	bits	per second	比特/秒
			比如：100Mdps	每秒传输100M bit = 100/8 =12.5M Byte
      移动4G的带宽：11Mbps	110*1024*1024 bits/sec
      移动5G的带宽：19Gbps	10*1024*1024*1024 bits/sec
需求：需要使用Fiddler模拟2G网速（弱网）
已知：上行带宽（上传）：2.7	Kbps	K bits/sec
		下行带宽（下载）：9.6	Kbps	
    
 计算出：上传每1KB数据，需要延迟多少时间？（毫秒）
 				8k bit		x
        ------ =	------
        2.7k bit	1000毫秒		1秒=1000毫秒
        x = 8/2.7*1000 = 2963ms
        
        下载每1KB数据，需要延迟多少时间》（毫秒）
					8k bit		y
          ------	=	------
          9.6k bit		1000ms
      y = 8/9.6*1000 = 833ms
      以上代码修改为：
      if (m_SimulateModem) {
            // Delay sends by 300ms per KB uploaded.
  				//上传每1kb数据包需要延迟300毫秒	发送	1KB=1024B
            oSession["request-trickle-delay"] = "2963"; 
            // Delay receives by 150ms per KB downloaded.
  				//下载每1KB数据包需要延迟150毫米	接收	1KB=1024B
            oSession["response-trickle-delay"] = "833"; 
        }
    
```

![image-20220523202716961](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523202716961.png)

##### <2>开启弱网调制：

设置Rules->Performance 表现-> 点击 Simulate Modem Speeds. 开启弱网模拟
																		模拟		调制		速度

![image-20220523203046786](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523203046786.png)

##### <3>关闭弱网调制：

设置Rules->Performance 表现-> 点击 Simulate MOdem Speeds. 取消弱网模拟

客户端效果：速度恢复
