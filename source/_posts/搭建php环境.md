---
title: 搭建php环境
date: 2019-01-09 13:50:53
categories: 
          - php
tags:
    - php
notshow: true
---
# 搭建PHP环境
<!-- more -->
## 1. PHP基本介绍

### 1.1 为什么学习PHP

PHP的优点：

a. 使用范围广，应用前景好；

b. 开发效率高，程序简洁；

c. 跨平台运行，几乎支持所有服务器环境和所有主流数据库；

d. 完全支持面向对象，也支持面向过程；

e. 内置函数丰富，完美支持正则表达式，支持通用MVC框架开发；

f. 与商业市场的粘合度非常高，渗透于大量的IT开源与闭源项目中；



### 1.2 什么是PHP

**PHP**: **Hypertext Preprocessor**  翻译过来就是：**超文本预处理器**

是一种被广泛应用的开放源代码的多用途脚本语言，它**可嵌入到 HTML中**，尤其适合 web 开发。 



PHP于1994年由[Rasmus Lerdorf](https://baike.baidu.com/item/Rasmus%20Lerdorf)创建，刚刚开始是[Rasmus Lerdorf](https://baike.baidu.com/item/Rasmus%20Lerdorf)为了要[维护](https://baike.baidu.com/item/%E7%BB%B4%E6%8A%A4)个人网页而制作的一个简单的用[Perl](https://baike.baidu.com/item/Perl)语言编写的程序，后来又用C语言重新编写了。PHP全称最早并不是叫做Hypertext Preprocessor，而是叫Personal Home Page，Hypertext Preprocessor是1997年之后才出现的。



PHP目前属于zend公司，由zend公司对其进行商业维护。公司总部设在美国加利福尼亚州的库比蒂诺，技术中心设在以色列特拉维夫的拉马特甘。



### 1.3 静态网站与动态网站的区别

1）  动态网站以数据库技术为基础，静态网站只是单纯的静态页面（如.htm、.html、.xml）；

2）  静态网站解析速度极快，但不易维护，动态网站牺牲了一定的速度，但是功能强大且维护方便；

 

**注意**：动态网站和动态效果不是一个概念，动态效果也可存在于静态的网站中！

------





## 2. 网站的基本概念

### 2.1 服务器

服务器，也称伺服器，是提供计算服务的设备。（可直观的理解为“电脑”）



### 2.2 IP

**概念**：表示[网络之间互连的协议](https://baike.baidu.com/item/%E7%BD%91%E7%BB%9C%E4%B9%8B%E9%97%B4%E4%BA%92%E8%BF%9E%E7%9A%84%E5%8D%8F%E8%AE%AE)。（IP）是Internet Protocol的外语缩写，中文缩写为“**网协**”。

IP地址是指互联网协议地址（英语：Internet Protocol Address，又译为网际协议地址），是IP Address的缩写。IP地址是[IP协议](https://baike.baidu.com/item/IP%E5%8D%8F%E8%AE%AE)提供的一种统一的地址格式，它为互联网上的每一个网络和每一台主机分配一个逻辑地址，以此来屏蔽物理地址的差异。



**注意**：我们通常口述表达所说的IP指的是IP地址的概念；而正统的IP指的是一种协议。



**IP地址其实就是用来表示计算机在互联网中的位置的地址编号！在互联网中，只能通过IP地址来找到其他的计算机**



### 2.3 域名

[域名](https://baike.baidu.com/item/%E5%9F%9F%E5%90%8D)（[Domain Name](https://baike.baidu.com/item/Domain%20Name)）：是由一串用“点”分隔的字符组成的Internet上某一台计算机或计算机组的名称，用于在数据传输时标识计算机的电子方位。



域名其实就是IP地址上的“**面具**” 。



### 2.4 DNS

dns是domain name service的缩写，它的作用简单的说，可以理解为：将域名翻译成ip地址。

互联网，或者服务器，是看不懂域名的，它们只懂IP地址，dns其实就是一个翻译，将域名翻译成绑定的IP地址，这样用户在浏览器中输入域名，服务器就可以通过dns知道用户请求的是哪个服务器上部署的网站，然后才将对应的网站内容返回给用户。



### 2.5 端口

"[端口](https://baike.baidu.com/item/%E7%AB%AF%E5%8F%A3)"是英文port的意译，可以认为是设备与外界通讯交流的出口。端口可分为**虚拟端口**和**物理端口**，其中虚拟端口指计算机内部或交换机路由器内的端口，不可见。例如计算机中的80端口、21端口、23端口等。物理端口又称为接口，是可见端口，计算机背板的RJ45网口，交换机路由器集线器等RJ45端口。电话使用RJ11插口也属于物理端口的范畴。

------







## 3. 安装apache

### 3.1 软件安装

#### 3.1.1 准备软件压缩包

![2_d1](\images\two\img_d1\2_d1.png)

#### 3.1.2 安装步骤

**1)  解压压缩包，**

![3_d1](\images\two\img_d1\3_d1.png)



**2) 点击进入httpd-2.4.29-Win32-VC15文件夹，剪切Apache24文件夹，**

![4_d1](\images\two\img_d1\4_d1.png)



**3) 将剪切的Apache24文件夹，粘贴到软件存放目录，比如我这里粘贴到F:\usr目录中，并且将Apache24改名为apache24**

![5_d1](\images\two\img_d1\5_d1.png)



**4) 修改apache主配置文件，**

**打开F:\usr\apache24\conf\httpd.conf文件，修改以下四个配置项：**

![6_d1](\images\two\img_d1\6_d1.png)

![7_d1](\images\two\img_d1\7_d1.png)

![8_d1](\images\two\img_d1\8_d1.png)

**修改完成后，保存文件！** 

5) 进入**F:/usr/apache24/bin**目录，打开命令窗口，输入**httpd –k install**安装apache

![9_d1](\images\two\img_d1\9_d1.png)

再输入**httpd –k star**t启动apache服务

![10_d1](\images\two\img_d1\10_d1.png)

6) 测试apache是否安装成功，打开浏览器，输入localhost，页面展示如下图则表示apache安装成功。

![11_d1](\images\two\img_d1\11_d1.png)



### 3.2 apache重点目录说明

![12](\images\two\img_d1\12.png)



### 3.3 httpd.exe相关应用

我们可以通过bin目录中的httpd.exe来执行某些apache控制的操作。![13_d1](\images\two\img_d1\13_d1.png)

**TIPS**：在使用httpd.exe执行相关操作指令时，可以省略".exe"，效果不变。



### 3.4 查看apache加载的模块

![49_d1](\images\two\img_d1\49_d1.png)



### 3.5 重启apache

操作指令：**httpd.exe  –k  restart**

![50_d1](\images\two\img_d1\50_d1.png)



### 3.6调出帮助列表

操作指令：**httpd.exe  -h**

![51_d1](\images\two\img_d1\51_d1.png)



### 3.6 检查配置语法

操作指令：**httpd.exe  -t**

![52_d1](\images\two\img_d1\52_d1.png)

------







## 4. 安装PHP



### 4.1软件安装

#### 4.1.1 准备软件压缩包

![14_d1](\images\two\img_d1\14_d1.png)

#### 4.1.2 安装步骤

1) 解压压缩包，

![15_d1](\images\two\img_d1\15_d1.png)

2) 剪切解压后的PHP目录php-7.1.14-Win32-VC32-x86，转移到软件安装目录wamp中， 将php-7.1.14-Win32-VC32-x86改名为php7，

![16_d1](\images\two\img_d1\16_d1.png)

3) 将PHP配置成为apache的一个模块，

1. 进入php7目录，指定当前环境的配置文件，

   ![17](\images\two\img_d1\17.png)

2. 打开apache24/conf/httpd.conf，将PHP配置为apache的一个模块，添加如下配置项

   ![21_d1](\images\two\img_d1\21_d1.png)

3. 打开php7/php.ini，增加如下配置项.

   ![19_d1](\images\two\img_d1\19_d1.png)

   ![20_d1](\images\two\img_d1\20_d1.png)

   4) 重启apache，测试访问PHP页面

   重启apache

   ![22](\images\two\img_d1\22.png)

   在F:/usr/apache24/htdocs目录中创建一个名为code1.php的文件，并且构建测试代码：

   ![23_d1](\images\two\img_d1\23_d1.png)

   打开浏览器，访问code1.php，成功则出现如下效果， 

   ![24_d1](\images\two\img_d1\24_d1.png)



------







## 5.安装MYSQL

### 5.1软件安装

#### 5.1.1 准备软件压缩包

![25_d1](\images\two\img_d1\25_d1.png)

#### 5.1.2 安装步骤

1) 在F:\usr 中创建一个新的目录，mysql5.5.2

![48_d1](\images\two\img_d1\48_d1.png)

2) 双击进行安装

![26](\images\two\img_d1\26.png)

![27](\images\two\img_d1\27.png)

3) 配置下面这个选项后**别急着点nex**t选项， 

![28](\images\two\img_d1\28.png)!29](\images\two\img_d1\29.png)

再次点击**Server data files**选项，改变其默认的安装路径，如下图所示，改变之后再点击**next**选项，

![29](\images\two\img_d1\29.png)

![30](\images\two\img_d1\30.png)![31](\images\two\img_d1\31.png)![32](\images\two\img_d1\32.png)![33](\images\two\img_d1\33.png)![34](\images\two\img_d1\34.png)![35](\images\two\img_d1\35.png)![36](\images\two\img_d1\36.png)![37](\images\two\img_d1\37.png)![38](\images\two\img_d1\38.png)![39](\images\two\img_d1\39.png)![40](\images\two\img_d1\40.png)![41](\images\two\img_d1\41.png)![42](\images\two\img_d1\42.png)![43](\images\two\img_d1\43.png)

测试使用MYSQL数据库，

打开cmd小黑窗口，输出登陆MYSQL的指令，如下图，

![44](\images\two\img_d1\44.png)

输出相关内容，显示了上图中的效果，说明MYSQL安装成功。 



------







## 6. 配置虚拟主机



### 6.1 什么是虚拟主机

**概念**：虚拟主机是指在网络服务器上分出一定的磁盘空间，用户可以租用此部分空间，以供用户放置站点及应用组件，提供必要的数据存放和传输功能。



### 6.2 虚拟主机的分类

目前对虚拟主机的分类没有明确的界定，一般要看从什么角度上来进行分类。

一种主流的分类类型是从操作系统上来进行划分，可分为：

1）  windows虚拟主机；

2）  Linux虚拟主机；



### 6.3 配置基于域名的虚拟主机

**目标**：配置一个名为www.day1.com的域名，指向F:/home/class/day1/code目录



#### 6.3.1 配置过程

1) 打开apache的主配置文件httpd.conf，开启引入httpd-vhosts.conf文件的配置，如下图去掉配置项前面的”#”，开启该配置项，

![45](\images\two\img_d1\45.png)

2) 打开 apache根目录/conf/extra/httpd-vhosts.conf文件，将下图中红框所示的部分全部加上“#”注释掉，

![46](\images\two\img_d1\46.png)

3) 在httpd-vhosts.conf文件中添加以下配置项，

![47](\images\two\img_d1\47.png)

4) 在day1/code/code1.php中构建测试代码,如下图， 

![53_d1](\images\two\img_d1\53_d1.png)

5) 重启apache,通过 www.day1.com 访问项目目录下的code1.php)文件，

重启apache

![54_d1](\images\two\img_d1\54_d1.png)

6) 打开C:/Windows/system32/drivers/etc/hosts文件，在最末尾添加如下图所示的配置项，让www.day1.com域名指向127.0.0.1也就是本地，

![55_d1](\images\two\img_d1\55_d1.png)![56_d1](\images\two\img_d1\56_d1.png)

第七步，使用浏览器测试访问，效果如下：

