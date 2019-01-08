---
title: PHP常用工具
date: 2019-01-08 10:59:47
tags:
---
# 常用网址

## 前端使用文档

| 作用                  | 网址                                                         |
| --------------------- | ------------------------------------------------------------ |
| 图片Base64互相转码    | http://imgbase64.duoshitong.com/                             |
| Vue-Router使用(中文)  | https://router.vuejs.org/zh/guide/essentials/navigation.html |
| webpack使用文档(英文) | https://webpack.js.org/concepts/                             |
| webpack使用文档(中文) | https://webpack.docschina.org/concepts/                      |
| scss使用文档(中文)    | https://www.sass.hk/docs                                     |
| mint使用文档(中文)    | http://mint-ui.github.io/docs/#/zh-cn2                       |
| mui使用文档           | http://dev.dcloud.net.cn/mui/                                |

## 后台使用文档

## 工具/插件



## 其他网址



# SVN

## 部署svn单仓库

注意:在svn服务器中，我们把存放代码的地方称之为 ==仓库==。而不是称为项目文件夹。

### 1、部署单仓部的步骤

在svn中创建单仓库的步骤总共有三步：

**步骤1**：建立项目文件夹 。如建立在D:/app/blog 

**步骤2**：把上面项目目录变为仓库。 

命令为： ==**svnadmin create  D:/app/blog**==（项目目录绝对路径）

**步骤3**：开启监管仓库的服务。

命令为：==svnserve  -d  -r  D:/app/blog== 

选项说明

-d：作为后台服务运行。

-r：监管的目录。

> ==注==：上面黑窗口正在监管仓库服务，不要关闭它，否则导致后面连接不上。

### 2、svn中三大指令的使用

- checkout ：检出指令，用于==首次==与svn服务器建立连接，获取代码到本地目录（第二次以后直接使用update更新指令获取代码。）
- commit：提交本地代码到svn仓库
- update：把svn仓库上最新代码更新到本地

### 3、连接svn服务器

**步骤1**：如在我们桌面中，建立一个项目检出目录myblog，用于存放检出的代码：

检出和版本库浏览器的区别：

检出checkout：是把仓库所有的代码都检出到本地目录。

版本库浏览器：它可以浏览仓库中有哪些文件，有选择性的检出指定文件。

 

**步骤2**：输入我们svn服务器的地址，指定一个检出代码的本地目录

检出成功之后，会在本地检出目录多出一个.svn的隐藏文件夹，同时版本为0， 说明是一个新建立的仓库，之前没有任何的commit提交。

### 4、上传代码到svn仓库中

**步骤1**：在检出的目录中，建立一些测试文件或目录，鼠标右键选择commit指令进行提交

**步骤2**：【重要】填写提交的备注，主要是用于后面代码的版本回退（代码找回）



### 5、单仓库的权限配置

权限可以细分两种：

- 匿名用户提交【了解】（不需要用户名和密码也可以提交，但是不安全，个人测试使用较多）
- 【==重点掌握==】允许授权用户提交（需要用户名和密码，安全一点，企业中使用都是需要密码账号的）

### （1）匿名用户提交

每个仓库的conf目录中，都会有以下三个配置文件：

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

 

### （2）[**重点**]授权用户的权限配置

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



## svn代码冲突的解决

> 当团队开发的时候，多个开发人员对同一个文件的相同行代码都进行了修改，那么后者提交的会失败，svn会会提示我们解决冲突。

 

下面就来演示造成冲突的场景以及怎么解决

### 1、造成冲突的场景

这里以dashen用户和cainiao用户对blog仓库的index.php的文件进行操作。

1. 首先，刚开始两者都要把代码给checkout进行检出下来，此时，两者的index.php文件的代码应该是完全一致的。

```php
<?php 
echo 'hello world';
```

1. 先是cainiao用户对index.php文件进行修改：增加3-5行`cainiao write`代码,并成功commit提交，如下：

```php
<?php 
echo 'hello world';
echo 'cainiao write';
echo 'cainiao write';
echo 'cainiao write';
```

上面修改成功提交之后，即svn仓库中index.php的文件的最新内容是cainiao用户提交的。

1. 随后dashen用户对index.php也进行了操作，增加3-7行`dashen write`代码，如下 :

```php
<?php 
echo 'hello world';
echo 'dashen write';
echo 'dashen write';
echo 'dashen write';
echo 'dashen write';
echo 'dashen write';
```

现在dashen用户准备commit提交代码会出现如下的提示：

出现上面的提示，说明提交的index.php文件的内容与svn仓库中的index.php文件内容有`冲突部分`。



产生冲突的原因：

cainiao用户：修改3-5行    

dashen用户：修改3-7行 

其中3-5都被两者修改过，导致仓库无法知道使用哪部分代码，所以后者提交失败，报冲突。

### 2、解决冲突

**步骤1**：鼠标选中有冲突的文件，鼠标右键选择更新，

可见，更新下来会多出`三个辅助文件`：

- 文件名(黄色标识)：把服务器上面最新文件内容与即将提交的冲突内容进行一个融合。
- 文件名.mine: 当前用户即将要提交的文件内容。
- 文件名.r(前版本号)：所有用户提交之前，即文件冲突之前，仓库上最新的文件内容。
- 文件名.r(后版本号)：仓库上最新的文件内容。

 

==解决冲突办法==：

把三个辅助文件都给删除，修改含有黄色感叹号的文件，进行代码整合修改，再次进行提交即可。

> 注：整合冲突代码的时候，千万不要覆盖人家代码，合并之前需要程序员之间彼此商量一下。

 

## svn中的版本回退(后悔药)

> 使用到版本回退的场景：
>
> 一般由于不小心误删文件或某段代码，或者想回到之前的功能版本代码，这时候就可以通过svn提供的更新至版本功能来找回。



**步骤1**：选中要回退的文件，更新至版本

在通过之前提交的日志来找回：

**步骤2** ：找到之前提交的日志信息，点击确定，即可回到之前的代码版本。

> 注意事项
>
> 1、在检出目录中，鼠标右键点击更新，是更新最新的版本，如果需要回退到指定的版本，需要通过更新至版本来实现。
>
> 2、如要要查看某个文件的版本，右键选中此文件更新至版本即可，可以查看当前文件所有的版本变化。 
>
> 3、若点击空白处，可以查看当前项目所有代码的版本



## svn中部署多仓库

> 引入

因为一个公司会有多个项目同时进行，比如有java项目，android项目、php项目。其实也就对应着多个仓库，那么不同的开发人员提交的仓库也就不一样。所以我们有必要为不同的项目分别创建一个仓库，便于项目的后期管理，也利于具体开发人员的权限分配。



> 实现步骤：

**步骤1**：如在app目录中建立多个项目文件夹（android、java）



注意：blog之前已经是仓库了，不要重复创建。

 

**步骤**3：监管所有仓库的==父目录==（D:/app）,这样才可以访问到其中的某个仓库项目代码



> 问题？怎么访问多仓库中的某个仓库代码？

答： svn://ip/仓库名/目录/子孙目录/....

如访问blog仓库，地址为：svn://127.0.0.1/blog/

如访问java仓库，地址为： svn://127.0.0.1/java/

如访问android仓库，地址为： svn://127.0.0.1/android/

 

如访问其中blog仓库项目：

> ==注==： svn://127.0.0.1/目录/子孙目录/... 这种url访问形式只针对单仓库有效，多仓库的访问ip后面需加仓库名。

## 多仓库的权限设置

由于这里有三个仓库，这里以其中一个仓库blog为例，进行权限设置。

还是修改三个文件：svnserve.conf 、passwd、authz 

svnserve.conf配置和passwd配置和之前单仓库配置一样，不用变。  

仅需修改authz配置文件权限部分即可：

```powershell
# 格式：
# [/目录/子目录/子子孙孙目录/....]
# @组名 = 权限rw
# 用户名 = 权限rw
# * = （其他人没有权限访问）

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

## SVN其他功能

### 1、清除用户名和密码

做法：鼠标右键TortoiseSVN-->Settings-->已保存数据-->清除全部-->确定

### 2、export导出指令

export指令：相当于拷贝项目,导出的代码不会含有隐藏文件.svn，即不受svn版本控制

### 3、更改svn服务器地址

步骤：TortoiseSVN-->重新定位-->输入新的仓库地址即可



## svn监管服务注册成window系统服务

### 1、创建SVN监管仓库服务

快捷键win+r，输入cmd,以管理员的方式执行以下命令:  

```powershell
sc create SVNService binpath= "D:\svn\server\bin\svnserve.exe --service -r D:\app" start= auto
```



> 特别注意:

==binpath=后面有个空格 start=后面有个空格（只能有一个空格）==，其中SVNService 是服务的名称，此服务名称可以自己自定义，只要不和系统其它服务名重名即可。

注册成功之后会在系统服务面板中出现对应的服务。

底部任务栏-->任务管理器-->服务-->找到所注册的服务

==设置为服务自动启动==：选择服务名鼠标右键属性选择自动即可



> ==注==：如果是以之前cmd窗口的形式监管仓库服务，就不可以再使用window服务的形式进行监管，两者只能有一个在监管仓库服务。（一山不容二虎）



### 2、服务相关控制指令

关闭、开启、重启服务:

```powershell
net   stop|start|restart   服务名 
```

如开启svn服务：

```powershell
net  start  SVNService
```

删除服务:

```powershell
sc  delete  服务名	
```

如删除svn服务：

```powershell
sc  delete  SVNService
```

> 注：删除服务成功之后，若再创建同名的服务会提示此服务已标记删除，换一个服务名重新创建就可。

### 3、cmd命令的批处理

我们可以把之前在cmd中写的命令直接写在==后缀名为bat==的文件中，然后以管理员方式运行bat文件就相当于在cmd命令行中运行命令是一样的，这样操作起来更加方便。 



如其中关闭svn服务的批处理文件stop_svn.bat的内容如下：

```powershell
net stop svnService
```

开启svn服务的start_svn.bat内容如下：

```powershell
net start svnService
```





## svn中的钩子程序

### 1、钩子介绍

抽象介绍(鸟语)：所谓钩子就是与一些版本库事件触发的程序，例如新修订版本的创建，或是未版本化属性的修改。每个钩子都会被告知足够多的信息，包括那是什么事件，所操作的对象，和触发事件的用户名。通过钩子的输出或返回状态，钩子程序能让工作继续、停止或是以某种方式挂起。 

  

说的简单点，我们可以利用钩子在提交前或者是提交后做一些操作。如:

- 利用**提交前的钩子**让用户在提交代码前强制用户必须填写备注信息(了解)。
- 利用**提交后的钩子**把svn仓库代码实时同步部署到网站web目录（==重点掌握，开发中使用较多==）

 

前钩子和后钩子触发的顺序图解：

钩子的种类：

每个仓库目录中都会有个hooks目录，其中包含了所有的钩子模板代码。 

其中使用最多的有两个钩子：提交前的钩子、提交后的钩子（重点，开发中使用较多）

### 2、钩子实战

#### （1）后钩子实时同步仓库代码到web站点

 利用**提交后的钩子post-commit**把svn仓库代码实时同步到网站web目录



blog仓库的检出目录：含有.svn关联文件即可。



检出目录：C:\Users\Administrator\Desktop\blog

web站点目录：F:\local.com\myblog。



**步骤1**：先确保web站点目录与相应的仓库要建立关联，只要含有==其仓库关联的.svn隐藏文件夹==即可。在web站点目录checkout检出就有了



**步骤2**：把blog仓库中的hooks的post-commit.tmpl复制一份在当前目录，并改名为post-commit.bat

post-commit.bat内容为：

```bash
SET SVN="D:\svn\sever\bin\svn.exe"
SET DIR="D:\local.com\blog"
SVN update %DIR% --username  dashen --password dashen123
```

> 注意：要确保上面设置的用户有写入的权限。



#### （2）前钩子强制用户填写提交时备注信息

利用**提交前的钩子**让用户在提交代码前强制用户必须填写备注信息。

**步骤1**：打开blog仓库的hooks目录，把pre-commit.tmpl文件复制一份在当前目录，改名为pre-commit.bat,

pre-commit.bat内容如下：

> ==注==：
>
> 如需要中文提示，为防止乱码需要把pre-commit.bat文件的编码改为ANSI。英文提示则不会乱码
>
> 使用echo将提示信息返回给客户端，在window平台下，必须使用 1>&2 作为结尾
>
> exit 0 表示结果正确,  exit 1 或者是非零数值，表示结果错误，svn只将错误信息返回给客户端



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

![93](D:\PHP\note\quick\93.jpg)

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
> $ git clone \<url>  ./                     #克隆远程仓库 
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
> $ git add  \<file>                           #跟踪指定的文件
>
> $ git mv  \<old> \<new>               #文件改名
>
> $ git rm  \<file>                            #删除文件
>
> $ git rm  --cached  \<file>           #停止跟踪文件但不删除
>
> $ git commit  -m  'msg'             #提交所有更新过的文件
>
> $ git commit  --amend              #修改最后一次提交

> **查看提交历史**
>
> $ git log                                                    #查看提交历史
>
> $ git log  -p  \<file>                                  #查看指定文件的提交历史
>
> $ git blame  \<file>                                  #以列表方式查看指定文件的提交历史

> **撤销**
>
> $ git reset --hard HEAD                              #撤销工作目录中所有未提交文件的修改内容
>
> $ git checkout HEAD \<file>                        #撤销指定的未提交文件的修改内容
>
> $ git revert \<commit>                                #撤销指定的提交

> **分支与标签**
>
> $ git branch                                                           #显示所有本地分支
>
> $ git checkout \<branch/tag>                             #切换到指定分支或标签
>
> $ git branch \<new-branch>                               #创建新分支
>
> $ git branch -d \<branch>                                   #删除本地分支
>
> $ git tag                                                                 #列出所有本地标签
>
> $ git tag \<tagname>                                            #基于最新提交创建标签
>
> $ git tag -d \<tagname>                                       #删除标签

> **合并与衍合**
>
> $ git merge \<branch>                                         #合并指定分支到当前分支
>
> ​	git merge --no-f dev -m '合并了'
>
> $ git rebase \<branch>                                        #衍合指定分支到当前分支

> **远程操作**
>
> $ git remote -v                                                          #查看远程仓库信息
>
> $ git remote show \<remote>                                 #查看指定远程仓库信息
>
> $ git remote add \<remote> \<url>                         #添加远程仓库
>
> $ git fetch \<remote>                                               #从远程库获取代码
>
> $ git pull \<remote> \<branch>                               #下载代码并快速合并
>
> $ git push \<remote> \<branch>                             #上传代码并快速合并；
>
> $ git push -u \<remote> \<branch>                        #首次上传代码
>
> $ git push \<remote> :\<branch/tag-name>         #删除远程分支或标签
>
> $ git push \<remote> <branch/tag-name> --tags  #上传所有标签
>
> ​	 