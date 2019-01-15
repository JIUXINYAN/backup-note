---
title: PDO
date: 2019-01-09 14:12:25
categories: 
          - php
tags:
    - php
notshow: true
---
# PDO与异常
<!-- more -->
# 1. PDO的基本概念

## 1.1 why使用PDO

在WEB开发中，能够使用的数据库不仅仅只有MYSQL，还可能使用其他的数据库，比如：ORACLE、FIREBIRD、MSSQL等。



在PHP程序中，我们执行的是相同的操作，但是所写的操作函数却不一样，以连接数据库操作为例：

MySQLi：mysqli_connect

MSSQL：mssql_connect

ORACLE：oci_connect



所以，当我们要切换数据库时，就必须更换为相应扩展的操作函数

![8](\images\two\img_d20\8.jpg)



这无疑将提高程序人员操作的门槛，如果需要在项目中更换数据库或者增加不同的数据库，那么一方面我们需要学习不同的数据库操作函数，非常麻烦；另一方面操作功能多了维护起来也会增加负担。

 

然而PDO却给我们提供了一个方便的操作方式，我们不再需要学习市面上各种各样的数据库操作，只需要学会使用PDO，那么就可以通过PDO来达到使用相同的操作方法，改变个别参数值，就能达到操作不同类型数据库的目的。



![3](\images\two\img_d20\3.png)



## 1.2 what是PDO

PDO：PHP Data Object  即 PHP数据对象

**概念：**PDO即PHP中专门用来操作数据库的一套扩展



PDO在手册中的位置：

![9](\images\two\img_d20\9.jpg)



# 2. PDO的基本操作

## 2.1 开启PDO扩展

第一步：打开PHP配置文件php.ini, 确认extension_dir配置项

![3](\images\two\img_d20\3.jpg)

第二步：继续在php.ini中配置PDO的extension配置项

![1](\images\two\img_d20\1.jpg)

第三步：确认php_pdo_mysqli.dll存在

![4](\images\two\img_d20\4.jpg)

第四步：重启apache，测试PDO是否开启成功，

![11](\images\two\img_d20\11.png)



## 2.2 连库的基本操作

引言：我们可以通过实例化PDO类的对象，来达到实现连库基本操作的目标



一旦实例化PDO类的对象，则PDO类中的构造方法将会被PHP自动调用执行，所以我们需要先了解一下PDO中的构造方法：

> **__construct**(基本参数，数据库账号，数据库密码)            负责初始化连库基本操作

参数详解：

> 基本参数： 包含数据库类型，数据库IP地址，端口号，字符集和默认的数据库名
>
> 基本参数的格式：‘数据库类型：host=IP地址；port=端口号；charset=字符集；dbname=数据库名’



演示案例：

code1.php

```php
<?php 
//数据库类型:host=IP地址;port=端口号;charset=字符集;dbname=数据库名
    
$dsn = 'mysql:host=localhost;port=3306;charset=utf8;dbname=test';
$pdo = new PDO($dsn,'root','123abc');
var_dump($pdo);
```

访问code1,效果为：

![2](\images\two\img_d20\2.jpg)



## 2.3 设置操作(增删改)

涉及的方法：

> exec(SQL语句)           执行增删改操作SQL语句



**==需求==**：完成以下操作

1. 使用PDO，向test数据库中的cz_user表实现新增一条数据；
2. 使用PDO，向test数据库中的cz_user表实现修改id=8的数据name值为'小红帽'；
3. 使用PDO，删除test数据库中的cz_user表id为1的数据；

**==解答==**：构建名为code2.php的文件，代码如下：

```php
<?php
//        数据库类型:host=IP地址;port=端口号;charset=字符集;dbname=数据库名
$dsn = 'mysql:host=localhost;port=3306;charset=utf8;dbname=test';
$pdo = new PDO($dsn, 'root', '123abc');

//新增数据的操作
$sql = 'insert into cz_user values (null, "袁崇焕", "abcdefg", "ych@admin.com")';
$re = $pdo->exec($sql);
var_dump( $re ); 

//修改数据操作
$sql = 'update cz_user set name="小红帽" where id=8';
$re = $pdo->exec($sql);
var_dump( $re ); 

//删除数据操作
$sql = 'delete from cz_user where id=1';
$re = $pdo->exec($sql);
var_dump( $re ); 
```



**==小结==**：在程序中，我们使用pdo统一都是使用exec方法来执行**增删改**操作的SQL语句；







## 2.4 查询操作

涉及方法：

【PDO类中】

> **query** (SQL语句)              执行查询操作SQL语句

【PDOStatement类中】

> **fetch** (解析类型)               一次解析一条数据
>
> **fetchAll** ()                         一次性解析所有数据
>
> **rowCount**()                      获取查询出来的数据的总行数
>
> **columnCount**()               获取查询出来的数据的总列数
>
> **fetchObject** ()                 一次解析一行数据。数据为对象类型



**==需求1==**：完成以下操作

1. 使用PDO，查询test数据库中的cz_user表id=3的数据；

**==解答1==**：构建名为code3.php的文件，代码如下：

```php
<?php
    echo "<pre>";
	//连库
    $dsn = 'mysql:host=localhost;port=3306;charset=utf8;dbname=test';
	//创建对象 此对象属于类PDO
    $pdo = new PDO($dsn, 'root', '123abc');

    //查询test数据库中的cz_user表id=3的数据
    $sql = 'select * from cz_user where id=3';
    $pdostatement = $pdo->query($sql);
    var_dump( $pdostatement ); echo '<hr/>';

    //$row = $pdostatement->fetch();//不指定就是默认情况
    $row = $pdostatement->fetch(PDO::FETCH_ASSOC);   //★★★
    //$row = $pdostatement->fetch(PDO::FETCH_BOTH);
    //$row = $pdostatement->fetch(PDO::FETCH_NUM);
    //$row = $pdostatement->fetch(PDO::FETCH_OBJ);
    echo '<pre>';
    print_r( $row ); echo '<hr/>';


    $row = $pdostatement->fetch(PDO::FETCH_ASSOC);
    echo '<pre>';
    var_dump( $row ); echo '<hr/>';


    /*
    1） fetch方法一次执行只能解析一条数据；
    2）如果不指定参数，则默认情况下将会返回一个既包含关联数组元素又包含索引数组元素的一维数组；
    3）fetch方法还可以指定解析数据的参数：
        PDO::FETCH_ASSOC      如果指定这个参数，则表示解析的数据是一个关联类型的数组
        PDO::FETCH_BOTH      这个参数表示既包含关联类型的数组元素又包含索引类型的数组元素的数组，不指定参数其实默认情况就是这个值
        PDO::FETCH_NUM          这个参数表示将会获得索引类型的数组数据
        PDO::FETCH_OBJ         这个参数表示将会获得对象类型的数据，包含所有的查询数据
    */

```

访问code3.php,效果：

![10](\images\two\img_d20\10.jpg)



**==小结1==**：

1. fetch方法每次执行只能得到一条数据

2. fetch方法还可以指定相应参数

   1) **PDO::FETCH_ASSOC** 如果指定这个参数，则表示解析的数据是一个关联类型的数组
   2) PDO::FETCH_BOTH 默认 这个参数表示既包含关联类型的数组元素又包含索引类型的数组元素的数组，不指定参数其实默认情况就是这个值
   3) PDO::FETCH_NUM 解析的数据是一个索引类型的数组
   4) PDO::FETCH_OBJ    解析的数据是一个对象类型的数据，包含了所有的查询数据





**==需求2==**：完成以下操作

1. 使用PDO，查询test数据库中的cz_user表id<7的所有数据；

**==解答2==**：构建名为code4.php的文件，代码如下：

```php
<?php 
	$dsn = "mysql:host=localhost;port=3306;charset=utf8;dbname=test";
	$pdo = new PDO($dsn,'root','123abc');

	$sql = "select * from cz_user where id<7";
	$pdostatement = $pdo->query($sql);
	//var_dump($pdostatement);
	$rows = $pdostatement->fetchAll();//一次性解析得到所有查询的数据
	echo "<pre>";
	var_dump($rows);
```



**==小结2==**：

1. fetchAll一次执行将会得到所有查询出来的数据
2. 他是一个二维数组，每个小数组既包含关联类型的元素,又包含索引类型的元素



**==需求3==**：完成以下操作

1. 使用PDO，查询test数据库中的cz_user表id<7的数据一共有几行；

**==解答3==**：构建名为code5.php的文件，代码如下：

```php
<?php
//        数据库类型:host=IP地址;port=端口号;charset=字符集;dbname=数据库名
$dsn = 'mysql:host=localhost;port=3306;charset=utf8;dbname=test';
$pdo = new PDO($dsn, 'root', '123abc');

$sql = 'select * from cz_user where id<7';
$pdostatement = $pdo->query($sql);
var_dump( $pdostatement ); echo '<hr/>';

//查询总共有多少行数据
$rowCount = $pdostatement->rowCount();
var_dump( $rowCount ); 
```

访问code5.php的效果：

![5](\images\two\img_d20\5.jpg)

**==小结3==**：

rowCount方法能够获得查询结果中总共行数；





**==需求4==**：完成以下操作

1. 使用PDO，查询test数据库中的cz_user表id<7的数据一共有几列；

**==解答4==**：构建名为code6.php的文件，代码如下：

```php
<?php
//        数据库类型:host=IP地址;port=端口号;charset=字符集;dbname=数据库名
$dsn = 'mysql:host=localhost;port=3306;charset=utf8;dbname=test';
$pdo = new PDO($dsn, 'root', '123abc');

$sql = 'select * from cz_user where id<7';
$pdostatement = $pdo->query($sql);
var_dump( $pdostatement ); echo '<hr/>';

//查询总共有多少列数据
$columnCount = $pdostatement->columnCount();
var_dump( $columnCount ); 
```

访问code6.php , 效果:

![6](\images\two\img_d20\6.jpg)

**==小结4==**：

columnCount方法能够获得查询结果中总共有多少列（字段）;





**==需求5==**：完成以下操作

1. 使用PDO中的fetchObject方法，查询test数据库中的cz_user表id=6的数据，查看打印效果；

**==解答5==**：构建名为code7.php的文件，代码如下：

```php
<?php 
	$dsn = 'mysql:host=localhost;port=3306;charset=utf8;dbname=day14';
	$pdo = new PDO($dsn,'root','123abc');

	$sql = "select * from stu3";
	

	$pdostatement = $pdo->query($sql);
	var_dump($pdostatement);echo "<hr>";
	
	echo "<pre>";
	$rows = $pdostatement -> columnCount();//一次性结得到所有查询的数据
	print_r($rows);echo "<hr>";
```

访问code6.php , 效果:

![6](\images\two\img_d20\6.jpg)



需求：

```php
<?php
//        数据库类型:host=IP地址;port=端口号;charset=字符集;dbname=数据库名
$dsn = 'mysql:host=localhost;port=3306;charset=utf8;dbname=test';
$pdo = new PDO($dsn, 'root', '123abc');

$sql = 'select * from cz_user where id=6';
$pdostatement = $pdo->query($sql);
var_dump( $pdostatement ); echo '<hr/>';

//返回一行对象类型的数据
$obj = $pdostatement->fetchObject();
echo '<pre>';
print_r($obj);
```

访问code7.php , 效果:

![7](\images\two\img_d20\7.jpg)

**==小结5==**：

这个方法的效果和fetch方法指定PDO::FETCH_OBJ是一样的。





# 3.PDO中的事务

## 3.1 MYSQL客户端中的事务

我们以zhangsan向lisi借钱为例子，如果要想在数据库实现zhangsan向lisi借100元钱，则过程应该是：

首先lisi的money需要减少100，必须要执行成功如下的SQL语句：

update user set money=money-100 where name='lisi';

 

其次,zhangsan的money需要增加100，必须要执行成功如下SQL语句：

update user set money=money+100 where name='zhangsan';

 

这个过程，必须是两条SQL语句同时都执行成功，才算是借钱成功，只要中途有任何一个执行不成功，都不能算借钱成功。



**提前准备**：

```PHP
#user表
create table user(
id int unsigned primary key auto_increment,
name varchar(30) not null default '',
money decimal(10, 2) not null default 0
)engine=Innodb charset=utf8;

#user表的两条数据
insert into user values (null, 'zhangsan', 1000);
insert into user values (null, 'lisi', 1000);
```



**==需求==**：使用黑窗口实现成功借钱的例子；

**==步骤==**：

1. 开启事务，开启事务的语句：

```mysql
start transaction;
```

![11](\images\two\img_d20\11.jpg)

2. 执行第一个子过程，让lisi的账户减少100

![12](\images\two\img_d20\12.jpg)

3. 执行第二个子过程，让zhangsan的账户增加100

![13](\images\two\img_d20\13.jpg)

4. 提交事务，提交事务的语句：

```mysql
commit;
```

![14](\images\two\img_d20\14.jpg)



**==需求==**：使用黑窗口实现失败借钱的例子；

**==步骤==**：

1. 开启事务，开启事务的语句：

![11](\images\two\img_d20\11.jpg)

执行第一个子过程，让lisi的账户减少100

![15](\images\two\img_d20\15.jpg)

这个时候lisi的媳妇杀出来，组织借钱，所以我们需要让整个事务失效

3. 回滚事务，回滚事务的语法：

```mysql
rollback;
```

![16](\images\two\img_d20\16.jpg)



**小结**：要想在mysql中实现事务，则：

1. 需要先开启事务：start transaction;
2. 然后执行事务的子过程语句
3. 如果所有子过程都没有问题则提交事务；如果子过程中有任何一个出现而难题，则回滚事务：rollback;





## 3.2 使用PDO实现事务

**==需求==**：使用PDO实现借钱的例子；

**==步骤==**：构建code8.php程序文件，代码如下：

```php
<?php

#实例化PDO类的对象
$dsn = 'mysql:host=localhost;port=3306;charset=utf8;dbname=test';
$pdo = new PDO($dsn, 'root', '123abc');

#1. 开启事务
$pdo->beginTransaction();

#2. 执行子过程
$flag = true;

//让lisi的账户减少100块
$sql = 'update useeeeeeeeer set money=money-100 where name="lisi"';
$re = $pdo->exec($sql);

if( !$re ){
    $flag = false;
}

//让zhangsan的账户增加100块
$sql = 'update user set money=money+100 where name="zhangsan"';
$re = $pdo->exec($sql);

if( !$re ){
    $flag = false;
}

#3. 根据$flag判断执行回滚操作还是执行提交操作
if( $flag ){//$flag为true则应该提交事务
    $pdo->commit();
}else{//$flag为false则应该回滚事务
    $pdo->rollBack();
}

echo '事务执行完毕！'; 
```



**小结**：事务其实就是把零散的过程打包成一个完整的过程，每一个字过程成功则整个事务才算成功，如果有一个子过程失败，则整个事务失败。

**注意**：如果要使用事务则数据表一定要是innodb引擎



# 4.PDO中的预处理技术

## 4.1 why使用预处理技术

在MYSQL中，其标准的执行SQL语句的流程是：

1. 构建SQL语句；
2. 通过黑窗口客户端发送SQL语句到MYSQL服务器；
3. MYSQL服务器接收SQL语句；
4. 解析SQL语句；
5. 执行SQL语句；
6. 将执行的结果返回；



在通常的情况下，无论我们在MYSQL中执行的是不是相同的操作，MYSQL都会每次去重新解析完整的SQL语句，那么，如果当我们的操作，每次执行的都是相同的，只不过数据不同，如下面新增数据的SQL语句：

```php
insert into cz_user values (null, 'zhangsan', 'aa','ls@admin.com');
insert into cz_user values (null, 'lisi', 'bb','ls@admin.com');
insert into cz_user values (null, 'wangwu', 'cc','ls@admin.com');
insert into cz_user values (null, 'zhaoliu', 'dd','ls@admin.com');
```

都是向cz_user表执行新增数据的动作，只不过每次新增的数据不同而已。但是MYSQL依然会每次都完整的去解析这些SQL语句。

 

这样就造成每次都重复的解析了相同的操作，浪费了一定的时间。所以，在MYSQL中，提供了一种名为预处理的技术，这个技术就是专门用来优化上述问题的技术。



## 4.2 MYSQL客户端实现预处理技术

### 4.2.1 不带参数的预处理

涉及的语句语法：

> 构建预处理语句语法：**prepare**  预处理语句名 **from**  “SQL语句”;
>
> 执行预处理语句语法：**execute**  预处理语句名;
>
> 删除预处理语句语法： **drop prepare**  预处理语句名;



**==需求==**：使用预处理技术执行"select * from cz_user"SQL语句；

**==步骤==**：

1. 构建预处理语句

![17](\images\two\img_d20\17.jpg)

2. 执行与处理语句语法：

![18](\images\two\img_d20\18.jpg)

3. 删除预处理语句

![19](\images\two\img_d20\19.jpg)



**==小结==**：本质上预处理技术就是将需要反复执行的SQL语句记录到MYSQL服务器端，以后需要执行，则指定这个被记录下来的预处理语句的名字即可；



### 4.2.2 携带参数的预处理

涉及的语句语法：

> 构建预处理语句语法：**prepare**  预处理语句名 **from**  "SQL语句";
>
> 新增参数数据语句语法： **set** @变量名=变量值；
>
> 执行预处理语句语法：**execute**  预处理语句名 **using**  @变量1,@变量2,...,@变量n ;
>
> 删除预处理语句语法： **drop prepare**  预处理语句名;



**==需求==**：使用预处理技术实现往cz_user表中添加数据；

**==步骤==**：

1. 构建预处理SQL语句

![20](\images\two\img_d20\20.jpg)

2. 准备数据

![21](\images\two\img_d20\21.jpg)

3. 携带参数执行预处理语句

![22](\images\two\img_d20\22.jpg)

4. 删除预处理语句

![23](\images\two\img_d20\23.jpg)

==**小结**==：携带参数的预处理技术在执行预处理SQL语句时是需要携带上参数数据的。



## PDO中实现预处理技术

涉及的方法：

【PDO类中】

> **prepare**  (SQL语句)     生成预处理语句

【PDOStatement类中】

> **bindParam**  (参数序号 ,$参数值)      绑定参数
>
> **execute** ([参数集合])     执行预处理语句



**==需求==**：使用PDO实现用预处理技术往cz_user表中添加数据，要求

1. 使用序号绑定参数的方式实现一次；
2. 使用"：字段名"绑定参数的方式实现一次；
3. 使用数组绑定参数的方式实现一次；

**==解答1==**：构建code9.php程序文件，代码如下：

```php
<?php

#实例化PDO类的对象
$dsn = 'mysql:host=localhost;port=3306;charset=utf8;dbname=test';
$pdo = new PDO($dsn, 'root', '123abc');

#1. 准备预处理语句
$sql = 'insert into cz_user values (null, ?, ?, ?)';
$pdostatement = $pdo->prepare($sql);

#2. 绑定参数
$name = '小霸王';
$pwd = '11aacc';
$email = 'xbw@admin.com';

$pdostatement->bindParam(1, $name);//1表示对应着第一个占位符
$pdostatement->bindParam(2, $pwd);//2表示对应着第二个占位符
$pdostatement->bindParam(3, $email);//3表示对应着第三个占位符

#3. 执行预处理语句
$re = $pdostatement->execute();
if( $re ){//执行成功
    echo '成功了哟'; 
}else{//执行失败
    echo '再接再厉'; 
}
```



==**解答2**==：

```php
<?php

#实例化PDO类的对象
$dsn = 'mysql:host=localhost;port=3306;charset=utf8;dbname=test';
$pdo = new PDO($dsn, 'root', '123abc');

#1. 准备预处理语句
$sql = 'insert into cz_user values (null, :name, :pwd, :email)';//使用“:”+字段名的形式构建占位符
$pdostatement = $pdo->prepare($sql);

#2. 绑定参数
$name = '小笨笨';
$pwd = '778899';
$email = 'xbb@admin.com';

$pdostatement->bindParam(':name', $name);//绑定参数时需要指定具体的占位符名字
$pdostatement->bindParam(':pwd', $pwd);
$pdostatement->bindParam(':email', $email);

#3. 执行预处理语句
$re = $pdostatement->execute();
if( $re ){//执行成功
    echo '成功了哟'; 
}else{//执行失败
    echo '再接再厉'; 
```



==**解答3**==：

```php
<?php

#实例化PDO类的对象
$dsn = 'mysql:host=localhost;port=3306;charset=utf8;dbname=test';
$pdo = new PDO($dsn, 'root', '123abc');

#1. 准备预处理语句
$sql = 'insert into cz_user values (null, :name, :pwd, :email)';//使用“:”+字段名的形式构建占位符
$pdostatement = $pdo->prepare($sql);

#2. 绑定参数
$arr = [
    ':name' => '小可爱',
    ':pwd' => '119900',
    ':email' => 'xka@admin.com'
];

#3. 执行预处理语句
$re = $pdostatement->execute($arr);//直接指定绑定参数的数组作为execute方法的参数即可
if( $re ){//执行成功
    echo '成功了哟'; 
}else{//执行失败
    echo '再接再厉'; 
}
```



==**小结**==：最好用的一种方式是使用数组的方式绑定占位符就的参数数据。





# 5.PDO中的异常处理

"异常"两个字的意思，我们可以理解为错误，它可以是执行时出现的错误，也可以是逻辑错误。



## 5.1 PHP中的异常

在PHP中，我们可以使用if..else判断来实现对逻辑错误的处理，其实，我们也可以使用异常的方式来同样实现对逻辑错误的处理。



PHP中有一个内置异常类Exception，我们可以通过这个类实现PHP中的异常，手册中的位置如下图： 

![24](\images\two\img_d20\24.jpg)



**==需求==**：实现逻辑判断，当价格小于0时，则输出提示信息"商品价格不能小于0！"，要求

1. 使用if..else的方式实现一次；
2. 使用PHP中的异常处理方式实现一次；

**==解答==**：构建code12.php程序文件，以if...else的方式来实现，代码如下：

```php
<?php

$price = -10;

if( $price<0 ){//商品的付款金额小于零，逻辑上存在错误
    echo '商品金额不能小于0'; 
    exit;
}
```

构建名为code13.php的文件，以PHP中异常的方式来实现，代码如下：

```php
<?php

$price = -10;

try{

    if( $price<0 ){
        $e = new Exception('商品价格不能小于0！');
        throw($e);
    }

}catch(Exception $a){

    echo $a->getMessage();
    exit;
}

echo '哈哈哈哈';
```

==**小结**==：

![25](\images\two\img_d20\25.jpg)



## 5.2 PDO中的异常

在PDO中，也封装了一个类用于实现对PDO中的错误进行异常处理方式的处理，这个类名字PDOException，它的本质就是继承了PHP的系统类Exception，所以PHP系统类Exception具有的操作，也都被PDOException所拥有。

![26](\images\two\img_d20\26.jpg)



涉及的方法：

【PDO类】

> **setAttribute**(属性名， 属性值)      设置PDO的模式属性

【PDOException类】

> **getMessage**()     获取错误信息



**==需求==**：使用PDO异常处理方式实现执行SQL语句出错的案例。

**==解答==**：构建code14.php程序文件，代码如下：

```php
<?php

#实例化PDO类的对象
$dsn = 'mysql:host=localhost;port=3306;charset=utf8;dbname=test';
$pdo = new PDO($dsn, 'root', '123abc');

#1. 首先必须将错误处理模式改变为异常模式
//$pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_WARNING);//将错误处理模式设置为警告模式
$pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);//将错误处理模式设置为异常处理模式

$sql = 'insert into cz_user valuuuuuuuuuues (null, "xx", "xxxx", "xxxx")';

#2. 构建try...catch结构，将执行SQL语句的代码放入try结构中监听
try{
    $re = $pdo->exec($sql);//监听执行SQL语句的方法
}catch(PDOException $aa){
    echo '出错的时间：' . date('Y-m-d H:i:s') . '<br/>'; 
    echo '错误的信息是：' . $aa->getMessage() . '<br/>';
    echo '错误的错误码值是：' . $aa->getCode() . '<br/>'; 
    echo '错误的行号：' . $aa->getLine() . '<br/>'; 
    echo '错误的文件：' . $aa->getFile(); 
}
```



==**小结**==：

1. 必须先设置错误处理模式为异常模式；
2. 然后需要使用try...catch结构对执行SQL语句的代码进行监听；





## 6. 案例：封装PDO操作类

### 功能分析

1. 连库基本操作（实例化PDO类的对象）
2. 增删改操作；
3. 查一条数据的功能；
4. 查多条数据的功能；
5. 使用PDO异常处理的方式获得错误信息，并且把信息保存到文件中；



### 代码实现

构建名为PDOTool.class.php的程序，代码如下，
