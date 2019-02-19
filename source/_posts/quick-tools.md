---
title: quick-工具
date: 2019-01-08 10:59:47
categories: 
          - quick
tags: 
    - tools
---
常用网址 | SVN | Git | hexo | Animate实现动画
<!-- more -->

# 常用网址

## 常用

| 作用                    | 网址                                                      |
| ----------------------- | --------------------------------------------------------- |
| css html js jq手册      | http://www.w3school.com.cn/h.asp                          |
| tp5开发手册             | https://www.kancloud.cn/manual/thinkphp5/118003           |
| php手册                 | http://www.w3school.com.cn/php/php_ref.asp                |
| 正则表达式              | http://tool.chinaz.com/regex                              |
| mint (基于Vue) 使用文档 | http://mint-ui.github.io/docs/#/zh-cn2                    |
| mui使用文档             | http://dev.dcloud.net.cn/mui/                             |
| element使用文档         | http://element-cn.eleme.io/#/zh-CN/component/installation |
| 图标库                  | https://www.iconfont.cn/                                  |
| 前端部件layer           | http://layer.layui.com/                                   |
| 前端动画效果            | https://daneden.github.io/animate.css/                    |
| mysql文档               | http://www.runoob.com/mysql/mysql-tutorial.html           |
| 小程序官方文档          | https://developers.weixin.qq.com/miniprogram/dev/         |
| 微信公众平台文档        | https://mp.weixin.qq.com/wiki                             |



## 前端文档

| 作用            | 网址                                                         |
| --------------- | ------------------------------------------------------------ |
| Node.js文档     | http://nodejs.cn/api/                                        |
| npm包文档（En） | https://www.npmjs.com/                                       |
| express文档(En) | http://www.expressjs.com.cn/4x/api.html                      |
| Vue-Router使用  | https://router.vuejs.org/zh/guide/essentials/navigation.html |
| webpack打包     | https://webpack.docschina.org/concepts/                      |
| scss使用文档    | https://www.sass.hk/docs                                     |
| Vant使用文档    | https://youzan.github.io/vant/#/zh-CN/quickstart             |

## 后台文档

| 作用        | 网址                                            |
| ----------- | ----------------------------------------------- |
| tp5开发手册 | https://www.kancloud.cn/manual/thinkphp5/118003 |
| php手册     | http://www.w3school.com.cn/php/php_ref.asp      |
| 正则表达式  | http://tool.chinaz.com/regex                    |



## 工具/插件

| 作用                      | 网址                                     |
| ------------------------- | ---------------------------------------- |
| hexo官网地址              | https://hexo.io/zh-cn/                   |
| 图片Base64互相转码        | http://imgbase64.duoshitong.com/         |
| JSON在线解析              | https://www.json.cn/                     |
| 前段模板                  | http://www.17sucai.com/boards/61177.html |
| 格式化(xml)，json检校工具 | http://www.bejson.com/otherformat/xml/   |
| 连接github小猫图标        | http://tholman.com/github-corners/       |



# SVN

## 单仓库

### 服务端

#### 部署单仓库

**步骤1**：建立项目文件夹 。如建立在D:/app/blog 

**步骤2**：把上面项目目录变为仓库。 

命令为： ==**svnadmin create  D:/app/blog**==（项目目录绝对路径）

![98](/images/98.jpg)

**步骤3**：开启监管仓库的服务。

命令为：==svnserve  -d  -r  D:/app/blog== 

选项说明

-d：作为后台服务运行。

-r：监管的目录。

> ==注==：上面黑窗口正在监管仓库服务，不要关闭它，否则导致后面连接不上。



#### 配置权限

权限可以细分两种：

- 匿名用户提交【了解】（不需要用户名和密码也可以提交，但是不安全，个人测试使用较多）
- 【**重点**】允许授权用户提交（需要用户名和密码，安全一点，企业中使用都是需要密码账号的）

**匿名用户提交**

每个仓库(服务端)的conf目录中，都会有以下三个配置文件：

- `svnserve.conf`：当前仓库的核心配置文件，可以开启某些文件的功能   
- `passwd`：给当前仓库的增加用户名和密码
- `authz`：给当前仓库的用户设置一些权限

> 权限w：write可更新可提交 ,
>
> 权限r：read 可更新不可提交
>
> 提示：后面学的linux中还有一种权限为x,代表可执行

 

设置匿名用户访问，仅需修改`conf/svnserve.conf`配置文件即可，把其中`anno-access = read`前面

的注释`#`号给去掉，把read改为write，如下：

```powershell
anon-access = write
```

> 注：最前面要顶格写，即不要留空格。只要保存配置文件会立刻生效，不需要重新监管仓库服务。



保存后在`检出目录`进行commit提交测试：成功会提示`版本1`，说明此仓库成功提交过1次。

若修改文件再次提交就会产生`版本2`，以此类推。

即svn仓库中，保留了2个代码版本。

 

**授权用户的权限配置**

授权即需要用户名和密码才可以进行代码的操作

 

需要修改仓库conf目录中的三个配置文件：svnserve.conf、passwd、authz

**步骤1**：修改`svnserve.conf`配置文件，修改以下4处配置

```powershell
anon-access = none	 	#设置为none,禁止匿名用户访问
auth-access = write  	#设置为write,允许授权用户可更新也可提交
password-db = passwd 	#代表开启passwd配置文件
authz-db = authz 	    #代表开启authz配置文件
```

 

**步骤**2：修改`passwd`文件，给当前仓库增加一些用户名和密码

```powershell
[users]
dashen = dashen123
cainiao = cainiao123
admin = admin123
```

格式： `用户名 = 密码（明文）`

> 提醒：以后在Linux中修改含有敏感的词汇，如密码，需要给这类文件设置严格的访问权限。这样更加安全。



**步骤3**：修改`authz`文件，设置组内用户权限，及给当前仓库的用户名分配一些访问权限（rw）

设置组及组内用户：

```powershell
[groups]
# 组名 = 组成员（多个用逗号隔开）
php_group = dashen 
cainiao_group = cainiao
```

分配权限：

```powershell
 
# 权限语法格式：
# [/目录/子目录/子孙目录/....]
# @组名 = 权限rw
# 用户名 = 权限rw
# * = （其他人没有权限访问）

# 对此单仓库的所有文件进行权限控制
[/] 
@php_group = rw
@cainiao_group = rw
admin = rw
* =

# 对此单仓库的core目录下面的文件进行权限控制
[/core]
@php_group = rw 
@cainiao_group = rw
admin = rw
* =

```

==注意==：上面目录core后面不可以加斜杠/。

再次进行commit提交，若出现一个输入密码的弹窗，说明配置授权用户访问成功：

==注意==：

- 如果没有w权限，提交的时候会提示==Access Denies==权限拒绝。 
- 权限有r但未有w,只能检出代码但不能提交。  





### 客户端

#### 获取项目

主要指令：

- checkout ：检出指令，用于**首次**与svn服务器建立连接，获取代码到本地目录（第二次以后直接使用update更新指令获取代码。）
- commit：提交本地代码到svn仓库
- update：把svn仓库上最新代码更新到本地



**步骤1**：如在我们桌面中，建立一个项目检出目录myblog，用于存放检出的代码：

![99](/images/99.jpg)

检出和版本库浏览器的区别：

检出checkout：是把仓库**所有的代码**都检出到本地目录。

版本库浏览器：它可以浏览仓库中有哪些文件，**有选择性**的检出指定文件。

 

**步骤2**：输入我们svn服务器的地址，指定一个检出代码的本地目录

![100](/images/100.jpg)

检出成功之后，会在本地检出目录多出一个.svn的隐藏文件夹，同时版本为0， 说明是一个新建立的仓库，之前没有任何的commit提交。

#### 上传代码

**步骤1**：在检出(checkout)的目录中，鼠标右键选择commit指令进行提交

![102](/images/102.jpg)

**步骤2**：【重要】填写提交的备注，主要是用于后面代码的版本回退（代码找回）

![103](/images/103.jpg)

点击确定之后，如下：

![104](/images/104.jpg)

说明仓库的权限没有配置。

成功则：

![105](/images/105.jpg)

![106](/images/106.jpg)

==注意==：

- 如果没有w权限，提交的时候会提示Access Deny权限拒绝。 
- 权限有r但未有w,只能检出代码但不能提交。



#### 图标说明

**图标异常(没有出现)的解决办法**

- win8，win10解决办法：

修改如下注册表：按win+r,输入regedit

需要修改注册表中的某些选项，参考下面的图片：

![107](/images/107.jpg)

找到对应的注册表的值（Tortoise字符打头的就是svn相关图标），==在前面加多空格，空格越多优先级越高==：

![108](/images/108.jpg)

最后在底部任务栏管理器选中window资源管理器-->鼠标右键重新启动即可,再去看检出目录就可以看到图标了。

**常见图标:**

- 绿的√：常规，说明此文件中的内容与svn服务器中对应文件内容一样。
- 红的！：修改，当我们对本地的某个文件进行修改，导致与svn服务器上面的对应的文件的内容不一致就会出现此图标。
- 蓝的？：无版本控制，说明此文件没有与svn服务器建立关联，说明没有被仓库管理过
- 灰的—：忽略，提交的时候这些文件就不会出现在提交的文件变更列表中，从而也不会提交到svn服务器中
  - 忽略一个具体的文件：1.jpg
  - 忽略某一类的文件：*.jpg
  - 具体操作：选中要忽略的文件鼠标右键-->TortoiseSVN-->增加到忽略列表。
- 黄的！：冲突，多个开发人员对同一个文件的==相同行代码都进行了修改==，那么后者提交的会覆盖前者提交的，但是svn不会进行覆盖，会提示我们解决冲突，把具有冲突的文件更新下来就是上面的黄色图标。

#### 代码冲突

**步骤1**：鼠标选中有冲突的文件，鼠标右键选择更新，

![109](/images/109.jpg)

![110](/images/110.jpg)

可见，更新下来会多出`三个辅助文件`：

- 文件名(黄色标识)：把服务器上面最新文件内容与即将提交的冲突内容进行一个融合。
- 文件名.mine: 当前用户即将要提交的文件内容。
- 文件名.r(前版本号)：所有用户提交之前，即文件冲突之前，仓库上最新的文件内容。
- 文件名.r(后版本号)：仓库上最新的文件内容。



==解决冲突办法==：

把三个辅助文件都给删除，修改含有黄色感叹号的文件，进行代码整合修改，再次进行提交即可。

> 注：整合冲突代码的时候，千万不要覆盖人家代码，合并之前需要程序员之间彼此商量一下。

 

#### 版本回退

**步骤1**：选中要回退的文件，右键=>TortoiseSVN=>更新至版本

在通过之前提交的日志来找回：选择显示日志

**步骤2** ：找到之前提交的日志信息，点击确定，即可回到之前的代码版本。

![111](/images/111.jpg)



> 注意事项
>
> 1、在检出目录中，鼠标右键点击更新，是更新最新的版本，如果需要回退到指定的版本，需要通过更新至版本来实现。
>
> 2、如要要查看某个文件的版本，右键选中此文件更新至版本即可，可以查看当前文件所有的版本变化。 
>
> 3、若点击空白处，可以查看当前项目所有代码的版本



## 多仓库

### 服务端

#### 部署多仓库

**步骤1**：如在app-test目录中建立多个项目文件夹（android、java）并把其余目录变为仓库

命令为： **svnadmin create D:\PHP\app-test\android** 

![112](/images/112.jpg)

注意：test_server之前已经是仓库了，不要重复创建。

**步骤**3：监管所有仓库的==父目录==（D:/app-test）,这样才可以访问到其中的某个仓库项目代码

命令为：**svnserve  -d  -r  D:\PHP\app-test**



#### 权限设置

由于这里有三个仓库，这里以其中一个仓库test_server为例，进行权限设置。

还是修改三个文件：svnserve.conf 、passwd、authz 

svnserve.conf配置和passwd配置和之前单仓库配置一样，不用变。  

仅需修改authz配置文件权限部分即可：

```powershell
# 对此多仓库的blog仓库的所有文件进行权限控制
[blog:/] 
@php_group = rw
@cainiao_group = rw
admin = rw
* =
# 对此多仓库的blog仓库的core目录下面的文件进行权限控制
[blog:/core]
@php_group = rw 
@cainiao_group = rw
admin = rw
* =
```

单仓库和多仓库的authz权限文件权限配置区别：

- 单仓库：[/目录/子目录/子孙目录/.....] 
- 多仓库：[当前仓库名:/目录/子目录/子孙目录/.....]

### 客户端

#### 获取项目

svn://ip/仓库名/目录/子孙目录/....

如访问test_server仓库，地址为：svn://127.0.0.1/test_server/

如访问java仓库，地址为： svn://127.0.0.1/java/

 

如访问其中test_server仓库项目：

![113](/images/113.jpg)

> ==注==： svn://127.0.0.1/目录/子孙目录/... 这种url访问形式只针对单仓库有效，多仓库的访问ip后面需加仓库名。



## 其他功能

### 清除用户名和密码

做法：鼠标右键TortoiseSVN-->Settings-->通用-->已保存数据-->清除全部-->确定

![114](/images/114.jpg)

### 拷贝项目

export指令：相当于拷贝项目,导出的代码不会含有隐藏文件.svn，即不受svn版本控制

![115](/images/115.jpg)



### 更改仓库地址

步骤：TortoiseSVN-->重新定位-->输入新的仓库地址即可



## svn中的钩子程序

- 利用**提交前的钩子**让用户在提交代码前强制用户必须填写备注信息。
- 利用**提交后的钩子**把svn仓库代码实时同步部署到网站web目录

 

钩子的种类：

每个仓库目录中都会有个hooks目录，其中包含了所有的钩子模板代码。 

其中使用最多的有两个钩子：提交前的钩子、提交后的钩子（重点，开发中使用较多）

![116](/images/116.jpg)



### 同步代码到web站点

 利用**提交后的钩子post-commit**把svn仓库代码实时同步到网站web目录

web站点目录：E:\local.com\test。

**步骤1**：先确保web站点目录与相应的仓库要建立关联，只要含有==其仓库关联的.svn隐藏文件夹==即可。在web站点目录checkout检出就有了



**步骤2**：把blog仓库中的hooks的post-commit.tmpl复制一份在当前目录，并改名为post-commit.bat

post-commit.bat内容为：

```bash
#REPOS="$1"
#REV="$2"
#TXN_NAME="$3"
#
#mailer.py commit "$REPOS" "$REV" /path/to/mailer.conf

SET SVN="D:\PHP\软件、工具\svn\server\bin\svn.exe"
SET DIR="E:\local.com\test"
SVN update %DIR% --username  dashen --password dashen123
```

> 注意：要确保上面设置的用户有写入的权限。



实时同步效果：

![117](/images/117.jpg)



### 强制填写备注信息

利用**提交前的钩子**让用户在提交代码前强制用户必须填写备注信息。

**步骤1**：打开blog仓库的hooks目录，把pre-commit.tmpl文件复制一份在当前目录，改名为pre-commit.bat,



pre-commit.bat内容如下：

```bash
@echo off
:: 
::  Stops commits that have empty log messages.
:: 

@echo off

set svnlook="D:\PHP\软件、工具\svn\server\bin\svnlook.exe"
setlocal

rem Subversion sends through the path to the repository and transaction id
set REPOS=%1
set TXN=%2
 
rem check for an empty log message
%svnlook% log %REPOS% -t %TXN% | findstr ....... > nul
if %errorlevel% gtr 0 (goto err) else exit 0 

:err
echo. 1>&2
echo Your commit has been blocked because you didn't give any log message 1>&2
echo 再写这么少字试试 1>&2
exit 1
```

成功如下：

![118](/images/118.jpg)



> ==注==：
>
> 如需要中文提示，为防止乱码需要把pre-commit.bat文件的编码改为ANSI。英文提示则不会乱码（用editplus另存）
>
> 使用echo将提示信息返回给客户端，在window平台下，必须使用 1>&2 作为结尾
>
> exit 0 表示结果正确,  exit 1 或者是非零数值，表示结果错误，svn只将错误信息返回给客户端



# 微信开发

## 订阅号&公众号

微信公众平台文档  https://mp.weixin.qq.com/wiki

微信公众平台：https://mp.weixin.qq.com/

重新启动公众平台：

- 登录127.0.0.1:8080 查看是否连接到本地文件

  ![119](/images/119.jpg)

-  成功后用黑窗口进入natapp文件，连接natapp和本地8080端口

  > \> cd D:\PHP\code\natapp_windows_amd64_2_3_9

  > \> natapp

  ![120](/images/120.jpg)

- 进入微信公众平台

  https://mp.weixin.qq.com/

  点击开发->基本配置->修改配置，更改服务器地址和token（token和a1.php文件下的token一样）

  ![121](/images/121.jpg)

- 配置成功后进入开发->开发者工具->公众平台测试账号，扫码登录 修改接口配置信息

  ![122](/images/122.jpg)



## 微信小程序

### 注册登录

- 一个邮箱只能申请一个小程序帐号

- 小程序码

  ![126](/images/126.jpg)

- 获得appid

  ![127](/images/127.jpg)

### 开发工具&模拟器

#### 下载开发工具

- 下载地址：<http://t.cn/RrKI5a3>

  下载相应版本的软件，下载后，双击运行安装，一路下一步即可。

- 安装成功

#### vscode开发工具

当前vscode还不支持小程序代码提示，所以要进一步安装相关vscode的插件，

minapp插件：

![129](/images/129.jpg)

wechat-snippet插件：

![130](/images/130.jpg)

wepy snippet插件：

![131](/images/131.jpg)

### 运行小程序

运行官方开发工具，填写项目信息，点击确定完成：

注意：选择为建立普通快速启动模板

![128](/images/128.jpg)

点击确定，进入开发界面：

![132](/images/132.jpg)

看到左侧部分显示了“Hello World”说明我们小程序就构建成功。



### 文件结构&配置

#### 文件结构

1. 一个小程序主体部分由三个文件组成，==必须放在项目的根目录==，
   - **app.js** ： 必需，小程序逻辑
   - **app.json** ： 必需，小程序公共设置
   - **app.wxss** ： 非必需，小程序公共样式表

![133](/images/133.jpg)

2. 项目根目录下的**pages**文件夹存放的是小程序中的**页面**；每个页面都由4个文件组成：

   （==注意：这四种文件**必须同名**的==）

   - **xx.js** ： 必需，页面逻辑
   - **xx.wxml**：必需，页面结构
   - **xx.wxss**：非必需，页面样式表
   - **xx.json**：非必需，页面配置

   比如：

   pages目录：

   ![134](/images/134.jpg)

   pages/index目录：

   ![135](/images/135.jpg)

#### app.json(公共设置)

app.json 文件用来对微信小程序进行全局配置，决定页面文件的路径、窗口表现、设置网络超时时间、设置多 tab(底部导航菜单) 等。

**注意：**1）app.json中不能添加任何注释，否则会报错；2）字符串用双引号引起来。

![136](/images/136.jpg)

可设置的属性如下：

| 属性               | 类型         | 必填 | 描述                   |
| ------------------ | ------------ | ---- | ---------------------- |
| **pages**          | String Array | 是   | 设置页面路径           |
| **window**         | Object       | 否   | 设置默认页面的窗口表现 |
| **tabBar**         | Object       | 否   | 设置底部tab的表现      |
| **networkTimeout** | Object       | 否   | 设置网络超时时间       |
| **debug**          | Boolean      | 否   | 设置是否开启debug模式  |

属性的配置可查看微信小程序文档

### 事件

#### 事件分类

| 类型               | 触发条件                                                     |
| ------------------ | ------------------------------------------------------------ |
| **touchstart**     | 手指触摸动作开始                                             |
| **touchmove**      | 手指触摸后移动                                               |
| touchcancel        | 手指触摸动作被打断，如来电提醒，弹窗                         |
| touchend           | 手指触摸动作结束                                             |
| **tap**            | 手指触摸后马上离开                                           |
| **longpress**      | 手指触摸后，超过350ms再离开，如果指定了事件回调函数并触发了这个事件，tap事件将不被触发 |
| transitionend      | 会在 WXSS transition 或 wx.createAnimation 动画结束后触发    |
| animationstart     | 会在一个 WXSS animation 动画开始时触发                       |
| animationiteration | 会在一个 WXSS animation 一次迭代结束时触发                   |
| animationend       | 会在一个 WXSS animation 动画完成时触发                       |
| touchforcechange   | 在支持 3D Touch 的 iPhone 设备，重按时会触发                 |

事件绑定：

```html
<!-- bind:事件名="函数" -->
<!-- 例如 -->
<view bind:tap="p_tap">
	<view bind:tap="s_tap">你过来呀</view>
</view>

<!-- 阻止冒泡 -->
<view bind:tap="p_tap">
	<view catch:tap="s_tap">你过来呀</view>
</view>
```

#### 事件对象

| 属性          | 类型    | 说明                           |
| ------------- | ------- | ------------------------------ |
| type          | String  | 事件类型                       |
| timeStamp     | Integer | 事件生成时的时间戳             |
| target        | Object  | 触发事件的组件的一些属性值集合 |
| currentTarget | Object  | 当前组件的一些属性值集合       |



# Git

## 获取git仓库

1. 在本地目录中执行git init指令，初始化一个仓库。 
2. 从远程服务器拉取一个仓库。如从github拉取，或是从自己搭建的git服务器拉取。 

## 克隆远程仓库代码到本地

克隆远程的仓库代码到指定目录: 

命令：**git  clone 仓库地址  [目录]**

注意：不写目录名称会**在当前目录**创建一个与github仓库同名的仓库。相当于

**git clone 仓库地址  ./**  

**仓库地址**：

![93](/images/93.jpg)

仓库地址协议有两种：https、ssh。ssh协议可以免去每次推送代码输入密码的烦恼。

完整命令：git  clone  https://github.com/JIUXINYAN/tour.git  ./  

克隆成功后，目录中会多一个.git的隐藏文件夹



## Git常用命令

> **master** ：默认开发分支                            **HEAD**：默认开发分支
>
> **origin**：默认远程仓库                            **HEAD^**：Head的父提交



> **全局设置**
>
> $ git config --global user.name 名字           # 用户名
>
> $ git config --global user.email 邮箱           # 用户邮箱
>
> $ git config user.name 名字                         # 用户名(当前项目有效)
>
> $ git config user.email 邮箱                         # 用户邮箱(当前项目有效)

> **创建仓库**
>
> $ git clone (url)  ./                     #克隆远程仓库 
>
> $ git init                                       #初始化本地仓库

> **修改和提交**
>
> $ git status                                   #查看状态
>
> $ git diff                                        #查看变更内容
>
> $ git add                                       #跟踪所有改动过的文件
>
> $ git add  (file)                           #跟踪指定的文件
>
> $ git mv  (old) (new)               #文件改名
>
> $ git rm  (file)                            #删除文件
>
> $ git rm  --cached  (file)           #停止跟踪文件但不删除
>
> $ git commit  -m  'msg'             #提交所有更新过的文件
>
> $ git commit  --amend              #修改最后一次提交

> **查看提交历史**
>
> $ git log                                                    #查看提交历史
>
> $ git log  -p  (file)                                  #查看指定文件的提交历史
>
> $ git blame  (file)                                  #以列表方式查看指定文件的提交历史

> **撤销**
>
> $ git reset --hard HEAD                              #撤销工作目录中所有未提交文件的修改内容
>
> $ git checkout HEAD (file)                        #撤销指定的未提交文件的修改内容
>
> $ git revert (commit)                                #撤销指定的提交

> **分支与标签**
>
> $ git branch                                                           #显示所有本地分支
>
> $ git checkout (branch/tag)                             #切换到指定分支或标签
>
> $ git branch (new-branch)                               #创建新分支
>
> $ git branch -d (branch)                                   #删除本地分支
>
> $ git tag                                                                 #列出所有本地标签
>
> $ git tag (tagname)                                            #基于最新提交创建标签
>
> $ git tag -d (tagname)                                       #删除标签

> **合并与衍合**
>
> $ git merge (branch)                                         #合并指定分支到当前分支
>
> ​	git merge --no-f dev -m '合并了'
>
> $ git rebase (branch)                                        #衍合指定分支到当前分支

> **远程操作**
>
> $ git remote -v                                                          #查看远程仓库信息
>
> $ git remote show (remote)                                 #查看指定远程仓库信息
>
> $ git remote add (remote) (url)                         #添加远程仓库
>
> $ git fetch (remote)                                               #从远程库获取代码
>
> $ git pull (remote) (branch)                               #下载代码并快速合并
>
> $ git push (remote) (branch)                             #上传代码并快速合并；
>
> $ git push -u (remote) (branch)                        #首次上传代码
>
> $ git push (remote) :(branch/tag-name)         #删除远程分支或标签
>
> $ git push (remote) <branch/tag-name) --tags  #上传所有标签
>



# hexo

保证自己电脑安装以下工具：

- git
- nodejs

安装hexo-cli

```
npm install hexo-cli -g  --registry https://registry.npm.taobao.org
```

hexo常用的几个命令：

hexo  n   '文章的名称'   ：新建文章

hexo g  ：   生成静态页面

hexo s    ：  启动本地服务

hexo d ：发布到线上仓库 ==username.github.io==

​	需要配置线上仓库：

​	1.配置 _config.yml 

```
deploy:
  type: git
  repo: git@github.com:qingtian-boy/qingtian-boy.github.io.git
  branch: master
```

1. 安装一个工具

```
npm install hexo-deployer-git --save
```



# Animate实现动画

- 导入动画类库：

  进入Animate.css :https://daneden.github.io/animate.css/

  点击下载，复制粘贴animate.css，放到项目中并导入

  ```html
  <link rel="stylesheet" type="text/css" href="./lib/animate.css">
  ```

- 定义 transition 及class类

  - 其中通过vue提供的自定义过渡类名 `enter-active-class、leave-active-class`来设置类。
  - 每个进场和出场提供两个class类名，第一个`animated`类是基本的，必须添加的样式名，任何想实现的元素都得添加这个。第二个是指定的动画样式名。 是由Animate.css提供的
  - :duration是定义进场和离场时动画的时长，单位毫秒，两者也可以单独定义`:duration=“{enter:200,leave:400}”`

  ```html
  <div id="app">
      <button @click="flag=!flag">toggle</button>
      <transition 
          enter-active-class="animated rotateIn" 
          leave-active-class="animated rotateOut"
          :duration="200">
          <h2 v-show="flag">我是h2，排名老二</h2>
      </transition>
  </div>
  ```





# Element组件

**文档**：http://element-cn.eleme.io/#/zh-CN/component/installation

## 安装

### npm安装

> \> cnpm i element-ui -S 



在main.js中引入

```javascript
//引入ElementUI模块
import ElementUI from "element-ui"
//引入EU样式
import "element-ui/lib/theme-chalk/index.css"
//把EU挂载到Vue上
Vue.use(ElementUI)
```



### CDN安装 

通过unpkg.com/element-ui获取到最新版本，在页面上引入js和css即可使用

```html
<!--引入样式 -->
<link ref="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
<!--引入组件库 -->
<script src="https://unpkg.com/element-ui/lib/index.js"></script>
```



## 基本组件(Base)

### 布局容器(Container)

把对应代码移植到 Home组件中

![169](/images/169.jpg)



## 表单(Form)

### 表单项

- 在elementUI官网中找到合适的代码

![154](/images/154.jpg)

- 移植到项目中进行修改使用

  ![155](/images/155.jpg)

![156](/images/156.jpg)

- 查看EU文档 发现输入框的图标字符需要添加属性prefix-icon

  ![157](/images/157.jpg)



### 表单验证

【例1】**登录页面表单验证**

- 打开文档，查找Form->Form表单->表单验证，查看代码

![140](/images/140.jpg)

![141](/images/141.jpg)

- 修改Login.vue中表单代码 在指定标签中添加rules和prop属性

  ![142](/images/142.jpg)

- 修改验证规则

  ![143](/images/143.jpg)

- 查看数据验证方式 ref用于捕获DOM对象 在提交按钮的确认事件中传入表单对象

  ![144](/images/144.jpg)

  ![145](/images/145.jpg)

- 修改Login组件的表单和代码 在登陆按钮中添加click事件 事件中进行数据验证 

   ![146](/images/146.jpg)

  ![147](/images/147.jpg)



## 导航(Navigation)

### 导航菜单

【例2】侧栏

![170](/images/170.jpg)

- 删除两个不需要的事件 @open="handleOpen"  @close="handleClose"

  注意：index属性的值不能相同

- 查看 导航菜单 折叠功能如何实现

![172](/images/172.jpg)

- 在el-menu元素上添加 :collapse属性 绑定数据 isCollapse

- 在操作按钮上添加点击事件

  ![173](/images/173.jpg)

- 把el-menu的父组件 width改为auto 侧边栏的宽度样式为自适应 

![171](/images/171.jpg)



## 数据(Data)

### 表格

了解表格使用方法

data 为对象数组，prop为每行的数据，label为标题

![176](/images/176.jpg)

![177](/images/177.jpg)

### 分页

完整功能分页

![178](/images/178.jpg)



![179](/images/179.jpg)