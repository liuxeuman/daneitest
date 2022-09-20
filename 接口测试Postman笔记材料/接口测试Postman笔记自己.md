[TOC]



# 课程介绍

## 一、接口测试基础（接口测试工具）

### 1、接口的本质

### 2、网络协议和接口的关系

### 3、Postman

### 4、Fiddler

### 5、接口测试流程

## 二、接口测试高级（接口自动化测试，python+requests）

### 基本内容：线性编程、函数、类、模块、包、测试框架pytest、unitest...

### Day01:测试环境搭建、接口基础、Postman基本使用

## 一、环境资料下载和安装

#### 1、首先下载和安装VMware

说明：VMware15或16，苹果笔记本用不了

#### 2、下载并解压Windows虚拟机文件

说明：可以在其中任意搭建环境，和物理机相对独立，作为测试机使用

​		目前测试机先使用物理机

#### 3、下载并解压WA服务器.rar

##### 1)目的：被测系统服务器

##### 2）特点：被测软件已经安装好了

##### 3）解压即可使用，打开后调节快照，可以恢复测试环境

##### 4）查看服务器ip

###### 	ifconfig ens33...

###### 或过滤出IP地址  ifconfig



###### 每个同学、每次重启后IP地址可能不同

##### 5）关于数据库

###### 数据库主机名（IP地址）：同上

###### 数据库的用户名：root。  密码：123456

###### 数据库名称：wa_test     （show databases 查看。  use wa_test选择某数据库）

###### 表：users用户表，info个人信息表 （show tables 查看   desc users 查看表结构）

###### 客户端工具：SQLyog连接和管理数据库资源

######  打开后，直接在命令行窗口中回车，查看IP地址，比如192.168.198.133

 打开浏览器，复制粘贴以下网址，回车，
 http://IP地址/apitest/get-json/
 比如：
 http://192.168.72.130/apitest/get-json/
 能返回以下内容表示服务器连接成功：
 {"age":22,"isNul":null,"isVip":true,"name":"Balla_兔子"}

#### 4、安装测试工具

##### 参考《接口测试工具安装.pdf》

##### 注意：先不要安装JMeter

#### 5、虚拟机联网配置

##### 通过VMware的设置-〉网络适配器

 	可以使用“桥接”或“仅主机“



## 二、接口基础知识

### 1、接口金字塔模型

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220512110306759.png" alt="image-20220512110306759" style="zoom: 25%;" />

#### 1）UI层：用户层面（User InterFace）便于上手，但是发现问题的能力较弱，

#### 2）Service层：服务层，也就是接口层，可以进行接口测试，要求接口测试技术，提前介入测试，发现问题的能力较强；（目前接口测试占比在提升30-50%以上）

#### 3）Unit层：单元层，可进行单元测试，更早介入，更底层，发现问题能力更强，技术要求更高

#### 不同层关系类比：

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220512111101093.png" alt="image-20220512111101093" style="zoom:25%;" />

结论：接口测试属于“灰盒测试”，既“表面”——便于开展测试，又靠近“底层”——便于发现问题。

### 2、接口的重要概念

#### 1）接口

##### 目前特指软件接口，以Web项目为背景，主要是Web接口

##### 接口也叫API（Application Programming Interface）应用程序编程接口

本质上是开发方编写的函数或方法（程序），是对某业务功能的设计和实现！

内涵，存在设计文迪昂（开发文档）——接口文档（API文档）、数据库设计文档...

​	由开发方的设计师设计，由开发方的程序员实现代码，由测试方测试接口！

#### 2）UI测试和接口测试的区别

##### Web前端：以浏览器为代表的技术，比如HTML（网页语言），JavaScript（前端动态脚本）、CSS（层叠样式表），都是在浏览器执行出现UI漂亮的、带有交互的界面。

##### Web后端：由后台服务器开发技术构成，比如Java Web开发技术、数据库、SQL、接口程序、都在后台执行，比如目前Wa服务器运行接口程序。

​	Web：实现B/S架构的全套技术规范，包括Web前端、Web后端技术；

​			（Browser/Server）浏览器/服务器

​			通过接口将Web前端、Web后端进行连接，通过前端访问后端。

##### <1>UI测试的原理：有用户界面，更直观，让用户更好上手，但难以发现后台问题

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220512114822088.png" alt="image-20220512114822088" style="zoom: 33%;" />

##### <2>接口测试的原理：在没有用户界面时，使用专业的工具充当用户界面

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220512115348707.png" alt="image-20220512115348707" style="zoom:33%;" />

内部接口：WA服务器提供的功能（公司内部开发、提供的）

http://192.168.72.130/apitest/get-json/

外部接口：比如京东商城  根据商品类别编号查询商品页面。  类别编号存于数据库

​				（其他机构提供的）

https://list.jd.com/list.html?cat=9987,653,655  查询手机商品页面

https://list.jd.com/list.html?cat=670,671,672   查询电脑商品页面

#### 3)客户端、客户机

##### <1>PC(个人电脑)

##### <2>安装浏览器，比如：Chrome、Edge、Firefox、IE等

##### <3>安装测试工具，比如：Postman、Fiddler、JMeter、Python等

比如：目前采用Postman+Fiddler组合

##### <4>通过某种网络协议、规则访问服务器

#### 4）服务器：

##### <1>分为Web服务器、数据库服务器

##### <2>Web服务器：web中间件（提供Web常用服务的软件）

​	运行接口程序的载体，是Web应用程序的“容器”，内部安装了许多接口程序

#### 5）请求（Request）

客户端向服务器发送HTTP请求（HTTP Request），为了获取服务器的资源，访问服务器的接口程序，进而可能访问到数据库；请求是将客户端的数据发给服务器进行处理，由某接口程序接收并处理；

​	请求包分为请求头部 和 请求主体：

##### <1>请求头：header

​	请求的附加信息，如客户端的操作系统、客户端使用的浏览器、客户端能够接受的字符编码、授权、客户端是否携带Cookie信息（数据消息）等；

​	尤其包括：访问接口的三要素

​		请求方法（Get或Post）、接口地址、请求参数

​							索取    提交

​	比如：以Get方法

​				接口地址：https://list.jd.com/list.html

​				请求参数：类别编号 cat 值 9987，653，655

​												category                              						product

​				目的：根据商品类别编号（手机类别）查询和手机有关的商品

##### <2>请求主体：body

 	Get方法，主体部分没有内容（0字节）

​	Post方法，发送的数据主要放在主体中携带！	

#### 6）响应（Response）

​	服务器将接口程序处理的数据结果，返回给客户端的过程；

​	响应包分为响应头部 和 响应主体：

##### <1>响应头：header

​	响应的附加信息，如HTTP响应状态码、响应内容类型（网页HTML、JSON文本、XML文本）、是否要求客户端设置Cookie信息等；

##### <2>响应主体：body

​	响应的正文部分，是接口的返回值，是测试时最关心的部分。

### 3、接口的组成要素

#### （1）接口地址（URL地址，URL：统一资源定位）就是一个网址

##### <1>形式：

​	http://192.168.72.130/:8000/sign/add_event/

​	协议名：//服务器主机名：端口号/应用名称/接口名 

##### <2>协议

HTTP（超文本传输协议）、HTTPS（安全的HTTP）、FTP（文件传输协议）、SMTP（简单邮件传输协议）、POP3（邮局协议第3版本)...

​	测试时，用什么协议，看需要和设计！

##### <3>服务器主机名：IP地址或域名

​	测试时，服务器IP地址是什么，就写什么；

​	局域网：内部接口访问，一般使用IP地址；比如：192.168.72.130

​	互联网：外部接口访问，一般使用域名；比如：list.jd.com

##### <4>端口号，比如8000

​	端口号是用一个数字表示使用服务器上的哪个软件 或 服务；

测试时，使用哪个端口号，是由环境搭建人员制定的；

行业中，默认端口：	

​		HTTP服务，默认80；HTTPS服务，默认443，一般可以省略不写

http://www.baidu.com. :80 可省略不写

Https://www.baidu.com :443 可省略不写

非默认，比如规定为8000，必须要写！

##### <5>应用名，比如sign

​	被测软件的名称或简称，由接口程序开发者设计的；

​	测试时，应用名是什么，要看需求；

##### <6>接口名，比如add_event

接口名也是接口文档设计好的，由大量程序员实现接口程序，我们测试；

实际测试时，接口名字很多，需要查看接口文档！

接口名末尾一般会带/，是否可以省略，要看设计。

#### （2）请求方法Reqeust Method

##### <1>如何发送和处理数据

##### <2>常见的请求方法（面试题）

get：主要用于获取资源（索取） 常用于查询、删除操作

post：主要用于提交资源（给予） 常用于增加、修改、删除

put：主要用于更新资源  一般是全部更新

patch：主要用于更新资源   一般是部分更新

delete：主要是用于删除资源

connect：在HTTPS安全通信时，先建立安全的连接通道

测试时，使用哪种犯法，取决于接口的设计和需求！

#### （3）请求类型：

​	Get方法不用考了，在遇到Post方法时需要区分以下类型：

##### <1>form表单：x-www-form-urlencoded

​		把要发送的数据a=1&b=2的形式放在请求主体（body）中

​									名称=值&名称=值& ...

##### <2>json: application/json

​	把要发送的数据以{"a":1,"b":2}的形式放在请求主体（body）中

##### <3>form-data：multipart/form-data

​	表单数据，用于发送文件，把客户端要提交的文本、文件放入请求主体（body）中携带！

​	测试时，选择哪种请求数据类型，取决于需求 和 设计；

#### （4）参数

客户端发送给服务器，提供的一些条件数据；

本质：要求服务器上的接口程序 处理的数据

比如：登录接口。需要提交 用户名 和 密码

##### <1>对于Get方法

参数放在URL地址中，属于请求的头部

http://192.168.72.130:8000/sign/add_event/?id=1&name=Tom

URL地址后  ？参数名=参数值&参数名=参数值&....

​						(QueryString 查询字符串)

id和name都是参数名

1和Tom都是参数值

名值对 & 拼接多对数据，表示“与”、“和”的意思 and

##### <2>对于Post方法

参数放在请求主体（body）中

具体形式，参考请求类型

测试时，接口是否有参数，参数的含义，名称和值，哪些是必须的，哪些是可选的，参数类型是什么，是否有约束，都要看接口文档，需求！

#### （5）返回值/响应结果

##### <1>HTTP响应状态码（Status Code）（面试题）

Web规范规定的，通过不同的响应码表示不同地问题，使用3位整数表示：

200：成功响应OK，表示服务器成功把结果返回给客户端，但内容有待查验；

301:永久重定向，如网址发生了永久改变，访问旧网址时自动跳转到新网址；

302:临时重定向，如登录成功后，跳转到新页面；

400:域名/服务器地址。 不存在或 请求错误（主要是参数错误）

401:客户端错误，需要授权，必须先提供有效认证，才能访问接口；

403:客户端错误，如客户端IP被封禁、客户端无法读写权限、客户端整数错误

404:客户端错误，资源找不到。访问接口的地址写错了，比如应用名，接口名

​						Not Found 找不到

500:服务器端错误，如服务器后台接口程序执行出现异常Exception、错误Error

​			后台接口程序出现bug的重要依据！

​	比如：NullPointerException 空指针异常。 访问空的内容！



技巧：Web官方资料

​	搜索：w3shchool

HTML->HTML参考手册->消息

1xx：信息 正在传输中，可先不关注

2xx：成功   不代表结果内容一定正确

3xx：重定向   重新开始一个请求

4xx：客户端错误 	要关注

5xx：服务器端错误		要重点关注！

##### <2>响应类型：

text/html：网页源代码 	文本

json：json文本、字符串

xml：XML配置文本

##### <3>响应体、响应文本（正文）

测试时，必须验证响应文本中的数据是否正确（符合需求）！

接口测试：为了测试请求包 和 响应包 和实际是否一致！

比如，返回json文本：

age":22,"isNul":null,"isVip":true,"name":"Balla_兔子"}

##### <4>对数据库的影响

测试时，必须确保数据库的数据操作也是正确的；

比如：登录时，确保数据库中有此记录；

​		注册后，确保数据库中添加了一条新纪录，（验库）

## 三、接口测试与接口自动化测试

### 1、接口测试

测试接口的功能、性能、安全性（来自需求）

功能：请求包和响应包 数据交互是否正确！

​			接口测试的“灵魂”：协议！ HTTP请求、HTTP响应

### 2、为什么要做接口测试？

#### （1）目前的开发进行前端 和 后端 分离的，便于分工实现；

#### 			通过接口 将前后端 对接

#### （2）界面UI测试：只关注了前端

#### 			接口测试：绕过前端，对后端的接口API进行测试

#### （3）测试左移：提前介入测试，提早发现问题，从更深层次发现问题

#### 			左右，对应前后

#### 			目的：降低后续的测试成本！  趋势：接口测试占比在增加 50%以上

### 3、接口测试的方法

#### （1）接口测试工具：初级的自动化测试

##### Postman+Fiddler

##### 或SoupUI+Fiddler

##### 或JMeter+fiddler

#### （2）高级自动化测试

#### Python+requests或Java技术

### 4、接口自动化测试

#### （1）靠工具和代码实现测试

#### （2）自动准备测试数据、自动执行用例、自动验证响应是否正确、自动验证数据库的数据是否正确、自动生成测试报告		

#### （3）接口测试的步骤

##### <1>需求分析、分析接口文档

##### <2>编写测试用例

##### <3>编写并调试代码/脚本

##### <4>搭建测试环境

##### <5>执行测试



## DAY02

## 复习

### 1、什么是接口？

​	API：应用程序编程接口	属于软件接口

特点：符合需求，开发方设计和实现，用户可以重复使用的功能

比如：Web接口、HTTP接口

基本访问要素？请求方法、接口URL地址、请求参数

Get方法 															类别编号=编号的值

https://list.jd.com/list.html?cat=9987,653,655

协议名://服务器域名：端口号/应用名/功能名？参数名=参数值

​									：443可省略

协议名：https		安全的HTTP协议

接口名：京东商城的商品模块中  根据商品类别编号查询商品列表页面

域名：list.jd.com

功能名：list.html 		列出商品信息页面

参数名：cat 			商品类别编号

参数值：9987，653，655 		有效商品类别数据，表示手机类别（京东数据库中）

预期结果：找到和手机有关的商品信息

### 2、为什么需要测试接口？

1）测试左移：提前介入测试，在前端未开发好时，可以通过测试接口，测试系统的功能、性能、安全等问题；

2）能够更深层次发现问题，发现问题的能力更强；

3）提高技术竞争力（就业薪资）

### 3、哪里需要测试接口？

看需求和接口的文档

​	只要是接口文档中描述的接口，一般都有重点测试！

### 4、如何测试接口？

1）分析需求

2）分析接口文档

3）搭建测试环境：

测试机Postman

服务器WA服务器，带有Mysql数据库

网络：局域网（内网）

4）设计接口测试用例

5）执行用例，发送请求，观察结果

6）提交缺陷，编写测试结果报告

结论：接口测试为了测试前端和后端之间的数据交互是否符合预期。

​			数据交互的核心：协议！ 数据包！Request请求包 和 Response应答包



## 一、Postman的基本使用

### 1、Postman简介

Postman是一个接口测试工具，作为开发人员、测试人员，测试和调试接口的客户端工具。重点是发送HTTP请求，获取响应结果，能够自动判断结果是否正确，可以展开接口的自动化测试。

### 2、Postman的使用步骤

#### 1）创建工作区（Workspace）

类似于管理一个项目

#### 2）创建用例集（Collections）

类似于模块、子模块

#### 3）创建文件夹（Folder）

将不同的接口用例分开管理

#### 4）创建请求（Request）

对应访问某接口，表示执行某条用例

核心：请求方法、接口地址、请求参数（Post方法还要指定请求类型）

#### 5）发送请求Send

以Postman作为客户端，将请求发给服务器，一般会携带参数，

从服务器返回响应结果，后续判断响应结果是否正确

区别：

​	HTTP请求：Request。客户端想Web服务器发送HTTP请求

​	HTTP响应：Response。Web服务器想客户端返回HTTP响应、应答

### 3、Postman工具基本功能介绍

#### 1）界面

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220513103714223.png" alt="image-20220513103714223" style="zoom: 33%;" />

#### 2）登录和注册

#### 3）设置

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220513104803966.png" alt="image-20220513104803966" style="zoom: 50%;" />

#### 4）新建工作区

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220513105420110.png" alt="image-20220513105420110" style="zoom:50%;" />

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220513105705019.png" alt="image-20220513105705019" style="zoom:50%;" />

#### 5）新建用例集：目前管理每天的用例（请求案例）

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220513110334189.png" alt="image-20220513110334189" style="zoom:50%;" />

#### 6）新建请求

在某用例集，某文件夹下，可以新建请求Add Request

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220513112652343.png" alt="image-20220513112652343" style="zoom: 50%;" />

### 4、案例与练习

#### 案例01:get方法访问百度首页

​	请求名称：test01_get方法访问百度首页

​	请求方法：Get

​	接口地址：https://www.baidu.com

​	参数：无

​	返回格式：text/html 		文本/HTML网页	就是网页HTML源代码文本

#### 关于请求的配置说明

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220513114218488.png" alt="image-20220513114218488" style="zoom:33%;" />



<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220513115354169.png" alt="image-20220513115354169" style="zoom: 50%;" />

#### 技巧：通过查看Console，查看Postman工作的过程，查看请求包，响应包的实际内容，作为调试接口用例的重要工具！

清空，使用Clear按钮

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220513141551251.png" alt="image-20220513141551251" style="zoom: 33%;" />

#### 案例02:get方法访问京东商城，根据商品类别编号查询商品信息页面

​	请求名称：test02_get方法访问京东商品列表

​	请求方法：Get

​	接口地址：https://list.jd.com/list.html

​	参数：

| 参数名 | 参数值       | 说明                         |
| ------ | ------------ | ---------------------------- |
| cat    | 9987,653,655 | 商品目前有效的商品类别：手机 |

请求举例：https://list.jd.com/list.html?cat=9987,653,655

返回格式：text/html

预期结果：含有手机类别有关的商品页面

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220513143807221.png" alt="image-20220513143807221" style="zoom:50%;" />

之前的案例主要访问“外部接口”，接口功能由百度、京东等机构提供；

后续多是访问“内部接口”，局域网内搭建了自己的服务器，部署了开发团队开发的接口程序，带有数据库环境Mysql；

前提：观察需求文档、接口文档（API文档、开发文档）、数据库说明书（数据字典DD），比如《apitest接口需求》结合了接口文档、数据库说明书。

练习：写一条sql语句，查询出admin账户的详细个人信息

思路：先通过子查询，查询users表，用户为admin的id是多少；

​		再通过主查询，查出info表中id为1的用户信息。

```sql
select * from  info where id=(select id from users where username='admin';
```

+----+-----------+--------+------------+----------+--------------------------+-------------------------------------+ | id | name      | gender | birth      | work_age | major                    | introduce                           | +----+-----------+--------+------------+----------+--------------------------+-------------------------------------+ |  1 | 管理员    | 男     | 1985-03-27 |       10 | 计算机科学与技术         | IT技术宅男，此处省略400字           | +----+-----------+--------+------------+----------+--------------------------+-------------------------------------+ 1 row in set (0.28 sec)

#### 案例03:test03_get方法访问无参的ui-login 接口

接口地址：http://192.168.72.131/apitest/ui-login/

请求方式：get 

参数：无 

返回格式：text/html 

预期包含文本：<td align=right>用户名<td><input type="text" name="username" 

size=20 maxlength=18>



<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220513161017674.png" alt="image-20220513161017674" style="zoom:75%;" />



#### 案例04:get访问无参接口

请求名称：test04_get方法访问one-param 接口

接口地址：http://192.168.72.131/apitest/one-param/

请求方式：get 

参数：无 

返回格式：text/html 

预期包含文本：请使用 ID 参数进行访问

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220513164136784.png" alt="image-20220513164136784" style="zoom:50%;" />

#### 案例05：get访问无参返回Json的接口

请求名称：test05_get访问无参接口并返回Json文本

请求方法：Get

接口地址：http://www.httpbin.org/get

参数：无

返回格式：Json

预期返回结果，形态为符合JSON语法格式的文本：

key键			velue值

```json
{"key1":"velue1","key2":"velue2"}
```

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220513170610001.png" alt="image-20220513170610001" style="zoom: 33%;" />



案例06:get获取Json数据

请求名称：test06_get获取Json数据

接口功能：获得 json 数据 

接口地址：http://192.168.72.131/apitest/get-json/ 

请求方式：get 

参数：无 

返回格式：json 

预期：包含 json 对象/json 字符串



#### 案例07:get访问有参接口

接口功能：根据用户id查询用户名

请求名称：test07-get根据用户id查询用户名

接口地址：http://192.168.72.131/apitest/one-param/ 

请求方法：get 

参数：id（含义：用户编号） 

| 参数名 | 参数值 | 说明                                     |
| ------ | ------ | ---------------------------------------- |
| id     | 1      | 用户id，从数据库user表中查到有效的id数据 |

数据库和表：用户信息存储在 wa_test 数据库的 users 表中 

响应类型：text/html 

预期返回：显示用户名、显示用户信息不存在

有效的数据：数据库users表中有此id

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220513175149003.png" alt="image-20220513175149003" style="zoom:33%;" />

无效的数据：数据库users表没有此id值

### 5、导出和导入测试用例集合

#### 1）导出：为了备份和分享

Export

#### 2）导入：为了复用和恢复

Import



## DAY03：Postman的使用，Json语法

## 复习：

### 1、访问接口的要素

比如：访问HTTP接口

#### 1）请求方法：Get或Post方法

#### 2）接口地址：URL地址

#### 3）请求参数：

​	Get请求参数以“查询字符串”格式在URL地址后携带（请求头部数据）

​		URL？参数名=参数值&参数名=参数值&....

Post请求参数主要在请求主体body部分携带

#### 4）响应结果：

HTTP响应码：200		302		404		500

​						成功		重定向	客户端错误		服务器错误

根据需求返回不同格式的结果：

html、json、xml、图片img、png、gif等格式

#### 5）必要时需要对数据库进行查验（验库）

### 2、Postman基本使用步骤？

#### 1）新建工作区Workspace  	对应某项目

#### 2）新建用例集Collections		对应某接口

#### 3）新建文件夹Folder				对应子接口、不同方法

#### 4）新建请求Request				对应某条用例、对接口的访问

##### 	请求方法，接口地址、请求参数	...

#### 5）发送请求，分析结果 Response

##### 	响应头部：比如HTTP响应码、响应内容类型

##### 	响应主体：返回的主要文本

#### 案例：使用多参数接口

##### 新建用例集day03

##### 接口功能：根据用户id、username查询用户的注册时间

##### 请求名称：test01_multi_params接口			意思：多个参数

##### 请求方法：Get

##### 接口地址：http://192.168.72.131/apitest/multi-params/

##### 请求参数：

| 参数名   | 参数值 | 说明                     |
| -------- | ------ | ------------------------ |
| id       | 1      | 用户id，比如使用有效数据 |
| username | admin  | 用户名，比如使用有效数据 |

##### 响应类型：text/heml		网页源代码文本

##### 预期返回：

##### 		如果存在，显示用户名和注册时间

​				{"登录名":"admin","注册时间":"2020-07-15 15:30:47"}

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220516102253736.png" alt="image-20220516102253736" style="zoom:33%;" />

##### 		如果不存在，显示用户信息      

​				{"Message":" 用户信息不存在"}

查看数据库：

​				<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220516102810133.png" alt="image-20220516102810133" style="zoom:33%;" />



## 一、JSON核心语法

### 1、对比三种文本格式的特点

#### 1）普通文本：优点：简单		缺点：无法表示复杂的数据信息

A，AB，ABC，CD，BC，....

1,12,123,34,23,...

name=Tom

age=23

salary=16000.6

#### 2）XML文本：可扩展标记语言（先了解）

##### 优点：可以表示非常复杂的数据层次关系

##### 缺点：数据比较臃肿，生成、解析、查找数据不方便

​	第一行固定的：xml文的声明，表示以下按照xml语法表示

​	表示的含义：中国的部分省市关系信息 	国家、省、城市

```xml
<?xml version="1.0" encoding="utf-8"?>
<country>
    <name>中国</name>
    <province>
        <name>黑龙江</name>
        <cities>
            <city>哈尔滨</city>
            <city>大庆</city>
        </cities>
    </province>
    <province>
        <name>广东</name>
        <cities>
            <city>广州</city>
            <city>深圳</city>
            <city>珠海</city>
        </cities>
    </province>
    <province>
        <name>山东</name>
        <cities>
            <city>济南</city>
            <city>青岛</city>
        </cities>
    </province>
    <province>
        <name>新疆</name>
        <cities>
            <city>乌鲁木齐</city>
        </cities>
    </province>
</country>
```



#### 3）JSON文本：（熟练掌握）

优点：既比普通文本复杂，能够储存比较复杂的业务数据；

​			又比XML简单，更精简，便于生成和解析；

缺点：几乎没有，目前作为接口采用的数据文本交换格式。

```json
{
    "name": "中国",
    "province": [{
        "name": "黑龙江",
        "cities": {
            "city": ["哈尔滨", "大庆"]
        }
    }, {
        "name": "广东",
        "cities": {
            "city": ["广州", "深圳", "珠海"]
        }
    }, {
        "name": "山东",
        "cities": {
            "city": ["济南", "青岛"]
        }
    }, {
        "name": "新疆",
        "cities": {
            "city": ["乌鲁木齐"]
        }
    }]
}
```

### 2、什么是JSON？JavaScript对象表示法

#### 1）JSON是介于普通文本和XML之间的一种数据文本格式；

​	既比普通文本复杂，又比XML简单，便于生成、表达、解析。

#### 2）JSON相比XML更轻量化，提高网络传输效率；

#### 3）JSON是一种跨平台、跨语言的文本；

#### 4）JSON具有面向对象特性，主要存储对象的属性数据！

面向对象思想初步：

类：class 类别		各种事物的概念、抽象 			人、车、动物、水果、

对象：	object目标、个体				某类事物的具体代表、个体、实例

​				比如：我的那辆车、我自己、我的那只宠物旺财、他手里的那个苹果、

​							某一个具体的JSON文本

​				

#### 5）接口测试经常使用JSON、XML作为返回结果的文本格式，有时发请求的参数也用；目前更多会使用JSON；

——主流的数据交换的文本格式

{ "登录名": "admin", "注册时间": "2020-07-15 15:30:47"}

### 3、基本语法

#### 1）JSON对象使用{}包围

#### 2）属性数据以“**名值对**”表示		区分大小写

​	“属性名”：属性值		说明：其他语言的属性吗，几乎没有加双引号

​	目前也称为：键值对	key-value		键具有唯一性	属性吗如果重复出现只认一个

比如：{"name":"Tom","name":Mary}	最后name值为Mary	写多次无意义

#### 3）多对属性之间使用逗号，分隔

```json
{"name":"tom","age":23}
```

错误写法：

{name:"tom",age:23}			JSON属性名都必须有英文双引号

{'name':'Tom,'age':23}			不支持单引号

#### 4）数组使用[]表示，内部元素所有逗号，分隔[,,,]

​	数组：表示一组数据，按照书写顺序排列

​	比如：["春","夏","秋","冬"]	

​				["篮球","游泳"]

​				[98,85,76]

#### 5)数据类型：

##### <1>字符串："文本"		必须使用双引号

##### <2>数字：整数、小数	直接写		比如：123		123.567	为了算术运算方便

##### <3>逻辑值：true	false	必须全小写	为了进行条件判断

​						真			假

##### <4>空值：null		表示该值没有意义，什么也不是

##### <5>对象：{}	其中写属性名、属性值

##### <6>数组：[]便于罗列数据

#### 6）JSON属性值可以是数组、对象，数组中的元素可以是JSON的任意类型，包括对象，数组，可以相互**嵌套**

比如：Tom有辆车

```JSON
{
  	"name":"Tom",
  	"car": {
  			"name":"BMW",
  			"price":56.8
		 }
}
```

比如：Tom有多辆车，属性值使用数组，数组的元素又是对象

```json
{
  	"name":"Tom",
  	"cars":[
      	{"name":"BMW","price":56.8},
        {"name":"劳斯莱斯","price":678.3}
    ]
}
```

​		简单的看：数组就是一组数据

```json
{
  	"id":1,
  	"name":"admin",
  	"cars":["BMW","劳斯莱斯","兰博基尼"]
}
```

对象的属性数据：成对出现	"id":1	多对数据逗号分隔

数组中的数据：没有名称，数据使用逗号分隔

##### 练习1:使用JSON语法表示一个员工的基本信息：

```JSON
{
  	"id":"1001",
  	"name":"张无忌",
  	"gender":true,
  	"birthday":"1998-09-16",
  	"salary":16000.50,
  	"job":"软件测试",
  	"tel":"13811889966",
  	"desc":null,
  	"hobby":["耍剑","骑马","摄影"],
  	"skill":[
  			{"name":"九阳神功","grade":9},
      	{"name":"乾坤大挪移","grade":9},
      	{"name":"太极拳","grade":9}
  ]
}
```

##### 练习2:阅读大量接口文档，看懂JSON示例

比如：天气预报接口文档、

###### （1）根据手机号码前7位查询归属地和运营商的结果：

```json
{
    "resultcode": "200",
    "reason": "Return Successd!",
    "result": {
        "province": "北京",
        "city": "北京",				//归属地
        "areacode": "010",
        "zip": "100000",
        "company": "移动",			//	运营商
        "card": ""
    },
    "error_code": 0
}
```

##### （2）根据无效的城市名查询天气返回的结果：

```json
{
    "reason": "暂不支持该城市",
    "result": null,
    "error_code": 207301		//接口文档设计的错误码 表示	错误的查询城市名
}
```

##### （3）查询出北京5月16日的天气预报：

```json
{
    "reason": "查询成功!",
    "result": {
        "city": "北京",
        "realtime": {
            "temperature": "22",
            "humidity": "19",
            "info": "晴",
            "wid": "00",
            "direct": "西北风",
            "power": "4级",
            "aqi": "29"
        },
        "future": [
            {
                "date": "2022-05-16",
                "temperature": "13/29℃",
                "weather": "晴",
                "wid": {
                    "day": "00",
                    "night": "00"
                },
                "direct": "南风"
            },
            {
                "date": "2022-05-17",
                "temperature": "15/30℃",
                "weather": "多云转晴",
                "wid": {
                    "day": "01",
                    "night": "00"
                },
                "direct": "南风转北风"
            },
            {
                "date": "2022-05-18",
                "temperature": "17/31℃",
                "weather": "多云",
                "wid": {
                    "day": "01",
                    "night": "01"
                },
                "direct": "西南风"
            },
            {
                "date": "2022-05-19",
                "temperature": "16/30℃",
                "weather": "晴",
                "wid": {
                    "day": "00",
                    "night": "00"
                },
                "direct": "西南风"
            },
            {
                "date": "2022-05-20",
                "temperature": "17/30℃",
                "weather": "晴",
                "wid": {
                    "day": "00",
                    "night": "00"
                },
                "direct": "南风"
            }
        ]
    },
    "error_code": 0
}
```



### 4、技巧：在线JSON校验、格式化工具		json.cn

https://www.json.cn		要求：浏览器使用Chrome、Edge

原理：通过前端技术JavaScript脚本处理，存在浏览器兼容性问题！

注意：粘贴文本时要使用ctrl+v才可触发校验程序

#### 1）在线校验

检查JSON语法是否正确，如果有错误，会提供错误提示：错误行号、错误原因

#### 2）在线格式化

##### <1>格式化之前：原始格式	Postman中Raw	经过“压缩”后的文本

​					去除了分隔空白，换行符，只需要写成一行文本即可；

​	优点：紧凑，网络传输效率高

​	缺点：可读性差

##### <2>格式化之后：Postman中 Pretty 美观的

​	优点：可读性好，便于人阅读

​	缺点：网络传输效率低，比较费流量

##### <3>如果将json文本保存使用，文件拓展名是.json

比如：emp1.json  保存刚才张无忌的信息

​		使用文本编辑器，比如记事本就可编辑

### 二、Postman使用全局变量

#### 1、什么是全局变量？（参数化的一种形式）

在整个工作区中，定义所有用例集都能“看见”的数据

​	变量名 和 变量值

​	name			Tom 	改为Mary  	改为Andi

后续当前工作区使用请求，使用name就能指代其值Tom

优点：名称不用改变，值可以改变，通过修改变量的值，让所有用例的数据都改变

#### 2、为什么需要使用全局变量？

在请求中，大量使用的数据，如果直接写，称为“字面值”，优点是直观，确定是如果需要改变，就会大面积改变，非常麻烦；

通过全局变量，使用时只需要写全局变量名，就能找到其值

如果修改时，只需要修改一次，就能大面积改变。（改一处，则处处改变）

#### 3、哪里需要使用全局变量？

比如：大部分请求需要统一使用的数据

​		IP地址、URL地址、认证码... 		"大家都指望的数据"

比如：每个请求频繁要改变的数据，比如登录时使用用户名、密码

​		适合作为局部变量（后续再补充：参数化）

#### 4、怎么使用全局变量？

需求：将当前工作区中所有的WA服务器IP地址，都使用全局变量，变量名ip1，变量值根据WA服务器实际查询结果填写，供后续请求使用。

##### 1）需要在Postman中设置全局变量

提供变量名、变量值，第一次给变量赋值（初始化）

后续可以改变变量的值，作为当前值

修改位置：右上角的“小眼睛”图标 	环境快速查看

步骤1:打开“小眼睛”

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220516170016583.png" alt="image-20220516170016583" style="zoom:33%;" />

步骤2:设置全局变量名、初始值，后续可更改

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220516170332716.png" alt="image-20220516170332716" style="zoom:33%;" />

取消打勾，表示不使用该全局变量

原因：查看WA服务器IP地址

如果需要添加：点击Edit，添加新的变量值

#### 2）后期请求都可使用ip1表示具体的IP地址值

用法：{{变量名}}	表示其值：192.168.72.131

比如原先的URL地址：http://192.168.72.131/apitest/multi-params

可以改为：http://{{ip1}}/apitest/multi-params

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220516172251771.png" alt="image-20220516172251771" style="zoom:33%;" />

如需修改：需要点击小铅笔编辑

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220516172204046.png" alt="image-20220516172204046" style="zoom: 33%;" />

##### 练习：将day02、day03用例集中所有ip地址都改为全局变量{{ip1}}

​				全局变量在整个工作区中，所有用例集都可用



Day04

# Postman发送Post请求，检查点（断言）

## 复习：

### JSON 	Web前端和Web后端之间交互的文本格式

​			客户端可以将JSON文本提交给服务器

​			服务器会将JSON文本结果返回给客户端

​			测试时，关注数据收发是否正确

​			具体语法参考Day03笔记，多看例子对比分析

### 全局变量：通过全局变量名，统一管理工作区、用例集中的常用数据

​	定义时：工具配置“小眼睛” 	使用时：{{变量名}}

## 一、Postman发送Post请求

### 1、面试题：Get请求和Post请求有何区别？

#### 1）请求参数：的位置不同：

##### Get请求：请求参数一定是在HTTP请求包的头部header携带！

​					没有请求主体body
​	形式：URL后？参数名=参数值&参数名=参数值&....
​								QueryString查询字符串

对于Postman，如何配置？	
				请求中的Params选项卡			就是参数Parameters
				通过名、值对配置、自定添加到URL地址后

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220517093340201.png" alt="image-20220517093340201" style="zoom:33%;" />

##### Post请求：请求参数主要在HTTP请求包的主体body部分携带！

​						少部分参数在URL后携带（取决于接口的设计）

形式：许多种
			form-data、x-www-form-urlencoded、raw等
在Postman中，如何配置？请求的**Body选项卡**中：

![image-20220517094533520](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220517094533520.png)

##### <1>none:请求没有Body内容

##### <2>form-data:表单数据（综合数据）

​	结构最为复杂，既能提交普通文本（Text），也能提交1个或多个文件（File）
​	数据包中使用特殊文本分隔符（好比“隔断”）将多个参数隔开
​	内容类型Content-Yype：multipart/form-data		多部分/表单数据

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220517095114293.png" alt="image-20220517095114293" style="zoom:33%;" />

##### <3>x-www-form-urlencoded	表单类型（最常用）

Post方法：默认采用该类型，形式：名值对，比如	neme=Tom&pwd=123

内容类型Content-Type：application/x-www-form-urlencoded
													应用程序

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220517095939062.png" alt="image-20220517095939062" style="zoom:33%;" />

##### <4>raw 提交原始的代码，比如JSON文本、JavaScript脚本等

内容类型举例（Content-Type）
				text/plain		普通文本
				application/Json			应用程序/JSON文本

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220517100652015.png" alt="image-20220517100652015" style="zoom: 67%;" />



##### <5>binary（最不常用）

只能上传一个文件，没有参数名，原意：二进制数据文件（底层文件），比如一个软件包

2）对于浏览器，Get请求参数在地址栏显示，信息不安全

Post请求数据在主体中，相对阿娜；（如果通过Fiddler抓包，都能获取到）

想要安全，需要加密处理，比如md5加密

3）Get写到的数据量有限，比如不超过2kb

Post请求可以携带大量数据，比如多个文件上传，要看需求和接口文档设计

4）Get：索取

​	适合向服务器索要各种Web资源，比如网页HTML、JS脚本、CSS样式表、图片jpg png gif、音频、视频、JSON或XML文本等、适合查询功能、删除

​	前端：写地址回车、点击超级连接、获取图片等资源

​	Post：提交、给予

​		适合向服务器提交表单信息，比如大量文本、文件，比如用户注册、订单提交等、适合增加、修改功能

​	前端：通过表单设置为method=“post”	方法为post

5）使用何种方法，取决于接口文档设计，我们进行测试





#### 2、Post方法案例

#### 1）案例01:Post发送表单的参数数据

接口功能：判断登录是否成功

请求名称：test_Post提交表单判断登录是否成功

请求方法：Post

接口地址：http://服务器 IP/apitest/text-login/

请求类型：form表单（x-www-form-urlencoded）

参数：

| 参数名   | 参数值 | 说明   |
| -------- | ------ | ------ |
| username | admin  | 用户名 |
| password | 123456 | 密码   |

数据库表：wa_test.users

响应类型：text/html

预期包含文本：用户xxx登录验证成功

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220517105831310.png" alt="image-20220517105831310" style="zoom:33%;" />

工作台

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220517110502551.png" alt="image-20220517110502551" style="zoom:33%;" />

#### 2）案例02:Post提交表单信息

接口功能：验证用户名和密码是否正确

请求方法：Post

接口地址：http://服务器ip/apitest/login/

请求参数类型：form表单

参数：

| 参数名   | 参数值 | 说明   |
| -------- | ------ | ------ |
| username | admin  | 用户名 |
| password | 123456 | 密码   |

数据库表：wa_test.users

响应类型：Json

预期结果：

​			HTTP响应码200，表示成功响应

如何验证失败：如果用户名正确，密码错误

```json
{
    "Status": 1004,
    "Result": "Password error",
    "Message": "密码错误"
}
```

如果用户名不对：

```JSON
{
    "Status": 1003,
    "Result": "Username error",
    "Message": "用户名或密码错误"
}
```

如果验证通过：

```json
{
    "Status": 1000,
    "Result": "Usercheck ok",
    "Message": "登录验证成功"
}
```

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220517114032882.png" alt="image-20220517114032882" style="zoom: 33%;" />

#### 案例03：发送json字符串，使用signup接口

接口功能：接受用户名、密码、确认密码和姓名，实现用户注册功能

请求名称：test03_通过Post提交json进行用户注册

请求方法：Post		适合提交大量信息，包括json代码

接口地址：http://服务器ip/apitest/signup/

请求参数类型：raw模式		json文本

请求参数：要求编写json文本，具有以下属性和数据
						username、password、confirm、name
						用户名、		密码、		确认密码、真实姓名

```JSON
{
  "username":"Tom",
  "password":"123456",
  "confirm":"123456",
  "name":"唐木"
}
```

需要查验的数据库表：wa_test.users\wa_test.info

​	返回格式：Json

返回值举例：

```JSON
{"status":1000,"Result":"Success","Message":"注册成功"}
```

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220517141355998.png" alt="image-20220517141355998" style="zoom: 50%;" />

观察控制台Console，请求包：

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220517142005211.png" alt="image-20220517142005211" style="zoom:33%;" />

控制台Console的响应包：

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220517142200612.png" alt="image-20220517142200612" style="zoom:33%;" />

查看数据库的影响：

```SQL
由于Mysql中，users的id，采用自增字段auto-increments
我们只需要添加用户名和密码，id会自动增长，原先1～3，之后就是4
由于4可能用过了，显示5		以上不重要，只要保证id是唯一即可
如果需要重置起始值：
alter	table users set auto_increments=4;
可编写SQL执行查询：
select * from info where name='唐木'
比如删除id为5的记录：
delete from info where id=4;
delete from users where id=4;
```

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/截屏2022-05-17 14.35.05.png" alt="截屏2022-05-17 14.35.05" style="zoom:33%;" />

由于后台数据库已经存在Tom，如果重复注册，会提示错误：

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/截屏2022-05-17 14.38.53.png" alt="截屏2022-05-17 14.38.53" style="zoom: 50%;" />

如果密码和确认密码不一致，会返回相关的错误提示；

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/截屏2022-05-17 14.40.19.png" alt="截屏2022-05-17 14.40.19" style="zoom:50%;" />



#### 4)案例04:Post请求访问send-json接口

接口功能：对json字符串的键进行排序

请求名称：test04_Post测试send-json接口

请求方法：Post

接口地址：http://服务器ip/apitest/send-json/

发送数据类型：json文本

josn文本举例：{"name":"张三","age":23,"inMarried":false,"child":null}

响应类型：json

响应结果：{ "age": 23, "child": null,"inMarried": false, "name": "张三"}

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/截屏2022-05-17 15.12.32.png" alt="截屏2022-05-17 15.12.32" style="zoom: 33%;" />

#### 5）案例05:Post发送form-data模式

需求：from-data，理解为综合表单数据，既可以提交普通文本，又可以提交多个文件，适合向服务器提交大量复杂信息

比如面试题：如何使用Postman向服务器提交多个照片？

​		Post方式，选择Body选项卡，选择form-data模式，提供参数名、文件路径

案例：uponfile接口

接口功能：上传一个文件

请求名称：test05_Post上传一个文件

请求方法：Post

接口地址：http://服务器 IP/apitest/upload-file/uponefile/

请求参数模式：form-data

| 参数名 | 参数值               | 说明                                               |
| ------ | -------------------- | -------------------------------------------------- |
| file   | 通过设置选择文件路径 | 文件名最好不要带中文名，提交时会将文件以数据包发送 |

响应类型：text/html

预期结果：包含文本“文件上传成功”

配置时注意：

![image-20220517154343744](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220517154343744.png)

查看控制台Console：

![image-20220517155411299](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220517155411299.png)

手工对WA服务器（Centos）查找文件：从/目录下开始	按照文件名json1.txt查找

![image-20220517155949242](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220517155949242.png)

#### 案例06:测试upfiles接口

接口功能：上传多个文件

请求名称：test06_Post上传多个文件

接口地址：http://服务器 IP/apitest/upload-file/uponefile/

请求参数类型：form-data	综合表单数据

参数：比如3个参数 ，名称自定义，比如f1 f2 f3

​		问及路径名建议英文和数字组合，避免中文编码问题

响应类型：text/html 

预期：包含文本“文件上传成功”

![image-20220517164741516](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220517164741516.png)

查看控制台Console 

![image-20220517165646911](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220517165646911.png)

通过查看后台系统目录结构，找到关系：新文件是随机名称

![image-20220517170858099](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220517170858099.png)

## 二、Postman执行基本顺序

### 1、工具界面设计和效果

#### 1）Pre-requestScript：请求之前的脚本

适合执行请求之前的准备工作，比如对密码进行加密后发送；

2）发送请求	Send

3）Tests：请求之后的脚本	测试

适合在请求之后，对响应结果进行检查，自动判断结果是否正确；

也可获取响应结果的重要数据，供后续请求使用（接口的关联）

如何证明？使用JavaScript脚本

```javascript
//在Postman中通过嵌入一些js脚本，为用例增强功能
//单行注视		不作为有效代码部分，起到解释说明文本的作用
/*
多行注释
一次注释多行文本内容
*/
//在控制台Console，打印输入一些文本、变量的值		使用JS内定的函数
console.log("Hello");		//JS的字符串既可以使用双引号，也可使用单引号
console.log('Hi');
//通过var定义	JS的局部变量
var ip="192.168.3.5"	
var name='Tom';
var	age=23;
console.log('服务器的IP:'+ip);	//+ 表示字符串的拼接
console.log('名字：'+name+'年龄'+age);
```

在“预请求脚本”中添加代码：

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220517175015432.png" alt="image-20220517175015432" style="zoom:50%;" />

在Tests选项卡写脚本：

![image-20220517175202695](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220517175202695.png)





# DAY05:Postman编程技巧、断言（检查点）

复习：

​	Post请求的发送方式，选择Body选项卡：
​	表单x-www-form-urlencoded、表单数据form-data、源代码raw

## 一、Postman编程技巧

### 1、Postman执行顺序

#### 1）先执行“预请求脚本”：Pre-request Script

适合在请求之前进行准备

#### 2）方式请求：按照配置方式Get或Post请求，访问URL，携带请求参数

#### 3）最后执行“Tests”部分脚本

适合在请求后对结果进行分析和处理

#### 案例：新建day05用例集，将day04中的test02拷贝到day05下，重命名为test01

在“Pre-request Scirpt”中写脚本:Postman是使用前端技术JavaScript写脚本

```javascript
//在控制台打印输出内容  console控制台   log日志
console.log('请求发送之前');
//定义一些局部变量（临时变量）供当前代码块使用
//JS中定义变量写var     就是变量的意思
//变量名 = 变量值   把值存起来，起代号
var name = 'Tom';
var age = 23;
console.log(name);
console.log(age);
console.log(age+1); //表达式    结果24
console.log(age); //目前还是23
age=25;     //重新给变量age赋值为25
console.log(age);   //目前是25
//字符串和其他数据拼接
console.log('名字' + name); //输出  名字：TOM
console.log('年龄' + age);  //输出  年龄：25
//用一句话输出名字和年龄
console.log('名字' + name , '年龄' + age);
//y以上的name和age都是JS的局部变量
//通过模板函数，设置一个Postman的环境变量，作为后续请求的条件
//比如：set an environment varlable
//     设置 一个 环境变量    变量名id   变量值1001
pm.environment.set("id","1001");
pm.environment.set("uname","Mary");
// 通过模板函数，设置一个Postman 的全局变量，效果类似“小眼睛”
//比如：Set a global variable
pm.globals.set("phone","13811116688");

```

在发送请求时，携带参数：id和uname，Postman使用{{id}}	{{uname}}

比如：Post方法也允许在URl后携带参数	？id={{id}}&{{uname}}

​			发送请求时，可以获取前置脚本设置的“环境变量”值（局部变量）

![image-20220518104420379](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220518104420379.png)

取值原理：{{ip1}}获取的是全局变量（小眼睛设置的）
						{{id}}	{{uname}}	是获取局部变量（通过前置脚本设置的“环境变量”）

![image-20220518205455535](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220518205455535.png)

设置了全局变量后：

![image-20220518205534842](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220518205534842.png)

在“Tests”选项卡中编写JS脚本：请求发送之后执行的脚本

目的：获取响应数据，对结果进行检查，判断是否符合预期；
			获取响应数据，供后续请求使用（接口的关联）

```javascript
console.log('请求发送之后执行的脚本');
//获取局部变量：id和uname   Postman的环境变量
//使用模板：Get an environment variable
//根据名称获取
var Js_id = pm.environment.get("id");
console.log(Js_id);		//1001
//获取uname，存入Js的变量中 变量名JS_uname
var JS_uname= pm.environment.get("uname");
//打印输入JS_uname
console.log(JS_uname);	//Mary
//获取全局变量phone，并打印输出
var JS_phone = pm.globals.get("phone");
console.log(JS_phone);
```

![image-20220518114258117](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220518114258117.png)

获取全局变量的数据，并使用：

![image-20220518205608823](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220518205608823.png)

要求在“Tests”选项卡中，编写获取响应结果内容的的脚本：

原因：只有发送了请求后，才有响应结果，需要在“后置”脚本中编写

```javascript
//获取HTTP响应码  Postman设计好的固定写法responseCode.code  区分大小写
//存于JS变量 r_code中
var r_code = responseCode.code;  //响应码 的 码值
console.log(r_code);
```

![image-20220518205657502](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220518205657502.png)

问题：如何获取HTTP响应主体文本？如何表达？

```javascript
//获取HTTP响应主体文本  responseBody  固定写法
//要求使用转化函数：JSON.parse()转化为JS中的对象
//JSON是统一的工具   parse 解析
var a1 = JSON.parse(responseBody);
console.log(a1);
//使用函数，获取JSON文本   将JS对象 转变为 JSON文本
var a2 = JSON.stringify(a1);    //string 字符串
console.log(a2);
```

![image-20220518210006043](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220518210006043.png)

可以进一步跟进js对象，获取其中的属性：根据属性名获取

```javascript
//获取HTTP响应主体文本  responseBody  固定写法
//要求使用转化函数：JSON.parse()转化为JS中的对象
//JSON是统一的工具   parse 解析
var a1 = JSON.parse(responseBody);
console.log(a1);
//继续获得a1的几个属性  语法：a1.属性名  a1的某属性
console.log(a1.Status); //1000
console.log(a1.Result); //Usercheck ok
console.log(a1.Message); //登录验证成功
//使用函数，获取JSON文本   将JS对象 转变为 JSON文本
var a2 = JSON.stringify(a1);    //string 字符串
console.log(a2);
```

2）![image-20220518211935452](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220518211935452.png)

技巧：判断js数据类型 typeof（数据或变量）

​		type		类型		of	的

```javascript
console.log(typeof(a1));  //object  JS对象  对象.属性名
console.log(typeof(a2));  //string  字符串  目前是JSON文本
//由来：JSON JavaScript对象表示法   和JS是“亲戚”
```

![image-20220518212105314](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220518212105314.png)

## 二、断言（检查点）Tests

### 1、什么是断言？

  断言（Assert）,预先断定结果是什么，和实际结果对比，如果一致，说明判断正确；如果不一致，说明检查失败！

​    自动化测试中，经常需要添加断言，对执行结果进行自动化检查，所以也称为“检查点”。

​    Postman中，要在请求发送之后，对结果进行检查，需要使用"Tests"选项卡写脚本。

### 2、为什么需要使用断言？

趋势：接口的自动化测试

​    请求自动发送过程中，不方便人工介入，需要提前写好断言脚本，说明预期结果是什么，在请求发送之后，就能自动判断结果是否符合预期，进行反馈。

### 3、在哪里添加断言？

   设计接口测试用例时，要根据预期结果进行分析，比如HTTP响应码，希望是200；比如响应文本中，希望返回“成功”字样等；

​     看需求、分析接口文档，对结果信息进行拆分和判断。

​     要求：要有一定的规律，适合对多次请求的结果进行统一检查！

​     甚至：需要查验数据库，对数据库的结果进行判断（验库）。

### 4、如何添加断言？Tests

#### 1）使用Postman提供模板函数，快速添加断言（选对模板，会填空即可）

##### <1> HTTP响应码的检查： 模板 **Status code: Code is 200**

##### <2> 判断**响应主体**文本中是否**含有**某文本：模板 **Response body: Contains string**

在day05用例集中，再拷贝day04的test02:

需求：检查HTTP响应码为200，检查响应文本含有1000、登录验证成功

```javascript
console.log('请求发送之后执行的脚本，适合对响应结果进行检查');
//检查HTTP响应码为200    只要HTTP响应码是200,就打印提示文本
//模板：Status code: Code is 200
pm.test("成功响应，返回200", function () {
    pm.response.to.have.status(200);
});
//检查响应文本含有：1000  只要响应文本含有1000,就打印提示文本
pm.test("响应文本含有：1000", function () {
    pm.expect(pm.response.text()).to.include("1000");
});
//检查响应文本含有：登录验证成功   只要含有预期文本，就打印提示
pm.test("响应文本含有：登录验证成功", function () {
    pm.expect(pm.response.text()).to.include("登录验证成功");
});
```

![image-20220518213006112](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220518213006112.png)

如果检查失败：

![image-20220518213031253](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220518213031253.png)

检查响应文本：

![image-20220518213100105](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220518213100105.png)

![image-20220518213243272](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220518213243272.png)

2）自己编程，实现断言（检查点）

需求：同上	检查HTTP响应码为200，响应文本含有1000、登录验证成功

将day04的test02拷贝到day05下，重命名为test03

技巧：通过tests["xxx"] =  true 或 false  进行判断和检查

```javascript
console.log('请求发送之后执行的脚本')
//Postan规定的检查语句 如果右边表达式为true，则打印提示文本
tests["检查成功提示文本1"] = true;
tests["检查成功提示文本2"] = false;
//检查HTTP响应码为200
//表示如果	响应码	恒等于 200，就打印提示文本信息
//比如实际结果是200
console.log(responseCode.cod === 200); //true 是200
console.log(responseCode.cod === 404); //false 不是404
tests["成功响应，返回200"] = responseCode.code === 200;
console.log("200" == 200 ); //true  只是值相等，近似相等
console.log("200" === 200);     //false     类型不同，不等
console.log(200 === 200);   //true  类型和值完全相等 完全相等
console.log(typeof("200")); //string 字符串
console.log(typeof(200)); //number 数字
//检查想英文版含有：1000    使用响应主体的has函数 有没有
tests["响应文本含有:1000"] = responseBody.has("1000");
//检查响应文本含有：ok
tests["响应文本含有:ok"] = responseBody.has("ok");
//检查响应文本含有1000
tests["响应文本含有:登录验证成功"] = responseBody.has("登录验证成功");

```

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220518165959650.png" alt="image-20220518165959650" style="zoom: 50%;" />

说明：



3）对HTTP响应主体内容，进行精确内容提取和判断

思路：获取responseBody，如果是JSON内容，需要使用Json.parse()函数，转化为JS对象，通过 对象.属性名 获取值比较；

```javascript
console.log('请求发送之后执行的脚本')
//获取HTTP响应码的实际结果a1
var a1 = responseCode.code;
console.log(a1);    //比如是200
//说明预期的HTTP响应码 a2 200
var a2 = 200;
//将 实际结果 和 预期结果进行对比 a3
var a3 = a1 === a2;
console.log(a3); //如果完全相等 true 否则 false
tests["成功响应，返回200"] = a3;
//重点：获取实际resonseBody,目前是JSON文本，要转化为JS对象
var b1 = JSON.parse(responseBody);
console.log(b1);
//结果：{Status: 1000, Result: "Usercheck ok", Message: "登录验证成功"}
//根据对象b1的属性名获取属性值 都是实际结果的属性
var b11 = b1.Status;
var b12 = b1.Result;
var b13 = b1.Message;
console.log(b11);
console.log(b12);
console.log(b13);
//添加断言  只要b13 和 预期文本 完全一致，就测试通过
tests["预期含有："+b13 + "实际查到了！"] = b13 ==="登录验证成功";
```



# DAY06:用例自动批量执行、参数化技术

## 一、用例自动批量执行

### 1、含义：

​	之前的接口用例都是手工执行，好处是逐条调试、跟踪、确保用例正常使用；
后续可以进行接口自动化：自动将用例批量执行

### 2、用途

​	接口的自动化，需要批量执行以往的用例，便于进行回归测试；
Postman进行参数化时候，通过批量执行，测试多组数据。

### 3、操作步骤技巧

​	需求：针对某个**用例集** 或者 某个**文件夹**folder，进行用例的批量执行

#### 1）针对某用例集，比如day05，点击Run，打开运行器，可以选择需要执行的请求

![image-20220519095322326](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519095322326.png)

运行后效果：如果未加检查点，会提示没有做检查；如果加过检查点，显示检查结果，进行自动化检查。

![image-20220519095721195](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519095721195.png)

技巧：通过文件夹管理某些请求，只对文件夹中的请求批量执行（局部、小

<img src="/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519102517257.png" alt="image-20220519102517257" style="zoom:50%;" />



## 二、参数化技术

### 1、什么是参数化？what？

​	参数化，也叫变量化

使用变量名代替原先的字面值，变量名无需改变，变量的值可以改变；
（以不变应万变！）不变的是变量名，变化的是变量的值

大大提高接口用例的可复用性、易维护性、数据多样性！

原先：

![image-20220519104122879](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519104122879.png)

全局变量：通过“小眼睛”配置，值比较固定，可以修改，整个工作区共享使用

局部变量：通过数据文件方式提供大量数据，用例集可用

### 2、为什么需要参数化？why？

目的：让脚本中的业务数据动态获取，满足大批量数据测试的要求；

​			某些需求中要求业务数据必须要满足，比如：
​							用户注册：用户名、手机号、邮箱号...
​		让每次发送请求时，能够自动改变数据！——参数化技术

从接口测试角度：可以减少用例的数量
		让一条用例可以重复使用多组数据，提高自动化测试的效率。

### 3、何处需要参数化？Where？

思路：根据业务需求，寻找会变化的数据

比如：请求参数添加，id、username、password、email、salary....（**入参**）

​			返回的结果，就是预期结果，也会变化
​			实际结果	单词：actual	随着每次条件的变化而变化
​			预期结果	单词：expect	作为检查点的判断依据，也需要变化（**出参**）

面试描述思路：
			在进行接口自动化时，为了测试大批量数据，采用参数化技术，根据业务需求设计**入参**和**出参**，设计用例并执行。
				入参：请求携带参数数据，是可以改变的；（因）
				出参：响应返回的结果数据，需要检查，也会随着入参的变化而变化；（果）

![image-20220519110617084](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519110617084.png)

### 4、如何进行参数化？How？

#### 1）全局变量Globals

##### <1>方法1:在“小眼睛”设置

![image-20220519113028183](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519113028183.png)

##### <2>方法2:在“pre-request Script”请求前置脚本，编写

```javascript
	pm.globals.set("pnone","13811116688");
//Postman 全局	设置
//在Postman的全局范围，设置一个全局变量，变量名phone，变量值“13811116688”
//后续请求中，可使用{{phone}}直接取值
```

#### 2）局部变量

思路：针对某个**用例集、文件夹**folder，指定数据文件，从文件中获取批量数据；结合Run运行器使用；

作用域：用例集、文件夹

可以使用的文件类型：**txt、csv、json**

##### <1>	txt 普通文本

##### <2>	csv 逗号分隔值 Comma-Separated Values

​				每一行表示一条记录，用逗号分隔的每一列表示每个属性
id,username,password,expect	列名就是参数名

1，admin，123456,成功		好比：第一条数据是有效数据
2,tom,123,成功

1,admin,123,失败					第三条数据测试无效

##### <3>json  	通过json数组，保存多个对象，管理属性数据

#### 3）参数化的基本步骤

##### <1>配置**请求**，确保请求可以正常发送（调试请求要素正常的，作为样本）

##### <2>添加**断言**，对响应结果进行自动检查

​		由于后续入参会改变可，则出参也会跟着改变，需要工具自动检查

##### <3>选择**数据**格式：txt或json，并准备测试数据

##### <4>**配置参数**并发送	

##### 	请求中{{参数名}}获取参数值

​	Tests代码中：可以通过**data.文件列名**	获取值 （一般是预期结果）

### 5、案例和练习

#### 1）练习读取txt文件的数据

需求：对login接口进行参数化

接口地址：http://服务器IP/apitest/login/

请求方法：Post

请求参数类型：form表单	就是x-www-form-urlencoded

请求参数说明：
			username	用户名	比如admin
			password	 密码		比如123456	123是无效的
涉及的数据库表：wa_test.users

返回格式：json

返回值举例：（查看接口文档 或 实际请求发送获取）



操作：

##### <1>新建用例集day06，新建文件夹test01_批量登陆测试

![image-20220519115845380](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519115845380.png)

##### <2>在文件夹下，新建请：用户登陆

![image-20220519120003943](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519120003943.png)

具体配置

![image-20220519140800883](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519140800883.png)

思路：尝试不同请求参数作为条件，观察不同的实际结果

比如：正确的用户名和密码

```json
{"Status":1000,"Result":"Usercheck ok","Message":"登录验证成功"}
```

比如：正确的用户名，密码不填

```json
{"Status":1002,"Result":"Password is null","Message":"用户名或密码为空"}
```

比如：不填用户名，密码正确

```json
{"Status":1001,"Result":"Username is null","Message":"用户名或密码为空"}
```

比如：用户名不存在

```json
{"Status":1003,"Result":"Username error","Message":"用户名或密码错误"}
```

##### <3>添加检查点，对结果进行自动检查	Tests选项卡

思路：检查HTTP响应码，都是200
			检查响应文本含有：状态码  1001 	1002	1003
			检查响应文本含有：某结果说明

![image-20220519142909263](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519142909263.png)



```javascript
//检查HTTP响应码为200
tests[""] = responseCode.code === 200;
console.log("响应码是：" + responseCode.code);
//获得实际结果：将responseBody的JSON文本转化为JS对象
var actual = JSON.parse(responseBody);
var actual_status = actual.Status;  //获得状态码
var actual_result = actual.Result;  //获得实际结果提示
console.log(actual_status);
console.log(actual_result);
//检查响应文本含有状态码
var expect_status = 1000;   //预期状态码
tests["响应文本含有" + expect_status] = actual_status === expect_status;
//检查响应文本含有结果说明
var expect_result = "Usercheck ok";
tests["响应文本含有" + expect_result] = actual_result === expect_result;
```

##### <4>使用txt文本，准备参数化数据（入参、出参）

在任何目录下，新建test01_case.txt文件

![image-20220519153210672](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519153210672.png)

注意：一般项目要求字符集采用“UTF-8”，如果字符集不统一，会出现中文乱码问题。
技巧：文件另存为UTF-8格式

![image-20220519153527664](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519153527664.png)

![image-20220519154433172](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519154433172.png)

批量执行：

![image-20220519154810105](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519154810105.png)

##### <6>对“出参”进行设置，修改Tests中检查点的预期结果

私用data.列名 获取数据文件中的每一列的值

比如：da ta.expect_status  就是出参的预期状态码
			data.expect_result 	就是出参的预期结果信息

代码修改如下：

```javascript
//检查HTTP响应码为200
tests["成功响应，返回200"] = responseCode.code === 200;
console.log("响应码是：" + responseCode.code);
//获得实际结果：将responseBody的JSON文本转化为JS对象
var actual = JSON.parse(responseBody);
var actual_status = actual.Status;  //获得实际状态码
var actual_result = actual.Result;  //获得实际结果提示
console.log(actual_status);
console.log(actual_result);
//检查响应文本含有状态码
//console.log(data.expect_status);
//使用data.列名  获取出参的不同列的值
var expect_status = data.expect_status;   //预期状态码
tests["响应文本含有：" + expect_status] = actual_status === expect_status;
//检查响应文本含有结果提示
var expect_result = data.expect_result;  //预期结果提示
tests["响应文本含有：" + expect_result] = actual_result === expect_result;
```

![截屏2022-05-19 16.45.11](/Users/liuxueman/Library/Application Support/typora-user-images/截屏2022-05-19 16.45.11.png)



#### 2）练习读取csv文件的数据

需求：对multi-params接口进行参数化

接口功能：根据用户id、username查询用户注册时间

接口地址：http://服务器ip/apitest/multi-params/

请求方法：Get

参数：id、username

数据库表：wa_test.users

预期返回：显示用户名和注册时间、用户信息不存在

测试用例（数据）：新建test02_case.asv  普通文本文件，重命名，记事本编辑

```
id,username,expect
1,admin,"注册时间": "2020-07-15 15:30:47"
2,hehe,用户信息不存在
3,hah,用户信息不存在
```

##### <1>新建并调试好请求

day06用例下，新建文件夹：test02_批量账户检查

请求名称：查询用户注册时间

![image-20220519171215853](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519171215853.png)

<2>在Tests选项卡添加检查点

```javascript
//检查HTTP响应码为200
pm.test("成功响应，返回200", function () {
    pm.response.to.have.status(200);
});
//检查响应文本含有预期文本
var expect = '"2020-07-15 15:30:47"';
pm.test("响应文本含有："+  expect, function () {
    pm.expect(pm.response.text()).to.include(expect);
});

```

##### <3>准备参数化用例数据文件：test02_case.csv

![image-20220519174400247](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519174400247.png)

<4>准备入参的设置：{{参数名}}	参数名安装csv文件的列名表示

![image-20220519174908164](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519174908164.png)

##### <5>准备出参的设置，Test选项卡

技巧：data.列名	作为预期结果获取

```javascript
//检查HTTP响应码为200
pm.test("成功响应，返回200", function () {
    pm.response.to.have.status(200);
});
//检查响应文本含有预期文本 注意：expect使用时直接写变量名，表示字符串值
var expect = data.expect;
console.log("预期文本:" + expect);
pm.test("响应文本含有："+  expect, function () {
    pm.expect(pm.response.text()).to.include(expect);
});

```

配置效果

![image-20220519181655011](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519181655011.png)

##### <6>使用运行法：Run 	批量执行用例数据

![image-20220519181711474](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519181711474.png)

预览效果

![image-20220519181731641](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519181731641.png)

如果出现中文编码问题：（中文乱码）需要对资源文件修改字符集	另存为UTF-8

执行结果

![image-20220519181750383](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519181750383.png)

如何调试

![image-20220519181802267](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220519181802267.png)





#### day07：

#### 3)读取JSON数据文件

案例：针对login接口进行参数化

接口地址：http://服务器IP/apitest/login/

请求方法：Post

参数类型：form表单

请求参数说明：username用户名	password密码

数据库表：wa_test.users

返回格式：JSON文本，比如

```json
{"Status":1000,"Result":"Usercheck ok","Message":"登录验证成功"}
或
{"Status":1001,"Result":"Username is null","Message":"用户名或密码为空"}
或
{"Status":1002,"Result":"Password is null","Message":"用户名或密码为空"}
或
{"Status":1003,"Result":"Username error","Message":"用户名或密码错误"}
或
{"Status":1004,"Result":"Password error","Message":"密码错误"}
```

##### <1>准备请求，配置好案例参数

在day06用例集下，新建文件夹：test03_批量登陆测试

请求名称：用户登陆

![image-20220520094159015](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220520094159015.png)

##### <2>在Tests选项卡中添加检查点：

```javascript
//检查HTTP响应码为200
var code = responseCode.code; //先保存好响应码
console.log(code);
var r1 = code === 200; //r1要么是true 要么是false
var msg; //保存打印的消息
//使用if else分支语句 进行判断
if(r1) { //如果r1为true，表示code为200 第1个分支
msg= "成功响应，返回200";
} else {  //否则 执行第2个分支
msg = "错误响应，响应码：" + code;
}
tests[msg] = r1; //如果r1位true 工具显示pass 否则fail
//检查响应主体中含有预期结果
//1.先获取实际结果 将响应的JSON转化为JS对象
var actual = JSON .parse(responseBody);
var actual_status = actual.Status;
var actual_result = actual.Result;
//2.和预期对比，作为判断条件
var expect_status = 1000;
var expect_result ="Usercheck ok";
var r2 = actual_status === expect_status;
var r3 =actual_result === expect_result;
if(r2) {
    msg = "含有预期状态码：" + expect_status;
} else {
    msg ="检查失败！实际状态码：" + actual_status;
}
tests[msg] = r2;
if(r3) {
msg = "含有预期的结果提示：" + expect_result;
} else {
    msg = "检查失败！实际结果提示：" + actual_result;
}
tests[msg] = r3;
```

执行效果：

![image-20220520105623650](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220520105623650.png)

<3>准备测试数据：含有用例的设计思路	有效、无效、为空、边界、条件组合

目前设计为JSON格式：
		直接定义一个数组[],通过多个对象{}，表示每条用例的设计

```json
[
  {"username": "admin", "password": "123456", "expect_status": 1000, "expect_result":"Usercheck ok"},
  {"username": "admin", "password": "", "expect_status": 1002, "expect_result":"Password is null"},
  {"username": "", "password": "123456", "expect_status": 1001, "expect_result":"Username is null"}
]
```

![image-20220520110721115](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220520110721115.png)

结果思路：

```json
[//广义认为：什么都是对象，就连数组也是对象	JSON文本具有面向对象特性
  {"属性名":"属性值"},	//数组的每个元素，就是一条用例，具有多个属性
  {"属性名":"属性值"},
  {"属性名":"属性值"}
]
```

建议：要求使用在线JSON校验工具检查JSON语法	WWW.JSON.CN

##### <4>修改请求的入参{{username}} 	{{password}}

![image-20220520114128666](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220520114128666.png)

<5>修改Tests中的出参：**data.属性名**	也适用于JSON中根据属性名获取属性数据

原理：每次迭代，都选取数组中的一个对象{},data.属性名，就是根据对象的属性名获取属性值！

```javascript
//2、和预期对比，作为判断条件
var expect_status = data.expect_status;
var expect_result = data.expect_result;
console.log("预期状态码：" + expect_status);    //控制台打印 是为了调试
console.log("预期状态码：" + expect_result);
```

![image-20220520115658008](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220520115658008.png)

##### <6>设置运行器：

预览效果：

![image-20220520115137523](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220520115137523.png)

运行结果：

![image-20220520114924600](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220520114924600.png)



重要技巧：

​	通过Console控制台打印整个请求和响应的执行过程，对重要变量进行打印跟踪个调试，注意txt、csv、json数据格式、类型，避免程序读取数据失败。



# Day07:Postman访问数据库

## 一、Poseman验库（落库检查）

### 1、什么是验库

​	验库，也称为落库检查
就是在自动化测试过程中，能够自动判断数据库中的数据是否存在、合理；

### 2、为什么需要验库？

​	添加断言时，关心两个方面，一个是接口的返回值，一个是对数据库的影响，这两方面都要正确；

​	验库就是对数据库中的数据进行确认，比如通过查询数据库验证实际结果是否存在，包括对数据库表中的行和列的检查。

#### 3、什么时候需要验库？

​	当访问接口时，只要对数据库有影响，就可以验库，根据业务和数据关系确定是否需要验库：

​	比如查询的结果是从数据库获取，我们可以查验数据库进行数据确认；
​	比如注册新账户后，通过查询数据库证明有新的记录产生，而且就是该记录；
​	比如在修改信息后，可以观察数据库的数据是否被修改；
​	比如删除信息后，观察数据库记录是否删除；

——CURD操作都可以验库（增删改查）

Create创建	Update修改	Read读取查询	Delete删除

通过Postman访问数据库，可以进行数据库的自动化控制，进行批量数据添加，从而实现测试数据的初始化（测试之前准备大量初始数据）

#### 4、采用什么工具

Postman基于javaScript编写脚本，JS有一种框架，：no de.js提供常用功能

node.js提供工具：xmysql 提供了很多restful接口，实现对数据库的CURD操作（增删改查）

#### 5、xmsql使用步骤

##### 1）前提：安装cnpm工具，并安装xmysql（已经提前安装，只需要检查环境）

```
在测试机、物理机中安装cnpm(淘宝的资源)
说明：npm 是 node.js包管理工具	install 安装	cnpm
npm install cnpm -g --registry=https://registry.npm.taobao.org
如何检查：
cnpm -v
安装xmysql
cnpm install -g xmysql
```

2）启动xmysql服务器

在安装有Postman和xmysql的测试机上启动！(目前就是物理机Windows机器）)

原理：Postman通过该服务访问Mysql数据库（Centos机器 安装Mysql）

打开cmd窗口

```
xmysql -h 数据库服务器ip地址 -u 数据库用户名 -p 数据库密码 -d 数据库名
```

比如：数据库服务器的Ip地址为192.168.72.136，用户名root，密码123456，数据库名wa_test;

```
xmysql -h 192.168.2.2 -u root -p 123456 -d wa_test
```

执行效果如下：

如果连接失败：

![image-20220520145322747](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220520145322747.png)

如果连接成功：

![image-20220520145607542](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220520145607542.png)

##### 3）使用Postman新建请求，对Mysql进行访问

访问增删查该的接口：

```
接口地址：http://localhost:3000/api/表名
请求方法：查询	Get
				增加 Post
				修改 Patch
				删除 Delete
```

#### 6、案例与练习

##### 1）案例1:向users表中插入一条记录

```
请求名称：test01_向users表中插入一条记录
接口地址：http://localhost:3000/api/users/
请求方法：Post	增加操作，使用Post提交数据
请求类型：表单	x-www-form-urlencoded
请求参数：数据库表的列名 和 值
			说明：由于id带有自增特性，添加时可不提供id的值，会自动添加
```

技巧：密码需要经过md5加密后，再存入数据库中

解决方法：在前置脚本（Pre-request SCript）中写代码：

```javascript
//通过MD5工具进行加密，并获得加密后的文本
//先使用md5函数加密，再通过toString函数提取密码的字符串文本
var md5_123456 =CryptoJS.MD5("123456").toString();
//将当前的密码设置到Postman的环境变量中，供后溪请求使用
pm.environment.set('md5_pw', md5_123456);
```

配置请求方法、地址、参数：使用密码时{{md5_pw}}

![image-20220520155525025](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220520155525025.png)

如果重复添加，会提示错误

![image-20220520160046212](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220520160046212.png)

在Tests中添加检查点：

原理：响应结果中显示一下属性，表示成功添加了1条记录

检查思路：主要JSON结果中，存在insertld属性，证明产生了新的id，添加成功

```json
{
    "fieldCount": 0,
    "affectedRows": 1,	//表示影响了1行
    "insertId": 5,			//表示刚才插入的id是 7
    "serverStatus": 2,
    "warningCount": 0,
    "message": "",
    "protocol41": true,
    "changedRows": 0
}
```

Tests中添加代码：

```javascript
//获得响应主体文本的JSON对象
var actual = JSON.parse(responseBody);
//尝试获取id值
var id = actual.insertId;
if(id != null) {//如果id不为null    表示存在    添加成功
    tests["记录添加成功，id：" + id] = true;    //PASS
}  else {   //否则说明添加失败
    tests["添加失败"] = false; //FAIL
}
```



##### 2)案例02:查询users表的所有行

```
请求名称：test02_查询users表的所有行
请求方法：Get 	查询就是索取，设计使用Get方法
接口地址：http://localhost:3000/api/users/
参数：目前没有

```

配置效果：属性名就是列名，属性的值就是列的值

![image-20220520170601408](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220520170601408.png)

##### 3)案例3：查询info表的所有行

```
请求名称：test03_查询info表的所有行
Get方法：http://localhost:3000/api/info/

```



问题：查询时如何进行条件查询

```
请求方法：Get
请求地址：http://localhost:3000/api/表名/?_wher=（列名1，eq，值1）～and（列名2，eq，值2）
注意：逗号左右不能加空格
eq：equal	相等
返回包含json数组的字符串
使用时，注意如何从数组中获取每个元素，就是每条记录信息
缺陷：查询不到信息时，会返回标准所有信息
```

##### 4）案例4：查询用户名为test01并且密码为123456的行，要求密码需要加密后比对

```
请求名称：test04_根据用户名和密码查询用户
请求方法：Get
接口地址：http://localhost:3000/api/users/?_where=(username,eq,test01)~and（password,eq,{{md5_pw}})
说明：需要通过前置脚本，对123456加密后，再存于Postman的环境变量中，变量名md5_pw

```

配置信息如下：



##### 5）案例5:查询info表中姓名为管理员的账号

```
请求名称：test05_info表中根据姓名查询id
请求方法：Get
请求地址：http://localhost:3000/api/info/?_where=(name,eq,管理员)
```

![image-20220521093747777](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521093747777.png)

在Tests选项卡中，为查询结果添加检查点：

```javascript
//获得JSON结果的js对象，目前是一个数组
var actual = JSON.parse(responseBody);
//如果数组长度>0    元素个数>0  才处理
if(actual.length > 0) {
    //获得数组的第1个元素，下标从0开始
    var user = actual[0];
    console.log(user);
    //获得用户的id属性
    var id = user.id;
    console.log(id);
    tests["用户的id：" + id] = true;
} else {
    tests["查无结果"]=true;
}
```

运行结果：

![截屏2022-05-21 10.27.30](/Users/liuxueman/Library/Application Support/typora-user-images/截屏2022-05-21 10.27.30.png)

查看表的记录条数（行数）：

```
请求方法：Get
请求地址：http://localhost:3000/api/表名/count?_where=(列名1,eq,值1)～and(列名2,eq,值2)
注意：count后不能写/
```

##### 6）案例6:查询用户表中的总行数

```
请求名称：test06_查询用户表中的总行数
请求方法：Get
请求地址：http://localhost:3000/api/users/count/
类似SQL中：select count(id) from users;	统计表中有效记录的条数
```

配置和执行效果：



![截屏2022-05-21 10.41.51](/Users/liuxueman/Desktop/截屏2022-05-21 10.41.51.png)

##### 7）案例7:通过查询确定用户不存在

用途：在注册时，需要先判断用户是否存在，如果用户不存在，则用户名可以使用！（后端校验，服务器端校验，通过后逃数据库检查数据是否可用）

```
用例名称：test07_查询确定用户不存在
请求方法：Get
请求地址：http://localhost:3000/api/users/count?_where=(username,eq,test00)
```

在Tests中写脚本

```javascript
//先解析出结果  JSON数组-》js的数组
var actual =JSON.parse(responseBody);
//获得数组actual中的第0个元素，获取其属性no_of_rows
var rows = actual[0].no_of_rows;
tests["返回的记录条数：" + rows] = true;
```

返回结果格式：JSON数组，就1个元素，表示一个对象，对象的属性no_of_rows表示查询的记录条数

```json
[
    {
        "no_of_rows": 0
    }
]
```

执行效果：

![image-20220521110045080](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521110045080.png)

##### xmysql如何删除数据：

```
在POstman中操作
请求方法：delete
请求地址：http://localhost:3000/api/表/主键值
请求参数：无
```

8）案例8:删除users表的一条记录

```
请求名称：test08_删除users表的记录
请求方法：delete
请求地址：http://localhost:3000/api/users/16
含义：针对users表删除主键id为16的记录		目前id为主键
```

结果举例：

```json
{
    "fieldCount": 0,
    "affectedRows": 0,
    "insertId": 0,
    "serverStatus": 2,
    "warningCount": 0,
    "message": "",
    "protocol41": true,
    "changedRows": 0
}
```

运行效果：

![image-20220521111045309](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521111045309.png)

对结果进行处理：Tests

```javascript
//先获取实际结果中的    影响记录条数
var actual = JSON.parse(responseBody);
var rows =actual.affectedRows;
//根据rows判断输出内容
if(rows != 0) { //rows不为0 表示有记录删除
    tests["删除了：" + rows + "行"] = true;
} else {    //否则  表示没有记录删除
    tests["未删除"] = true;
}
```

![image-20220521113656017](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521113656017.png)

如何修改记录？

```
请求方法：patch
请求地址：http://localhost:3000/api/表名/主键值
修改的数据：设置在Body选项卡中，使用表单形式，选择x-www-form-urlencoded	
					设置属性名，就是列名	属性值，就是新的值
					
```

##### 8）案例8:修改users表的一条数据

```
请求名称：test08_酷盖users表数据
请求方法：Patch
请求地址：http://localhost:3000/api/users/6
```

查看数据库 ：

![image-20220521114508138](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521114508138.png)

配置效果：

![image-20220521114924919](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521114924919.png)

![image-20220521115112512](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521115112512.png)



# day08:

## 1、综合练习：

## 使用Postman结合xmysql工具向users表批量添加10条记录，用户名、密码自由指定，id由自增序列自动产生。可以使用参数化实现。

## 2、解题思路：

需要使用xmysql服务，由Postman对数据库直接操作；

使用Post方法发送请求，添加用户记录

由于记录比较多，使用参数化方式，批量添加；

适当添加检查点，保证添加成功；

### 1）新建用例集：day08，新建文件夹：user记录的批量添加	后续使用Run批量执行

### 2）准备请求：向users表插入记录

将

前置脚本：Pre-request Script

```javascript
//通过MD5工具进行加密，并获得加密后的文本
//先使用md5函数加密，再通过toString函数提取密码的字符串文本
var md5_123456 =CryptoJS.MD5("123456").toString();
//将当前的密码设置到Postman的环境变量中，供后溪请求使用
pm.environment.set('md5_pw', md5_123456);
```

后置脚本：

```javascript
//获得响应主体文本的JSON对象
var actual = JSON.parse(responseBody);
//尝试获取id值
var id = actual.insertId;
if(id != null) {//如果id不为null    表示存在    添加成功
    tests["记录添加成功，id：" + id] = true;    //PASS
}  else {   //否则说明添加失败
    tests["添加失败"] = false; //FAIL
}
```

3）准备参数化数据文件：add_users.json	建议格式使用在线校验www.json.cn

```json
[
  {"username":"test001","password":"1001"},
  {"username":"test002","password":"1002"},
  {"username":"test003","password":"1003"},
  {"username":"test004","password":"1004"},
  {"username":"test005","password":"1005"},
  {"username":"test006","password":"1006"},
  {"username":"test007","password":"1007"},
  {"username":"test008","password":"1008"},
  {"username":"test009","password":"1009"},
  {"username":"test010","password":"1010"},
]
```

#### 4)配置请求入参：

修改Post请求中的参数：{{username}}

![image-20220521143713653](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521143713653.png)

在前置中修改脚本：

```javascript
//获取json文件中属性名为password的值
var pwd = data.password;
console.log(pwd);
//通过MD5工具进行加密，并获得加密后的文本 
//先使用MD5函数加密，再通过toString函数提取密码的字符串文本 
var md5_123456 = CryptoJS.MD5(pwd).toString();
//将当前密码设置到Postman的环境变量中，供后续请求使用 
pm.environment.set("md5_pw", md5_123456);
```





![image-20220521120326068](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521120326068.png)

![image-20220521120319432](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521120319432.png)



## 二、接口关联

### 1、什么是关联

​	让多次请求之间有关的的动态数据产生联系！

### 2、为什么需要关联

​	复杂的业务往往需要发送多次请求才能完成任务；
比如：完成一次注册用户后再查回用户的全部信息

请求1:发送请求，添加一个用户
		请求1的响应结果，会出现用户id，是**动态数据**，每次都不一样！（未知数）
		在响应结果中获取用户id，存入Postman的环境变量中，供后续请求使用

请求2:根据最新用户id查询所有属性信息
			从环境变量中获取动态的用户id，作为**请求参数**使用！

思考：参数化	和 关联的区别？（面试题）

​	参数化：数据由测试人员自己准备，批量执行；	（已知条件）	主动提供
​				{{username}}

​	关联：动态数据由之前请求的结果动态产生的；		（未知的条件）	被动接受
​				是一种特殊的“参数化”{{id}}	都使用变量

### 3、何处需要关联

​	只要之前请产生的结果中，存在**动态数据**，刚好后续请求需要使用，需要通过接口的关联技术实现。

​	解决问题：多接口如何产生联系，如何调试多请求的接口（面试题）



### 4、如何进行关联

​	需求：添加好用户信息后，立即查询出该用户的完整信息

#### 1）新建用例集、文件夹，准备好两个请求

比如：day08下，新建文件夹：注册并查询用户信息

![image-20220521155444864](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521155444864.png)

请求2:新建：test02_根据id查询users信息

```
请求名称：test02_根据id查询users信息
请求方法：Get
请求地址：http://localhost:3000/api/users/?_where=(id,eq,36)
```

配置效果：

![image-20220521160005292](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521160005292.png)

添加检查点：检查结果中含有id的值

```javascript
//获取实际结果 数组
var actual = JSON.parse(responseBody);
if(actual.length > 0) {		//表示数组有结果
    var user = actual[0];
    var id = user.id;
    var name = user.username;
    tests["用户的id：" + id + "用户名" + name] = true;
} else {
    tests["查无此用户"] = false;
}

```

#### 2）处理动态数据，存于环境变量，供后续请求使用

请求1:Tests后置脚本中，请求发送后提取响应中的“动态数据”，并存入环境变量，变量名id

```javascript
//获得响应主体文本的JSON对象 var actual = JSON.parse(responseBody); //尝试获取id值 var id = actual.insertId; if(id != null) { //如果id不为null 表示存在 添加成功 tests["记录添加成功，id:" + id] = true; //PASS //将id设置到Postman的环境变量中，变量名id Run运行器中的请求可用！ pm.environment.set("id", id); } else { //否则说明添加失败 tests["添加失败"] = false; //FAIL }
```

请求2:将Get请求中的参数改为{{id}}

```
http://localhost:3000/api/users/?_where=(id,eq,{{id}})
```

![image-20220521205431607](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521205431607.png)

#### 3）针对文件夹，批量执行请求，实现关联：

![image-20220521205405426](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521205405426.png)

配置效果：

![image-20220521205329689](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521205329689.png)

执行效果

![image-20220521205310351](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521205310351.png)

控制台Console日志分析

![image-20220521205223578](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521205223578.png)

## 三、Postman实现Mock

### 1、什么是Mock？

​	在接口测试中，可用模拟接口的设计和实现，提供接口访问；

### 2、什么时候需要使用Mock？

​	实际开发过程中，Web前端和后端可用分工开发，没有必要等到后端都开发好，才开发前端，可以同时进行；
可以通过快速模拟接口实现，交给前端调用；
也可以快速检测测试方的用例是否合理。（测试左移，提前开展开发和测试工作）

​	概括为：在后台接口程序未实现时，可以模拟部分结果，通过定制的URL地址访问、供前端、用例调试。甚至可以模拟一些非法数据、海量数据，让前端出现问题加以解决。

​	目标：更容易区分Web前端还是后端问题。

### 3、如何实现Mock？

​	需求：模拟login接口的实现，提供不同参数案例和结果返回
​			（比如目前WA服务器中内容都不存在，包括Web服务器、数据库）

思路：由Postman未每个合法用户分配“云服务”提供了服务器
			需要申请访问“云服务”的URL地址

#### 1）接口设计：

请求方法：Post

接口地址：https://xxxxx/apitest/login/
					自动生成的	接口文档设计的虚拟路径	结果也是模拟的

请求参数：Body 	表单x-www-form-urlencoded

​			username和 password

返回结果：

如果使用admin和123456

```json
{"Status":1000,"Result":"Usercheck ok","Message":"登录验证成功"}
```

如果使用hehe和123

```json
{"Status":1004,"Result":"Password error","Message":"密码错误"}
```

#### 2)需要使用Postman的账号登陆成功，才能申请Mock的“云服务”！

3）新建用例集：mock1

4）有机mock1，选择“Mock Collection”模拟

![image-20220521174318221](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521174318221.png)

填写Mock服务的名称Name：testmock

​	点击Create Mock Server	窗口Mock服务器（Postman提供的云服务）

![image-20220521174721538](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521174721538.png)

![image-20220521174831368](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521174831368.png)

拷贝Mock服务器的URL地址：

```
https://cb2f8d73-576b-482a-ab08-6e21a629efb6.mock.pstmn.io
```

5）在mock1用例集下，新建一个请求，Add Request，命名：test1

6）针对test1，右上角：Add Example	添加模拟的接口实现例子1

![截屏2022-05-21 17.54.11](/Users/liuxueman/Library/Application Support/typora-user-images/截屏2022-05-21 17.54.11.png)

进行配置：就是模拟请求数据和响应结果

```
例子名称：test1_01			（显示e.g 
请求方法：Post
接口地址：将云服务地址	和 接口文档地址	整合
https://cb2f8d73-576b-482a-ab08-6e21a629efb6.mock.pstmn.io/apitest/login/
请求参数：在Body中
		username	admin
		password	123456
模拟的结果：
{"Status":1000,"Result":"Usercheck ok","Message":"登录验证成功"}

```

![image-20220521205045182](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521205045182.png)

#### 7）在新建请求test1中，直接测试该Mock用例1

![image-20220521205123272](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220521205123272.png)

再模拟一个无效数据返回结果：新建例子2

![image-20220523215859779](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523215859779.png)

填写例子2的配置（

![image-20220523093136736](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523093136736.png)

发送请求：

![image-20220523093303845](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523093303845.png)

适当修改例子2，在响应头部Header，设置返回内容类型Content	Type，指定为：application/json；charset=UTF-8

![image-20220523094130669](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523094130669.png)

保存后，再次发送请求

![image-20220523215753864](/Users/liuxueman/Library/Application Support/typora-user-images/image-20220523215753864.png)







