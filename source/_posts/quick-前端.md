---
title: quick-前端
date: 2019-01-08 15:10:47
categories: 
          - quick
tags: 
    - vue&node
    - javascript
    - jquery
---
JavaScript | Ajax | JQuery | Nodejs | Vuejs
<!-- more -->
# JavaScript

## API

> **1.浏览器：HTML、JS、JavaScript**
>
> **2. 浏览器API**
>
> API**是一些预先定义的函数**
>
> **3. Web API**
>
> 浏览器提供的一套操作浏览器功能和页面元素的API（BOM和DOM）

 JavaScript由**ECMAScript**和**DOM**、**BOM**三者组成。

1. **DOM**：文档对象模型（Document Object Model），提供了一些操作html元素的一些编程接口。
2. **BOM** ：浏览器对象模型（Broswer Object Model），主要处理与浏览器进行交互的接口。
3. **ECMAScript**：Javascript是ECMAScript 语言规范的实现，其中核心知识在于**两链一包**（作用域链、原型链、闭包）,这是js知识精华部分。 

> 注意：BOM和DOM都是浏览器提供给js的API,DOM负责操作html,BOM负责操作浏览器对象，一旦离开浏览器这个宿主就没法玩了。例如在nodejs在就不存在DOM和BOM





## BOM

### window.

#### 属性

| 属性                   | 功能                                                         |
| ---------------------- | ------------------------------------------------------------ |
| **window.innerWidth**  | 获取浏览器内部的宽度(不包含浏览器的左右两边边框)             |
| **window.innerHeight** | 获取浏览器内部的高度(不包含浏览器的菜单栏和地址栏以及上下的边框) |
| **window.outerWidth**  | 获取整个浏览器的宽度                                         |
| **window.outerHeight** | 获取整个浏览器的高度                                         |

```html
<script type="text/javascript">
    var str = "<h2></h2>";
        str += "浏览器的宽度：" + window.outerWidth;
        str += "<br />浏览器的高度：" + window.outerHeight;
        str += "<br />浏览器内部的宽度：" + window.innerWidth;
        str += "<br />浏览器内部的高度：" + window.innerHeight;

    document.write(str)
</script>
```



#### 方法

**对话框：**

**window.alert('message')** ： 向浏览器窗口中弹出一个警告提示框

**window.prompt()**：向浏览器窗口中弹出一个用户输入对话框,返回用户输入的值

**window.confirm(message)**：向浏览器窗口中弹出一个用户确认框 如果点击了确定按钮会返回一个true如果点击了取消按钮会返回一个false,一般用在防止用户误删除进行提示。

```html
    <a href="http://baidu.com" onclick="return confirm('确认删除?')">删除</a>
```

注：返回true会跳转到href中，返回false不会跳转



**控制台：**

- **console.clear()** : 清空控制台。
- **console.error()**  : 打印一条错误信息
- **console.table()** : 将数组或对象数据在控制台以表格形式打印
- **console.log()** ： 打印字符串，使用方法比较类似C的printf、PHP的echo等格式输出



**其他：**

**window.open(url,name,options)**：打开一个新窗口

参数：

- url: 新窗口的地址

- name：新窗口名称

- options:窗口的选项，如窗口的高度、宽度等信息。多个选项用逗号分隔。选项如下：

  | channelmode=yes\|no\|1\|0 | 是否使用剧院模式显示窗口。默认为 no。                        |
  | ------------------------- | ------------------------------------------------------------ |
  | directories=yes\|no\|1\|0 | 是否添加目录按钮。默认为 yes。                               |
  | fullscreen=yes\|no\|1\|0  | 是否使用全屏模式显示浏览器。默认是 no。处于全屏模式的窗口必须同时处于剧院模式。 |
  | height=pixels             | 窗口文档显示区的高度。以像素计。                             |
  | left=pixels               | 窗口的 x 坐标。以像素计。                                    |
  | location=yes\|no\|1\|0    | 是否显示地址字段。默认是 yes。                               |
  | menubar=yes\|no\|1\|0     | 是否显示菜单栏。默认是 yes。                                 |
  | resizable=yes\|no\|1\|0   | 窗口是否可调节尺寸。默认是 yes。                             |
  | scrollbars=yes\|no\|1\|0  | 是否显示滚动条。默认是 yes。                                 |
  | status=yes\|no\|1\|0      | 是否添加状态栏。默认是 yes。                                 |
  | titlebar=yes\|no\|1\|0    | 是否显示标题栏。默认是 yes。                                 |
  | toolbar=yes\|no\|1\|0     | 是否显示浏览器的工具栏。默认是 yes。                         |
  | top=pixels                | 窗口的 y 坐标。                                              |
  | width=pixels              | 窗口的文档显示区的宽度。以像素计                             |

- **window.close()：**关闭当前浏览器窗口

##### 定时器

- **setTimeout(函数，时间)：** 定时器

在指定的毫秒数到达之后执行指定的函数，只执行一次

基本语法：

```javascript
setTimeout('start()',3000)
```



- **setInterval(函数，时间)：** 定时器

定时调用的函数，可以按照给定的时间(单位毫秒)周期调用函数，触发N次

基本语法：

```javascript
setInterval('start()',3000)
```



清除定时器：

① setTimeout() => clearTimeout()

② setInterval() => clearInterval()

基本语法：

```javascript
var s1 = setTimeout(‘display()’,3000);
clearTimeout(s1);

var s2 = setInterval(‘display()’,3000);
clearInterval(s2);
```



setTimeout递归调用：

![64](\images\64.jpg)







### screen.

screen对象： 屏幕对象 它可以获取到与屏幕相关的数据。比如：屏幕的分辨率

属性：

通过浏览器查看：

![1](\images\2.png)

其中较重要属性：

| **属性名**        | **功能**       |
| ----------------- | -------------- |
| **screen.width**  | 获取屏幕的宽度 |
| **screen.height** | 获取屏幕的高度 |



### navigator.

navigator对象： 浏览器对象 它可以获取到浏览器的相关数据。比如浏览器的名称、版本等等

在浏览器控制台输入navigator，即可查看到所有的属性：

![1](\images\1.png)

两个重要的属性：

| 属性名               | 功能                               |
| -------------------- | ---------------------------------- |
| navigator.appName    | 获取到浏览器官方名称               |
| navigator.appVersion | 获取到浏览器的版本内核等信息       |
| navigator.userAgent  | 获取到浏览器的版本内核、组织等信息 |

谷歌chrome浏览器测试如下:

![3](\images\3.png)

Mozilla:是组织名称

netscape：网景公司



- 案例：判断是否是IE浏览器

```html
<script type="text/javascript">
function isIE(){
	var userAgent = navigator.userAgent; //取得浏览器的userAgent字符串  
	// userAgent.indexOf("MSIE") > -1 //IE11以下浏览器  
	// userAgent.indexOf('Trident') > -1 //IE11没有MSIE字样，但有Trident字样
	// userAgent.indexOf('Edge') > -1 //判断是否IE的Edge浏览器  
	if(userAgent.indexOf("MSIE") > -1 || userAgent.indexOf('Trident') > -1 || userAgent.indexOf('Edge') > -1 ){
		return true;
	}else{
		return false;
	}
}

if( isIE() ){
	alert('是');
}else{
	alert('不是');
}
</script>
```



### Location.

history对象： 历史对象，它主要是用来记录浏览器的访问历史记录！,也可以进行页面重定向

**注意：**只有访问过后才会有历史记录



**1. Location对象属性**

 如：访问百度

访问后在控制台输入location，获取url相关信息

![4](\images\4.png)



利用 location对象的href属性，可以实现页面的重定向

| 属性名            | 功能                                  |
| ----------------- | ------------------------------------- |
| location.href获取 | 设置或者获取到浏览器地址栏中的URL地址 |

- location.href = url;  往url地址中进行跳转

**2. location对象的方法**

| 方法名            | 功能         |
| ----------------- | ------------ |
| location.reload() | 刷新当前页面 |



### history.

注意：只有访问过页面后才会有历史对象

history对象的方法

| 方法名                   | 功能                              |
| ------------------------ | --------------------------------- |
| history.back()[重点掌握] | 加载上一个URL页面   后退          |
| history.forward()        | 加载下一个URL页面  前进           |
| history.go(n)            | 加载history列表中的某个具体的页面 |

- **history.go(1) **相当于 **history.forward()**
- **history.go(-1) 相当于 ** **history.back()**

![5](\images\5.png)

- **location.reload()**

 



## DOM

> **1. 什么是DOM模型**
>
> DOM是JS操作网页的接口，全称为“文档对象模型(Document Object Model)”。它的作用是将玩野转为一个JavaScript对象，从而可以用脚本进行各种操作

### document.

| 对象名                   | 功能                                |
| ------------------------ | ----------------------------------- |
| document.documentElement | 获取到根元素 html标签               |
| document.body            | 获取到body标签对象                  |
| document.forms           | 获取到所有表单元素 返回是一个集合   |
| document.images          | 获取到所有的图片元素 返回是一个集合 |
| document.domain          | 获取当前文档的域名。                |
| document. title          | 获取当前文档的标题。                |
| document. url            | 获取当前文档的 URL。                |

> 注：凡是在JS中遇到“集合”两字  它就类似于数组   它的访问方式与数组一样  需要通过下标来访问。
>
> 如果要查询更多的属性可以在浏览器控制台进行打印document即可。



#### 获取元素

| 方法名                                       | 功能                                                         |
| -------------------------------------------- | ------------------------------------------------------------ |
| document.getElementById(id)                  | 通过**id的属性值**来获取元素,它只能获取到一个元素            |
| document.getElementsByTagName(tag)           | 通过**标签名**来获取元素  它返回是一个**数组**    如果要访问其中的某一个标签对象 要**使用下标来访问**！ |
| document.getElementsByName(name)             | 通过**标签的name属性值**来获取元素  它返回是一个**数组**    如果要访问其中的某一个标签对象 要使**用下标来访问**！ |
| document.getElementsByClassName(class)       | 通过**类名**获取元素，返回对象集合。注意：此方法IE8及以下版本浏览器不支持 |
| document.querySelector(#id/.类名)            | 返回匹配到id元素，id前面需要加#号，类似于css的ID选择器       |
| document.querySelectorAll(.类名/标签名/层级) | 获取**某一类元素**，返回匹配到的对象集合，同样需要下标获取指定的元素 |
| document.createElement(标签名)               | 创建节点元素                                                 |
| document.createTextNode(文本)                | 创建文本节点，一般用`节点对象.innerHTML`                     |



### dom对象

#### 属性

##### **obj.内容**

| 属性                  | 描述                                                    |
| --------------------- | ------------------------------------------------------- |
| **dom对象.innerHTML** | 获取非表单元素内容,包含标签.如:a,h1-h6,div,li,span,p..  |
| **dom对象.innerText** | 获取非表单元素内容，不包含标签。                        |
| **dom对象.value**     | 获取表单元素的值如:input,textarea,radio,checkbox,select |
| **dom对象.className** | 获取dom对象的class类名                                  |

##### **.obj父子查找**

| 属性                            | 描述                           |
| ------------------------------- | ------------------------------ |
| **父节点.firstElementChild**    | 获取父节点的第一个子节点       |
| **父节点.lastElementChild**     | 获取父节点的最后一个子节点     |
| **父节点.children**             | 获取父节点所有的子节点         |
| **节点.nextElementSibling**     | 找当前节点对象的下一个兄弟节点 |
| **节点.previousElementSibling** | 找当前节点对象的上一个兄弟节点 |

> 小技巧：想查看更多属性可以用console.dir(dom对象)进行打印查看



#### 方法

##### **attr操作**     

k:属性名（可以是自定义属性）v:属性值

| 方法                           | 描述     |
| ------------------------------ | -------- |
| **dom对象.setAttribute(k,v)**  | 设置属性 |
| **dom对象.getAttribute(k)**    | 获取属性 |
| **dom对象.removeAttribute(k)** | 删除属性 |

##### 增删克隆

| 方法                                           | 描述                                                   |
| ---------------------------------------------- | ------------------------------------------------------ |
| **父节点.appendChild(子节点)**                 | 在父节点后面追加子节点                                 |
| **父节点.insertBefore(新节点,老节点)**         | 在父节点之前插入新节点到老节点之前                     |
| **dom对象.parentElement.removeChild(dom对象)** | 删除节点                                               |
| **dom对象.cloneNode()**                        | 浅克隆；只克隆dom对象标签本身                          |
| **dom对象.cloneNode(true)**                    | 深克隆；克隆dom对象标签整体（包含dom对象内部所有元素） |

##### style操作

通过DOM对象的style属性可以对标签的style样式进行操作。

```javascript
DOM对象.style.fontSize = '50px';  //# 设置字体大小为50px
DOM对象.style.backgroundColor = 'green'; // 设置背景色为绿色，值设为16进制如#00ff00也行
```

style操作样式和js操作样式的转化（驼峰法），如果CSS属性中有中划线要去掉，并且将中划线后面首字母改为大写。如下：

```html
css写法: background-color    js写法：backgroundColor
css写法: font-size           js写法：fontSize
```

> **注意：**JavaScript它只能操作标签的行内样式！即style。





------



## JS方法

### String

| 属性                       | 描述                                                         |
| -------------------------- | ------------------------------------------------------------ |
| `strVariable`.**length**   | 指出 **String** 对象中的字符数。**String**  对象中的最后一个字符的索引为 **length** - 1。 |
| `objectName`.**prototype** | 用 **prototype** 属性提供对象的类的一组基本功能。对象的新实例“继承”赋予该对象原型的操作。 |
| `object`.**constructor**   | **constructor** 属性是所有具有 prototype 的对象的成员。      |



#### 1. 字符串—数组 转换

| 方法        | 描述                                   |
| ----------- | -------------------------------------- |
| **join()**  | 把数组粘合成一个字符串。返回值：字符串 |
| **split()** | 把字符串打散为数组                     |

**join()**

```javascript
arr.join(separator)

var arr = ['a','b','c'];
console.log(arr.join('-'));  // 'a-b-c'
console.log(arr.join(''));  // 'abc'
console.log(arr.join());  // 'a,b,c'
```

**split()**

```javascript
str.split([delimiter][, limit])

var str = "Hello?World!";
console.log(str.split()); // ["Hello?World!"]
console.log(str.split('?')); // ["Hello", "World!"]
console.log(str.split('')); // ["H","e","l","l","o","?","W","o","r","l","d","!"]
console.log(str.split('',5)); // ["H","e","l","l","o"]
```



#### 2. 除空白

| 方法       | 描述                                 |
| ---------- | ------------------------------------ |
| **trim()** | 移除字符串两侧的空白字符和其他字符。 |

**trim()**

```javascript
str.trim()

var str = '   a b c  ';
console.log( str.trim() );	// 'a b c'
console.log( str ); 	// '   abc  '
```



#### 3. 截取

| 方法            | 描述                                                         |
| --------------- | ------------------------------------------------------------ |
| **substr()**    | 用于截知道位置 从哪到哪截。 返回 str 中从**指定位置开始**到**指定长度**的子字符串，start可为负值 |
| **substring()** | 返回从 start 到 end（不包括）之间的字符，start、end均为 非负整数。若结束参数(end)省略，则表示从start位置一直截取到最后。 |
| **slice()**     | 返回从 start 到 end （不包括）之间的字符，可传负值           |

**substr()**

```javascript
str.substr(start[,length])

var str = "javascript";
console.log(str.substr(5,3));  // "cri"
console.log(str.substr(-4,2));  // "ri"
```

**substring()**

```javascript
str.substring(start[, end])

var str = 'javascript';
console.log(str.substring(1,4)); //"ava"
console.log(str.substring(1));  // "avascript"
```

**slice()**

```javascript
str.slice(start[,end])

var str = 'this is awesome';
console.log(str.slice(1,3));  // "hi"
console.log(str.slice(10,-1));  // "esom"
console.log(str.slice(10,-2));  // "eso"
```



#### 4. 大小写转换

| 方法              | 描述                                                         |
| ----------------- | ------------------------------------------------------------ |
| **toLowerCase()** | 将 str 转换为小写，并返回 str 的一个副本，不影响字符串本身的值 |
| **toUpperCase()** | 将 str 转换为大写，并返回 str 的一个副本，不影响字符串本身的值 |

**toLowerCase()**

```javascript
str.toLowerCase()

var str = 'JavaScript';
console.log( str.toLowerCase() ); // 'javascript'
console.log(str);  // 'JavaScript'
```

**toUpperCase()**

```javascript
str.toUpperCase()

var str = 'JavaScript';
console.log( str.toUpperCase() ); // 'JAVASCRIPT'
console.log(str);  // 'JavaScript'
```



#### 5. 查找

| 方法              | 描述                                                         |
| ----------------- | ------------------------------------------------------------ |
| **indexOf()**     | 返回indexOf()在字符串 str 中首次出现的位置,从 start 位置开始查找，如果不存在，则返回 -1。start可以是任意整数，默认值为 0。 |
| **lastIndexOf()** | 返回lastIndexOf在字符串 str 中最后出现的位置,从 start 位置 向前开始查找，如果不存在，则返回 -1。 |
| **charAt()**      | 返回字符串的第 n 个字符，如果不在 0~str.length-1之间，则返回一个空字符串。 |

**indexOf()**

```javascript
indexOf(substr[,start])

var str = "javascript";
console.log( str.indexOf('s') );   // 4
console.log( str.indexOf('php',5) ); // -1
console.log( str.indexOf('a',2) );  // 3
```

**lastIndexOf()**

```javascript
lastIndexOf(substr[,start])

console.log( 'javascript'.lastIndexOf('a') ); // 3
console.log( 'javascript'.lastIndexOf('o') ); // -1
```

**charAt()**

```javascript
str.charAt(n)

var str = "javascript";
console.log( str.charAt(5) ); // 'c'
console.log( str.charAt(15) ); // ''
```



#### 6. 替换

| 函数          | 描述                |
| ------------- | ------------------- |
| **replace()** | 替换 str 的子字符串 |

**replace()**

```javascript
str.replace(regexp|substr, newSubStr|function)

//普通替换
var str = "i love you";
console.log( str.replace('love','hate') );  // "i hate you"

//正则替换
var tel = '13534566789'; 
var reg = /(\d{3})\d{4}(\d{4})/g;
console.log( tel.replace(reg,"$1****$2") );  // 135****6789

//驼峰转换
function strCovert(css){
    //定义一个正则尽可能找到我们要替换的内容
    var reg = /-([a-z])/g;
    var newStr = css.replace(reg,function($0,$1){
        //$0:代表正则匹配的结果
        //$1:代表正则匹配的第1个括号中的结果
        console.log('$0:',$0); // -b -c 
        console.log('$1:',$1); // b  c 
        return $1.toUpperCase();
    });
    return newStr; 
}
var css = 'border-bottom-color'; 
console.log(strCovert(css)); //"borderBottomColor"
```



#### 7. 其他

| 函数         | 描述                         |
| ------------ | ---------------------------- |
| **repeat()** | 重复一个str字符串length次    |
| **concat()** | 将value与字符串str拼接在一起 |

 **repeat()**

```javascript
str.repeat(length)

console.log( '*'.repeat(3) ); //***
console.log( 'php'.repeat(3) ); //phpphpphp
```

**concat()**

```javascript
str.concat(value，...)

var str = 'JavaScript';
console.log( str.concat('php','mysql') ); // JavaScriptphpmysql
```



### Array



#### 1. 排序

| 函数       | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| **sort()** | 对数组进行排序，指定回调函数callback进行排序 。返回值：对数组的引用。注意，数组在原数组上进行排序，不制作副本。 |

**sort()**

```javascript
arr.sort(callback)

var arr = [14,8,24];
arr.sort( function(a,b){ 
    return a-b; // 或return  a>b   
}) ;  
console.log(arr);  // [8, 14, 24]  升序

var arr = [14,8,24];
arr.sort(function(a,b){ 
	return b-a; //  或return b>a  
}) ;  
console.log(arr); //[24, 14, 8] 降序
```



#### 2. 操作

| 函数           | 描述                                                         |
| -------------- | ------------------------------------------------------------ |
| **push()**     | 向数组尾部添加一个或多个元素 ，成功返回数组的新长度  。(增)  |
| **unshift()**  | 向数组头部添加一个或多个元素 ，成功返回数组的新长度。  (增)  |
| **pop()**      | 将删除arr的最后一个元素，把数组长度减1，并且返回它删除的元素的值。如果数组已经为空，则pop()不改变数组，返回undefined。  (删) |
| **shift()**    | 方法shift()将把arr的第—个元素移出数组，并返回那个元素的值，并且将余下的所有元素前移一位，以填补数组头部的空缺 。 (删) |
| **splice()**   | 从一个数组中移除一个或多个元素，如果必要，在所移除元素的位置上插入新元素，返回所移除的元素。(删，改) |
| **reverse()**  | 将元素的顺序颠倒。索引下标重新规划下标(改)                   |
| **concat()**   | 将两个数组合并。索引下标重新规划下标(改)                     |
| **includes()** | 用来判断一个数组是否包含一个指定的值，如果是返回 true，否则false。 (查) |
| **indexOf()**  | 返回某个指定的字符串值在字符串中首次出现的位置。 (查)        |

**push()**

```javascript
arr.push(value,...)

var arr = ['a','b','c'];
console.log( arr.push('d') ); // 4
console.log( arr.push('e','f') ); // 6
console.log(arr); //["a","b","c","d","e","f"]
```

**unshift()**

```javascript
arr.unshift(value,...)

var arr = ['a','b','c'];
console.log( arr.unshift('d') ); // 4
console.log( arr.unshift('e','f') ); // 6
console.log(arr); // ["e","f","d","a","b","c"]
```

**pop()**

```javascript
arr.pop()

var arr = ['a','b','c'];
console.log(arr.pop()); // c
console.log(arr.pop()); // b
console.log(arr.pop()); // a
console.log(arr.pop()); // undefined
```

**shift()**

```javascript
arr.shift()

var arr = ['a','b','c'];
console.log( arr.shift('d') ); // 'a'
console.log(arr); // ["b", "c"]
```

**splice()**

```javascript
//arrayObject.splice(index,howmany,[item1,.....,itemX])
//参数：index:删除项目的位置；howmany:删除项目的个数(0表示不删除);[]:可选。向数组添加的新项目。

arr.splice(2,1)//删除坐标为2的数据
arr.splice(2,0,"William")//表示在坐标为2的地方插入新数据“William”
arr.splice(2,1,"William")//表示把坐标为2的地方的数据改为“William”
arr.splice(2,3,"William")//表示把坐标为2,3,4连续3个数删掉，替换成"William"
```

**reverse()**

```javascript
arr.reverse()

var arr = [1,2,3,4,5];
console.log( arr.reverse() ); // [5,4,3,2,1]
```

**concat()**

```javascript
var arr1 = [1,2,3,4,5];
var arr2 = [6,7,8];
console.log( arr1.concat(arr2) ); // [1,2,3,4,5,6,7,8]
```

**includes()**

```javascript
//arr.includes(searchElement,[fromIndex])
//参数：searchElement:查询的数组内的值；fromIndex:查询的值所在的坐标

[1, 2, 3].includes(2);     // true
[1, 2, 3].includes(4);     // false
[1, 2, 3].includes(3, 3);  // false
[1, 2, 3].includes(3, -1); // true
[1, 2, NaN].includes(NaN); // true
```

#### 3. 其他

| 函数          | 描述                                                         |
| ------------- | ------------------------------------------------------------ |
| **isArray()** | 检测一个变量是否是数组。                                     |
| **foreach()** | 遍历数组元素                                                 |
| **map()**     | 遍历数组，数组里的元素经过指定回调函数进行加工处理。 返回一个新的数组 |
| **filter()**  | 过滤数组中的某些元素，在回调函数中设置条件，不满足的都会被过滤掉，返回一个新数组。 |

**isArray()**  

```javascript
function isArray(value){
    return Object.prototype.toString.call(value) == '[object Array]';
}

var arr = [1,2,3,4,5];
console.log(isArray(arr)); // true
console.log(isArray({})); // false
```

**foreach()**

```javascript
var arr = ['a','b','c'];
arr.forEach(function(v,key){
    //v当前循环的元素 key当前元素的下标
    console.log(key,v)
});
```

**map()**

```javascript
var age = [18,23,28,30];
var newArr = age.map(function(v){
    //给每个元素加10岁
    return v+10;
});
console.log(newArr); // [28, 33, 38, 40]
```

**filter()**  

```javascript
var age = [18,23,28,30];
var newArr = age.filter(function(v){
    //v当前循环的元素
    //返回年龄大于25的元素
    return v>25;
});

console.log(newArr);// [28, 30]
```



### Math

#### **取区间**

在JavaScript中，如果想获取某一范围区间的整数，可以使用如下公式：
$$
[min,max] = Math.floor(Math.random() * (max – min + 1) + min)
$$




## 事件

### 绑定方式

常用的有四种事件绑定方式：

- 行内绑定（静态绑定）：直接写在标签中，<标签名  事件名=“函数名()” />

```html
 <div onclick='deal()' >content</div>
```

- 动态绑定（w3c标准浏览器）：

```javascript
var box = document.getElementById('box'); 
box.onclick = function(){}
```

- 事件监听绑定 (w3c标准浏览器和ie浏览器特有的绑定方式)

```javascript
addEventListener(eventType, handler, useCapture); //w3C
```

> 参数说明：
>
> - eventType 指定事件类型(不要加on) 如：click
>
> - handler事件的处理函数(监听函数)
>
>   ​	注意：如果事件处理函数handler是有名函数，则可以通函数名来移除，匿名函数无法移除。
>
> - useCapture可选。布尔值，指定事件是否在捕获或冒泡阶段执行。
>
>   true 事件监听函数在捕获阶段执行
>
>   false 默认，事件监听函数在冒泡阶段执行



- ie浏览器特有的绑定方式

```javascript
attachEvent(eventType, handler); //IE
```

> 参数说明：
>
> - eventType指定事件类型(注意加前缀on)
> - handler是事件处理函数  



### 常用事件

#### 页面事件

| 属性        | 描述                                                         |
| ----------- | ------------------------------------------------------------ |
| **onload**  | 当页面加载完成后执行，body里面所有元素(包括图片)都加载完后再执行。不能同时编写多个， |
| **onready** | 简写 $(function(){});  DOM结构绘制完毕后就执行 ；可以同时编写多个，并且都可以得到执行 |



#### 鼠标事件

| 属性            | 描述                                 |
| --------------- | ------------------------------------ |
| **onblur**      | 元素**失去焦点**时触发               |
| **onfocus**     | 元素**获取焦点**时触发               |
| **onclick**     | 当用户点击某个对象时调用的事件句柄。 |
| **onmouseover** | 鼠标移到某元素之上。                 |
| **onmouseout**  | 鼠标从某元素移开。                   |
| **onmousedown** | 鼠标按钮被按下。                     |
| **onmouseup**   | 鼠标按键被松开。                     |
| **onmousemove** | 鼠标经过元素时                       |
| **ondblclick**  | 鼠标双击一个对象时                   |



#### 键盘事件

| 属性           | 描述                       |
| -------------- | -------------------------- |
| **onkeydown**  | 某个键盘按键被按下。       |
| **onkeypress** | 某个键盘按键被按下并松开。 |
| **onkeyup**    | 某个键盘按键被松开。       |



#### 框架/对象 事件

| 属性         | 描述                                                |
| ------------ | --------------------------------------------------- |
| **onerror**  | 在加载文档或图像时发生错误。(object,body和frameset) |
| **onload**   | 一张页面或一幅图像完成加载。                        |
| **onresize** | 窗口或框架被重新调整大小。                          |
| **onscroll** | 当文档被滚动时发生的事件。                          |



#### 表单事件

| 属性         | 描述                                                         |
| ------------ | ------------------------------------------------------------ |
| **onsubmit** | 表单**提交**时触发                                           |
| **onselect** | 用户**选取文本**时触发 (input和textarea)                     |
| **onreset**  | 表单**重置**时触发                                           |
| **onchange** | 该事件在表单元素的**内容改变**时触发(input,keygen,select和 textarea) |
| **oninput**  | 元素**获取用户输入**时触发(Chrome/IE9.0/Firefox4.0/Safari5.0/Opera) |
| **onsearch** | 用户向**搜索域输入**文本时触发(<input="search">) (Chrome/Safari/Opera15.0) |



### event

基本语法

```javascript
//IE内核的浏览器
var event = window.event;
//W3C内核的浏览器
dom对象.onclick = function(event){
    event就是w3c内核下的事件对象
}
但是实际项目开发中，为了解决兼容性问题，我们通常按如下形式编写：
dom对象.onclick = function(e){
    var event = window.event||e;
}
```



### 事件代理/委托

使用事件对象的几个属性：

event.target：对事件启用目标的引用，属性返回触发事件的那个节点

event.currentTarget：属性返回事件当前所在的节点，即正在执行的监听函数所绑定的那个节点。



### event方法

| 方法                                                    | 描述                                             |
| ------------------------------------------------------- | ------------------------------------------------ |
| **addEventListener**(eventType, handler, useCapture)    | 绑定监听事件听函数                               |
| **attachEvent**(eventType, handler);                    | IE中事件**绑定**函数                             |
| **removeEventListener**(eventType, handler, useCapture) | 监听事件**移除**事件函数                         |
| **detachEvent**(eventType, handler);                    | IE中事件**移除**事件函数                         |
| event.**stopPropagation**()                             | w3c浏览器的**阻止冒泡**                          |
| event.**cancelBubble** = true;                          | IE浏览器**阻止冒泡**                             |
| event.**preventDefault**()                              | w3c**阻止默认**行为方法                          |
| event.**returnValue** = false;                          | IE**阻止默认**行为方法                           |
| event.**target**                                        | 对事件启用目标的引用，属性返回触发事件的那个节点 |
| event.**currentTarget**                                 | 属性返回事件当前所在的节点                       |



### 事件模型

在JavaScript中事件模型可分为三类：

- DOM0级模型 （原始模型）
- DOM2级模型（w3c标准模型）
- IE事件模型

#### DOM0

- DOM0事件模型又称为原始事件模型
- 在该模型中，事件流阶段有两种：目标阶段和**冒泡阶段**
- DOM0事件模型绑定事件有两种方式：**行内绑定**、**动态绑定**。
- DOM0级的好处：大部分浏览器都支持以上两种的写法,兼容性最好，包括IE。

#### DOM2

- DOM2事件模型也属于事件监听绑定（w3c标准浏览器和ie浏览器特有的绑定方式）。
- 在该事件模型中，事件流有三个阶段:捕获阶段、目标阶段和冒泡阶段

#### IE

- IE事件模型事件流阶段有两种：目标阶段和**冒泡阶段**
- IE事件模型的绑定事件和移除事件



## 正则

### 使用正则

```javascript
var  reg = /pattern/flags;
reg.test(xxxxx);

//例 
var reg = /\./g;
var balance = '100';
reg.test(balance)
```

> 参数说明：
>
> - 其中pattern就是我们的正则规则， 两个斜线/ /称为正则的定界符,flags就是正则标识。
> - flags常用的正则标识有以下几个:
>   - g：代表global表示全局匹配模式，即正则将被应用于匹配整个字符串，不加g只会匹配到第一个就会立即停止向后匹配。
>   - i：代表ignore,匹配的时候，表示不区分大小写。
>   - m: 代表Multiline ，匹配多行。



### 正则语法

#### 元字符

| 代码   | 说明                                                         |
| ------ | ------------------------------------------------------------ |
| **.**  | 匹配除换行符以外的任意字符                                   |
| **\w** | 匹配包括下划线的任何单词字符。等价于'[A-Za-z0-9_]'           |
| **\s** | 匹配任何空白字符，包括空格、制表符、换页符等等。等价于 [ \f\n\r\t\v] |
| **\d** | 匹配一个数字字符。等价于 [0-9]。                             |
| **\b** | 匹配一个单词边界，也就是指单词和空格间的位置。                                       例如， 'er\b' 可以匹配"never" 中的 'er'，但不能匹配 "verb" 中的 'er'。 |
| **^**  | 匹配输入字符串的开始位置。                                   |
| **$**  | 匹配输入字符串的结束位置。                                   |

#### 限定符

| 代码/语法     | 说明                                                         |
| ------------- | ------------------------------------------------------------ |
| **+**         | 匹配前面的子表达式一次或多次。等价于 {1,}。                  |
| *****         | 匹配前面的子表达式零次或多次。等价于{0,}。                   |
| **？**        | 匹配前面的子表达式零次或一次。等价于 {0,1}。                 |
| **{*n*}**     | *n* 是一个非负整数。匹配确定的 *n* 次。                      |
| **{*n*,}**    | *n* 是一个非负整数。至少匹配*n* 次。                         |
| **{*n*,*m*}** | *m* 和 *n* 均为非负整数，其中*n* <= *m*。最少匹配 *n* 次且最多匹配  *m* 次。 |

#### 反义词

| 代码/语法   | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| **\W**      | 匹配任何**非单词字符**。等价于'\[^A-Za-z0-9_]'               |
| **\S**      | 匹配任何**非空白字符**，包括空格、制表符、换页符等等。等价于 \[^ \f\n\r\t\v] |
| **\D**      | 匹配一个**非数字字符**。等价于 \[^0-9]。                     |
| **\B**      | 匹配**非单词边界**，也就是指单词和空格间的位置。例如,'er\b'能匹配 "verb" 中的 'er'，但不能匹配 "never" 中的 'er'。 |
| **\[^abc]** | 匹配除了x、y、z以外的任何字符。同**\[^a-c]**                 |

#### 其他字符

| 代码   | 说明                                                         |
| ------ | ------------------------------------------------------------ |
| **\\** | 如匹配`? () * . @ \ /`等特殊符号，需要在其前面加个反斜杠`\`进行转义 |
| **\|** | 满足竖线左边或右边的其中一个规则即算匹配到。                 |
| **\n** | n是一个非负整数。代表引用正则缓存区中第n个的括号中匹配到内容。 |



### 正则属性

| 属性           | 说明                                                         |
| -------------- | ------------------------------------------------------------ |
| **global**     | 布尔值，表示是否设置了g标识。                                |
| **ignoreCase** | 布尔值，表示是否设置了i标识。                                |
| **multiline**  | 布尔值，表示是否设置了m标识。                                |
| **source**     | 该正则表达式的字符串表示。                                   |
| **lastIndex**  | 整数，表示开始匹配目标字符串的起始下标位置，默认从0开始。如果加了全局标识g，此属性值会受到正则`test`方法或`exec`方法的影响。 |

### 正则方法

| 方法                                     | 说明                                                         |
| ---------------------------------------- | ------------------------------------------------------------ |
| stringobj.**search**(reExp)              | 返回与正则表达式查找内容匹配的第一个子字符串的**位置**       |
| stringObj.**replace**(reExp,replaceText) | 返回根据正则表达式进行文字替换后的字符串的复制。             |
| rgExp.**test**(str)                      | test方法检查在字符串中**是否存在**一个模式，如果存在则返回 **true**,否则就返回 **false**。 |
| *rgExp*.**exec**(str)                    | 用正则表达式模式在字符串中运行查找，并返回包含该查找结果的一个**数组**。 |
| stringObj.**match(**rgExp)               | 使用**正则表达式**模式对字符串执行查找，并将包含查找的结果作为**数组**返回。 |

> 参数描述：
>
> stringObj 
>
> 要执行的 **String** 对象或字符串文字。
>
> rgExp 
>
> 为包含正则表达式模式或可用标志的**正则表达式**对象。
>
> replaceText 
>
> 必选项。替换成什么。
>



## 面向对象

### 对象存储形式

原理图：

![6](\images\6.png)



### 创建对象

#### Object或{}

- 通过`new Object()`方式创建

```javascript
var obj = new Object();

obj.name = "悟空";
obj.age = '500';
obj.getName = function(){
    return this.name+this.age;
}
```

- 通过字面量形式`{}`来创建对象

```javascript
var obj1 = {
    "name":"八戒",
    "age":"400",
    "getName":function(){
        return this.name+this.age;
    }
};
```

#### 工厂方式

```javascript
function createObj(name,age){
    var obj = new Object();
    obj.name = name;
    obj.age = age;
    obj.getName = function(){
        return "姓名："+this.name + "芳龄："+this.age;
    }
    return obj;
}
//调用工厂函数获取对象
var obj1 = createObj('zs',33);
var obj2 = createObj('li',44);
//调用方法
console.log( obj1.getName() );
console.log( obj2.getName() );
```

 

#### 构造函数

```javascript
function Person(name,age){
    this.name = name;
    var age = age;
    this.getName = function(){
        return "大名："+this.name+"年龄："+age;
    }
}

//实例化对象
var p1 = new Person('王大锤','100'); 
console.log(p1);
console.log( p1.getName() );
```

 

#### 构造函数+原型对象组合

```javascript
function Person(name,age){
	this.name = name;
	this.age = age;
}
Person.prototype.getName = function(){
    return "大名："+this.name;
}
Person.prototype.getAge = function(){
    return "年龄："+this.age;
}

//实例化对象
var p1 = new Person('王大锤','100');
var p2 = new Person('王小捶','50');
console.log( p1.getName() );
console.log( p2.getName() );
```


### 设置对象属性

| 对象的属性          | 说明             |
| ------------------- | ---------------- |
| this.attr = ''      | 设置公有属性attr |
| var attr = ''       | 设置私有属性attr |
| classname.attr = '' | 设置静态属性attr |



### 原型链

**原型对象**

当系统加载构造函数的同时，会自动在内存中生成一个对象。我们把这个对象就称之为“原型对象”。

![7](\images\7.png)



### 原型对象检测

| 方法                           | 描述                                                    |
| ------------------------------ | ------------------------------------------------------- |
| obj2.**isPrototypeOf**(obj)    | 检测obj2对象是否是obj对象的原型对象。                   |
| obj.**constructor**            | 检测obj的构造函数,指obj是通过哪个构造函数创建出来的。   |
| 'attr' **in** obj              | 检测一个obj自身空间或原型对象空间是否存在属性attr       |
| obj.**hasOwnProperty**('attr') | 判断当前obj对象空间中是否存在一个属性attr               |
| **delete** obj.attr            | 用于删除自身对象空间obj中的属性attr，不会删除原型上的。 |

### 异步执行

在JS中，代码分为同步执行和异步执行。大部分代码为同步执行，有三种情况为异步：定时器、时间绑定、Ajax



# Ajax

## 创建Ajax

① 基于IE内核的浏览器

```javascript
var xhr = new ActiveXObject(‘Microsoft.XMLHTTP’);
```

② 基于W3C内核的浏览器

```javascript
var xhr = new XMLHttpRequest();
```

**解决Ajax对象的兼容性问题（封装，重点）**:

① 创建一个createXhr函数，用于创建Ajax对象（解决Ajax对象的兼容性问题）

```javascript
function createXhr() {
	//判断window对象下是否具有XMLHttRequest
	if (window.XMLHttpRequest)	
	{	//W3C浏览器
		return new XMLHttpRequest();
	}else{
        //IE内核浏览器
		return new ActiveXObject('Microsoft.XMLHTTP');
	}
}
```

② 调用createXhr函数，获取Ajax对象 "

![68](\images\68.jpg)

## Ajax属性&方法

属性：

- **readyState **： Ajax状态码
  0：表示对象已建立，但未初始化，只是 new 成功获取了对象，但是未调用open方法
  1：表示对象已初始化，但未发送，调用了open方法，但是未调用send方法
  2：已调用send方法进行请求
  3：正在接收数据（接收到一部分），客户端已经接收到了一部分返回的数据
  **4：接收完成，客户端已经接收到了所有数据**
- **status** ：http响应状态码
  200：代表成功获取服务器端数据
  404：未找到页面等等……
- **responseText**：如果服务器端返回字符串，使用responseText进行接收
- responseXML ：如果服务器端返回XML数据，使用responseXML进行接收
- **onreadystatechange**：当 readyState 状态码发生改变时所触发的回调函数

方法：

- **open(method,url,[aycs])**：初始化Ajax对象 (打开)
  method:http请求方式，get/post
  url:请求的服务器地址
  aycs:同步与异步 

- **setRequestHeader(header,value)**：设置请求头信息
  header ：请求头名称
  value ：请求头的值

- **send([content])** ：发送Ajax请求
  content ：如果是get请求时，此参数为null;

  如果是post请求时，此参数就是要传递的数据

  

**注意: 所有相关的事件绑定必须在调用send()方法之前进行.**



## 发送get

get五步走

- 第一步：创建Ajax对象（前提）
- 第二步：设置回调函数onreadystatechange
- 第三步：初始化对象open
- 第四步：发送Ajax请求send
- 第五步：判断与执行xhr.readyState == 4
- 字符串：xhr.responseText
- XML ：xhr.responseXML

 

几个遗漏的小问题：

① 在服务器端，我们都是通过echo进行返回数据的，我们可不可以将其更改为return？

答：不行，Ajax属于客户端语言，所以要求PHP服务器端页面的数据必须返回到客户端浏览器，但是return只能返回数据到PHP服务器端，不能返回到客户端，所以如果使用return作为返回，则客户端接收不到任何数据。

② 当我们发送Ajax请求时，如果服务器端页面不存在，其可以返回数据么？

答：即使页面不存在，Ajax也会返回数据。404



## 缓存问题

### 缓存的产生

原因：
在Ajax的get请求中，如果运行在IE内核的浏览器下，
其如果**向同一个url发送多次请求**时，就会产生所谓的缓存问题。
缓存问题最早设计初衷是为了加快应用程序的访问速度，
但是其会影响Ajax实时的获取服务器端的数据。

### 客户端解决缓存问题

① 产生缓存的问题就是 我们的客户端向同一个 url 发送了多次请求；
如果我们每次请求的url不同，那么，缓存问题就不会存在了；

我们可以在请求地址的后面加上一个无意义的参数，参数值使用时间戳即可，缓存问题就被解决了；

**new Date().getTime()** ： 获取当前时间的毫秒时间戳
修改代码如下：

```javascript
var url = 'demo03.php?username='+username.value+'&_='+new Date().getTime();
xhr.open('get',url);
```



② 设置响应头禁用客户端缓存

服务器端在相应客户端请求时，可以设置相应头详细，如：
header(‘Content-type:text/html; charset=utf-8’) ：告诉客户端浏览器，使用utf-8的编码格式解析页面信息。

在php代码中添加一下代码：

```javascript
//告诉客户端浏览器不要缓存数据
header("Cache-Control: no-cache");
```





## 发送POST

post请求六步走：

- 第一步：创建Ajax对象 var xhr = createXhr()
- 第二步：设置回调函数 xhr.onreadystatechange = function(){}
- 第三步：初始化Ajax对象 xhr.open(‘post’,’demo.php’)
  第四步：设置请求头信息 xhr.setRequestHeader()
- 第五步：发送Ajax请求 xhr.send(data)，send方法在数据行位置
- 第六步：判断与执行 xhr.readyState == 4 && xhr.status == 200

```javascript
//请求地址
var url = 'demo04.php';
//open参数为post
xhr.open('post',url);
//设置请求头
xhr.setRequestHeader('Content-type','application/x-www-form-urlencoded');
//设置post请求参数值
xhr.send('username='+username.value);
```

ajax中get请求与post请求的区别是：
 1：传参方式：
	get请求在url尾部传递参数；
​	post 请求在send()方法中传递参数

 2：请求头：
	post 请求需要生命请求头 **xhr.setRequestHeader('Content-type','application/x-www-form-urlencoded')**
​	get 不需要设置；

 3：参数值类型：
​	get 传参值只能是数字、字符串
	post 可以传递数字、字符串意外，还可以传递二进制数据；





# JQuery

## JQ事件

### 页面事件

| 属性        | 描述                                                |
| ----------- | --------------------------------------------------- |
| **ready()** | 当DOM载入就绪可以查询及操纵时绑定一个要执行的函数。 |



### 鼠标事件

| 属性             | 描述                                 |
| ---------------- | ------------------------------------ |
| **blur()**       | 元素失去焦点时触发                   |
| **focus()**      | 元素获取焦点时触发                   |
| **click()**      | 当用户点击某个对象时调用的事件句柄。 |
| **mouseover()**  | 鼠标移到某元素之上。                 |
| **mouseout()**   | 鼠标从某元素移开。                   |
| **mousedown()**  | 鼠标按钮被按下。                     |
| **mouseup()**    | 鼠标按键被松开。                     |
| **mousemove()**  | 鼠标经过元素时                       |
| **dblclick()**   | 鼠标双击一个对象时                   |
| **mousenter()**  | 当鼠标指针穿过元素时触发,与下同用    |
| **mouseleave()** | 当鼠标指针离开元素时触发,与上同用    |



### 键盘事件

| 属性           | 描述                       |
| -------------- | -------------------------- |
| **keydown()**  | 某个键盘按键被按下。       |
| **keypress()** | 某个键盘按键被按下并松开。 |
| **keyup()**    | 某个键盘按键被松开。       |



### 框架/对象 事件

| 属性           | 描述                                                |
| -------------- | --------------------------------------------------- |
| **error()**    | 在加载文档或图像时发生错误。(object,body和frameset) |
| @@@@**onload** | 一张页面或一幅图像完成加载。                        |
| **resize()**   | 当调整浏览器窗口的大小时                            |
| **scroll()**   | 当用户滚动指定的元素时                              |



### 表单事件

| 属性           | 描述                                                         |
| -------------- | ------------------------------------------------------------ |
| **submit()**   | 表单提交时触发                                               |
| **select()**   | 用户选取文本时触发 (input 和 textarea)                       |
| @@@**onreset** | 表单重置时触发                                               |
| **change()**   | 该事件在表单元素的内容改变时触发(input,keygen,select和 textarea) |
| @@**oninput**  | 元素获取用户输入时触发(Chrome/IE9.0/Firefox4.0/Safari5.0/Opera) |
| @@**onsearch** | 用户向**搜索域输入**文本时触发(<input="search">) (Chrome/Safari/Opera15.0) |



## 选择器

### 基本

**使用语法:**

`$("选择器")`

| 选择器                   | 描述                                     |
| ------------------------ | ---------------------------------------- |
| **#id**                  | 通过标签的id属性值获取元素(开发使用最多) |
| **element**              | 通过标签的名字获取元素                   |
| **.class**               | 通过标签class类名获取元素(开发使用最多)  |
| **selector1，selector2** | 通过逗号隔开获取指定选择器的元素         |

**使用范例：**

> - 匹配id=box的元素：`$("#box")`
>
> - 匹配class=box的元素：`$(".box")`
>
> - 匹配标签名为div的元素：`$("div")`
>
> - 匹配id=box和class=select的元素：`$("#box,.select")`
>
>   匹配id=box和id=box2的元素：`$("#box,#box2")`
>
> - 匹配类名class为select的ul元素：`$('ul.select')`



### 层级

**使用语法:**

`$("选择器")`

| 选择器           | 描述                                             |
| ---------------- | ------------------------------------------------ |
| **parent child** | 后代(子孙)选择器' 获取祖先下面的满足条件子孙元素 |
| **parent>child** | 子元素选择器'匹配父元素下面的指定的子元素        |

**使用范例：**

> - 匹配ul元素中名为li的子元素：`$('ul > li')`    大于号(>)隔开找子元素
>   匹配ul元素中名为li的子孙元素：`$('ul li')`	 空格隔开找子孙元素



### 筛选

**使用语法:**

`$("选择器")`

| 选择器                       | 描述                                |
| ---------------------------- | ----------------------------------- |
| selector**:first**           | 匹配第一个元素                      |
| selector**:last**            | 匹配最后一个元素                    |
| selector**:even**            | 匹配下标值为偶数的所有元素          |
| selector**:odd**             | 匹配下标值为奇数的所有元素          |
| selector**:eq(index)**       | 匹配下标为index的元素               |
| selector**:gt(index)**       | 匹配下标大于index的所有元素         |
| selector**:lt(index)**       | 匹配下标小于index的所有元素         |
| selector1**:not(selector2)** | 匹配除了selector2选择器以外所有元素 |
| selector**:contains(text)**  | 匹配包含文本text的元素,类似模糊查询 |

**使用范例：**

> - 匹配第一个div元素：`$('div:first')`或 `$('div:first-child')`
>
> - 匹配最后第一个div元素：`$('div:last')` 或 `$('div:last-child')`
>
> - 匹配下标为偶数的div元素：`$('div:even')`
>
> - 匹配下标为奇数的div元素：`$('div:odd')`
>
> - 匹配下标为2的div元素：`$('div:eq(2)')`
>
> - 匹配下标大于2的div元素：`$('div:gt(2)')`
>
>   匹配下标大于2的div元素的第一个元素：`$('div:gt(2):first')`
>
> - 匹配下标小于2的div元素：`$('div:lt(2)')`
>
> - 匹配除了id不为box的div元素：`$('div:not(#box)')`
>
> - 匹配内容含关键字蛋的div元素：`$('div:contains(蛋)')`



### 属性

**使用语法:**

`$("选择器")`

| 选择器                                     | 描述                                                         |
| ------------------------------------------ | ------------------------------------------------------------ |
| **[attribute]**                            | 匹配含有attribute属性的元素                                  |
| **[attribute=value]**                      | 匹配attribute等于value的元素【重点掌握】   $("input[type='text']") |
| **[attribute!=value]**                     | 匹配属性不等于value的元素                                    |
| **[attribute^=value]**                     | 匹配属性以value开头的元素                                    |
| **[attribute$=value]**                     | 匹配属性以value结束的元素                                    |
| **[attribute*=value]**                     | 匹配属性中包含value的元素                                    |
| **[attribute1]\[attribute2]\[attribute3]** | 任意多个属性选择器                                           |

**使用范例：**

> 强烈推荐**标签和属性组合**一起使用，能够准确的找到指定元素。
>
> - 如：找到属性名为type=text的input元素：
> - $("[type='text']")  但推荐写法：$("input[type='text']") 



### 表单

**使用语法:**

`$("选择器")`

| 选择器                | 描述                                                 |
| --------------------- | ---------------------------------------------------- |
| selector**:input**    | 匹配所有的表单元素                                   |
| selector**:text**     | 匹配单行文本框type='text'  推荐：**$("input:text")** |
| selector**:password** | 匹配单行密码框  推荐：**$("input[type=password]")**  |
| selector**:radio**    | 匹配单选按钮 推荐：**$("input[type='radio']")**      |
| selector**:checkbox** | 匹配多选按钮                                         |
| selector**:submit**   | 匹配提交按钮                                         |
| selector**:reset**    | 匹配重置按钮                                         |
| selector**:image**    | 匹配图片按钮                                         |
| selector**:button**   | 匹配普通按钮                                         |
| selector**:file**     | 匹配文件上传                                         |
| selector**:hidden**   | 匹配隐藏域                                           |

**使用范例：**

| jQuery选择器   | 说明                        |
| -------------- | --------------------------- |
| 匹配文本域     | $(“input[type=text]”)       |
| 匹配单选按钮   | $(“input[type=’radio’]”)    |
| 匹配复选框按钮 | $(“input[‘type=’checkbox’]) |
| 匹配隐藏域     | $(“input[type=’hidden’]”)   |



### 表单属性

语法:

- :enabled 匹配表单控件可用的  
- :disabled 匹配表单控件不可用的，多用于`<input type='text'  disabled='disabled'/>`元素
- :checked 匹配被选中的,多用于单选和多选按钮
- :selected 匹配被选中的， 多用于select下拉框

使用范例：

| 选择器                                                       | 说明                 |
| ------------------------------------------------------------ | -------------------- |
| selector**:enable**                                          | 匹配可用的元素       |
| selector**:disabled**                                        | 匹配不可用的元素     |
| **input\[type='radio'][checked]**或 **input[type='radio']:checked** | 匹配选中的单选框     |
| **select option:selected**                                   | 匹配选中的select元素 |



## JQ方法

### 筛选方法

| 方法                    | 描述                                    |
| ----------------------- | --------------------------------------- |
| **.eq(n)**              | 当前操作中第n个对象,类似索引            |
| **.first()**            | 第一个元素                              |
| **.last()**             | 最后一个元素                            |
|                         |                                         |
| **.has()**              | 包含特定后代的元素                      |
| **.children()**         | 匹配其每个子元素 , 第一层               |
| **.find(‘xx’)**         | 包含的所有xx的元素,子子孙孙             |
| **.next()**             | 紧邻其后的一个同辈元素                  |
| **.nextAll()**          | 其之后所有的同辈元素                    |
| **a.nextUntil("b")**    | a元素之后到b之间所有的同辈元素,掐头去尾 |
| **.prev()**             | 紧邻其之前的一个同辈元素                |
| **.prevAll()**          | 其之前所有的同辈元素                    |
| **a.prevUntil("b")**    | a元素之前到b之间所有的同辈元素,掐头去尾 |
| **.parent()**           | 每个this元素的父元素                    |
| **parents()**           | 每个this元素的所有祖先元素,body,html    |
| **a.parentsUntil("b")** | a元素之前到b之间所有的父级元素,掐头去尾 |
| **.siblings()**         | 所有的同辈元素,不包括自己               |

**使用范例：**

> |为或者，[ ]为可选
>

**eq(index|-index)**

> 参数：
>
> - `index`: 指示元素基于0的位置,这个元素的位置是从0算起。
>
>   `-index`: 指示元素的位置，从集合中的最后一个元素开始倒数。(1算起)

**.first()**

匹配第一个li元素：`$('li').first()` 

**.last()**

匹配最后一个li元素：`$('li').last()` 

**has(expr|ele)**

> 参数：
>
> - `expr`：一个选择器字符串。
>
>   `ele`：一个DOM元素

**.children([expr])**

> 参数：
>
> - `expr`：一个选择器字符串。
>
>   `none`：所有子元素

**.find(expr|obj|ele)**

> 参数：
>
> - `expr`：一个选择器字符串。
>
>   `obj`：一个用于匹配元素的jQuery对象
>
>   `ele`：一个DOM元素

**next([expr])**

`none`：下一个兄弟元素

**nextAll([expr])**

> 参数：
>
> - `expr`：一个选择器字符串。
>
>   `none`：选择所有兄弟元素

**.nextUntil(\[expr|ele][,fil])**

参数：

> - `expr`：一个选择器字符串。
>
>   `ele`：一个DOM元素
>
> - `fil`：一个字符串，其中包含一个选择表达式匹配元素。

**parent(\[expr])**

> 参数：
>
> - `expr`：一个选择器字符串。
>
>   `none`：选择所有父辈元素

**parents(\[expr])**

> 参数：
>
> - `expr`：一个选择器字符串。
>
>   `none`：选择所有祖先元素

**sibling(\[expr])**

> 参数：
>
> - `expr`：一个选择器字符串。
>
>   `none`：选择所有同辈元素



### 查询操作

| 方法            | 描述                                |
| --------------- | ----------------------------------- |
| **.hasClass()** | 元素是否含有某个特定的类,返回布尔值 |
| **.first()**    | 第一个元素                          |
| **.last()**     | 最后一个元素                        |

使用范例：

**.hasClass(class)**

> 参数：
>
> - `class`：用于匹配的类名



### 属性操作

| 方法               | 描述                                       |
| ------------------ | ------------------------------------------ |
| **.attr()**        | 设置或返回被选元素的属性值。               |
| **.removeAttr()**  | 从匹配的元素中删除一个属性                 |
| **.prop()**        | 获取在匹配的元素集中的第一个元素的属性值。 |
| **.removeProp()**  | 用来删除由.prop()方法设置的属性集          |
| **.addClass()**    | 为每个匹配的元素添加指定的类名。           |
| **.removeClass()** | 从所有匹配的元素中删除全部或者指定的类。   |
| **.toggleClass()** | 如果存在（不存在）就删除（添加）一个类。   |



**attr(① name|② properties|③ key , value|fun(index,attr) )**

> 参数：
>
> 1. name：属性名称 (只写属性名时，为获取属性name的值)
>
>    例：$("img").attr("src");
>
> 2. properties：作为属性的“名/值对”对象 
>
>    例：$("img").attr({ src: "test.jpg", alt: "Test Image" });
>
> 3. key , value|fun(index,attr) ：
>
>    - key：属性名称
>    - value：属性值
>    - fun(index,attr)：
>      - index：当前元素的索引值
>      - attr：原先的属性值。
>
>    例：$("img").attr("title", function() { return this.src });

**.removeAttr(name)**

> 参数：
>
> - name：要删除的属性名

**.prop(① name,bool|② properties|③ key , value|fun(value,attr) )**

> 参数：
>
> 1. name：
>
>    - name：属性名称 
>    - boolean：true 为选中 faluse为取消选中
>
>    例：$("input[type='checkbox']").prop("checked,true");
>
> 2. properties：作为属性的“名/值对”对象 
>
>    例：$("input[type='checkbox']").prop({  disabled: true});
>
> 3. key , value|fun(index,attr) ：
>
>    - key：属性名称
>    - value：属性值
>    - fun(index,attr)：
>      - index：当前元素的索引值
>      - attr：原先的属性值。
>
>    例：$("input[type='checkbox']").prop("checked", function( i, val ) {  return !val;});

**.removeProp(name)**

> 参数：
>
> - name：要删除的属性名

**.addClass(class|fn)**

> 参数：
>
> - class：个或多个要添加到元素中的CSS类名，请用空格分开
> - fun(index,class)：
>   - index：当前元素的索引值
>   - class：原先的class属性值。
>
> 例如：$('ul li:last').addClass(function() {  return 'item-' + $(this).index();});

**.removeClass([class|fn])**

> 参数：
>
> - class：一个或多个要删除的CSS类名，请用空格
> - fun(index,class)：
>   - index：当前元素的索引值
>   - class：原先的class属性值。
>
> 例如：$('li:last').removeClass(function() {
>     return $(this).prev().attr('class');
> });





## JSON

**在JavaScript中:**

两个json相关的操作方法：

> - JSON.parse(json字符串);  将json格式的字符串转化为js中的变量[对象]
> - JSON.stringify(json对象);  将json对象转化为json格式的字符串

**在PHP中:**

| 函数                | 描述                                                  |
| ------------------- | ----------------------------------------------------- |
| **json_encode**     | 将变量(数组)转化为json格式的字符串                    |
| **json_decode**     | 将 JSON 格式的字符串，转换为 PHP 变量[数组或对象格式] |
| **json_last_error** | 返回最后发生的错误                                    |

- **json_encode**


> `json_encode ( $value [, $options = 0 ] )`
>
> 参数：
>
> - **value**: 要编码的值。该函数只对 UTF-8 编码的数据有效。
>
> - **options**:由以下常量组成的二进制掩码：
>
>   JSON_HEX_QUOT, JSON_HEX_TAG, JSON_HEX_AMP, JSON_HEX_APOS, **JSON_NUMERIC_CHECK,->256 转为中文**
>
>   **32->数字带冒号 相加同时转**
>
>   JSON_PRETTY_PRINT, JSON_UNESCAPED_SLASHES, JSON_FORCE_OBJECT
>



- **json_decode**


> ` json_decode ($json [,$assoc = false [, $depth = 512 [, $options = 0 ]]])`
>
> 参数：
>
> - **json_string**: 待解码的 JSON 字符串，必须是 UTF-8 编码数据
>
> - **assoc**: 当该参数为 TRUE 时，将返回数组，FALSE 时返回对象。
>
> - **depth**: 整数类型的参数，它指定递归深度
>
> - **options**: 二进制掩码，目前只支持 JSON_BIGINT_AS_STRING 。
>
>   
>
> - **json_last_error**



# Nodejs

**nodejs特点**：

1. 事件驱动(当事件被触发时，执行传递过去的回调函数)

2. 单线程 (JavaScript运行机制)

3. 非阻塞 I/O 模型，当执行I/O操作时，不会阻塞。（I/O=input/output） (JavaScript运行机制)

   IO:磁盘读写IO,网络IO

4. 拥有世界最大的开源库生态系统 —— npm（Nodejs Package Manager即node包管理器）



## NPM

### NPM使用

基本步骤：

1. 在 https://www.npmjs.com/ 网站找到需要的模块，查看install语句
2. 在项目的根目录下，执行`npm install 模块名称`安装
3. 注意：通过`npm install 模块名`本地安装的模块，会自动下载到当前目录下的`node_modules`目录下，如果该目录不存在，则创建，如果已存在则直接把模块下载进去。
4. 在代码中通过 `require('模块名');` 加载该模块

### NPM常用模块

#### **自带的模块**

见 http://nodejs.cn/api/url.html

| 模块     | 作用                     |
| -------- | ------------------------ |
| **fs**   | 文件管理系统             |
| **url**  | 用于处理与解析 URL。     |
| **http** | 使用 HTTP 服务器与客户端 |
| **path** | 处理文件与目录的路径。   |



#### **需要安装的模块**

> **express模块**
>
> **`项目必装`**——框架

> **body-parser模块**
>
> **`项目必装`**——是express的一个中间件 用于对post请求体进行解析。可以解析JSON、Raw、文本、URL-encoded格式的请求体

> ##### mysql模板
>
> **`项目必装`**——这是一个mysql的node.js驱动。 
>
> ```javascript
> var mysql      = require('mysql');
> var connection = mysql.createConnection({
>   host     : 'localhost',
>   user     : 'me',
>   password : 'secret',
>   database : 'my_db'
> });
>  
> connection.connect();
> 
> connection.query('select *from t1', function (error, results, fields) {
>   if (error) throw error;
>   console.log(results);
> });
>  
> connection.end();
> ```

> **jquery**包
>
> 在入口文件main.js中导入npm下载的jquery包
>
> ```javascript
> //这是项目的入口文件main.js
> //注意：如果需要webpack对此js文件进行打包处理
> 
> console.log('main.js');
> 
> //引入jquery
> //import '../lib/js/jquery.js';
> import $ from 'jquery';
> 
> $(function(){
>     //隔行换色
>     $('div li:even').css('background-color','#ccc');
>     $('div li:odd').css('background-color','darkcyan');
> 
> })
> ```
>
> 

> ##### **mime模块**
>
> mime模块作用：
>
> - 查询**文件的类型**`mime.lookup(path)` 
>
>   通过文件及其扩展查询与文件关联的MIME类型，也可以通过MIME类型反向查找文件的扩展名。 
>
>   ```javascript
>   var mime = require('mime');
>   
>   mime.lookup('/path/to/file.txt');         // => 'text/plain'
>   mime.lookup('file.txt');                  // => 'text/plain'
>   mime.lookup('.TXT');                      // => 'text/plain'
>   mime.lookup('htm');                       // => 'text/html'
>   ```
>
> -  查询**文件护展名**`mime.extension(type)`
>
>   ```javascript
>   mime.extension('text/html');                 // => 'html'
>   mime.extension('application/octet-stream');  // => 'bin'
>   ```
>
> - 查找**类型编码**`mime.charsets.lookup()` 
>
>   ```javascript
>   mime.charsets.lookup('text/plain');        // => 'UTF-8'
>   ```

> ##### moment模板
>
> 日期时间转换
>
> - 日期格式化
>
>   ```javascript
>   moment().format('MMMM Do YYYY, h:mm:ss a'); // 十二月 31日 2018, 11:49:12 中午
>   moment().format('dddd');                    // 星期一
>   moment().format("MMM Do YY");               // 12月 31日 18
>   moment().format('YYYY [escaped] YYYY');     // 2018 escaped 2018
>   moment().format();                          // 2018-12-31T11:49:12+08:00
>   ```
>
> - 

> ##### md5模板
>
> 用于进行密码加密
>
> ```javascript
> var md5 = require('md5');
>  
> console.log(md5('message'));//78e731027d8fd50ed642340b7c9a63b3
> ```

> 
>

### 常用命令

- **npm安装模块**

npm i ：安装package.json中所有内容

npm install xxx ：利用 npm 安装xxx模块到当前命令行所在node_modules目录；
npm install  xxx -g：利用npm安装全局模块xxx；

- **本地安装**

npm install xxx：安装但不写入package.json；
npm install xxx –save ：安装并写入package.json的”dependencies”中；==其中--save等价于-S==
npm install xxx –save-dev：安装并写入package.json的”devDependencies”中。==其中--save-dev等价于-D==

- **npm 删除模块**

npm uninstall xxx：删除xxx模块； 

npm uninstall  xxx -g：删除全局模块xxx；

- **npm全局安装**

npm install 包名 -g：npm 全局安装指的是把包安装成了一个命令行工具。

npm 全局安装实际做了2件事：

1. 下载包到一个指定的目录
2. 创建一段命令行执行的代码。

- **安装淘宝npm（cnpm）**，提高安装速度

输入以下命令安装cnpm指令

```
npm install -g cnpm --registry=https://registry.npm.taobao.org

```

   输入命令==cnpm -v== 测试是否ok

```
cnpm -v

```



### package.json文件

**作用**：

1. package.json 文件是一个包说明文件（项目描述文件），用来管理组织一个项目所使用的包。
2. package.json 文件是一个 json 格式的文件
3. 位于当前项目的根目录下

**常见项**

- name: 包的名称，由小写英文字母、数字和下划线组成，不能包含空格。
- description：包的简要说明。
- author：包的作者
- version：符合语义化版本识别规范的版本
- keywords：关键字数组，通常用于搜索。
- maintainers：维护者数组，每个元素包含name、email（可选）、web（可选）字段。
- contributors：贡献者数组，格式与maintainers相同。包的作者应该是贡献者数组的第一个元素。
- licenses：许可证数组，每个元素要包含type（许可证的名称）和url（链接到许可证文本的地址）字段。
- repositories：仓库托管地址数组，每个元素要包含type（仓库的类型，如git）、url（仓库的地址）和path（相对于仓库的路径，可选）字段。
- dependencies：记录项目所依赖的包，一个关联数组，由包名称和版本号组成
- devDependencies：记录项目==开发时==所依赖的包，一个关联数组，由包名称和版本号组成，一般记录第三方插件或工具包。
- main： 当包被require时，指定包的入口js文件，即从这个js文件开始执行。

**创建一个 package.json 文件**

- 手动创建一个
- 通过 `npm init` 命令根据引导创建 package.json 文件。
- 或直接通过 `npm init -y` 或 `npm init -yes`  命令直接创建一个包含默认信息的package.json文件

## express

**express 特点**
- 实现了路由功能 
- 中间件（函数）功能
- 对 req 和 res 对象的扩展了其他功能
- 可以集成其他模板引擎

### 启动一个web服务器

1. npm 搜索express，安装
2. 创建 package.json文件
3. 安装 express 模块：`npm install express --save `
4. 加载 express 模块
5. 创建 express 实例（一般叫 app ）
6. 设计路由
7. 启动监听服务

**注意**： 

- 在 express 中，request 对象 和 response 对象一样使用，同时这两个对象还额外添加了其他的好用功能
- res.send() 是 res.end()的扩展，res之前的方法都是可以用的。
- res.send() 和 res.end() 区别：
  - res.send() 参数可以是 a Buffer object、a String、 an object、 an Array.
  - res.end() 参数类型只能是 Buffer 对象或者是字符串
  - res.send() 会自动发送更多的响应报文头，其中就就包括 Content-Type: text/html; charset=utf-8，所以没有乱码

### req

request对象：http://www.expressjs.com.cn/4x/api.html#req 

属性：

| 属性               | 说明                                                         |
| ------------------ | ------------------------------------------------------------ |
| req.baseUrl        | 基础路由地址                                                 |
| **req.body**       | post发送的数据解析出来的对象                                 |
| req.cookies        | 客户端发送的cookies数据                                      |
| **req.hostname**   | 主机地址 去掉端口号 （127.0.0.1）                            |
| **req.ip**         | 查看客户端的ip地址 (::ffff:127.0.0.1)                        |
| req.ips            | 代理的IP地址                                                 |
| **req.method**     | 与请求的HTTP方法相对应的字符串:GET、POST、PUT等。            |
| req.originalUrl    | 对req.url的一个备份                                          |
| **req.params**     | 在使用/:id/:name 匹配params                                  |
| **req.path**       | 包含请求URL的路径部分 （/login）                             |
| req.protocol       | http 或https协议 (http或https)                               |
| **req.query**      | 查询字符串`www.aa.com?username=zhangsan&password=123`解析出来的对象  { username:zhangsan } |
| **req.route**      | 当前匹配的路由 是一个对象                                    |
| **req.subdomains** | 请求域名中的子域名的数组`  "tobi.ferrets.example.com"` ,地址的数组（["ferrets", "tobi"]） |
| req.xhr            | 如果请求的`x - request - with`报头字段是“XMLHttpRequest”，则该属性为true，表示请求是由jQuery等客户端库发出的。 |

方法：

**req.accepts(types)**

> 根据请求的Accept HTTP报头字段检查指定的内容类型是否可接受。该方法返回最佳匹配，或者如果指定的内容类型中没有一个是可接受的，则返回false 
>

```javascript
// Accept: text/html
req.accepts('html');
// => "html"


// Accept: text/*, application/json
req.accepts('html');
// => "html"
req.accepts('text/html');
// => "text/html"
req.accepts(['json', 'text']);
// => "json"
req.accepts('application/json');
// => "application/json"

// Accept: text/*, application/json
req.accepts('image/png');
req.accepts('png');
// => undefined

// Accept: text/*;q=.5, application/json
req.accepts(['html', 'json']);
// => "json"
```

**req.get(field)**

> 返回指定的HTTP请求头字段(不区分大小写的匹配)。 
>

```javascript
req.get('Content-Type');
// => "text/plain"

req.get('content-type');
// => "text/plain"

req.get('Something');
// => undefined
```

**req.is(type)**

> 如果传入请求的“content - type”HTTP头字段与类型参数指定的MIME类型匹配，则返回匹配的内容类型。如果请求没有正文，则返回null。否则返回false。 
>

```javascript
// With Content-Type: text/html; charset=utf-8
req.is('html');       // => 'html'
req.is('text/html');  // => 'text/html'
req.is('text/*');     // => 'text/*'

// When Content-Type is application/json
req.is('json');              // => 'json'
req.is('application/json');  // => 'application/json'
req.is('application/*');     // => 'application/*'

req.is('html');
// => false
```

**req.param(name [, defaultValue])**

>  返回当前参数名的值。 

```javascript
// ?name=tobi
req.param('name')
// => "tobi"

// POST name=tobi
req.param('name')
// => "tobi"

// /user/tobi for /user/:name
req.param('name')
// => "tobi"
```


### res

response对象：http://www.expressjs.com.cn/4x/api.html#res

| 属性                | 说明                                                         |
| ------------------- | ------------------------------------------------------------ |
| **res.headersSent** | 布尔属性，指示应用程序是否为响应发送HTTP报头。               |
| **res.locals**      | 对象，该对象包含响应局部变量，作用域限定于请求，因此仅对该请求/响应周期(如果有)中呈现的视图可用。 |

方法：

**res.cookie(name, value [, options])**

> 将cookie名称设置为值。值参数可能是转换为JSON的字符串或对象。 
>
> 选项参数是一个可以具有以下属性的对象。 

| 属性     | 类型              | 说明                                                         |
| -------- | ----------------- | ------------------------------------------------------------ |
| domain   | String            | cookie的域名。默认是应用程序的域名。 (.shop.com)             |
| path     | String            | cookie的路径。默认值为" / "。 (/admin)                       |
| encode   | Function          | 用于cookie值编码的同步函数。默认为encodeURIComponent。       |
| expires  | Date              | 在GMT时间的cookie到期日期。如果没有指定或设置为0,则创建一个会话cookie。 |
| httponly | Boolean           | 将cookie标记为只能通过web服务器访问。                        |
| maxAge   | Number            | 方便的选项,将过期时间与当前时间相对于毫秒。 (90000)          |
| secure   | Boolean           | 标记cookie只使用HTTPS。                                      |
| signed   | Boolean           | 指示是否应该签名。                                           |
| sameSite | Boolean or String | “SameSite”集cookie属性的值。                                 |

```javascript
res.cookie('name', 'tobi', { domain: '.example.com', path: '/admin', secure: true });
res.cookie('rememberme', '1', { expires: new Date(Date.now() + 900000), httpOnly: true });

//maxAge选项是一个方便选项,在毫秒内设置“过期”。
res.cookie('rememberme', '1', { maxAge: 900000, httpOnly: true });

//您可以将对象传递为值参数
res.cookie('cart', { items: [1,2,3] });
res.cookie('cart', { items: [1,2,3] }, { maxAge: 900000 });
```

 **res.clearCookie(name [, options])**

> 清除指定的cookie。 
>

```javascript
res.cookie('name', 'tobi', { path: '/admin' });
res.clearCookie('name', { path: '/admin' });
```

**res.download(path \[, filename]\[, options][, fn])**

> 将文件转换为“附件”。 
>

```javascript
res.download('/report-12345.pdf');

res.download('/report-12345.pdf', 'report.pdf');

res.download('/report-12345.pdf', 'report.pdf', function(err){
  if (err) {
    // Handle error, but keep in mind the response may be partially-sent
    // so check res.headersSent
  } else {
    // decrement a download credit, etc.
  }
});
```

**res.end(\[data][, encoding])**

> 结束响应过程。 
>

**res.get(field)**

返回字段指定的HTTP响应头。该匹配是不区分大小写的。 

```javascript
res.get('Content-Type');
// => "text/plain"
```

**res.json([body])**

> 发送JSON响应。该方法通过使用JSON.stringify()向JSON字符串发送一个响应(使用正确的内容类型)。
>

```javascript
res.json(null);
res.json({ user: 'tobi' });
res.status(500).json({ error: 'message' });
```

**res.location(path)**

> 将响应位置HTTP头设置为指定的路径参数。 
>

```javascript
res.location('/foo/bar');
res.location('http://example.com');
res.location('back');
```

**res.redirect([status,] path)**

> 重定向到从指定路径派生的URL,指定的状态,一个对应于HTTP状态代码的正整数。如果没有指定,状态默认为302“发现”。 
>

```javascript
res.redirect('/foo/bar');
res.redirect('http://example.com');
res.redirect(301, 'http://example.com');
res.redirect('../login');
```

 **res.render(view \[, locals][, callback])**

>  呈现视图并将呈现的HTML字符串发送给客户机。 
>

```javascript
// send the rendered view to the client
res.render('index');

// if a callback is specified, the rendered HTML string has to be sent explicitly
res.render('index', function(err, html) {
  res.send(html);
});

// pass a local variable to the view
res.render('user', { name: 'Tobi' }, function(err, html) {
  // ...
});
```

**res.send([body])**

> 发送HTTP响应。
>
> body参数可以是缓冲区对象、字符串、对象或数组。
>

**res.sendFile(path \[, options][, fn])**

> 在给定路径上传输文件。基于文件名的扩展设置内容类型响应HTTP头字段。除非在选项对象中设置根选项,否则路径必须是文件的绝对路径。 
>

 下表提供了选项参数的详细信息。 

| 属性         | 说明                                                         | 默认值   |
| ------------ | ------------------------------------------------------------ | -------- |
| maxAge       | 以毫秒或ms格式设置cache控制头的max-age属性                   | 0        |
| root         | 相对文件名的根目录。                                         |          |
| lastModified | 将最后修改的头设置为操作系统上文件的最后修改日期。设置错误以禁用它。 | Enabled  |
| headers      | 对象包含HTTP头以服务于文件。                                 |          |
| dotfiles     | 服务网络文件的选项。可能的值是  “allow”, “deny”, “ignore” 。 | “ignore” |
| acceptRange  | 启用或禁用接受远程请求。                                     | true     |
| cacheControl | 启用或禁用设置Cache-Control响应头。                          | true     |
| immutable    | 启用或禁用Cache-Control响应头中的不可变指令。如果启用,还应该指定maxAge选项,以启用缓存。不可变指令将防止支持客户端在maxAge选项的生活过程中提出条件请求,以检查文件是否已经更改。 | false    |

```javascript
app.get('/file/:name', function (req, res, next) {

  var options = {
    root: __dirname + '/public/',
    dotfiles: 'deny',
    headers: {
        'x-timestamp': Date.now(),
        'x-sent': true
    }
  };

  var fileName = req.params.name;
  res.sendFile(fileName, options, function (err) {
    if (err) {
      next(err);
    } else {
      console.log('Sent:', fileName);
    }
  });

});
```

**res.set(field [, value])**

> 将响应的HTTP头字段设置为值。要同时设置多个字段,将对象传递为参数。 
>

```javascript
res.set('Content-Type', 'text/plain');

res.set({
  'Content-Type': 'text/plain',
  'Content-Length': '123',
  'ETag': '12345'
});
```

和`res.header(field [, value])`一样. 

**res.status(code)**

> 为响应设置HTTP状态。 
>

```javascript
res.status(403).end();
res.status(400).send('Bad Request');
res.status(404).sendFile('/absolute/path/to/404.png');
```

**res.type(type)**

> 为MIME的设置Content-Type HTTP header。如果类型包含“/”字符,则将Content-Type HTTP设置为类型。 
>

```javascript
res.type('.html');              // => 'text/html'
res.type('html');               // => 'text/html'
res.type('json');               // => 'application/json'
res.type('application/json');   // => 'application/json'
res.type('png');                // => image/png:
```
### 路由

**分类：**

- app.get(path,callback)

  若`get请求方式`中的req.url 中的 pathname部分和 `path`完全匹配，则执行callback的回调函数中的逻辑

- app.post(path,callback)

  若`post请求方式`中的req.url 中的 pathname部分和 `path`完全匹配，则执行callback的回调函数中的逻辑

- app.all(path,callback)

  1. 在进行路由匹配的时候不限定方法，什么请求方法都可以
  2. 请求路径中pathname要求与 `path` 完全匹配

- app.use(path,callback)

  1. 在进行路由匹配的时候不限定方法，什么请求方法都可以
  2. 请求路径中pathname第一部分只要与` path` 匹配即可，并不要求完全匹配

**==注意==**:app.all和app.use的区别：

- 相同点：不限定请求方法
- 不同点：
  - all,要求pathname和path部分完全匹配
  - use,要求pathname第一部分与path完全匹配即可 



# Vuejs

## v- 指令

| 指令                         | 作用                                                    |
| ---------------------------- | ------------------------------------------------------- |
| **v-cloak**                  | 能够解决插值表达式偶尔闪烁的问题                        |
| **v-text**                   | 将标签中的内容进行覆盖 不解析html                       |
| **v-html**                   | 将标签中的内容进行覆盖 并解析其中html                   |
| **v-bind / :**               | 绑定属性的指令,绑定后才可以使用data中的数据             |
| **v-on / @**                 | 绑定事件                                                |
| **v-model**                  | 这个指令用于在表单上创建双向数据绑定。                  |
| **v-for**                    | 根据遍历数组来进行渲染                                  |
| **v-if/ v-else/ v-else-if ** | 可以实现条件渲染，Vue会根据表达式的值的真假来渲染元素   |
| **v-show**                   | 用于根据条件展示元素;它只是简单的切换css的dispaly属性。 |

**v-cloak**

> 能够闪烁的问题
>

```html
<div id="app" v-cloak>
    <div>
        {{message}}
    </div>
</div>
```

**v-text 和 v-html**

```html
<!-- msg:'<b>haha</b>' -->
<span v-text="msg"></span> <!--{{msg}} -->

<div v-html="msg"></div> <!--haha-->
```

**v-bind / :**

> **(1)对象语法** :
>

```html
<!--进行类切换的例子-->
<div id="app">
  <!--当data里面定义的isActive等于true时，is-active这个类才会被添加起作用-->
<!--当data里面定义的hasError等于true时，text-danger这个类才会被添加起作用-->
    <div :class="{'is-active':isActive, 'text-danger':hasError}"></div>
</div>
<script>
    var app = new Vue({
        el: '#app',
        data: {
            isActive: true,  
            hasError: false
        }
    })
</script>

<!--渲染结果：-->
<div class = "is-active"></div>
```

> **(2)数组语法** :
>

```html
<div id="app">
    <!--数组语法：errorClass在data对应的类一定会添加-->
    <!--is-active是对象语法，根据activeClass对应的取值决定是否添加-->
    <p :class="[{'is-active':activeClass},errorClass]">12345</p>
</div>
<script>
    var app = new Vue({
        el: '#app',
        data: {
            activeClass: false,
            errorClass: 'text-danger'
        }
    })
</script>

<!--渲染结果：-->
<p class = "text-danger"></p>
```

>  **(3)直接绑定数据对象** 
>

```html
<div id="app">
    <!--在vue实例的data中定义了classObject对象，这个对象里面是所有类名及其真值-->
    <!--当里面的类的值是true时会被渲染-->
    <div :class="classObject">12345</div>
</div>
<script>
    var app = new Vue({
        el: '#app',
        data: {
            classObject:{
                'is-active': false,
                'text-danger':true
            }           
        }
    })
</script>

<!--渲染结果：-->
<div class = "text-danger"></div>
```



## 修饰符 

### 事件修饰符

- **.stop**

> 阻止冒泡修饰符 
>

```html
<div @click="parent">parent
    <div @click.stop="child">child
        <div @click="grandson.stop">grandson</div>
    </div>
</div>
```

- **.prevent**

> 阻止元素发生默认行为 
>

```html
<a href="www.baidu.com" @click.prevent="parent"></a>
```

- **.capture**

> 事件捕获
>

```html
 <div @click.capture="parent">parent
 	<div @click="child">child
 		<div @click="grandson">grandson</div>
 	</div>
 </div>
<!-- 点击grandson按钮控制台信息 -->
<!-- parent
	grandson
	child-->
```

- **.self**

> 只点该对象自己身上才运行
>

```html
 <div @click="parent">parent
     <div @click.self="child">child
         <div @click="grandson">grandson</div>
     </div>
</div>
```

- **.once**   

> 只执行一次 
>

```html
 <div @click="parent">parent
 	<div @click.once="child">child
		<div @click="grandson">grandson</div>
 	</div>
 </div>
```


### 按键修饰符

> 在**监听键盘**事件时，我们经常需要监测常见的键值。 Vue 允许为 **v-on** 在监听键盘事件时添加按键修饰符： 
>

```html
<!-- 只有在 keyCode 是 13 时调用 vm.submit() -->
<input v-on:keyup.13="submit">

<!-- 还可以用别名：-->
<input @keyup.enter="submit">
```

全部的按键别名：

- **enter**
- **tab**
- **delete** (捕获 “删除” 和 “退格” 键)
- **esc**
- **space**
- **up**
- **down**
- **left**
- **right**



### 其他修饰符

- **lay**

> 在改变后才触发（也就是说只有光标离开input输入框的时候值才会改变） 
>

```html
<input v-model.lazy="msg" >
```

- **number**

> 将输出字符串转为Number类型[·](http://caibaojian.com/vue-js-on-form.html)（虽然type类型定义了是number类型，但是如果输入字符串，输出的是string） 
>

```html
<input v-model.number="age" type="number">
```

- **trim**

> 自动过滤用户输入的首尾空格 
>

```html
<input v-model.lazy.trim="msg" >
```


## Vue实例

| 属性或方法     | 说明                                                         |
| -------------- | ------------------------------------------------------------ |
| **el**         | Vue实例的DOM根元素                                           |
| **data**       | Vue实例观察的数据的对象                                      |
| **methods**    | 保存所需的方法                                               |
| **components** | 保存组件                                                     |
| **props**      | 当前组件接收到的props对象 [父组件传值给子组件]               |
| **watchs **    | 用来监听属性变化                                             |
| **computed**   | 当其所依赖的属性的值发生变化的时候，这个属性的值会自动更新，与之相关的东西也会自己更新。 |
| **router**     | 创建路由                                                     |
| **childrend**  | 实现路由嵌套                                                 |
| **render**     | 渲染组件                                                     |

### **el**

> 类型：（HTMLElement）挂载元素 
>

### **data**

> 类型（Object）对象
>

### **methods**

> 类型（Object）对象
>

```javascript
var vm = new Vue({
    el: "#app",
    data: { 
        a: 'hello', 
        b: 'hi' 
    }，
    methods:{
    	hi:function(){
    		console.log('hi')
		},
         hello(){
 			console.log('hello')                
         }
	},
});
console.log(vm.$data.a);  // 'hello'
console.log(vm.$data.b);  // 'hi'
```

### **components**

> 类型（Object）对象
>

```html
<div id="app">
    <login></login>
</div>
<template id="tem_login">
    <div>
        <h1>login- {{msg}}</h1>
        <button @click="show">按钮</button>
    </div>
</template>
```

```javascript
var vm = new Vue({
    el:"#app",
    data:{
        msg:'123'
    },
    components:{
        'login':{
            template:'#tem_login',
            data:function(){
                return{
                    msg:'123'
                }
            },
            methods:{
                show(){
                    console.log('show'+this.msg)
                }
            },
        },
    }
})
```

### **props**

> 类型：（array）数组
>

```html
<div id="app">
    <h1> {{msg}} </h1>
    <son :parentmsg="msg" :parentmoney="money"></son>
</div>
<template id='son_tem'>
	<h1>{{sonmsg}}-{{parentmsg}}-{{parentmoney}}</h1>
</template>
```

```javascript
var vm = new Vue({
  el:'#app',
  data:{
    msg:'app父组件',
    money:'100'
  },
  components:{
    'son':{
      template:'#son_tem',
      data:function(){
        return {
          sonmsg:'我是儿子'
        }
      },
      props:['parentmsg','parentmoney']
    }
  }
})
```

显示效果：

![94](\images\94.jpg)

###  **watch**

> 类型：（Object）对象
>
> 例：效果：当姓或名的值改变时，全名自动改变
>

```html
<div id="app">
	姓：<input type="text" v-model='firstname'><br>
	名：<input type="text" v-model='lastname'><br>
	全名：<span>{{fullname}}</span>
</div>
```

```javascript
new Vue({
    el:'#app',
    data:{
        firstname:'',
        lastname:'',
        fullname:''
    },
    //watch用来监听属性变化
    watch:{
        firstname:function(newVal,oldVal){
            this.fullname=newVal+this.lastname
        },
        lastname:function(newVal,oldVal){
            this.fullname=this.firstname+newVal
        }
    },
}) 
```

### **computed**

> 类型：（Object）对象
>
> 例：效果：当姓或名的值改变时，全名自动改变
>
> html与上watch的相同
>

```javascript
new Vue({
    el:'#app',
    data:{
        //无需定义fullname
        firstname:'',
        lastname:'',
    },
    computed:{
        //此处相当于定义fullname
        fullname:function(){
            return this.firstname+'-'+this.lastname
        }
    }
})
```

### **router**

> 类型：VueRouter实例
>

###  **children**

> 类型：数组 
>

```html
<!-- 需要引入路由组件类库 -->
<script src="./lib/vue-router-3.0.1.js"></script>

<div id="app">
    <router-link to="/account">account</router-link>
    <router-view></router-view>
</div>
<template id="tmp1">
    <div>
        account组件<br>
        <router-link to="/account/login">登录</router-link>
        <router-link to="/account/register">注册</router-link>
        <router-view></router-view>
    </div>
</template>
```

```javascript
var login = {
        template:"<h1>登录组件</h1>"
    };
    var register = {
        template:"<h1>注册组件</h1>"
    };
    var account = {
        template:"#tmp1"
    };
    //创建路由对象
    var router = new VueRouter({
        routes:[
            {
                path:'/account',
                component:account,
                children:[
                    {path:'login',component:login},
                    {path:'register',component:register}
                ]
            },
        ],
    })

new Vue({
    el:'#app',
    router,
})
```

效果：

![95](\images\95.jpg)

点击后：

![96](\images\96.jpg)

再点击后：

![97](\images\97.jpg)

### **render**

> createElement是一个方法，调用它能把指定的组件模板渲染为 html 结构
>
> return 的结果，会替换页面中el指定的那个 容器

```javascript
var login = {
    template: '<h1>我是登录组件</h1>'
  };
  var register = {
    template: '<h1>我是注册组件</h1>'
  };
 var vm = new Vue({
    el: "#app",
    data: {
      msg: '123'
    },
   render: function (createElement) { 
        return createElements(login)
   }
});
```


## 解决回调地狱promise

回调地狱问题：

```javascript
//依次异步读取1.txt、2.txt、3.txt的文件内容
//解决办法：在第一个异步任务读取成功之后再读取第二个异步任务，第二个异步任务成功之后，再读取第三个异步任务

fs.readFile('./files/1.txt','utf8',function(err,data){
  if(err){
    throw err;
  }
  console.log(data);
  //读取第二个异步任务
  fs.readFile('./files/2.txt','utf8',function(err,data){
    console.log(data);
    //在执行异步任务读取3.txt内容
    fs.readFile('./files/3.txt','utf8',function(err,data){
      console.log(data);
    })
  })
})
////以上产生的问题：
//回调地狱问题（层层包裹进行回调，代码也不够优雅）
```

promise函数使用：

两个参数：

- **resolve** 异步执行成功的回调函数  
- **reject** 异步执行失败的回调函数



注意：

- new Promise返回的是一个promise对象，这个对象有一个方法叫做then,
- **then**方法：可以指定成功和失败的回调函数
- **catch**方法： 上面所有的promise如果其中一个有错误，则终止下面的所有的promise执行，且直接进入到catch，获取promise的异常错误信息
- **promise.then(successCallback,errorCallback).cache(func);**

```javascript
var  fs = require('fs');
var promise = new Promise(function(resolve,reject){
  fs.readFile('./files/1.txt', 'utf8', function (err, data) {
    if (err) {
      reject(err);
    } else {
      resolve(data);
    }
  })
});

promise.then(
  function (data) {
  //then第一个函数是成功的回调，参数是resolve(data)中的data
  console.log('成功：' + data);
}, 
  function (err) {
  //then第二个函数是失败的回调函数，参数是reject(err)中的err错误对象
  console.log('失败：' + err);
});
```

使用promise解决以上问题：

```javascript
//封装一个异步读取文件的内容的函数
//此函数返回对应异步任务的promise对象
function getFileByPath(path) {
  return new Promise(function (resolve,reject) {
    fs.readFile(path, 'utf8', function (err, data) {
      if(err){
        //失败
        reject(err);
      }else{
        resolve(data);
      }
    })
  });
}

var result = []; 
getFileByPath('./files/1.txt')
.then(function(data){
  console.log("成功："+data);
  result.push(data);
  return getFileByPath('./files/2.txt');
}) //上面的then通过getFileByPath返回的是一个promise对象，所以可以继续.then串联调用（链式调用）
.then(function(data){ 
  console.log("成功："+data);
  result.push(data);
  return getFileByPath('./files/3.txt');
})
.then(function(data){
  result.push(data);
  console.log("成功："+data);
})
.catch(function(err){   
  console.log('catch:'+err);
})

```

简化：

使用promise.all

```javascript
//getFileByPath方法和上面相同
var promise2 = getFileByPath('./files/2.txt');
var promise3 = getFileByPath('./files/3.txt');
var promise1 = getFileByPath('./files/1.txt');

//执行多个异步任务，
Promise.all([promise3,promise2,promise1]).then(function(data){
  console.log(data);
},function(err){
  console.log('错误了：'+err);
})
```

**小结**：

- Promise.all尤其是在一个页面**有多个ajax程序**的时候，特别好用。
- 如果页面中某一块数据，是依赖于前几个ajax成功的返回结果才显示此数据，如果其中有一个失败，则同样可以在then的第二个参数做失败的业务
- promise.all的成功结果是返回一个**数组**，且数组中数据的结果顺序与promise.all数组的传参顺序是一样的。



## 路由

### **命名路由&路由参数**

```javascript
var router = new VueRouter({
    routes:[
        {path:'/login/:age/:name',component:login,name:'denglu'},
        {path:'/register',component:register},
    ]
});
```

```html
<div id="app">
    <router-link :to="{name:'denglu',params:{age:123,name:'大锤'}}">登录</router-link>	
    <router-link :to="{name:'zc'}">注册</router-link>	
    <router-view></router-view>
</div>
```

### **编程式导航&声明式导航**

- 声明式导航：通过 `<router-link>`进行跳转,其本质还是渲染成`a标签`实现跳转
- 编程式导航：通过` this.$router.push()`进行跳转，类似于js的`location.href`进行跳转

编程式：

```html
<button @click="jump">跳转</button>
```

```javascript
var router = new VueRouter({
    routes:[
        {path:'/login/:age/:name',component:login,name:'dl'},
        {path:'/register',component:register,name:'zc'},
    ]
});

var app = new Vue({
  el:"#app",
  router,
  methods:{
    jump(){
      router.push('/register');
      this.$router.push({ name:'dl',params:{age:200,name:"大锤"}});
    }
  }
});
```

### 向前向后

```javascript
methods:{
    goBack(){
         this.$router.go(-1);
    }
    goahead(){
        this.$router.go(1);
    }
},
```

```html
<button @click="goback">返回</button>
<button @click="goahead">前进</button>
```



## Webpack打包

webpack 是前端的一个项目构建工具，它是==基于 Node.js== 开发出来的一个前端工具；可以解决各个包之间的复杂依赖关系；

### Webpack.config.js 配置

#### 入口起点(entry)

用法：`entry: string|Array<string>` 

```javascript
module.exports = {
  entry: './path/to/my/entry/file.js'
};
```

#### 输出(output)

在 webpack 中配置 `output` 属性的最低要求是，将它的值设置为一个对象，包括以下两点：

- `filename` 用于输出文件的文件名。
- 目标输出目录 `path` 的绝对路径。

```javascript
var path = require('path');
module.exports = {
  output: {
    filename: 'bundle.js',
    path: path.join(__dirname,'dist')
  }
};
```

#### 模式(mode)

支持的字符串值：

`development` `production ` `none `

```javascript
module.exports = {
  mode: 'development'//快一点
};
```

如果不设置，webpack 会将 `production` 作为 `mode` 的默认值去设置。 

#### loader

##### 1. 打包JS文件

打包jquery和script代码（基础配置 无需loader）

1. 使用`npm i jquery -S`安装jquery类库

2. 创建`main.js`并书写各行变色的代码逻辑：

   ```javascript
   // 导入jquery类库
   import $ from 'jquery'
   
   $('li:even').css('backgroundColor','lightblue');
   $('li:odd').css('backgroundColor','pink');
   ```

3. webpack.config.js 文件

   ```javascript
   var path = require('path');
   module.exports = {
       entry: path.join(__dirname, 'src/main.js'),
       output: {    //打包后的项目出口文件
           path: path.join(__dirname, 'dist'),
           filename: 'bundle.js'
       }
   }
   ```



##### 2. 打包css文件

- 安装`npm install style-loader css-loader -D`
- style-loader和css-loader作用
  - `css-loader`: 加载.css文件,对样式进行代码编译。
  - `style-loader`:使用`<style>`将样式注入到我们的HTML页面
- 修改webpack.config.js配置文件
  - rules：匹配文件的规则，指定哪些文件格式交给哪些loader进行处理 
  - test正则匹配的css文件
  - use指定对应的loader来处理（加载顺序是从右往左）

```javascript
module.exports = {
    mode:"development",
    entry:'./src/main.js',
    output:{
        path:path.join(__dirname,'dist'),
        filename:'bundle.js'
    },
    module:{
        rules:[
            {test:/\.css$/,use:[
                {loader:'style-loader'},
                {loader:'css-loader'}
            ]},
        ]
    }
}
```

##### 3. 处理css中的图片路径和字体路径

- 安装`npm install url-loader file-loader -D`

- 在`webpack.config.js`中添加处理url路径的loader模块：

  **图片**：

  ```json
  {
      test: /\.(jpg|png|gif|bmp|jpeg)$/,
      loader: 'url-loader',
      options: {
         limit:3000,
         name: '[name]-[hash].[ext]'
       }
  },
  ```

  - limit：图片的大小（字节），图片小于limit则会自动打包为Base64编码，否则文件名会重命名为随机的一串字符。

    base编码不会发送http请求，而文件名重命名会发起http请求。

  - name:指定文件的名称，选项有：

    - `[name]`:图片的原名
    - `[ext]`:图片的后缀
    - `[hash]`:生成唯一的hash值，还可以指定生成的长度[hash:8]

  

  **字体**：

  ```json
  {
  	test: /\.(ttf|eot|svg|woff|woff2)$/,
  	use: ['url-loader']
  },
  ```

  

### **实时打包构建**

node --> nodemon

webpack  --> webpack-dev-server

- `npm install webpack-dev-server -g`安装到全局中。

- 安装完成之后，在项目根目中命令行直接运行`webpack-dev-server`来进行打包。

- 通过package.json文件中的`scripts`选项，来进行运行webpack-dev-server命令，新增如dev指令：

  ```json
  "scripts": {
  	"dev": "webpack-dev-server"
  }
  ```

- 在项目根目录中运行：`npm run dev` 即可。

- webpack-dev-server将打包好的文件放在了**==内存中==**，优点：速度快

- 修改index.html中script的src属性为:`<script src="/bundle.js"></script>`

- 为了能在访问`http://localhost:8080/`的时候直接访问到index首页，可以使用`--contentBase src`指令来修改指定启动的根目录（此处为src）；

  ```json
  "scripts": {
      "dev": "webpack-dev-server  --contentBase src" 
  }
  ```

- 热更新（--hot）：表示启用浏览器热更新,通过它可以实现修改-运行同步的效果 ,每次不会重新打包所有的文件，仅会把修改过的部分更新到bundle.js文件中;

  --open 表示自动打开浏览器，

  --port 6666 表示打开的端口号为6666，

  ```json
  "scripts": {
      "dev": "webpack-dev-server  --contentBase src  --port 6666 --open --hot"
  }
  ```

- 设置模式为开发模式（速度快）

  ```javascript
  module.exports = {
      mode:"development",//开发模式
      entry:'./src/main.js',
      output:{
          path:path.join(__dirname,'dist'),
          filename:'bundle.js'
      }
  }
  ```



# Vue项目开发

## 准备工作

### Vue-cli 脚手架工具

- 安装全局脚手架工具

  >  \>cnpm i vue-cli -g

- 创建项目文件夹，使用vue-cli对项目进行初始化，创建项目

  ![123](\images\123.jpg)

- webpack配置文件

   添加自己喜欢的参数 优化开发体验 

  ![124](\images\124.jpg)

  了解vue-cli在webpack配置文件中 设置的解析路径 别名

  ![125](\images\125.jpg)

- vue-cli自动搭建项目 没有安装sass-loader 自行安装

  cnpm i sass-loader node-sass -D



