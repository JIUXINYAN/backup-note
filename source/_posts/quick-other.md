---
title: quick-other
date: 2019-01-08 14:48:48
categories: 
          - quick
tags: 
    - linux
---
Linux | NoSql | MongoDB
<!-- more -->
# Linux

## 文件和目录

### linux目录

**/**

> 表示Linux的根目录，作用是存放一切Linux相关目录和文件，包括核心和非核心的

#### 第一级目录

| 目录            | 作用                                                         |
| --------------- | ------------------------------------------------------------ |
| **/bin**        | 存放最经常使用的命令                                         |
| **/sbin**       | 存放系统管理员使用的系统管理程序                             |
| **/home**       | 存放普通用户的主目录，每个主目录以用户账号命名               |
| **/root**       | 为系统管理员的用户主目录                                     |
| **/dev**        | 管理设备                                                     |
| **/media**      | 镜像光盘的目录，如U盘光驱等，识别后会挂载到这个目录下        |
| **/mnt**        | 挂载的文件夹，可以将外部的存储挂载在/mnt上，进入该目录就可以查看内容 |
| **/etc**        | 存放配置文件                                                 |
| **/usr**        | 存放用户安装的应用程序和文件                                 |
| **/usr/local**  | 存放主机额外安装软件                                         |
| **/lib**        | 系统开机时所需要最基本的动态连接共享库                       |
| **/boot**       | 存放启动linux时使用的一些核心文件                            |
| **/tmp**        | 存放一些临时文件                                             |
| **/selinux**    | 安全目录                                                     |
| **/opt**        | 存放主机额外安装软件                                         |
| **/var**        | 变量、日志                                                   |
| **/proc**       | 系统内存的映射。获取系统信息 (别动)                          |
| **/srv**        | 存放服务启动后需要提取的数据 (别动)                          |
| **/sys**        | 内核相关目录 (别动)                                          |
| **/lost+found** | 一般为空目录，非法关机后就存放了一些文件                     |



### linux文件

![185](D:\PHP\note\quick\185.jpg)

![186](D:\PHP\note\quick\186.jpg)

#### 文件类型

| 表示  | 文件类型               |
| ----- | ---------------------- |
| **-** | 普通文件               |
| **d** | 目录                   |
| **l** | 软连接                 |
| **c** | 字符设备【键盘，鼠标】 |
| **d** | 块文件，硬盘           |

### 权限

#### 文件权限

| 表示  | 权限                                       |
| ----- | ------------------------------------------ |
| **r** | 代表可读(read) : 可以读取、查看            |
| **w** | 代表可写(write) : 可以修改，不代表可以删除 |
| **x** | 代表可执行(execute) : 可以被执行           |

#### 目录权限

| 表示  | 权限                                                   |
| ----- | ------------------------------------------------------ |
| **r** | 代表可读(read) : 可以读取，ls查看目录内容              |
| **w** | 代表可写(write) : 可以修改，目录内创建+删除+重命名目录 |
| **x** | 代表可执行(execute) : 可以进入该目录                   |



## linux命令

### 开机关机

| 命令格式                  | 作用                         |
| ------------------------- | ---------------------------- |
| **[shutdown](#shutdown)** | 按照规定关机，以分钟作为单位 |
| **[halt](#halt)**         | 关机，作用如上               |
| **[reboot](#reboot)**     | 重启操作系统（不推荐）       |
| **sync**                  | 把内存的数据同步到磁盘       |

<span id='shutdown'>**shutdown**</span>

> **参数**：

- -t seconds : 设定在几秒钟之后进行关机程序
- -r : 关机后重新开机
- -h : 关机后停机
- -c : 取消目前已经进行中的关机动作
- time : 设定关机的时间
- message : 传送给所有使用者的警告讯息

```shell
立即关机
# shutdown -h now

立即重启
# shutdown -r now

1分钟后关机
# shutdown -h 1

指定5分钟后关机
# shutdown +5 “System will shutdown after 5 minutes”
```

<span id='reboot'>**reboot**</span>

> **参数**：

- -n : 在重开机前不做将记忆体资料写回硬盘的动作
- -w : 并不会真的重开机，只是把记录写到 /var/log/wtmp 档案里
- -d : 不把记录写到 /var/log/wtmp 档案里（-n 这个参数包含了 -d）
- -f : 强迫重开机，不呼叫 shutdown 这个指令
- -i : 在重开机之前先把所有网络相关的装置先停止

```shell
重新启动
# reboot
```

<span id='halt'>**halt**</span>

> **参数**：

- -n : 在关机前不做将记忆体资料写回硬盘的动作
- -w : 并不会真的关机，只是把记录写到 /var/log/wtmp 档案里
- -d : 不把记录写到 /var/log/wtmp 档案里（-n 这个参数包含了 -d） -f : 强迫关机，不呼叫 shutdown 这个指令
- -i : 在关机之前先把所有网络相关的装置先停止
- -p : 当关机的时候，顺便做关闭电源（poweroff）的动作

```shell
关闭系统
# halt

关闭系统并关闭电源
# halt -p

关闭系统，但不留下纪录
# halt -d
```





### 系统管理

| 命令格式                         | 作用                                 |
| -------------------------------- | ------------------------------------ |
| **[id](#id)**                    | 用于显示用户的ID，以及所属群组的ID。 |
| **[useradd](#useradd)**          | 添加用户                             |
| **[userdel](#userdel)**          | 删除用户                             |
| **[usermod](#usermod)**          | 修改用户账号 修改用户所在组          |
| **[groupadd](#groupadd)**        | 新增组                               |
| **groupdel**                     | 删除组                               |
| **[groupmod](#groupmod)**        | 修改组                               |
| [**--help** / **man**](#history) | 查看帮助                             |
| **[history](#history)**          | 显示当前登录用户的操作历史           |
| **[crond](#crond)**              | 进行定时任务的设置                   |
| **[whereis](#whereis)**          | 在特定目录中查找符合条件的文件       |

<span id='id'>**id**</span>

> **语法**：

```shell
id [-gGnru][--help][--version][用户名称]
```

> **参数**：

- -g 　显示用户所属群组的ID。
- -G 　显示用户所属附加群组的ID。
- -n 　显示用户，所属群组或附加群组的名称。
- -r 　显示实际ID。
- -u 　显示用户ID。
- -help 　显示帮助。
- -version 　显示版本信息。

```shell
显示当前用户ID 当前用户群组的ID
# id
# id -g

显示某个用户ID 群组ID
# id zwj
# id -g zwj
```





<span id='useradd'>**useradd**</span>

> **语法**：

```shell
useradd [-mMnr][-c <备注>][-d <登入目录>][-e <有效期限>][-f <缓冲天数>][-g <群组>][-G <群组>][-s <shell>][-u <uid>][用户帐号]
```

> **参数**：

- -c (备注)　加上备注文字。备注文字会保存在passwd的备注栏位中。
- -d (登入目录) 　指定用户登入时的启始目录。
- -D 　变更预设值．
- -e (有效期限) 　指定帐号的有效期限。
- -f (缓冲天数) 　指定在密码过期后多少天即关闭该帐号。
- -g (群组) 　指定用户所属的群组。
- -G (群组) 　指定用户所属的附加群组。
- -m 　自动建立用户的登入目录。
- -M 　不要自动建立用户的登入目录。
- -n 　取消建立以用户名称为名的群组．
- -r 　建立系统帐号。
- -s (shell)　 　指定用户登入后所使用的shell。
- -u (uid) 　指定用户ID。

```shell
添加一个用户zsx
# useradd zsx

为添加的zsx用户指定组super
# useradd -g super zsx

创建一个系统用户
# useradd -r zsx

为新添加的用户指定home目录
# useradd -d /home/myd zsx

建立用户且制定ID
# useradd zsx -u 544
```



<span id='groupadd'>**groupadd**</span>

```shell
创建一个组moster
# groupadd monster
```



<span id='userdel'>**userdel**</span>

> **参数**：

- -r 　删除用户登入目录以及目录中所有文件。

```shell
删除用户账号
# userdel zsx
```



<span id='usermod'>**usermod**</span>

> **语法**：

```
usermod [-LU][-c <备注>][-d <登入目录>][-e <有效期限>][-f <缓冲天数>][-g <群组>][-G <群组>][-l <帐号名称>][-s <shell>][-u <uid>] 用户
```

> **参数**：

- -c <备注> 　修改用户帐号的备注文字。
- -d <登入目录> 　修改用户登入时的目录。
- -e <有效期限> 　修改帐号的有效期限。
- -f <缓冲天数> 　修改在密码过期后多少天即关闭该帐号。
- -g <群组> 　修改用户所属的群组。
- -G <群组> 　修改用户所属的附加群组。
- -l <帐号名称> 　修改用户帐号名称。
- -L 　锁定用户密码，使密码无效。
- -s (shell) 　修改用户登入后所使用的shell。
- -u (uid) 　修改用户ID。
- -U 　解除密码锁定。

```shell
将tom用户从police组移动到bandit组
# usermod -g bandit tom
```



<span id='groupmod'>**groupmod**</span>

> **语法**：

```shell
groupmod [-g <群组识别码> <-o>][-n <新群名>][群名]
```

> **参数**：

- -g  (群组识别码) 　设置欲使用的群组识别码。
- -o 　重复使用群组识别码。
- -n  (新群组名称) 　设置欲使用的群组名称。

```shell
修改群名 把linuxso改为linux
# groupmod -n linux linuxso 
```



<span id='help'>**--help**和**man**</span>

```shell
查看ls指令有哪些选项
# ls --help
查看某个命令的帮助(英文文档)
# man cd
退出
# :q
```



<span id='history'>**history**</span>

```shell
查看所有历史记录
# history

显示最近10条历史记录
# history 10

执行历史编号为5的指令
# history
# !5
```



<span id='crond'>**crond**</span>

> **语法**：

```shell
crontab [选项]
```

> 常用选项：

- -e  编辑crontab定时任务
- -l    查询crontab任务
- -r    删除当前用户所有的crontab任务

```shell
修改群名 把linuxso改为linux
# groupmod -n linux linuxso 
```



<span id='whereis'>**whereis**</span>

> **语法**：

```shell
whereis [-bfmsu][-B <目录>...][-M <目录>...][-S <目录>...][文件...]
```

> 参数：

- -b 　只查找二进制文件。
- -B<目录> 　只在设置的目录下查找二进制文件。
- -f 　不显示文件名前的路径名称。
- -m 　只查找说明文件。
- -M<目录> 　只在设置的目录下查找说明文件。
- -s 　只查找原始代码文件。
- -S<目录> 　只在设置的目录下查找原始代码文件。
- -u 　查找不包含指定类型的文件。

```shell
查看指令bash的位置
# whereis bash
```



### 文件目录

ln -s file1 lnk1 创建一个指向文件或目录的软链接  

ln file1 lnk1 创建一个指向文件或目录的物理链接  



file file1 outputs the mime type of the file as text  

iconv -l 列出已知的编码  

| 命令格式            | 作用                                                         |
| ------------------- | ------------------------------------------------------------ |
| [**cd**](#cd)       | 切换目录                                                     |
| **[pwd](#pwd)**     | 显示当前所在的工作目录                                       |
| [**ls**](#ls)       | 列出目录当中的内容（目录和文件）                             |
| [**mkdir**](#mkdir) | 创建目录                                                     |
| [**rm/rmdir**](#rm) | 删除文件或目录                                               |
| [**mv**](#mv)       | 移动目录或重命名                                             |
| **[cp](cp)**        | 复制文件或目录                                               |
| **[touch](#touch)** | 创建文件 / 修改文件或目录的时间属性                          |
| **[cat](#cat)**     | 用于输出文件内容                                             |
| **[more](#more)**   | 类似 cat ，不过会以一页一页的形式显示，                      |
| **[less](#less)**   | 与 more 类似，但less 可以随意浏览文件，more 仅能向前移动     |
| **[ln](#ln)**       | 类似快捷方式，为某一个文件在另外一个位置建立一个同步的链接。 |
| **[chown](#chown)** | 改变文件的拥有者及其所在组                                   |
| **[chgrp](#chgrp)** | 修改文件所在组                                               |
| **[chmod](#chmod)** | 修改文件权限                                                 |

<span id='cd'>**cd**</span>

```shell
进入/home目录
# cd /home

返回上一级目录
# cd ..

返回上两级目录
# cd ../..

进入个人的主目录
# cd
# cd ~user1

返回上次所在的目录
# cd -					
```



<span id='ls'>**ls**</span>

> **参数** :

- -a 显示隐藏文件及目录
- -l 详细列出
- -r 文件以反序显示(英文字母)
- -t 文件以建立时间先后次序列显示

```shell
列出目录当中的内容（目录和文件）
# ls

显示目录下文件或者子目录的详细信息
# ls -l
# ll

使用选项 -h:表示以人性化的方式显示列表
# ls -lh

使用选项 -a（all）：表示显示全部文件（包括隐藏文件）
# ls -a

查看目录中的文件
# ls -F   

显示包含数字的文件名和目录名
# ls [0-9]   

查看文件所有者
# ls -ahl
```



<span id='mkdir'>**mkdir**</span>

```shell
创建一个叫做 'dir1' 的目录'  
# mkdir dir1 

同时创建两个目录
# mkdir dir1 dir2 

创建一个目录树
# mkdir -p /tmp/dir1/dir2   
```



<span id='rm'>**rm**</span>

> **参数**：

- -i 删除前逐一询问确认。
- -f 亦直接删除，无需逐一确认。
- -r 将目录及以下的文件以前删除。

```shell
删除一个叫做 'dir1' 的目录并同时删除其内容
# rm -rf dir1     

删除一个叫做 'dir1' 的空目录
# rmdir dir1   

删除一个叫做 'file1' 的文件
# rm -f file1  

 同时删除两个目录及它们的内容
# rm -rf dir1 dir2
```



<span id='mv'>**mv**</span>

> **参数**：

- -i: 询问是否覆盖旧文件;
- -f: 无需询问覆盖;

```shell
移动 一个file1文件到dir1目录中
# mv file1 dir1

重命名文件
# mv file1 file2

如果存在dir2：移动 一个dir1目录到dir2目录中/如果dir2不存在：重命名dir1
# mv dir1 dir2 
```



<span id='cp'>**cp**</span>

> **参数**：

- -a：复制目录时使用，保留链接、文件属性，并复制目录下的所有内容。dpR 
- -d：复制时保留链接。
- -f：覆盖已经存在的目标文件而不给出提示。
- -i：覆盖目标文件之前给出提示，
- -p：除复制文件的内容外，还把修改时间和访问权限也复制到新文件中。
- -r：若文件是一个目录文件，将复制该目录下所有的子目录和文件。
- -l：不复制文件，只是生成链接文件。

```shell
复制file1文件，改名为file2
# cp file1 file2   

复制dir目录下的所有文件到当前工作目录
# cp dir/* .   

复制dir1目录到当前工作目录
# cp -a /tmp/dir1 .   

复制一个目录
# cp -a dir1 dir2   
```



<span id='touch'>**touch**</span>

> **参数**：

- a 改变文件的读取时间记录。
- m 改变文件的修改时间记录。
- c 假如文件不存在，不会建立新的文件。
- d 设定时间与日期，可以使用各种不同的格式。
- t 设定文件的时间记录，格式与 date 指令相同。
- --no-create 不会建立新文件。
- --help 列出指令格式。
- --version 列出版本讯息。

```shell
如果文件不存在则创建文件file1 / 存在则表示修改文件的时间属性为当前系统时间
# touch file1

修改一个文件或目录的时间戳 - (YYMMDDhhmm)
# touch -t 0712250000 file1   
```



<span id='cat'>**cat**</span>

> **参数**：

- -n ：由 1 开始对所有输出的行数编号。
- -b：和 -n 相似，只不过对于空白行不编号。
- -s：当遇到有连续两行以上的空白行，就代换为一行的空白行。

```shell
把 file1 的内容加上行号后覆盖在file2文档里
# cat -n file1 > file2
```



<span id='more'>**more**</span>

> **参数**：

- -num 一次显示的行数
- -d 提示使用者，在画面下方显示 [Press space to continue, 'q' to quit.] ，如果使用者按错键，则会显示 [Press 'h' for instructions.] 而不是 '哔' 声
- -f 计算行数时，以实际上的行数，而非自动换行过后的行数（有些单行字数太长的会被扩展为两行或两行以上）
- -p 不以卷动的方式显示每一页，而是先清除萤幕后再显示内容
- -c 跟 -p 相似，不同的是先显示内容再清除其他旧资料
- -s 当遇到有连续两行以上的空白行，就代换为一行的空白行
- +/pattern 在每个文档显示前搜寻该字串（pattern），然后从该字串之后开始显示
- +num 从第 num 行开始显示

```shell
显示文件file1
# more file1

逐页显示 testfile 文档内容，如有连续两行以上空白行则以一行空白行显示。
# more -s testfile

从第 20 行开始显示 testfile 之文档内容
# more +20 testfile
```

> **常用操作命令**

- Enter 向下n行，需要定义。默认为1行
- Ctrl+F 向下滚动一屏
- 空格键 向下滚动一屏
- Ctrl+B 返回上一屏
- = 输出当前行的行号
- ：f 输出文件名和当前行的行号
- V 调用vi编辑器
- !命令 调用Shell，并执行命令
- q 退出more



<span id='less'>**less**</span>

> **参数**：

- --b <缓冲区大小> 设置缓冲区的大小
- -e 当文件显示结束后，自动离开
- -f 强迫打开特殊文件，例如外围设备代号、目录和二进制文件
- -g 只标志最后搜索的关键词
- -i 忽略搜索时的大小写
- -m 显示类似more命令的百分比
- -N 显示每行的行号
- -o <文件名> 将less 输出的内容在指定文件中保存起来
- -Q 不使用警告音
- -s 显示连续空行为一行
- -S 行过长时间将超出部分舍弃
- -x <数字> 将"tab"键显示为规定的数字空格

```shell
查看文件
# less file1

ps查看进程信息并通过less分页显示
# ps -ef |less
```

>  **附加备注**

1.全屏导航

- ctrl + F - 向前移动一屏
- ctrl + B - 向后移动一屏
- ctrl + D - 向前移动半屏
- ctrl + U - 向后移动半屏

2.单行导航

- j - 向前移动一行
- k - 向后移动一行

3.其它导航

- G - 移动到最后一行
- g - 移动到第一行
- q / ZZ - 退出 less 命令

4.其它有用的命令

- v - 使用配置的编辑器编辑当前文件
- h - 显示 less 的帮助文档
- &pattern - 仅显示匹配模式的行，而不是整个文件

5.标记导航

当使用 less 查看大文件时，可以在任何一个位置作标记，可以通过命令导航到标有特定标记的文本位置：

- ma - 使用 a 标记文本的当前位置
- 'a - 导航到标记 a 处



<span id='ln'>**ln**</span>

> **必要参数**：

- -b 删除，覆盖以前建立的链接
- -d 允许超级用户制作目录的硬链接
- -f 强制执行
- -i 交互模式，文件存在则提示用户是否覆盖
- -n 把符号链接视为一般目录
- -s 软链接(符号链接)
- -v 显示详细的处理过程

```shell
创建一个名叫linkToRoot的软连接 链接到/root目录
# ln -s /root linkToRoot 
```



<span id='chown'>**chown**</span>

> **语法**：

```
chown [-cfhvR] [--help] [--version] user[:group] file
```

> **必要参数**：

- user : 新的文件拥有者的使用者 ID
- group : 新的文件拥有者的使用者组(group)
- file：文件名
- -c : 显示更改的部分的信息
- -f : 忽略错误信息
- -h :修复符号链接
- -v : 显示详细的处理信息
- -R : 处理指定目录以及其子目录下的所有文件
- --help : 显示辅助说明
- --version : 显示版本

```shell
使用root创建一个文件apple.txt，然后将其所有者修改成Tom
# chown tom apple.txt

将/home/kkk目录下所有目录文件的所有者修改成tom
# chown -R tom kkk/

将/home/kkk目录下所有目录文件的所有者修改成tom,所在组改成bandit
# chown -R tom:bandit kkk/
```



<span id='chgrp'>**chgrp**</span>

> **语法**：

```
chgrp [-cfhRv][--help][--version] group file

chgrp [-cfhRv][--help][--reference=<参考文件或目录>][--version] file
```

> **必要参数**：

- -c    效果类似"-v"参数，但仅回报更改的部分。
- -f    不显示错误信息。
- -h    只对符号连接的文件作修改，而不更动其他任何相关文件。
- -R 　递归处理，将指定目录下的所有文件及子目录一并处理。
- -v 　显示指令执行过程。
- --help 　在线帮助。
- --reference=<参考文件或目录> 　把指定文件或目录的所属群组全部设成和参考文件或目录的所属群组相同。
- --version 　显示版本信息

```shell
使用root创建一个文件orange.txt，然后将其所在组改为police
# chgrp police orange.txt

将/home/kkk目录下所有目录文件的所有者修改成tom
# chgrp -R bandit kkk/
```



<span id='chmod'>**chmod**</span>

> **语法**：

```
chmod [-cfvR] [--help] [--version] mode file
```

> **mode**：

```
[ugoa...][[+-=][rwxX]...][,...]
```

- **ugoa**
  - u 表示该文件的拥有者
  - g 表示属于同一个群体(group)者
  - o 表示其他以外的人
  - a 表示这三者皆是。
- **+-=**
  - \+ 表示增加权限
  - \- 表示取消权限
  - = 表示唯一设定权限。
- **rwxX**
  - r 表示可读取
  - w 表示可写入
  - x 表示可执行
  - X 表示只有当该文件是个子目录或者该文件已经被设定过为可执行。

> **其他参数** :

- -c : 若该文件权限确实已经更改，才显示其更改动作
- -f : 若该文件权限无法被更改也不要显示错误讯息
- -v : 显示权限变更的详细资料
- -R : 对目前目录下的所有文件与子目录进行相同的权限变更(即以递回的方式逐个变更)
- --help : 显示辅助说明
- --version : 显示版本

```shell
给abc文件的所有者读写执行的权限，给所在组读执行权限，给其他组读执行权限
# chmod u=rwx,g=rx,o=rx abc
# chmod 755 abc

给abc文件的所有者除去执行的权限，增加组写的权限
# chmod u-x,g+w abc

给abc文件的所有用户添加读的权限
# chmod a+r abc
```



### 时间日期

| 指令格式          | 作用                       |
| ----------------- | -------------------------- |
| **[date](#date)** | 显示或设定系统的日期与时间 |
| **[cal](#cal)**   | 显示日历                   |



<span id='date'>**date**</span>

> **日期**：

- %a : 星期几 (Sun~Sat)
- %A : 星期几 (Sunday ~Saturday)
- %b : 月份 (Jan~Dec)
- %B : 月份 (January..December)
- %c : 直接显示日期与时间
- %d : 日 (01~31)
- %D : 直接显示日期 (mm/dd/yy)
- %h : 同 %b
- %j : 一年中的第几天 (001..366)
- %m : 月份 (01..12)
- %U : 一年中的第几周 (00..53) (以 Sunday 为一周的第一天的情形)
- %w : 一周中的第几天 (0..6)
- %W : 一年中的第几周 (00..53) (以 Monday 为一周的第一天的情形)
- %x : 直接显示日期 (mm/dd/yy)
- %y : 年份的最后两位数字 (00~99)
- %Y : 完整年份 (0000~9999)

> **参数**：

- -d datestr : 显示 datestr 中所设定的时间 (非系统时间)
- --help : 显示辅助讯息
- -s datestr : 将系统时间设为 datestr 中所设定的时间
- -u : 显示目前的格林威治时间
- --version : 显示版本编号

```shell
2019年 01月 27日 星期日 17:45:13 CST
# date

2019年01月27日 星期日 17时46分41秒
# date "+%c" 

01/27/19
# date "+%D"

17:50:41
# date "+%T"

按自己的格式输出 
2019-01-27 17:56:20
# date "+%Y-%m-%d %H:%M:%S"

设置时间
2019年 10月 10日 星期日 11:22:22 CST
#date -s "2019-10-10 11:22:22"
```



<span id='cal'>**cal**</span>

```shell
显示当前月的日历
# cal

显示2020年的日历
# cal 2020
```



### 搜索查找

| 指令格式              | 作用                           |
| --------------------- | ------------------------------ |
| **[find](#find)**     | 在指定目录下查找文件           |
| **[locate](#locate)** | 查找符合条件的文档，快速定位   |
| **[grep](#grep)**     | 用于查找文件里符合条件的字符串 |



<span id='find'>**find**</span>

> **语法**

```shell
find path -option [-print] [-exec -ok command ] {} \;
```

> **option**：

- -**name** 按照指定的文件名查找模式查找文件
- **-user** 查找属于指定用户名所有文件
- **-size** 按照指定的文件大小查找文件

```shell
根据名称查找/home目录下的hello.txt文件
# find /home -name "hello.txt"
将目前目录及其子目录下所有延伸档名是txt的文件列出来
# find . -name "*.txt"

查找/home目录下，属于用户名为zsx的文件
# find /home -user zsx

查找整个linux系统下大雨20m的文件（+n大于 -n小于 n等于）
# find / -size +20M
```



<span id='locate'>**locate**</span>

> **参数**：

- -d或--database= 配置locate指令使用的数据库。locate指令预设的数据库位于/var/lib/slocate目录里，文档名为slocate.db，您可使用 这个参数另行指定。
- --help 　在线帮助。
- --version 　显示版本信息。

```shell
创建locate数据库
# updatedb

查询文件或目录
# locate file1/dir1

手工升级数据库 
# locate -u 
```



<span id='grep'>**grep**</span>

> **参数**：

- -n  : 在显示符合样式的那一行之前，标示出该行的列数编号。
- -i :忽略字母大小写

```shell
在file1中，查找“yes”所在行，显示行号
# cat file1 | grep -n yes

在file1中，查找“yes”所在行，忽略字母大小写
# cat file1 | grep -i yes

统计/home文件夹下文件的个数
# ls -l /home | grep "^-" | wc -l

统计/home文件夹下目录的个数
# ls -l /home | grep "^d" | wc -l

统计/home文件夹下文件的个数，包括子文件夹里的
# ls -lR /home | grep "^-" | wc -l
```



### 备份压缩

| 指令                | 说明                                            |
| ------------------- | ----------------------------------------------- |
| **[gzip](#gzip)**   | 压缩文件，压缩成"*.gz"文件,压缩后不会保留原文件 |
| **[gunzip](#gzip)** | 解压文件，解压"*.gz"文件                        |
| **[zip](#zip)**     | 压缩文件，压缩成"*.gz"文件,压缩后不会保留原文件 |
| **[unzip](#zip)**   | 解压文件，解压"*.gz"文件                        |
| **[tar](#tar)**     | 打包指令，既可以压缩也可以解压                  |



<span id='gzip'>**gzip** /**gunzip**</span>

> **参数**：

- -v　显示指令执行过程。
- -l　列出压缩文件的相关信息。
- -r   递归处理，将指定目录下的所有文件及子目录一并处理。

```shell
压缩目录下的所有文件
# gzip *

显示压缩文件的信息
# gzip -l a.gz

解压gz文件
# gunzip a.gz
```



<span id='zip'>**zip** /**unzip**</span>

> **参数**：

- -r  递归处理，将指定目录下的所有文件和子目录一并处理 
- -d<目录> 指定文件解压缩后所要存储的目录。

```shell
将/home下所有文件进行压缩成mypackage.zip
# zip -r mypackage.zip /home/

将mypackage解压到/opt/tmp目录下
# unzip -d /opt/tmp/ mypackage.zip
```



<span id='tar'>**tar**</span>

> **参数**：

- -c  产生.tar打包文件
- -v 显示详细信息
- -f 制定压缩后的文件名
- -z 打包同时压缩
- -x 解包.tar文件

```shell
压缩多个文件 将/zsx/file1.txt和/zsx/file2.txt压缩成a.tar.gz
源文件保留
# tar -zcvf a.tar.gz file1.txt file2.txt

将/zsx下所有文件 压缩成myzsx.tar.gz
# tar -zcvf myzsx.tar.gz /home/zsx/

将a.tar.gz解压到当前目录
# tar -zxvf a.tar.gz

将a.tar.gz解压到 /home/zsx/a
# tar -zxvf a.tar.gz -C /home/zsx/a
```



### 分区磁盘

| 指令                  | 说明                                      |
| --------------------- | ----------------------------------------- |
| [**crontab**](#crond) | 任务调度相关                              |
| **lsblk -f**          | 查看系统的分区和挂载情况                  |
| **mount / umount**    | 挂载与断开                                |
| **df -h**             | 查询系统整体磁盘使用情况                  |
| [**du -h**](#du)      | 查询指定目录的磁盘占用情况 默认为当前目录 |

<span id="df"> **df**</span>

> **参数**：

- -h 带计量单位
- -a 含文件

```shell
通常
# df -h
```



<span id="du"> **du**</span>

> **参数**：

- -s 指定目录占用大小汇总
- -h 带计量单位
- -a 含文件
- --max-depth=1  子目录深度
- -c  列出明细的同时，增加汇总值

```shell
通常
# du -h

查询/opt目录的磁盘占用情况，深度为1
# du -ach --max-depth=1 /opt
```



### 进程服务

| 指令                    | 说明                                             |
| ----------------------- | ------------------------------------------------ |
| [**ps**](#ps)           | 查看目前系统中，有哪些正在执行，以及他们执行状况 |
| [**pstree**](#pstree)   | 可以更加直观的看进程信息                         |
| **[top](#top)**         | 动态查看进程                                     |
| **[netstat](#netstat)** | 查看系统网络情况                                 |
| [**kill**](#kill)       | 通过进程号终止进程                               |
| **killall**             | 通过进程名称杀死进程，支持通配符                 |
| **[service](#service)** | 服务管理                                         |



<span id="ps"> **ps**</span>

> **参数**：

- -a: 显示当前终端的所有进程信息
- -u: 以用户的格式显示进程信息
- -x: 显示后台进程运行的参数
- -e : 显示所有进程
- -f : 全格式
- PID: pid，进程识别号
- TTY: 终端的机号
- TIME: 此进程所消耗CPU时间
- CMD: 正在执行的命令或进程名

```shell
通常
# ps -aux

查看有没有ssd服务
# ps -aux | grep sshd

查看指令的父进程
# ps -ef | more
```

> 显示

![201](D:\PHP\note\quick\201.jpg)

> 指令说明：

- **System V  展示风格**
- USER：用户名称
- PID：进程号
- PPID：父进程 （0为没有父进程）
- %CPU：进程占用CPU的百分比
- %MEN：进程占用物理内存的百分比
- VSZ：进程占用的虚拟内存大小 (KB)
- RSS：进程占用的物理内存大小 (KB)
- TTY：终端名称，缩写
- STAT：进程状态，S-睡眠，s-表示该进程是会话的先导进程，N-表示进程拥有比普通优先级更低的优先级，R-正在运行，D-短期等待，Z-僵死进程，T-被跟踪或者被停止等等
- START：进程的启动时间
- TIME：CPU时间，即进程使用CPU的总时间
- COMMAND：启动进程所用的命令和参数，如果过长会被截断显示



<span id="pstree"> **pstree**</span>

> **参数**：

- -p：显示进程的PID
- -u：显示进程所属用户

```bash
以树状的形式显示进程的pid
# pstree -p

以树状的形式显示进程的用户id
# pstree -u
```



<span id="top">**top**</span>

与ps很相似。他们都是用来显示正在执行的进程。top在执行一段时间可以更新正在运行的进程

> 基本语法

top [选项]

> 选项

- -d 秒数  指定top命令每隔几秒更新，默认是3秒在top命令的交互模式当中可以执行的命令
- -l  使top不显示任何限制或者死循环
- -p  通过制定监控进程ID来仅仅监控某个进程的状态

> 交互操作说明

- P  以CPU使用率排序，默认就是此选项
- M  以内存的使用率排序
- N  以PID排序
- q   退出top
- u   监视特定用户
- k   终止指定的进程

> 【例1】监视特定用户

1. 输入top

![208](D:\PHP\note\quick\208.jpg)

1. 输入u指定特定用户 ，输入用户名root

![210](D:\PHP\note\quick\210.jpg)

> 【例2】终止指定的进程

1. 输入top
2. 输入k，指定需要杀死的进程

![209](D:\PHP\note\quick\209.jpg)

> 【例3】指定系统状态更新时间（每隔10秒自动更新）

1. 输入top -d 10

![209](D:\PHP\note\quick\209.jpg)



<span id="netstat">**netstat**</span> 

> 语法

netstat [选项]

> 选项

- -an  按一定瞬息排列输出
- -p 显示哪个进程在调用

> 【例1】监视特定用户



<span id="service"> **service**</span>

> 语法

```shell
# service 服务名 [start|stop|restart|reload|status]

在centOS7以后不再使用service 而是改为systemctl
```

> 【例】查看当前防火墙的状况，关闭防火墙和重启防火墙

1. 查看防火墙状态：service iptables status

   centOS7:  systemctl status firewalld （active为开启，dead为关闭）

2. 关闭防火墙：service iptables stop

   centOS7:  systemctl stop firewalld

3. 开启防火墙：service iptables start

   centOS7:  systemctl start firewalld

> 注意：以上关闭或启用防火墙为临时生效，系统重启后还是回归以前的设置
>
> 若要自启动或关闭永久生效，要使用[chkconfig](#chkconfig)指令，或进入[服务管理](#fuwuguanli)关闭





<span id="kill"> **kill / killall**</span>

> **参数**：

- -l <信息编号> 　若不加<信息编号>选项，则-l参数会列出全部的信息名称。
- -s <信息名称或编号> 　指定要送出的信息。
- -9  强制杀死进程

> 【例1】踢掉某个非法用户

查看进程：ps -aux |grep sshd

![202](D:\PHP\note\quick\202.jpg)

踢除进程：kill 3692

> 【例2】终止远程登录服务sshd，在适当时候再次重启sshd服务

查看sshd服务的进程号：为上图2385

终止进程：kill 2385

> 【例3】终止多个gedit编辑器 

终止进程：killall gedit

> 【例4】强制终止一个终端

查看终端：ps -aux | grep bash

![203](D:\PHP\note\quick\203.jpg)

终止终端：kill -9 3842



### 网络通讯

| 指令                    | 说明                                        |
| ----------------------- | ------------------------------------------- |
| **[telnet](#telnet)**   | 检查linux的某个端口是否在监听，并且可以访问 |
| **[netstat](#netstat)** | 得知整个Linux系统的网络情况                 |
| service network restart | 重启网络                                    |

<span id="telnet">**telnet**</span>

> 语法

**telnet ip 端口**

```shell
检查22端口是否在监听
# telnet ip 22
```



<span id="netstat">**netstat**</span>

> 语法

**netstat [选项]**

> 选项说明

- -an	按一定顺序排列输出
- -p     显示哪个进程在调用

```shell
查看系统所有的网络服务
# netstat -anp

查看服务名为sshd的服务的信息
# netstat -anp | grep sshd
```



## Shell

### crond任务调度

> 1. 如果只是简单的任务，可以不用写脚本，直接在crontab中加入即可
> 2. 对于比较复杂的任务，需要些脚本完成(shell)编程

- 设置任务调度文件：/etc/crontab
- 设置个人任务调度。执行crontab -e命令
- 接着输入任务到调度文件

如： */1 * * * * ls -l /etc/ >> /tmp/to.txt 

意思是说每小时的每分钟执行 ls -l /etc/ >> /tmp/to.txt

> 占位符说明：

| 项目    | 含义                 | 范围                  |
| ------- | -------------------- | --------------------- |
| 第一个* | 一小时当中的第几分钟 | 0-59                  |
| 第二个* | 一天当中的第几小时   | 0-23                  |
| 第三个* | 一个月当中的第几天   | 1-31                  |
| 第四个* | 一年当中的第几个月   | 1-12                  |
| 第五个* | 一周当中的星期几     | 0-7（0和7都表示周日） |

> 特殊符号说明：

| 特殊符号 | 含义                                                         |
| -------- | ------------------------------------------------------------ |
| *****    | 代表任何时间。比如第一个*就代表一小时中每分钟都执行一次的意思 |
| **，**   | 代表不连续的时间。比如"0 8,12,16 * * * 命令"，就代表在每天的8:00，12:00，16:00都执行命令 |
| **-**    | 代表连续的时间范围。比如"0 5 * * 1-6 命令"，代表在周一到周六的凌晨5:00执行任务 |
| ***/n**  | 代表每个多久执行一次。比如"*/10 * * * * 命令"，代表每个10分钟就执行一次命令 |

> 特定时间执行案例：

| 时间              | 含义                                    |
| ----------------- | --------------------------------------- |
| 45 22 * * * 命令  | 在22点45分执行命令                      |
| 0 17 * * 1 命令   | 在每周一的17:00执行命令                 |
| 0 5 1,15 * * 命令 | 每月的1号和15号的凌晨5点执行命令        |
| 40 4 * * 1-5 命令 | 每周一到周五的凌晨4:40执行命令          |
| */10 4 * * * 命令 | 每天凌晨4点，每个10分钟执行一次命令     |
| 0 0 1,15 * 1 命令 | 每月1号和15号，每周一的0:00都会执行命令 |

><span id="crond">crond相关指令：</span>

- crontab -r  终止任务调度
- crontab -l  列出当前有哪些任务调度
- service crond restart 重启任务调度



## Linux分区

### 硬盘说明

- Linux硬盘分为**IDE硬盘**和**SCSI硬盘**，目前基本是SCSI硬盘

- 对于**IDE硬盘**，驱动器标识符为 “**hdx~**”：

  1. 其中"**hd**"表明所在设备为**IDE硬盘**
  2. "**x**"表示盘号（a为基本盘，b为基本从属盘，c为辅助主盘，d为辅助从属盘）
  3. "**~**" 代表分区，前四个分区用数字1到4表示，他们是主分区或者扩展分区，从5开始就是逻辑分区。

  例，**hda3**表示为第一个IDE硬盘上的第三个主分区或扩展分区

- **对于SCSI硬盘**，则标识为"**sdx~**"，“**sd**”用来表示分区所在设备的类型，其余与IDE硬盘表示方法一样
- **lsblk -f** 命令，用来查看系统的分区和挂载情况

![187](D:\PHP\note\quick\187.jpg)



### 增加硬盘

【案例】添加一块硬盘2G

#### 1）虚拟机添加硬盘

![188](D:\PHP\note\quick\188.jpg)

![189](D:\PHP\note\quick\189.jpg)

#### 2）分区

1. 设置分区

![190](D:\PHP\note\quick\190.jpg)

2. 输入m -> 输入n添加一个新的分区

![191](D:\PHP\note\quick\191.jpg)

3. 输入p确定划一个主分区->输入1表示主分区的第一块分区->默认回车->输入w 把信息写入硬盘并退出

![192](D:\PHP\note\quick\192.jpg)

#### 3）格式化

> 指令：mkfs -t ext4 /dev/sdb1

ext4是分区类型

![193](D:\PHP\note\quick\193.jpg)

#### 4）挂载

1. 创建一个/home/newdisk

   > mkdir  /home/newdisk

2. 挂载

   > mount  /dev/sdb1  /home/newdist

3. 查看挂载是否成功

   > lsblk -f

#### 5）设置自动挂载

1. 编辑文件 vim /etc/fstab 保存退出

![194](D:\PHP\note\quick\194.jpg)

2. 使其生效，自动挂载

> mount -a

3. 重启

> reboot

#### 6）断开挂载

> umount  /dev/sdb1  或者   umount  /newdisk

注：需要离开该目录才能卸载



## 网络配置



### 虚拟机网络连接

#### 桥接模式

![28](D:\PHP\note\quick\28.png)

- 桥接模式，Linux可以和其他的系统通信。但是可能造成ip冲突

#### NAT模式

![29](D:\PHP\note\quick\29.png)

- 网络地址转换方式：linux可以访问外网，不会造成ip冲突



### 查看网络IP和网关

#### 修改虚拟网卡的ip地址

![196](D:\PHP\note\quick\196.jpg)

当前为192.168.159.xxxx

#### 查看网关

在linux中查看

![198](D:\PHP\note\quick\198.jpg)

在windows中查看vmnet8 网络配置

![199](D:\PHP\note\quick\199.jpg)

### 网络环境配置

#### 自动获取

![195](D:\PHP\note\quick\195.jpg)

下次登录时自动连接网络

缺点：linux启动后会自动获取IP缺点是每次自动获取的IP地址可能不一样。不适用与做服务器，服务器的IP需要是固定的



#### 指定固定的IP

直接修改配置文件来制定IP，并可以连接到外网

【案例】将ip地址配置为静态，ip地址为192.168.159.131[NAT模式]

- 编辑网卡的配置文件 （以下为eth0网卡）

> vim /etc/sysconfig/network-scripts/ifcfg-eth0

![200](D:\PHP\note\quick\200.jpg)

【桥接模式】

![30](D:\PHP\note\quick\30.png)

- 重启网络服务

> service network restart



## <span id="fuwuguanli">服务管理</span>

### 查看服务名

>  方式1：使用setup->系统服务就可以看到

终端输入：setup

![204](D:\PHP\note\quick\204.jpg)

选择系统服务，可看到服务

![205](D:\PHP\note\quick\205.jpg)

> 方式2：ll /etc/init.d/服务名称

![206](D:\PHP\note\quick\206.jpg)



### 服务的运行级别

> 查看或者修改默认级别：**vim /etc/inittab**

![207](D:\PHP\note\quick\207.jpg)

Linux系统有7种运行级别：常用的是3和5

- 0：系统停机状态
- 1：单用户工作状态
- 2：多用户状态，不支持网络
- 3：多用户状态，登陆后进入控制台命令模式
- 4：系统未使用，保留
- 5：X11控制台，登陆后进入图形GUI模式
- 6：系统正常关闭并重启



### 设置自启动

通过<span id="chkconfig">**chkconfig**</span>可以给每个服务的各个运行级别设置自启动/关闭

> 基本语法

```shell
查看所有服务
# chkconfig  --list [| grep xxx]

某个服务的运行状态
# chkconfig 服务名 --list

给某个服务的哪个运行级别制定是否自启动
# chkconfig --level 5 服务名 on/off
```

> 注：chkconfig重新设置服务后自启动或关闭，需要重启机器才能生效



## RPM和YUM

### RPM包管理

#### 查询

```shell
查询已安装的rpm列表
# rpm -qa | grep xx

查询有没有安装火狐
# rpm -qa | grep firefox

查询软件包信息
# rpm -qi firefox

查询软件包中的文件
# rpm -ql firefox

查询文件所属的软件包
# rpm -qf /etc/passwd
```



#### 卸载

```shell
删除firefox软件包
# rpm -e firefox
```

> 注意：如果其他软件包依赖于您要卸载的软件包，卸载则会产生错误信息

如： **rpm -e foo**

removing these packages would break dependencies:foo is needed by bar-1.0-1

若要删除此包 可以增加参数 --nodeps，就可以强制删除

如：**rpm -e --nodeps foo**



#### 安装

> 参数：

- i   安装
- v   提示
- h   进度条

> 【例】安装Firefox浏览器

1. 找到Firefox的安装rpm包，需要挂载上centos的iso文件，然后到/media/下去找到该rpm

   ![211](D:\PHP\note\quick\211.jpg)

   ![212](D:\PHP\note\quick\212.jpg)

2. 复制该rpm包 拷贝到opt目录下

   ```shell
   # cp firefox-45.0.1-1.el6.centos.x86_64.rpm  /opt/
   ```

3. 切换到/opt/目录，并安装

   ```shell
   # cd /opt/
   # rpm -ivh firefox-45.0.1-1.el6.centos.x86_64.rpm
   ```



### YUM包管理

yum是一个shell前端软件包管理器。基于rpm包管理，能够从指定的服务器自动下载rpm包并且安装，可以自动处理依赖性关系，并且一次安装所有依赖的软件包

> 基本指令

- 查询yum服务器是否有需要安装的软件

  yum list | grep xx软件列表

- 安装指定的yum包

  yum install xxx 下载安装

> 【例】安装Firefox浏览器

1. 查看Firefox rpm在yum服务器上是否存在

   ```shell
   # yum list | grep firefox
   ```

2. 安装

   ```shell
   # yum install firefox
   ```



#### 更换yum源

国内比较有名有速度的yum源有：

- 网易开源镜像站：http://mirrors.163.com
- 阿里云开源镜像站：http://mirrors.aliyun.com
- 中科大的Linux安装镜像源：http://centos.ustc.edu.cn
- 搜狐的Linux安装镜像源：http://mirrors.sohu.com
- 北京首都在线科技：http://mirrors.yun-idc.com

使用前可以 ping 一下以上更新源，看哪个快就用哪个

>  【例】以163的为例更换yum源

1. 查看163的使用帮助文档：http://mirrors.163.com/.help/centos.html

![213](D:\PHP\note\quick\213.jpg)

2. 备份/etc/yum.repos.d/CentOS-Base.repo

   ```shell
   # cd /etc/yum.repos.d/
   # mv CentOS-Base.repo CentOS-Base.repo.backup
   ```

3. 根据系统版本下载对应的repo文件

   ```shell
   centos 6 ：
   # wget http://mirrors.163.com/.help/CentOS6-Base-163.repo
   centos 7 ：
   # wget http://mirrors.163.com/.help/CentOS7-Base-163.repo
   ```

4. 将下载回来的repo文件改名

   ```shell
   centos 6 ：
   # mv CentOS6-Base-163.repo CentOS-Base.repo
   centos 7 ：
   ># mv CentOS7-Base-163.repo CentOS-Base.repo
   ```

5. 生成缓存

   ```shell
   # yum clean all
   # yum makecache
   ```

6. 重启系统

   ```shell
   # reboot
   ```

7. 更新现有的软件

   ```shell
   # yum -y update
   ```



## WEB环境搭建

### 底层软件库

运行以下命令确保底层软件库都已安装

```
shell># yum -y install gcc gcc-c++ autoconf automake zlib libxml2 libxml2-devel ncurses-devel libmcrypt libtool cmake bison make pcre pcre-devel libevent openssl openssl-devel gd-devel bzip2 bzip2-devel libcurl curl-devel python python-devel mysql-devel expat-devel
```

### 安装MySQL

​	MySQL从5.5版本开始，通过`./configure`进行编译配置方式已经被取消，取而代之的是`cmake`工具。需要下载`CMake`编译器、`Boost`库、`ncurses`库和`GNU`分析器生成器`bison`这4种工具，可以用`yum install`的方式安装 `cmake`、`bison`、`boost`、`ncurses`

MySQL二进制文件可以 http://dev.mysql.com/downloads/mysql 或者 http://mirrors.sohu.com/mysql 去下载

注意要下载与操作系统对应的版本及位数（32位或64位），编译安装需要下载源码版(Source Code)，此处以mysql-5.7.24tar.gz为例

**以下 安 装中 涉 及的 几点 需 要提 前 说明 的问 题 ：**

- 所有 下 载的 文件 将 保存 在 /root 目 录下
- mysql 将以 mysql 用户 运 行， 而 且将 加入 service 开 机 自动 运 行
- mysql 将被 安 装在 /usr/local/mysql/ 目录 下
- mysql 默认 安 装使 用 utf8 字符集
- mysql 的数 据 和日 志文 件 保存 在 /usr/local/mysql/data/ 目录 下
- mysql 的配 置 文件 保存 于 /usr/local/mysql/etc/my.cnf

> 注意 从 MySQL 5.7.5 开 始 Boost 库是 必需 的



#### 安装依赖库

1. 安装 cmake 和 bison 与 ncurses

   ```shell
   # yum -y install -y cmake bison ncurses
   ```

2. 下载 Boost

   ```shell
   # wget http://sourceforge.net/projects/boost/files/boost/1.59.0/boost_1_59_0.tar.gz
   ```

3. 解压

   ```shell
   # tar -zxvf boost_1_59_0.tar.gz
   ```

4. 移动

   ```shell
   # mv boost_1_59_0 /usr/local/boost
   ```



#### 安装MySQL

1. **建立mysql安装目录和用户**

   在/usr/local/mysql建立【data】、【tmp】、【log】、【etc】4个目录

   ```shell
   建立/usr/local/mysql
   # mkdir -pv /usr/local/mysql
   进入该目录
   # cd /usr/local/mysql
   创建四个目录
   # mkdir data tmp log etc
   添加mysql用户组
   # groupadd mysql
   把用户设为不可登录
   # useradd -g mysql -s /usr/sbin/nologin mysql
   ```

2. **下载mysql** (D盘下有)

   ```shell
   # cd ~
   # wget http://mirrors.sohu.com/mysql/MySQL-5.7/mysql-5.7.24.tar.gz
   ```

3. **解压并进入目录**

   ```shell
   # tar -zxvf mysql-5.7.24.tar.gz
   # cd mysql-5.7.24
   ```

4. **进行软件配置和环境检测**

   复制粘贴以下内容进行配置

   - cmake     #设置安装目录
   - -DCMAKE_INSTALL_PREFIX=/usr/local/mysql        #设置sock目录
   - -DMYSQL_UNIX_ADDR=/usr/local/mysql/tmp/mysql.sock    #设置数据库存放目录
   - -DMYSQL_DATADIR=/usr/local/mysql/data    #设置配置文件my.cnf存放目录
   - -DSYSCONFDIR=/usr/local/mysql/etc     #设置mysql的默认使用用户
   - -DMYSQL_USER=mysql    #设置默认字符集
   - -DDEFAULT_CHARSET=utf8    #默认校对规则
   - -DDEFAULT_COLLATION=utf8_general_ci    #指明安装额外字符集的支持
   - -DWITH_EXTRA_CHARSETS:STRING=utf8,gbk    #去除debug模式
   - -DWITH_DEBUG=0     #以下几条开启常用的引擎
   - -DDOWNLOAD_BOOST=1      #如果没有指定boost底层库，从互联网下载

   ```
   [root@localhost mysql-5.7.24]# cmake \
   -DCMAKE_INSTALL_PREFIX=/usr/local/mysql \
   -DMYSQL_UNIX_ADDR=/usr/local/mysql/tmp/mysql.sock \
   -DMYSQL_DATADIR=/usr/local/mysql/data \
   -DSYSCONFDIR=/usr/local/mysql/etc \
   -DMYSQL_USER=mysql \
   -DDEFAULT_CHARSET=utf8 \
   -DDEFAULT_COLLATION=utf8_general_ci \
   -DWITH_EXTRA_CHARSETS:STRING=utf8,gbk \
   -DWITH_DEBUG=0 \
   -DWITH_MYISAM_STORAGE_ENGINE=1 \
   -DWITH_INNOBASE_STORAGE_ENGINE=1 \
   -DWITH_ARCHIVE_STORAGE_ENGINE=1 \
   -DWITH_PARTITION_STORAGE_ENGINE=1 \
   -DENABLED_LOCAL_INFILE=1 \
   -DWITH_EMBEDDED_SERVER=1 \
   -DMYSQL_USER=mysql \
   -DWITH_BOOST=/usr/local/boost \
   -DDOWNLOAD_BOOST=1
   ```

5. **编译软件并且进行安装**

   ```shell
   # make 
   # make install
   ```

   > **另外**：如果过程中出现报错而中断，需要删除CMakeCache.txt文件后再执行 4.步骤内容（没出错请不要执行以下两行指令）：
   >
   > \# make clean
   >
   > \# rm -rf CMakeCache.txt 或者  unlink CMakeCache.txt

#### 配置

1. **使用递归，把mysql目录所有者设置为mysql这个用户**

   ```shell
   # chown -R mysql:mysql /usr/local/mysql
   ```

    如果 /etc/my.cnf 存在的话，请删除

   ```shell
   # unlink /etc/my.cnf
   ```

2. **进入MySQL安装目录下**

   ```shell 
   # cd /usr/local/mysql
   ```

3. **根据实际情况优化mysql配置**

   ```shell
   # vim etc/my.cnf
   ```

   大概内容如下：

   ```
   [client]
   default-character-set = utf8
   port = 3306
   socket = /usr/local/mysql/tmp/mysql.sock
   
   [mysqld]
   datadir =/usr/local/mysql/data
   port = 3306
   socket = /usr/local/mysql/tmp/mysql.sock
   user = mysql
   symbolic-links = 0
   pid-file = /usr/local/mysql/tmp/mysql.pid
   
   explicit_defaults_for_timestamp = true
   sql_mode = ERROR_FOR_DIVISION_BY_ZERO,NO_ZERO_DATE,NO_ZERO_IN_DATE,NO_AUTO_CREATE_USER
   
   slow_query_log = on
   slow_query_log_file = /usr/local/mysql/log/slow.log
   long_query_time = 2
   
   log_error = /usr/local/mysql/log/mysql.err
   ```

4. **初始化和启动**

   1) **初始化mysql的基本表**

   > mysql5.7以前：

   ```shell
   shell># /usr/local/mysql/scripts/mysql_install_db  \
   --defaults-file=/usr/local/mysql/my.cnf \
   --basedir=/usr/local/mysql \
   --datadir=/usr/local/mysql/data \
   --user=mysql
   ```

   > mysql5.7及以上：

   --initialize会生成一个随机密码(~/.mysql_secret)，而--initialize-insecure不会生成密码

   ```shell
   shell># /usr/local/mysql/bin/mysqld \
   --initialize-insecure \
   --basedir=/usr/local/mysql \
   --datadir=/usr/local/mysql/data \
   --user=mysql
   ```

   > 注意：
   >
   > ​	如果初始化出错，则需要用 rm -rf /usr/local/mysql/data/* 将 mysql 的 data 目录下的文件和目录都删除，然后再重新运行以上语句

5. **启动mysql**

   ```shell
   # /usr/local/mysql/bin/mysqld_safe > /dev/null 2>&1 &
   ```

   查看是否启动

   ```shell
   # ps -ef|grep mysqld
   ```

   ![214](D:\PHP\note\quick\214.jpg)

   看到两条以上则启动成功

6. **修改mysql的root密码**

   ```shell
   # /usr/local/mysql/bin/mysqladmin -u root password 123abc
   ```

7. **增加到开机启动**

   先将mysqld设置为服务

   ```shell
   # cp /usr/local/mysql/support-files/mysql.server /etc/rc.d/init.d/mysqld
   ```

   将mysqld服务加入启动项

   ```shell
   # chkconfig --add mysqld
   ```

   设置为自启动

   ```shell
   # chkconfig --level 345 mysqld on
   ```

   > level<等级代号> 　指定读系统服务要在哪一个执行等级中开启或关毕。

   - 等级0表示：表示关机
   - 等级1表示：单用户模式
   - 等级2表示：无网络连接的多用户命令行模式
   - 等级3表示：有网络连接的多用户命令行模式
   - 等级4表示：不可用
   - 等级5表示：带图形界面的多用户模式 
   - 等级6表示：重新启动

8. **将mysql命令加入到环境变量里**

   ```shell
   # PATH=$PATH:/usr/local/mysql/bin
   ```

   为了重启后仍能有效

   ```shell
   # echo 'PATH=$PATH:/usr/local/mysql/bin' >> /root/.bashrc
   ```

9. ###【如果需要对外开放 3306 端口】

   ```shell
   # iptables -I INPUT -p tcp --dport 3306 -j ACCEPT
   ```

10. **创建一个软链接**

    ```shell
    # mkdir -pv /var/lib/mysql
    # ln -s /usr/local/mysql/tmp/mysql.sock /var/lib/mysql/mysql.sock
    ```

#### 启动mysql

```shell
# mysql -uroot -p123abc
关闭
mysql> quit;
```



### 安装PHP

安装PHP之前，首先要检查安装libxml2、libxml2-devvel、gd-devel

```shell
# rpm -qa | grep libxml2*
# rpm -qa | grep gd-devel*
```

![215](D:\PHP\note\quick\215.jpg)

如果没有安装，可以使用yum -y install命令进行安装。

php可以到 http://php.net/downloads.php 或者 http://mirrors.sohu.com/php/ 去下 载,此处 以php-7.2.2.tar.gz为例 

**以下安装中涉及的几点需要提前说明的问题：**

- 所有下载的文件将保存在 /root 目录下
- php 将以 FastCGI模式运行，监听 9000 端口(默认端口)
- php 将被安装在 /usr/local/php 目录下
- php 的配置文件保存于 /usr/local/php/etc/php.ini
- php 的扩展库文件，如果可以的话，尽量放在 /usr/local/php/lib/php/extensions/ 目录

#### 安装

1. **下载php**

```shell
# cd ~
# wget http://am1.php.net/distributions/php-7.2.2.tar.gz
```

2. **解压并进入目录**

```shell
# tar -zxvf php-7.2.2.tar.gz
# cd php-7.2.2
```

3. **进行软件的配置和环境检测**

   以上内容的解释如下：

   - ./configure \
   	 --prefix=/usr/local/php \						# 指定php安装目录
   	 --with-config-file-path=/usr/local/php/etc \		# 设置php.ini配置文件存放的路径
   	 --enable-fpm \								# 开启PHP-FPM，用于控制PHP-CGI的FastCGI进程
   	 --enable-opcache \							# PHP新增opcache功能
   	 --with-zlib-dir \								# 加载zlib库
   	 --with-bz2 \									# 加载bz2的压缩库
   	 --with-libxml-dir=/usr \						# 加载xml库
   	 --with-gd \									# 加载gd库
   	 --with-freetype-dir \							# 加载字体库
   	 --with-jpeg-dir \								# 加载jpeg库
   	 --with-png-dir \								# 加载png库
   	 --enable-mbstring \							# 开启mbstring加密库
   	 --with-mysql=/usr/local/mysql \				# 加载mysql，并指定mysql基本路径
   - --with-mysqli=/usr/local/mysql/bin/mysql_config \ # 加载mysqli库，并指定mysql配置工具
   	 --with-pdo-mysql=/usr/local/mysql \			# 加载pdo对mysql的支持
   	 --with-iconv \									# 开启转换字符集
   	 --disable-ipv6 \								# 关闭ipv6支持
   	 --enable-static \								# 以静态方式编辑php库
   	 --enable-inline-optimization \					# 开启优化线程
   	 --enable-sockets \							# 开启sockets支持
   	 --enable-soap \								#开启soap对web service的支持
   	 --with-openssl \								# 开启ssl支持
   	 --with-curl									# 模拟浏览器

```
./configure \
--prefix=/usr/local/php \
--with-config-file-path=/usr/local/php/etc \
--enable-fpm \
--enable-opcache \
--with-zlib-dir \
--with-bz2 \
--with-libxml-dir=/usr \
--with-gd \
--with-freetype-dir \
--with-jpeg-dir \
--with-png-dir \
--enable-mbstring \
--with-mysql=/usr/local/mysql \
--with-mysqli=/usr/local/mysql/bin/mysql_config \
--with-pdo-mysql=/usr/local/mysql \
--with-iconv \
--disable-ipv6 \
--enable-static \
--enable-inline-optimization \
--enable-sockets \
--enable-soap \
--with-openssl \
--with-curl
```

4. **编译软件并且进行安装**

```shell
# make && make install
```

#### 配置

1. **复制配置文件**

   ```shell
   # cp php.ini-production /usr/local/php/etc/php.ini
   # cp sapi/fpm/init.d.php-fpm /etc/rc.d/init.d/php-fpm
   赋予其可执行权限
   # chmod +x /etc/rc.d/init.d/php-fpm
   拷贝产生 php-fpm 的配置文件
   # cd /usr/local/php/etc
   # cp php-fpm.conf.default php-fpm.conf
   ```

2. **配置php.ini**

   ```shell
   # vim php.ini
   ```

   - 找到 ;date.timezone = 修改为 date.timezone = Asia/Shanghai

   - 根据自己的需求调整以下选项的值

     error_reporting = E_ALL & ~E_NOTICE & ~E_STRICT & ~E_DEPRECATED

     ```
     display_errors = On
     
     max_execution_time = 60
     
     max_input_time = 60
     
     memory_limit = 256M
     
     post_max_size = 256M
     
     upload_max_filesize = 256M
     ```

3.  **配置 php-fpm.conf**

   ```shell
   # cd /usr/local/php/etc/php-fpm.d
   # cp www.conf.default www.conf
   
   # vim www.conf
   ```

   - 找到 user = nobody 和 group = nobody，将 nobody 改成 www
   - 找到 listen.owner=nobody 和 listen.group= nobody，将 nobody 改成 www

   > 注意：

   必须得先新增www用户，否则无法启动php

   ```shell
   # groupadd www
   # useradd -g www -s /usr/sbin/nologin www
   ```

4. 将php-fpm加入服务并自动启动

   ![216](D:\PHP\note\quick\216.jpg)

```shell
# service php-fpm start
测试启动是否成功 如图
# ps -ef | grep php-fpm

# chkconfig --add php-fpm
# chkconfig --level 345 php-fpm on
```

> level<等级代号> 　指定读系统服务要在哪一个执行等级中开启或关毕。

- 等级0表示：表示关机
- 等级1表示：单用户模式
- 等级2表示：无网络连接的多用户命令行模式
- 等级3表示：有网络连接的多用户命令行模式
- 等级4表示：不可用
- 等级5表示：带图形界面的多用户模式
- 等级6表示：重新启动



### 安装Apache

安装apache之前，首先要先确保已安装 APR 和 APR-util

shell># yum -y install apr*

apache 可以到 http://mirrors.sohu.com/apache/ 下载，此处理以 httpd-2.4.37.tar.gz 为例

**以下安装中涉及的几点需要提前说明的问题：**

- 所有下载的文件将保存在 /root 目录下
- apache 将以 www用户运行，而且将加入 service 开机自动运行
- apache 将被安装在 /usr/local/httpd 目录下
- apache 的每个网站将存放在 /mydata/wwwroot 目录下，默认网站为php32
- apache 的配置文件保存于 /usr/local/httpd/conf/httpd.cnf

#### 安装依赖库

1. 安装 apr 和 apr-util

   ```shell
   # cd ~
   # wget http://archive.apache.org/dist/apr/apr-1.4.8.tar.gz
   ```

2. 创建目录

   ```shell
   # mkdir /usr/local/apr
   ```

3. 解压安装apr依赖库

   ```shell
   # tar -zxf apr-1.4.8.tar.gz
   # cd apr-1.4.8
   # ./configure --prefix=/usr/local/apr
   # make && make install
   ```

4. 解压安装apr-util依赖库

   ```shell
   # tar -zxf apr-util-1.5.2.tar.gz
   # cd apr-util-1.5.2
   # ./configure --prefix=/usr/local/apr-util --with-apr=/usr/local/apr/bin/apr-1-config
   # make && make install
   ```

#### 安装apache

1. **下载apache**

   ```shell
   # cd ~
   # wget http://mirrors.sohu.com/apache/httpd-2.4.37.tar.gz
   ```

2. **解压并进入目录**

   ```shell
   # tar -zxvf httpd-2.4.37.tar.gz
   # cd httpd-2.4.37
   ```

3. **进行软件的配置和环境检测**

   > **注意：**

   ​	CentOS6才需要加最后那两条参数， --with-apr=/usr/local/apr  --with-apr-util=/usr/local/apr-util

   > 以下内容解释

   ![31](D:\PHP\note\quick\31.png)

   ```
   ./configure \
   --prefix=/usr/local/httpd \
   --enable-deflate \
   --enable-expires \
   --enable-headers \
   --enable-so \
   --enable-modules=most \
   --with-mpm=worker \
   --enable-rewrite \
   --enable-static-ab \
   --enable-ssl \
   --with-apr=/usr/local/apr \
   --with-apr-util=/usr/local/apr-util
   ```

4. **编译软件并且进行安装**

   ```shell
   # make && make install
   ```

#### 配置

1. **简单配置**

   ```shell
   创建网站根目录
   # mkdir -pv /mydata/wwwroot
   # chown www:www /mydata/wwwroot
   # cd /usr/local/httpd/conf
   开始配置
   # vim httpd.conf
   ```

   内容修改如下：

   User www

   Group www

   ![32](D:\PHP\note\quick\32.png)

   ServerName localhost:80

   ![33](D:\PHP\note\quick\33.png)

   将 DocumentRoot 以及整个 Directory 标签代码段的内容都注释掉

   ![35](D:\PHP\note\quick\35.png)

   ![36](D:\PHP\note\quick\36.png)

   DirectoryIndex index.htm index.html index.php

   ![37](D:\PHP\note\quick\37.png)

   modules/mod_rewrite.so	的注释去掉

   ![38](D:\PHP\note\quick\38.png)

   /httpd-vhosts.conf开启

   ![34](D:\PHP\note\quick\34.png)

   保存并退出

2. **优化虚拟主机配置**

   httpd.conf中的每个 VirtualHost 代码段都是一个独立的虚拟主机配置。当配置多个虚拟主机时，需要在 httpd.conf 里写多个 VirtualHost 代码段，那么主配置文件就会变得重复、臃肿。==所以建议，将 VirtualHost 代码段都写在另一个文件（例如：conf/extra/httpd-vhosts.conf）或多个文件（例如按客户或项目分组），然后再用 Include 指令包含进来。==

   - 创建php33根目录

     ![39](D:\PHP\note\quick\39.png)

   - 文档httpd-vhosts.conf

     ```shell
     # vim /usr/local/httpd/conf/extra/httpd-vhosts.conf
     ```

     ```
     # 默 认 的 网 站 根 目 录
     <VirtualHost *:80>
         ServerName localhost
         DocumentRoot "/mydata/wwwroot/php33/www/"
         <Directory />
             # 允 许 访 问 该 目 录
             Require all granted
             # 允许执行 .ht acces s 文件中的指令。
             AllowOverride All
             # 不 允 许 浏 览 目 录
             Options -Indexes
         </Directory>
     </VirtualHost>
     ```

   保存

3. **设为服务并开机自运行**

   - 编辑 apachectl

     ```shell
     # vim /usr/local/httpd/bin/apachectl
     ```

     加入以下注释内容

     ```shell
     # add by php32 2018-11-19
     # chkconfig: 2345 85 15
     # description: Activates/Deactivates Apache Web Server
     ```

     ![41](D:\PHP\note\quick\41.png)

     找到 $HTTPD -k $ARGV

     改成 $HTTPD -k $ARGV -f /usr/local/httpd/conf/httpd.conf

     保存

     ```shell
     启动 apache
     # service httpd start 或 /usr/local/httpd/bin/apachectl start
     将 httpd 设置为服务
     # cp /usr/local/httpd/bin/apachectl /etc/rc.d/init.d/httpd
     加入启动项
     # chkconfig --add httpd
     # chkconfig --level 345 httpd on
     ```

   - 查看httpd是否启动

     ```shell
     # ps -ef|grep httpd
     ```

#### 整合PHP

1. 修改 apache 的配置文件

   ```shell
   # vim /usr/local/httpd/conf/httpd.conf
   ```

   去掉以下两项的注释

   ```
   LoadModule proxy_module modules/mod_proxy.so
   LoadModule proxy_fcgi_module modules/mod_proxy_fcgi.so
   ```

   在底部加上

   ```
   <FilesMatch \.php$>
   	SetHandler "proxy:fcgi://127.0.0.1:9000"
   </FilesMatch>
   ```

   保存

2.  重启 apache

   ```shell
   # service httpd restart
   ```

#### 开放端口

1. 将 80 端口加入防火墙

   ```shell
   # iptables -I INPUT -p tcp --dport 80 -j ACCEPT
   ```

2. 添加至自启动文件

   ```shell
   # echo 'iptables -I INPUT -p tcp --dport 80 -j ACCEPT' >> /etc/rc.d/rc.local
   ```



## vim

### 快捷键

| 快捷键           | 说明               |
| ---------------- | ------------------ |
| **yy** / **5yy** | 复制当前行 复制5行 |
| **dd**           | 删除当前行         |
| **p**            | 粘贴               |
| **u**            | 上一步操作         |
|                  |                    |



### 编辑模式

| 命令  | 说明           |
| ----- | -------------- |
| **i** | 光标前插入内容 |
| **a** | 光标后插入内容 |
| **o** | 下一行插入内容 |
| **I** | 行首插入内容   |
| **A** | 行末插入内容   |
| **O** | 上一行插入内容 |

### 末行模式

| 命令          | 说明                |
| ------------- | ------------------- |
| **:w**        | 保存                |
| **:q**        | 退出                |
| **:wq / :x**  | 保存退出            |
| **:q!**       | 强制退出            |
| **:w!**       | 强制保存(写入)      |
| **:wq!**      | 强制保存退出        |
| **:set nu**   | 设置行号            |
| **:set nonu** | 取消行号            |
| **/aa**       | 搜索'aa'，n为下一个 |
|               |                     |
|               |                     |
|               |                     |
|               |                     |



# NoSql

## Memcache

> **优点**

- 纯内内存的存储机制，不占据硬盘空间，速度快
- 内置分布式算法，使得开发不需要自己去实现算法，只需要克隆就可以形成分布式集群服务器

> **缺点**

- 安全性很差，因为它是用telnet协议
- 容量小，只有 64M，1个 key 只能存储 1M
- 由于 Memcache 把数据置于内存中，重启就会丢失，数据无法持久保存
- 数据零散，无法遍历



### Linux中

#### 安装

> 此命令安装memcache服务器+telnet客户端+telnet服务端

```shell
# yum -y install memcached telnet telnet-server
```



#### 启动服务

##### 启动Memcache

```shell
# service memcached start  	# 启动
# service memcached status 	# 查看状态
# service memcached stop	# 停止
# service memcached restart	# 重启
```

> 注意：
>
> ​	如果需要开启自启动 memcache服务，使用 shell># chkconfig memcached on
>
> （建议暂不开启）

##### 启动Telnet

```shell
# service xinetd start		# 启动
# service xinetd status		# 查看状态
# service xinetd stop		# 停止
# service xinetd restart	# 重启
```



#### telnet连接Memcache

```
命令格式：telnet [memcache 的服务器地址] [端口]

```

> 注意：刚打开 telnet 客户端敲入回车键会出现 ERROR，并不是代表连接失败而是因为 memcache 服务器在等待你输入正确的指令

- ctril + ] 去除memcache命令行 在输入quit退出
- ctrl+BackSpace  删除键

![220](D:\PHP\note\quick\220.jpg)

#### 开启PHP扩展

##### Memcache扩展

###### 安装

- 下载

  https://github.com/websupport-sk/pecl-memcache/archive/php7.zip

- 把文件上传到Linux服务器上

- 解压并进入目录

  ```shell
  # unzip pecl-memcache-php7.zip
  # cd pecl-memcache-php7
  ```

- 生成编译文件

  ```shell
  # /usr/local/php/bin/phpize
  ```

- 进行软件配置和环境检测

  ```shell
  # ./configure --with-php-config=/usr/local/php/bin/php-config
  ```

- 编译软件并且进行安装

  ```shell
  # make && make install
  ```

  ![42](D:\PHP\note\quick\42.png)

  如图安装成功

###### 配置

- 修改php.ini 加载Memcache组件

  ```shell
  # vim /usr/local/php/etc/php.ini
  ```

  添加扩展 extension = "memcache.so"

  ![43](D:\PHP\note\quick\43.png)

- 重新启动PHP进程

  ```shell
  # pkill -9 php-fpm
  # service php-fpm start
  ```

- 检查是否添加成功

  ![225](D:\PHP\note\quick\225.jpg)

  或者

  ```
  /usr/local/php/bin/php -m
  ```

  ![227](D:\PHP\note\quick\227.jpg)

##### Memcached扩展

###### 安装依赖库

- 下载

  ```shell
  # wget http://pecl.php.net/get/igbinary-2.0.8.tgz
  # wget https://launchpad.net/libmemcached/1.0/1.0.18/+download/libmemcached-1.0.18.tar.gz
  ```

- 安装igbinary依赖库

  - 解压并进入目录

    ```shell
    # tar -zxvf igbinary-2.0.8.tgz
    # cd igbinary-2.0.8
    ```

  - 生成编译文件

    ```shell
    # /usr/local/php/bin/phpize
    ```

  - 进行软件配置和环境检测

    ```shell
    # ./configure --prefix=/usr/local/igbinary --with-php-config=/usr/local/php/bin/php-config
    ```

  - 编译软件并且进行安装

    ```shell
    # make && make install
    ```

- 安装libmemcached依赖库

  - 解压并进入目录

    ```shell
    # tar -zxvf libmemcached-1.0.18.tar.gz
    # cd libmemcached-1.0.18
    ```

  - 进行软件配置和环境检测

    ```shell
    # ./configure --prefix=/usr/local/libmemcached --with-memcached
    ```

  - 编译软件并且进行安装

    ```shell
    # make && make install
    ```

###### 安装memcached

- 下载

  ```shell
  # wget http://pecl.php.net/get/memcached-3.0.4.tgz
  ```

- 解压并进入目录

  ```shell
  # tar -zxvf memcached-3.0.4.tgz
  # cd memcached-3.0.4
  ```

- 生成编译文件

  ```shell
  # /usr/local/php/bin/phpize
  ```

- 进行软件配置和环境检测

  ```shell
  # ./configure --with-php-config=/usr/local/php/bin/php-config --enable-memcached --enable-memcached-json --enable-memcached-igbinary --with-libmemcached-dir=/usr/local/libmemcached --disable-memcached-sasl
  ```

- 编译软件并且进行安装

  ```shell
  # make && make install
  ```

###### 配置

- 修改php.ini 加载Memcached组件

  ```shell
  # vim /usr/local/php/etc/php.ini
  ```

  添加扩展 extension = "memcached.so"

  ![219](D:\PHP\note\quick\219.jpg)

- 重新启动PHP进程

  ```shell
  # pkill -9 php-fpm
  # service php-fpm start
  ```

- 检查是否添加成功





### windows中

#### 开启PHP扩展

- 查看PHP版本号与线程

  ![222](D:\PHP\note\quick\222.jpg)

- 下载扩展文件

  https://github.com/nono303/PHP7-memcache-dll

- 复制到php扩展文件目录下

  ![223](D:\PHP\note\quick\223.jpg)

- 修改php.ini文件

  ![224](D:\PHP\note\quick\224.jpg)

- 保存并重启apache服务

  ![225](D:\PHP\note\quick\225.jpg)

开启扩展成功

#### 安装&开启服务

- 下载memcache服务软件

  官网地址：http://memcached.org/

- 解压文件

  ![226](D:\PHP\note\quick\226.jpg)

- 启动memcache服务

  ```shell
  D:\PHP\toolsmore\memcache\memcached-win64-1.4.4-14\memcached> memcached.exe
  ```

  > memcached基本参数设置

  - -p 监听的端口
  - -l 连接的IP地址, 默认是本机
  - **-d start 启动memcached服务**
  - **-d restart 重启memcached服务**
  - **-d stop|shutdown 关闭正在运行的memcached服务**
  - -d install 安装memcached服务
  - -d uninstall 卸载memcached服务
  - -u 以的身份运行 (仅在以root运行的时候有效)
  - -m 最大内存使用，单位MB。默认64MB
  - -M 内存耗尽时返回错误，而不是删除项
  - -c 最大同时连接数，默认是1024
  - -f 块大小增长因子，默认是1.25
  - -n 最小分配空间，key+value+flags默认是48
  - -h 显示帮助

  > 其中，加粗的三个参数只能在加入服务后才可使用

- 添加win系统服务中（可选）

  - 管理员身份打开黑窗口
  - 进入memcached目录
  - 指令：memcached.exe -d install

- 删除win系统服务 (可选)

  - 管理员身份打开黑窗口
  - 进入memcached目录
  - 指令：memcached.exe -d uninstall

### 常用指令

| 命令          | 详情                                                 |
| ------------- | ---------------------------------------------------- |
| **add**       | 创建一个存在内存中的 key => value的键值对            |
| **get**       | 获取一个 memcache 的 key 中 value                    |
| **set**       | 修改或者添加一个键值对，键存在则是修改，不修改则添加 |
| **delete**    | 主动删除一个键值对                                   |
| **incr**      | 自增n                                                |
| **decr**      | 自减n                                                |
| **flush_all** | 清空 memecache 中所有数据                            |

- **过期时间**

  单位为秒

- **add**

  ```
  add [key 的名称][标识符][过期的时间][字节的大小]
  【例】
  add age 0 0 2
  12
  ```

  > **注意**：一个回车代表2个字符

- **get**

  ```
  get [key 的名称]
  
  【例】
  get age
  ```

- **set**

  ```
  set [key 的名称][标识符][过期的时间][字节的大小]
  【例】
  set age 0 0 3
  100
  ```

- **delete**

  ```
  delete [key 的名称]
  
  【例】
  delete age
  ```

- **incr**

  ```
  incr [key 的名称] [value]
  【例】
  incr age 2
  14
  ```

- **decr**

  ```
  decr [key 的名称] [value]
  【例】
  decr age 2
  12
  ```

- **flush_all**

  同重启memcache，为清空memcache中所有数据

  > 注意事项：重启telnet服务并不会清除 memcached 当中数据

  telnet只要启动过一次，将来发生启动或停止，但 memcached 没有停止的情况下，memcached 并不会丢失数据，除非 memcached 自己发生重启或停止，所有链接都会被终止与所有数据都丢失。



### 类常用方法

| 类方法                      | 说明                                                         |
| --------------------------- | ------------------------------------------------------------ |
| **addServer(host, port)**   | host 就是 Linux 服务器地址，port默认是 11211（memcached端口），用于连接 memcached 服务器 |
| **addServers(servers)**     | 用于连接分布式 memcached 服务器，主要分布式                  |
| **set(key, value, expire)** | 用于修改或添加内存的 memcached 数据，该方法有3个参数         |
| **get(key)**                | 获取对于键值对                                               |
| **delete(key)**             | 删除 memcached 当中键值对                                    |

#### 连接服务器

![45](D:\PHP\note\quick\45.png)

![44](D:\PHP\note\quick\44.png)

#### set方法

>  参数说明：

- key 为键名
- value 是键值
- flag 使用MEMCACHE_COMPRESSED指定对值进行压缩(使用zlib)
- exipre 是过期时间，expire 默认为0表示永远不过期，如果设置为秒，最大只能设置为30天的秒数(30 * 86400秒)

> 操作复合类型

![46](D:\PHP\note\quick\46.png)效果如下所示：

![47](D:\PHP\note\quick\47.png)

> 设置过期时间

```php
$memc->set('string','hello',10)
```

#### 操作分布式服务器

memcache内置自动分布算法的原理：

![48](D:\PHP\note\quick\48.png)

【例】使用分布式的链接服务器，插入100条数据分布到不同的服务器中

```php
<?php
        $memc = new Memcached();
        //定义服务器的数量
        $addServers = [
                //['ip','port','权重']
                ['192.168.82.43',11211,50],
                ['192.168.230.11',11211,50],
        ];
        //连接
        $memc->addServers($addServers);

        //分别为服务器添加100数据
        for ($i = 1;$i<=100;$i++){
                $memc->set('i'.$i,$i);
        }
        echo'success';               
```



## Redis

radis有5种数据类型，还有1种服务器命令类型(key服务器指令，不支持windows)

- String（字符串类型）
- list（链表）
- hash（哈希表类型）
- set（无序的集合）
- sorted set（有序集合，缩写为zset）

而且 Redis 通过简单的配置把数据从内存保存到硬盘当中进行持久保存。

Redis 为高并发而生，是NoSql中的佼佼者

Redis读的速度是 110000次/秒，写的速度是81000次/秒。

### Redis和Memcache区别

- Redis 拥有安全认证的密码机制，Memcache 没有
- Redis 是内存 + 硬盘的存储机制存储大小远超 memcached 的  64M
- Redis 的 1 个 key 最大可以存储 1G，而 memcached是 1M
-  Redis 是一个持久化的 NoSql产品，Redis 会以一种叫做快照的模式（把数据存储在硬盘中）操作数据，所以无论是重启还是杀死 Redis的进程，都不会导致 Redis的数据丢失。

### 安装和启动

> 安装命令：

```shell
# yum -y install redis 
```

有可以报以下错误：

```
[root@localhost www]# yum -y install redis
已加载插件：fastestmirror, refresh-packagekit, security
设置安装进程
Loading mirror speeds from cached hostfile
No package redis available.
错误：无须任何处理
```

我们当前这个yum没有这个包，可以先安装：

```shell
# yum install epel-release
```



### 启动登录客户端

#### 启动redis服务器

```
命令：service redis start | restart | stop
```

> 注意：

- 使用 service redis status 会发现 Redis 服务已停，不准确
- 建议使用 **ps -ef | grep redis**

#### 链接Redis

```shell
# redis-cli
没有空格

退出
exit
```

> 注意：Redis 默认端口为：6379

#### 停止redis服务

```shell
# service redis stop
```

> 注意：如果使用 service redis stop 无法停止 redis 服务，需要使用 pkill -9 redis 命令强制杀死 redis 进程



### 数据类型&命令

#### String数据类型

string 是 Redis 最基本的类型

> **管理命令**

| 命令       | 详情                                           |
| ---------- | ---------------------------------------------- |
| **get**    | 获取Redis中的key对应的值，如果key不存在返回nil |
| **set**    | 用于设置或者修改Redis中的键值对                |
| **expire** | 设置键的过期时间                               |
| **del**    | 删除键的值                                     |

- **get**

  ```
  get key
  
  【例】
  get age
  ```

- **set**

  ```
  set key value
  
  【例】
  set age 12
  ```

- **expire**

  ```
  expire key seconds
  
  【例】
  expire age 5
  ```

- **del**

  ```
  del key
  
  【例】
  del age
  ```

#### hash数据类型

在哈希表中设置一个字段(key)和一个字段的值(value)，用一张表来表示一些特定的信息，如下所示：

| id   | username  | age  | job  |
| ---- | --------- | ---- | ---- |
| 1    | qiudachui | 18   | IT   |
| 2    | lidachui  | 17   | IT   |

> **管理命令**

| 命令        | 详情                                                       |
| ----------- | ---------------------------------------------------------- |
| **hget**    | 在一张指定的哈希表中获取字段的值，如果字段不存在将返回 nil |
| **hset**    | 用于设置或修改哈希表中的字段值                             |
| **hmset**   | 用于设置哈希表中多个字段值                                 |
| **hgetall** | 在哈希表获取所有的字段和值                                 |

- **hget**

  ```cmd
  hget key field
  
  #【例】
  ip:6379> hget userInfo:qiudachui username
  ip:6379> hget userInfo:qiudachui age
  ip:6379> hget userInfo:qiudachui job
  ```

- **hset**

  ```cmd
  > hset key field value
  
  #【例】
  ip:6379> hset userInfo:qiudachui username qiudachui
  ip:6379> hset userInfo:qiudachui id 1
  ip:6379> hset userInfo:qiudachui job IT
  ip:6379> hset userInfo:qiudachui age 22
  ```

- **hmset**

  ```cmd
  > hmset key field value [field value ...]
  
  #【例】
  ip:6379> hmset userInfo:lidachui id 2 username lidachui age 17 job IT
  ```

- **hgetall**

  ```cmd
  hgetall key
  
  #【例】
  ip:6379> hgetall userInfo:lidachui
  ```

> **注意**
>
> ​	此处key为 tablename:username，因为每个key都要唯一，若只写tablename则新增的数据会覆盖前面的数据，可以改写成tablename:1等等，但要保证唯一

#### list数据类型

链表数据结构中的栈：先进后出

链表数据结构中的队列：先进先出

> **管理命令**

| 命令       | 详情                                                         |
| ---------- | ------------------------------------------------------------ |
| **lpush**  | 从左加入一条数据，在栈中加入一条数据                         |
| **rpush**  | 从右加入一条数据，在列表中加入一条数据                       |
| **lrange** | 在链表中获取一个范围(索引的范围)的数据                       |
| **lpop**   | 弹出头部元素，并且返回其值                                   |
| **rpop**   | 弹出最后一个元素，并且返回其值                               |
| **ltrim**  | 让列表只保留指定区间内的元素，不在指定区间之内的元素都将被删除 |

- **lpush**

  ```cmd
  lpush key value [value ...]
  
  #【例】在一个名为 qiudachui 栈中压入数据：one、two、three
  ip:6379> lpush qiudachui one
  ip:6379> lpush qiudachui two
  ip:6379> lpush qiudachui three
  #或
  ip:6379> lpush qiudachui one two three
  ```

- **rpush**

  ```cmd
  rpush key value [value ...]
  
  #【例】在一个名为 lidachui 队列中压入数据：one、two、three
  ip:6379> rpush lidachui one
  ip:6379> rpush lidachui two
  ip:6379> rpush lidachui three
  #或
  ip:6379> rpush lidachui one two three
  ```

- **lrange**

  ```cmd
  lrange key start stop
  
  #【例1】：获取的所有数据
  ip:6379> lrange qiudachui 0 -1
  
  #【例2】从位置为1的地方开始获取到最后
  ip:6379> lrange qiudachui 1 -1
  ```

- **lpop**

  ```cmd
  lpop key
  
  #【例】
  ip:6379> lpop lidachui
  ```

- **rpop**

  ```cmd
  rpop key
  
  #【例】
  ip:6379> rpop lidachui
  ```

- **ltrim**

  ```cmd
  ltrim key start stop
  
  #【例】
  ip:6379> rpush jack one two three four five
  #查询结果如下
  ip:6379> lrange jack 0 -1
  1) "one"
  2) "two"
  3) "three"
  4) "four"
  5) "five"
  #截取
  ip:6379> ltrim jack 2 4
  #查询结果如下
  ip:6379> lrange jack 0 -1
  1) "three"
  2) "four"
  3) "five"
  ```

> 注意： ltrim 保存区间必须具有连续性，而不是能是断开连续的

#### set数据类型(无序)

> **管理命令**

| 命令         | 详情                                                         |
| ------------ | ------------------------------------------------------------ |
| **sadd**     | 在无序集合当中添加一个元素，该元素如果存在该元素不会被重复添加 |
| **smembers** | 查看一个无序集合中的所有元素                                 |
| **sdiff**    | 以一个集合作为标准去求另外一个集合不存在的元素，我们称为差集 |
| **sinter**   | 一个集合和另外一个集合共同的元素，我们称为交集               |
| **sunion**   | 求出两集合合并后所有的元素并去掉重复的元素的结果称为并集     |
| **scard**    | 统计集合中的元素个数，并返回总数的整型值，该命令一般在社交网络中用于统计粉丝数 |
| **srem**     | 用于删除无序集合中的元素，在社交网络开发中用于黑名单功能     |

- **sadd**

  ```cmd
  sadd key member [member ...]
  
  #【例】创建一个zhangsan无序集合
  ip:6379> sadd zhangsan a1
  ip:6379> sadd zhangsan b1
  ip:6379> sadd zhangsan c1
  ip:6379> sadd zhangsan d1
  #或
  ip:6379> sadd lisi a1 b1 c2 d2 e2
  ```

- **smembers**

  ```cmd
  smembers key
  
  #【例】
  ip:6379> smembers zhangsan
  ```

- **sdiff**

  ```cmd
  sdiff key [key ...]
  
  #【例】以张三作为标准求李四的差集(李四没有的)
  ip:6379> sdiff zhangsan lisi
  ```

- **sinter**

  ```cmd
  sinter key [key ...]
  
  #【例】
  ip:6379> sinter zhangsan lisi
  ```

- **sunion**

  ```cmd
  sunion key [key ...]
  
  #【例】
  ip:6379> sunion zhangsan lisi
  ```

- **scard**

  ```cmd
  scard key
  
  #【例】
  ip:6379> scard zhangsan
  ```

- **srem**

  ```cmd
  srem key member [member ...]
  
  #【例】例如删除 zhangsan 集合中为 a1 的元素
  ip:6379> srem zhangsan a1
  ```

#### zset数据类型(有序)

​	sorted set 是 set 的一个升级版本，在 set 有基础上增加了一个顺序属性，这一属性在添加修改元素的时候可以指定，每次指定后，zset 会自动重新按新的值调整顺序。有序列表值完成的是集合元素排序的功能，一般很少用于其他方向。

> **管理命令**

| 命令          | 详情                                                 |
| ------------- | ---------------------------------------------------- |
| **zadd**      | 向有序集合中添加元素。如果该元素存在，则更新其顺序。 |
| **zrange**    | 按序号升序(由小到大)获取有集合中的内容               |
| **zrevrange** | 按序号升序(由小到大)获取有集合中的内容               |

- **zadd**

  ```cmd
  zadd key score member [score member ...]
  
  #【例】创建一个wangwu有序集合
  ip:6379> zadd wangwu 1 a1
  ip:6379> zadd wangwu 2 b1
  ip:6379> zadd wangwu 3 c1
  ip:6379> zadd wangwu 4 d1
  #或
  ip:6379> zadd zhaoliu 1 a1 2 b1 3 c2 4 d2
  ```

  > 注意：1，2，3叫序号，不叫索引，liminxian的序号是1，而索引号是0

- **zrange**

  ```cmd
  zrange key start stop [WITHSCORES]
  
  #【例】
  ip:6379> zrange stars 0 -1
  ```

- **zrevrange**

  ```cmd
  zrevrange key start stop [WITHSCORES]
  
  #【例】
  ip:6379> zrevrange stars 0 -1
  ```

### 管理命令

| 命令       | 详情                                                         |
| ---------- | ------------------------------------------------------------ |
| **keys**   | 返回当前数据库里面的键(key)                                  |
| **exists** | 判断一个键(key)是否存在                                      |
| **del**    | 删除指定的键，返回 1 代表删除键名成功，返回 0 代表删除失败   |
| **type**   | 返回一个键的数据类型                                         |
| **expire** | 设置键的有效期，如果不调用该命令设置键名，默认的情况下键名本身就是永远不过期 |
| **ttl**    | 查看一个 key 的过期剩余时间                                  |

- **keys**

  ```cmd
  # 返回当前数据库里面的所有键(key)
  ip:6379> keys * 
  # 查询key的存在，有则返回名称
  ip:6379> keys zhangsan
  ```

- **exists**

  ```cmd
  #【例】判断 stars 是否存在 Redis 中
  ip:6379> exists stars
  ```

  > 注意：如果返回 0 代表该键名不存在，如果返回 1 代表键名存在

- **del**

  ```cmd
  #【例】删除zhangsan
  ip:6379> del zhangsan
  ```

- **type**

  ```cmd
  #【例】返回zhangsan的数据类型
  ip:6379> type zhangsan
  ```

- **expire**

  ```cmd
  #【例】设置一个 key 在 20 秒后过期
  ip:6379> expire name 20
  ```

- **ttl**

  ```cmd
  #【例】查看一个name的过期剩余时间
  ip:6379> ttl name
  ```

  > **注意**：返回-1表示永不过期 -2表示已过期

### 安全认证

​	在默认情况下 Redis 不需要任何密码就可以登陆，任何客户端只要连接6379端口就可以调用Redis命令，安全性不够，如果希望提高 Redis 的安全性，我们可以为 Redis 设置一个密码。Redis把设置密码的过程称为安全认证功能(Redis Auth)

密码存放在 Redis 的配置文件中(例如：/etc/redis.conf)

设置安全认证的步骤如下：

- 使用 vim 打开 /etc/redis.conf 文件，查找到 foobared，

  ```shell
  # vim /etc/redis.conf
  ```

- 把 requirepass 前面的#(井号)去除，将后面的 foobared 修改为：123456(Redis认证密码)

  ![228](D:\PHP\note\quick\228.jpg)

-  设置完成后保存并退出

> **注意**：内容必须顶格，requirepass前面不能有任何空格等

- 重启 Redis 服务

  ```shell
  # service redis restart
  ```

- 使用 redis-cli 命令登陆，发觉可以进入客户端界面但是无法操作

- 使用安全认证密码进行登陆

  ```shell
  # redis-cli -a 123456
  ```




### Redis的持久化 AOF 设置

在 Redis 当中，Redis 有两种持久化模式，默认为快照样式(用于保存数据到硬盘的模式)

#### 快照模式

默认安装完成就会自动开启的持久化模式

快照文件默认存储以下位置：/var/lib/redis/dump.redb

```
shell># cd /var/lib/redis
shell># ls -lh
```

![49](D:\PHP\note\quick\49.png)

默认情况下快照模式==没有利用计算机的内存==，只是单方面反数据置于硬盘当中，如果希望 Redis 把硬盘+内存的存储方式利用起来，则要调整为 aof 模式

#### Aof模式

如果开启硬盘+内存方式存储数据，Redis 默认情况下会先把数据存放到内存中，然后每隔 1 秒钟不把内存的数据同步到硬盘中

首先我们需要观察 /var/lib/redis 下有没有存在一个 .aof 的文件，查看结果如下图所示：

```
shell># /var/lib/redis
shell># ls -lh
```

> 注意：如果只有快照文件，而没有 aof 的文件，说明 redis 没有开启 aof 持久化模式



##### 设置aof模式

1. 使用 vim 打开 /etc/redis.conf 文件，搜索appendonly

```
shell># vim /etc/redis.conf
```

> 注意：如果 appendonly 为 no 表示当前是快照模式，不是 aof 模式

2. 把 appendonly 的选项由 no 改为 yes

   ![50](D:\PHP\note\quick\50.png)

3. 重启 redis 服务

   ```shell
   # service redis restart
   ```

4. 查看是否可启成功

   进入 /var/lib/redis 目录下去查看是否有 .aof 文件

   ```
   shell># cd /var/lib/redis
   shell># ls -lh
   ```

   > 注意：如果我们添加数据，会改变 appendonly.aof 文件的大小



#### PHP 中开启 Redis 扩展

##### 安装

1. 下载

   下载地址：https://codeload.github.com/phpredis/phpredis/zip/develop

2. 上传到服务器

   可以使用 rz 上传或 ftp 上传

   > 注意：必须得安装了 vsftpd  或  lrzsz，我们这里以 rz 为例

3. 解压与进入目录

   ```shell
   # unzip phpredis-develop.zip
   # cd phpredis-develop
   ```

4. 生成编译文件

   ```shell
   # /usr/local/php/bin/phpize
   ```

5. 进行软件配置和环境检测

   ```shell
   # ./configure --with-php-config=/usr/local/php/bin/php-config
   ```

6. 编译软件并且进行安装

   ```shell
   # make && make install
   ```

##### 配置

1. 修改 php.ini 加载 Redis 组件

   ```shell
   # vim /usr/local/php/etc/php.ini
   ```

   ![229](D:\PHP\note\quick\229.jpg)

2. 结束PHP进程

   ```shell
   # pkill  -9  php-fpm
   ```

3. 重新启动PHP进程

   ```shell
   # service php-fpm start
   ```

4. 检查是否添加成功

   - 在站点目录下创建一个phpinfo.php文件，输入phpinfo()
   - shell># /usr/local/php/bin/php -m 查看是否含有redis

5. 把本地访问机制关闭

   - 使用vim打开/etc/redis.conf文件，找到bind 127.0.0.1这个选项如下所示：

     ```shell
     # vim /etc/redis.conf
     ```

   - 在bind前面加上#号进行注解

     ![51](D:\PHP\note\quick\51.png)

   - 重启redis服务器

     ```shell
     # service redis restart
     ```

### PHP操作Redis

#### 连接Redis

![52](D:\PHP\note\quick\52.png)

#### 各种数据类型的操作

##### string 类型

![230](D:\PHP\note\quick\230.jpg)

##### hash 类型

![231](D:\PHP\note\quick\231.jpg)

##### set无序集合

![233](D:\PHP\note\quick\233.jpg)

##### zset有序集合

![232](D:\PHP\note\quick\232.jpg)

> 注意：

​	Zrange 与 zRevRange 有4个参数，第4个参数默认为：false，如果想键值调换就把第4个参数设置为：true

### Redis 实现消息队列

在银行办理业务的过程就是使用 Redis 的消息队列完成，过程分以下两个步骤：

- 取号(把取号人的数数据压入 list 队列中)
- 叫号(把 list 队列中的头部元素弹出队列)



取号代码如下:

```php
<?php
    $redis = new Redis();
    //连接
    $redis->connect('192.168.230.11',6379);
    //设置密码
    $redis->auth('123456');

    //设置排队人数
    $array = [
        '001号贵宾--大锤，请到6号窗口',
        '002号贵宾--大锤，请到4号窗口',
        '003号贵宾--大锤，请到3号窗口',
    ];
    //添加到队列中
    foreach($array as $v){
        $redis->rpush('setList',$v);
    };
    echo "success";
```

叫号代码如下:

![234](D:\PHP\note\quick\234.jpg)



# MongoDB

​	MongoDB是一个介于关系型数据库和非关系型数据库之间的产品，是非关系型数据库当中功能最丰富，最像关系型数据库，但是 MongDB 做不到关系型数据库的连表，外键等操作，它的存储数据方式有点类似于 JSON 格式，MogoDB叫做 Bson（big json）格式。

- MongoDB是一个面向集合的，模式自由的文档型数据库。
- MongoDB能很好地支持PHP。
- MongoDB安全性是所有NoSql最好的。
- MongoDB安装的文件比较大，占据了一定的硬盘空间。

> 缺点：

不支持连表查询，不支持 sql 语句，不支持事务存储过程等，所以不适合存储数据关系比较复杂的数据，一般主要是当做一个==数据仓库==来使用。

> 适用于：

日志系统，股票数据等。

> 不使用于：

电子商务系统等需要连多表查询的功能。

国内职场中应用 MongoDB 最广泛的网站(PHP+MongoDB)：youku(优酷)、tudou(土豆)

> 概念

- **文档**

		==文档==是 MongoDB 中数据的==基本单元==，类似==关系型数据库的行==，多个键值对有序地放置在一起便是文档。

MongoDB 中以文档的方式存取记录，如一条记录格式如下：

```
{'username':'php32', 'age':18, email:'123456.gd@163.com', sex:'男'}
```

- **集合(表)**

集合就是一组文档，==多个文档组成一个集合，集合类似于 MySQL 里面的表。==

模式自由（schema-free）：==意思是集合里面没有行和列的概念。==

> 注意：

MongoDB 中的==集合不用创建、没有结构==，所以可以放不同格式的文档。

- **数据库**

多个集合可以组成数据库。一个MongoDB实例可以承载多个数据库，们之间完全独立。

MongoDB 中的数据库和 MySQL 中的数据库概念类似，只是==无需创建==。

==一个数据库中可以有多个集合。==

==一个集合中可以有多个文档(MongoDB里面的每一个文档，代表mysql的数据表中的每一行数据)。==

## 安装 启动

1. 创建仓库

```shell
shell># vim /etc/yum.repos.d/mongodb-org-3.4.repo
```

2. 把下面的内容复制到文件中 保存退出

```shell
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

3. yum安装 

```shell
shell># yum install -y mongodb-org
```

4. 启动 MongoDB

```shell
shell># service mongod start	# 启动
shell># service mongod stop		# 停止
shell># service mongod restart	# 重启
shell># service mongod status	# 查看状态
```





## db相关命令

### 登录退出

命令格式：`mongo [-u 登陆名][-p 登陆密码][ip:端口/数据库]`

例如：mongo -uroot -p123456 localhost:27017/admin

```shell
连接 mongodb
# mongo -uroot -p123456 localhost:27017/admin
退出
mongo>quit()
```

> 注意：MongoDB 默认是没有用户与密码

### 查看所有db

命令格式：`show dbs`

相当于 MySQL 中的 show databases(); 命令

```shell
# 显示所有数据库
MongoDB> show dbs;
#或
MongoDB> show databases;
```

> 说明：

- local 是本地系统数据库，默认是显示的，它不能被删除，否则 MongoDB会直接崩溃
- admin 是管理员数据库，默认是隐藏的

### 查看目前db

命令：`db`

> 说明：相当于 MySQL 中的 select database(); 命令。

```shell
# 显示目前所在的数据库
MongoDB> db
```

### 选择/创建db

命令：`use 数据库名`

例如：use php32

```shell
# 选择 admin 数据库，因为 admmin 这个数据库本身就存在
MongoDB> use admin
# 创建 php32 数据库
MongoDB> use php32
```

> 说明：

- 如果 php33数据库存在，use 命令就是相当于MySQL中的 use 命令，选择数据库。
- 如果 php33数据库不存在，use 命令就是相当于MySQL中的 create database php33命令。

### 删除db

命令：`db.dropDatabase()`

注意：删除数据库会让集合和文档全部丢失

```mongodb
MongoDB> db.dropDatabase()
```

> 注意：

- 删除数据库会让集合和文档全部丢失
- 绝对不能删除 local 数据库，因为这是一个系统数据库，删除则 MongoDB崩溃

### 帮助文档

命令：`db help()`

作用：显示数据库的帮助文档信息

```shell
# 显示帮助文档
MongoDB> db.help()
```



命令：`db.集合名称.help()`

作用：显示当前操作数据库中的集合相关帮助文档信息

```shell
# 显示集合帮助指令
MongoDB> db.class1.help()
```

## 集合相关命令

### 显示当前集合

命令：`show tables`

```shell
# 显示所有表名(集合)
MongoDB> show tabels
#也可以使用 show collections 来替代
MongoDB> show collections
```

### 创建集合

命令：`db.集合名.insert({bson 数据})`

```shell
# 在 php32 中创建一个集合为：class
MongoDB> db.class.insert({name:'hehe', age:18})

# 定义一个 _id 为 300 的文档(记录)
MongoDB> db.class2.insert({_id:300, name:'lidachui'})

# 在 class3 集合插入 1000 条学生记录
MongoDB> for(var i=1;i<=10;i++){
... db.class2.insert({_id:i,name:'stu'+i,lesson:'php'+i})
... }
```

> 注意：添加会默认创建一个_id的字段，并且是对象类型

### 查询数据

命令：`db.集合名称.find({条件})[.limit().skip().count(true)]`

```shell
# 查询class2集合中_id 大于6的信息记录
MongoDB> db.class2.find({_id: {'$gt':6}})

# 查询class3中_id小于或者等于10的文档
MongoDB> db.class3.find( {_id:{'$lte':10}} )

# 查询class3中_id小于等于5的文档，并且只显示前面的3条记录
MongoDB> db.class3.find( {_id:{'$lte':5}} ).limit(3)

# 查询_id小于等于5的文档，跳过前面2条记录，显示后面的3条记录
MongoDB> db.class3.find( {_id:{'$lte':5}} ).skip(2).limit(3)

# 统计class3集合有多少数据(文档)
MongoDB> db.class3.find().count(true)

# 查询 _id小于等于7的文档，并且跳过前面3条记录，统计当前查询出多少条记录(个文档)
MongoDB> db.class3.find( {_id:{'$lte':7}}).skip(3).count(true)
```

> 注意：

- 如果在 MongoDB 中没有使用 count(true)，是无法把 skip 和 limit 看成一个条件
- count()一定要放到最后

### sort排序

语法：`db.集合名称.find().sort( {字段:-1/1} )`

参数说明：

- 1：代表升序排列，相当于 asc 的操作，默认为 asc
- -1：代表降序排列，相当于 desc 的操作

```shell
#查找 _id 小于 10 的文档，按照 _id 字段降序(从大到小)排列
MongoDB> db.class3.find({_id:{'$lt':10}}).sort({_id:-1})
```

### update

命令格式：`db.集合名称.update( {条件},{'$set':{字段名:值}}, false, true )`

> 说明：

- 第3个参数表示关闭只修改单行记录功能，false 表示修改可以发生在多行记录中
- 第4个参数表示启动批量修改功能

```shell
# 把class3集合_id<=5，name值改为tp5
MongoDB> db.class3.update({_id:{'$lte':5}},{'$set':{name:'tp5'}},false,true)
```

### remove

语法：`db.集合名称.deleteMany( {条件} )`

> 注意：如果条件为空，则代表删除集合所有的文档

案例1：删除 class2 集合中的 name='dachui' 的数据

```shell
# 案例1：删除 class2 集合中的 name='dachui' 的数据
MongoDB> db.class2.deleteMany( {name:'dachui'} )
或
MongoDB> db.class2.remove( {name:'dachui'} )

# 删除 class2 中所有数据(文档)
MongoDB> db.class2.deleteMany({})
或
MongoDB> db.class2.remove({})
```

### $or 操作符

作用：相当于 MySQL 当中 or 操作符

```shell
# 查询 _id 为1 或者 _id 大于或等于 997 的文档
MongoDB> db.class3.find({'$or':[{_id:1},{_id:{'$gte':997}}]})

# 查询 _id = 10 或者 name = stu99 或者 _id = 100 的记录(文档)
MongoDB> db.class3.find({'$or':[{_id:10},{name:'stu99'},{_id:100}]})

# 查询 _id 小于等于 5 或者 name 为 stu100 文档
MongoDB> db.class3.find({'$or':[{_id:{'$lte':5}},{name:'stu100'}]})
```

### $and 操作符

作用：相当于 MySQL 中 and 操作符

```shell
# 查询 _id 为5 与 name = stu5 的文档
MongoDB> db.class3.find({'$and':[{_id:5},{name:'stu5'}]})
```

### $in 操作符

作用：相当于 MySQL 中 in 操作语句，不过 in 在 MongoDB 中是非常快速，因为 $in 一定可以使用上索引

```shell
# 查询 _id 为 33，55，77，99 的记录
MongoDB> db.class3.find( {'_id':{'$in':[33,55,77,99]}} )
```

## 索引和执行计划

索引目的提高查询的效率，如果在查询中能够使用上定义的索引就表示就是一个速度很快的查询

### 创建索引

语法格式：`db.集合名称.ensureIndex( {字段:1},{索引的属性} )`

{字段:1}：表示在某个字段中设置索引，1 表示 true

```shell
# 为 class2 的 name 字段添加普通索引
MongoDB> db.class2.ensureIndex( {name:1} )
 
# 为 class3 的 name 字段添加唯一性索引
MongoDB> db.class3.ensureIndex( {name:1},{unique:true} )
```

### 执行计划 explain

执行计划是查看一个 find() 是否可以使用上索引

语法：`db.集合名称.find( {条件} ).explain()`

```shell
# 查看是否使用索引
MongoDB> db.class3.find({name:'sut101'}).explain()
```

### 索引相关指令

#### getIndexes() 

命令的作用：用于查询一个集合当中的索引有哪些

```shell
# 查询 class3 中使用了哪些索引
MongoDB> db.class3.getIndexes()
```

#### dropIndex()

命令作用：删除集合中指定的索引

```shell
# 删除 class3 中的索引，索引名称 name_1 的索引
MongoDB> db.class3.dropIndex( "name_1" )
```



## 安全权限验证

MongoDB号称世界上 NoSQL 产品中最安全的产品，MongoDB 拥有权限验证机制和加密功能，

### 启动安全验证

1. 切换到隐藏数据库 admin 当中

   ```shell
   MongoDB> use admin
   ```

2. 添加用户并指定权限

   > 语法：

   `db.createUser({user:("username"),pwd:("password"),roles:[{role:("root"),db:"dbName"}]})`

   > 参数说明：

   - username：用户名
   - password：密码
   - root：权限
   - dbName：数据库名

   ```shell
   MongoDB> db.createUser({user:"root",pwd:"123456",roles:[{role:"root",db:'admin'}]})
   ```

   > 注意：密码必须要用引号引住

   当我们添加完用户后，会出现一个system.users 的集合，专门用于存放 MongoDB 的管理员数据

   ```shell
   MongoDB> show tables
   system.users
   system.version
   
   MongoDB> db.system.users.find()
   { "_id" : "admin.root", "user" : "root", "db" : "admin", "credentials" : { "SCRAM-SHA-1" : { "iterationCount" : 10000, "salt" : "ioc0EPFBytxNdBdgPyFNJg==", "storedKey" : "wGr9Xm+z02dZ5slccRHMZrjZfnM=", "serverKey" : "vDaOb64fKAr1LB3aupKvzGKCbOk=" } }, "roles" : [ { "role" : "root", "db" : "admin" } ] }
   ```

3. 使用 exit 命令退出 MongoDB

   ```shell
   MongoDB> exit
   ```

   建议为了包含 Mongodb.conf 不被其他用户修改，所以要停止

   ```shell
   shell># service mongod stop
   ```

4. 修改 /etc/mongodb.conf 文件

   - 打开

   ```shell
   # vim /etc/mongodb.conf
   ```

   - 找security选项,中的#去掉，并在其下一行，空两个空格，加上`authorization: enabled`

     

   - 保存退出
