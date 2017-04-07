# BOM对象 -- 浏览器对象模型

从对象的角度重新认识整个js的所有知识点

## 概述

整个js其实全是对象

比如 

var str = ‘11’ 
var arr = [1,2,3,4,5,6,7] --
var num=1 -- Number

背后都会自动被编译成一个对象，我们看不到，因为系统将这些复杂隐藏起来了，我们只需要会用就可以了。


我们前面学习的所有知识点其实都是对象的某个属性或者方法而已

万物皆对象

三大对象：

- 内置对象16个

字符串String，数组Array，日期Date，正则Regexp，数字Number，数学Math，错误Error，函数Function，Object，Null，Cookie, Session, Boolean...

- BOM对象

windows ，document , history ，location , Screen , Navigator

- 自定义对象

重点：函数对象的属性和方法

前面学习的创建面向对象的N种方法，其实就是自定义对象。


### BOM对象 -- 浏览器对象模型

BOM是浏览器对象模型的简称
Browser Object Model

前面我们讲了面向对象，分析了人，学生，产品的行为属性和方法。

说白了就是将浏览器打开的网页看成一个对象

### 网页的特性分析

下面我们分析下网页的行为属性：

window ，document , history ，location , Screen , Navigator

- 窗口（打开的网页整体看做一个窗口）
- 屏幕（网页是显示在一个屏幕上的）
- 导航栏
- 历史访问记录
- 标题
- 网页主题内容
- 地址栏
- 收藏

![](http://on9plnnvl.bkt.clouddn.com/17-3-24/40164690-file_1490326375181_100b2.png)


## 1.窗口Window

我们将打开的整个网页看做窗口对象

窗口对象中封装了和窗口相关的属性和方法，比如打开一个窗口，关闭一个窗口

![](http://on9plnnvl.bkt.clouddn.com/17-3-24/38406943-file_1490327427347_13496.png)


```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
<button id="btn">打开一个新的窗口</button>
<button id="btn2">打开一个新的窗口2</button>
<button id="btn3">打开星座的详细信息</button>
</body>
</html>
<script>
    document.getElementById('btn').onclick=function() {
        window.open('http://www.baidu.com')
    }

    document.getElementById('btn2').onclick=function() {
        window.open ('http://www.baidu.com','newwindow','height=500,width=500,top=100,left=100,toolbar=no,menubar=no,scrollbars=no, resizable=no,location=no, status=no')
    }
//    我们可以控制窗口的各种属性：
//    宽为100，高为400，距屏顶0象素，屏左0象素，无工具条，无菜单条，无滚动条，
//    不可调整大小，无地址栏，无状态

    document.getElementById('btn3').onclick=function() {
        window.open ('detail.html')
    }
</script>
```

- 上述代码，点击中间的按钮：

![](http://on9plnnvl.bkt.clouddn.com/17-3-24/39302168-file_1490327578859_10541.png)

- 控制窗口的各种属性：

![](http://on9plnnvl.bkt.clouddn.com/17-3-24/71391484-file_1490327721444_a0b8.png)

### 面向对象分析窗口对象

```
/*
看看开发JS的这位编程大牛中的大神是如何使用面向对象分析窗口的

其实你会发现：也不难

所以面向对象学习的不是语法规范，而是如何将现实世界抽象成代码中的对象，然后进行编程
*/
Function window {
高度
宽度
}
Wndow.prototype={
打开窗口open
关闭当前窗口close
}

```
### window其他对象属性

地址栏，网页内容，导航栏等都是呈现在一个窗口中的，所以这些其实都是窗口的一部分

所以window对象更新：

```
Function window {
    高度
    宽度
    地址栏Location
    网页内容document
    历史访问history
    导航栏
}
Wndow.prototype={
    打开窗口open（）
    关闭当前窗口close（）
}

```

**注意：**

> 面向编程的重要的是如何提取属性和方法提取的目的是封装细节，方便别人使用

> 这里js鼻祖使用对象封装了细节，我们无需关注，只需要记住对象的属性和方法，会使用就可以了。

> 不要纠结对象的语法格式，只需要知道如何定义属性，如何定义方法就可以了。

> 在js中我们一般将属性放在构造函数中，将方法放在原型中，至于为什么，前面我们已经详细讲解了

### 自定义全部变量的本质

任何我们定义的全局变量 函数 对象等都会成为window对象的属性

比如： var sum = 1

因此我们可以也通过window.sum来访问这个变量

```
<script>
    //1 任何我们定义的全局变量 函数 对象等都会成为window对象的属性
//    1  document其实是window对象的属性
    var name="属性";
    var fn = function(){
        document.write('方法')
    }
    document.write(window.name);
    window.fn();
</script>
</script>
```

### window内置全部变量和方法

- JavaScript 全局对象

全局属性和函数可用于所有内建的 JavaScript 对象。

![](http://on9plnnvl.bkt.clouddn.com/17-3-24/65175496-file_1490341585456_8e43.png)

    - Infinity
        
        不知道怎么获取
        
        表示js所有识别的最大的值
        
        1.7976931348623157e+308
        
        最小值：5e-324
        
    - 指数表示法
    
        如果数字巨大，可以使用指数表示法
        
        比如：
        
        1e1表示在1后面加1个0 ：10
        
        2e+3表示在2后面加3个0:    2000
        
        2e-3表示将2的小数点右移3位： 0.002
    
    - NaN
        
        它表示’不是数字‘的数字
        
        事实上 他是一个数字类型：
        
        typeof NaN  ：number
        
        如果我们再数字运算中使用了不恰当的操作数，导致运算失败，该运算就会返回NaN
        
        例如:var a = 10 * 'f'  --- NaN


- Window方法 -- 对话框

    - alert() 函数：弹出消息对话框（对话框中有一个OK按钮）

    - confirm() 函数：弹出消息对话框（对话框中包含一个OK按钮与Cancel按钮）

    - prompt() 函数：弹出消息对话框（对话框中包含一个OK按钮、Cancel按钮与一个文本输入框）
    
        ![](http://on9plnnvl.bkt.clouddn.com/17-3-24/79916517-file_1490340896931_16377.png)

- Window方法 - 时间等待与间隔函数

    setTimeout() 函数
    
    clearTimeout() 函数
    
    setInterval() 函数
    
    clearInterval() 函数

- Window方法 – 获取失去焦点

    focus() 函数：使窗体或空间获得焦点
    
    blur() 函数：使窗体或控件失去焦点


- Window方法 – 新窗口

    open() 函数：打开(弹出)一个新的窗体 
    
    close() 函数：关闭窗体 

![](http://on9plnnvl.bkt.clouddn.com/17-3-24/75058737-file_1490328422565_15751.png)

```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
</head>
<body>

<!--方法-->
<div>
    <input type="button" value="获得焦点"
           onclick="document.getElementById('testInput').focus()" />
    <input type="button" value="失去焦点"
           onclick="document.getElementById('testInput').blur()" />
    <input type="text" value="text" id="testInput"
           onblur="alert('我已失去焦点')" />
</div>

<!--方法-->
<div style="height:150%; width:150%; background-color:#ddd">
    <input type="button" id="btn1" value="移动滚动条！"
           onclick="window.scrollTo(100,100);" />　　
    <!--//相当于设置绝对位置-->
    <input type="button" id="btn2" value="移动滚动条！"
           onclick="window.scrollBy(100,100);" />　　
    <!--//相当于累加-->
</div>

<!--方法-->
<a href="2.html" target="2">在新窗口打开连接</a>
<a href="#" onclick="window.open('http://www.baidu.com');">在已建立连接的页面打开新地址</a>

</body>
</html>

<script>
    /*parseInt将其他类型数据转换成整数，转换失败就返回NaN*/
    window.parseInt('123')      /*123*/
    window.parseInt('abc123')   /*NaN*/
    window.parseInt('123abc')   /*123*/

    /*parseFloat将其他类型数据转换成小数，转换失败就返回NaN*/
    window.parseInt('123')      /*123*/
    window.parseInt('1.23')   /*1.23*/
    window.parseInt('1.23abc')   /*1.23*/

    /*inNaN 确定某个数值是否可以参与运算*/
    isNaN(123)   /*123可以参与运算，不是NaN，返回false*/


    /*eval 会将字符串当做js代码执行*/
    eval('var num=2')
    console.log(num+2)  /*结果是4*/
</script>

```



## 2.地址栏对象Location

地址栏对象表示的窗口的网页地址：

英文名称-Location

![](http://on9plnnvl.bkt.clouddn.com/17-3-24/42560260-file_1490334051842_fa7f.png)

### 面向对象分析地址栏

如果我们用面向对象思想分析网页地址，看看其包含哪些属性：

- URL网址：http://www.baidu.com
    
    URL属性

    我们在浏览器的地址栏里输入的网站地址叫做URL(Uniform Resource Locator，统一资源定位符)。

    就像每家每户都有一个门牌地址一样，每个网页也都有一个Internet地址。

    当你在浏览器的地址框中输入一个URL或是单击一个超级链接时，URL就确定了要浏览的地址


- 协议：http ftp

    - HTTP是Hyper Text Transfer Protocol，超文本传输协议
    - href：Hypertext Reference的缩写。意思是超文本引用。
        href 属性的值可以是任何有效文档的相对或绝对URL，包括片段标识符和JavaScript代码段。
    - MIME 类型
        MIME (Multipurpose Internet Mail Extensions) 是描述消息内容类型的因特网标准。
        MIME 消息能包含文本、图像、音频、视频以及其他应用程序专用的数据。
    
- 端口号：默认80
- 查询字符串？name=shukui&&password=123456

    什么是查询字符串？
    
    传参用
    
    举例：
    
    一个页面数据传给另一个页面，那就可以通过查询字符串，结构是？name=shukui&&password=123456
    
    window.location.search获取

### Location对象

```
function Location （）{
    this.href    		URL
    this.port		端口号
    this.protocol		协议
    this.host		
}
Location.prototype={
    reload:function(){}  表示重新加载当前页面
}
```

window.location.search

### 改变当前窗口地址

![](http://on9plnnvl.bkt.clouddn.com/17-3-24/99510052-file_1490341969568_2d47.png)

```
// 改变当前窗口地址
window.location = 'https://www.baidu.com';
// 如果在当前窗口下这样输入，则会在当前地址下面+该地址搜索
window.location = 'www.baidu.com'
location.href = "http://www.baidu.com";
location.assign("http://www.baidu.com");
location.replace("http://www.baidu.com");
// 刷新当前页面
window.location.reload();
window.location.reload(false);
// 服务器重新获取
window.location.reload(true);

```

![](http://on9plnnvl.bkt.clouddn.com/17-3-24/64533556-file_1490334554142_1622c.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
<button id="btn">打开一个新的窗口</button>
<button id="btn2">打开一个新的窗口2</button>
<button id="btn3">打开一个新的窗口Location（当前窗口内）</button>
<button id="btn4">刷新当前页面</button>
</body>
</html>
<script>
    document.getElementById('btn').onclick=function() {
        window.open('http://www.baidu.com')
    }

    document.getElementById('btn2').onclick=function() {
        window.open ('http://www.baidu.com','newwindow','height=100,width=400,top=0,left=0,toolbar=no,menubar=no,scrollbars=no, resizable=no,location=no, status=no')
    }

    //    我们可以控制窗口的各种属性：
    //    宽为100，高为400，距屏顶0象素，屏左0象素，无工具条，无菜单条，无滚动条，
    //    不可调整大小，无地址栏，无状态


    document.getElementById('btn3').onclick=function() {
        /*改变当前窗口的地址，则会打开新的网页*/
        window.location ='test.html'
        console.log(location.href)
        console.log(location.port)
        console.log(location.protocol)
    }

    document.getElementById('btn4').onclick=function() {
        /*改变当前窗口的地址，则会打开新的网页*/
       location.reload()
    }
</script>
```

### window总体概览

![](http://on9plnnvl.bkt.clouddn.com/17-3-24/88262171-file_1490334978201_1853b.png)

```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
<script>
    window.onload=function(){
        //打开链接
        document.getElementsByTagName('button')[0].onclick = function(){
//        window.location = "http://www.baidu.com";
        // location.href = "http://www.baidu.com";
        location.assign("http://www.baidu.com");
//      location.replace("http://www.baidu.com");
//        replace和assign的区别
//        replace()方法所做的操作与assign()方法一样，
//        但它多了一步操作，即从浏览器的历史记录中删除了包含脚本的页面，
//        这样就不能通过浏览器的后退按钮和前进按钮来访问它了，
//        assign()方法却可以通过后退按钮来访问上个页面。
        }
        //刷新页面
        document.getElementsByTagName('button')[1].onclick = function(){
            location.reload(true);    //从服务器重载当前页面
//        location.reload(false);   //从浏览器缓存中重载当前页面
//        location.reload();        //从浏览器缓存中重载当前页面
        }

//    hash：如果URL中包含有“#”，该方法将返回该符号之后的内容
//    （例如：http://www.itcast.cn/index.html#welcome的hash是“#welcome”）。

//    host：服务器的名字，例如www.itcast.cn。

//    hostname：通常等于host，有时会省略前面的www。

//    href：当前页面载入的完整URL。

//    pathname：URL中主机名之后的部分。例如：http://www.itcast.cn/html/js/index.html的pathname是“/html/js/index.html”。

//    port：URL中声明的请求端口。默认情况下，大多数URL没有端口信息（默认为80端口），所以该属性通常是空白的。像http://www.itcast.cn:8080/index.html这样的URL的port属性为8080。

//    protocol：URL中使用的协议，即双斜杠（//）之前的部分。例如http://www.itcast.cn中的protocol属性是http：
//    ftp://www.itcast.cn的protocol属性等于ftp:。

        //search：执行GET请求的URL中的问号?后的部分，又称查询字符串。
        // 例如http://www.itcast.cn/search.html?name=shukui中的search属性为?name=shukui。

//        document.write(
//                "hash:"+location.hash+"<br>"+
//                "host:"+location.host+"<br>"+
//                "hostname:"+location.hostname+"<br>"+
//                "href:"+location.href+"<br>"+
//                "pathname:"+location.pathname+"<br>"+
//                "port:"+location.port+"<br>"+
//                "protocol:"+location.protocol+"<br>"+
//                "search:"+location.search
//        );
    }

</script>
<button>打开链接</button>
<button>重新加载当前页面 - 刷新</button>
<hr>

</body>
</html>

</script>
```

## 3.历史访问记录对象history

**备忘录项目中可以使用**

H5中有一个：`window.history.pushState`

```
if (window.history && history.pushState) {
    history.pushState(title, '不支持', "?t=" + title);
}
```

### 示例1

![](http://on9plnnvl.bkt.clouddn.com/17-3-24/12487860-file_1490335616858_1001a.png)

```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
<input type=button value=刷新 onclick="window.location.reload()">
<input type=button value=前进 onclick="window.history.go(1)">
<input type=button value=后退 onclick="window.history.go(-1)">
<input type=button value=前进 onclick="window.history.forward()">
<input type=button value=后退
       onclick="window.history.back()">
<input type=button value=后退+刷新
       onclick="window.history.go(-1);window.location.reload()">
</body>
</html>

```

### 示例2

test0.html:

![](http://on9plnnvl.bkt.clouddn.com/17-3-24/9220617-file_1490342627838_15089.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
<button id="btn1">打开一个新的窗口Location</button>
<button id="btn2">前进</button>
</body>
</html>
<script>
    document.getElementById('btn1').onclick=function() {
        /*改变当前窗口的地址，则会打开新的网页*/
        window.location ='test1.html'
    }
    document.getElementById('btn2').onclick=function() {
        /*改变当前窗口的地址，则会打开新的网页*/
        history.forward()
    }
</script>
```

test1.html:

![](http://on9plnnvl.bkt.clouddn.com/17-3-24/88232912-file_1490342672128_21cc.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        div{
            font-size:50px
        }
    </style>
</head>
<body>
<div>页面1</div>
<button id=btn>打开页面2</button>
<button id=btn1>回退</button>
<button id=btn2>前进</button>
</body>
</html>
<script>
    document.getElementById('btn').onclick=function() {
        /*改变当前窗口的地址，则会打开新的网页*/
        window.location ='test2.html'
    }

    document.getElementById('btn1').onclick=function() {
        history.back()
    }

    document.getElementById('btn2').onclick=function() {
        history.forward()
    }
</script>
```

test2.html:

![](http://on9plnnvl.bkt.clouddn.com/17-3-24/95056324-file_1490342703573_2563.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        div{
            font-size:50px
        }
    </style>
</head>
<body>
<div>页面2</div>
<button id=btn>回退</button>
</body>
</html>
<script>
    document.getElementById('btn').onclick=function() {
        /*改变当前窗口的地址，则会打开新的网页*/
        history.back()
    }
</script>
```

## 4.DOM对象

### 基础

window窗口的核心内容当然是就是我们每天看到的网页了

![](http://on9plnnvl.bkt.clouddn.com/17-3-24/18043794-file_1490342808220_11a8b.png)

- html是一种树结构

    我们编写的html内容会被编译成一个dom树

    ![](http://on9plnnvl.bkt.clouddn.com/17-3-24/79812546-file_1490342855702_faca.png)

- DOM对象树结构

    ![](http://on9plnnvl.bkt.clouddn.com/17-3-24/17867771-file_1490342882338_9dbe.png)

- 编译成一颗树的目的

    当我们把html文档编译成一棵树之后，我们就可以对这颗树进行编程 :增删查改

    - 增：新增一个节点 - 树长出一个新的枝
    - 删：删除某个节点 - 砍掉树的某个枝
    - 查：可以查找树的各个元素
    - 改：可以修改元素

- 树结构的特点和术语

    - 根节点
    - 元素节点 
    - 兄弟节点
    - 父亲节点
    - 儿子节点
    - 子孙节点
    - 祖父节点
    - 属性和属性值

### DOM查询

#### 原生js查询

- 查询 - 基础

    getElementById
    
    getElementByTagName
    
    getElementByClassName


- 查询 - 兄弟姐妹 八辈祖宗

    ```
    parentNode    		获取该节点的父节点    
    childNodes    		获取该节点的子节点数组
    firstChild    			获取该节点的第一个子节点
    lastChild    			获取该节点的最后一个子节点
    nextSibling    		获取该节点的下一个兄弟元素
    previoursSibling    		获取该节点的上一个兄弟元素
    firstElementChild        	第一个子元素节点
    lastElementChild        	最后一个子元素节点
    nextElementSibling       	   下一个兄弟元素节点
    previousElementSibling    	 前一个兄弟元素节点
    childElementCount        	子元素节点个数量
    ```

- 祖宗八辈图

    ![](http://on9plnnvl.bkt.clouddn.com/17-3-24/5130941-file_1490343264027_936a.png)
    
#### jquery查询

- jquery查询：常规选择器

        elemen
        
        根据给定（html）标记名称选择所有的元素
        
        #id 
        
        选择一个具有给定id属性的单个元素
        
         .class
         
        选择给定样式类名的所有元素。


- jquery查询：层级选择器

        parent > child  
        选择所有指定“parent”元素中指定的"child"的直接子元素
        ancestor descendant 
        选择所有指定“parent”元素中指定的"child"的直接子元素
        prev + next 
        选择所有紧接在 “prev” 元素后的 “next” 元素
        prev ~ siblings
        匹配 “prev” 元素之后的所有 兄弟元素。具有相同的父元素，并匹配过滤“siblings”选择器




- jquery查询：基本过滤器

        :eq(index)  	在匹配的集合中选择索引值为index的元素
        :gt(index) 	选择匹配集合中所有大于给定index的元素
        :lt(index) 		选择匹配集合中所有索引值小于给定index参数元素
        :not(selector)  	选择所有元素去除不匹配给定的选择器的元素
        :even  		选择所引值为偶数的元素，从 0 开始计数。 
        :odd       		选择索引值为奇数元素，从 0 开始计数。
        :first 		选择第一个匹配的元素
        :last 		选择最后一个匹配的元素

- jquery查询：内容过滤

         :contains(text) 
        选择所有包含指定文本的元素
        :empty 
        选择所有没有子元素的元素（包括文本节点）
        :has(selector) 
        选择元素其中至少包含指定选择器匹配的一个种元素

- jquery查询：可见过滤
        
        :hidden  
        选择所有隐藏的元素
         :visible  
        选择所有可见的元素

### DOM新增或者创建

#### 基础

- 新增基础方法

        div.innerHTML='124'
        div.innerHTML='<p>123</p>'

-  通过创建元素的方式新增 

    textContent -- 重要

    ```
    var p= document.createElement("p"); 
    p.textContent = "新建一个P节点"; 
    document.getElementById("div1").appendChild(p); 
    ```

#### jquery 创建

```
var $li_1 = $("<li>香蕉</li>");    
//  创建一个<li>元素，包括元素节点和文本节点                                               
var $li_2 = $("<li>雪梨</li>");    
//  创建一个<li>元素，包括元素节点和文本节点

var $parent = $("ul");        
// 获取<ul>节点。<li>的父节点
 $("ul").append($li_1);        
// 添加到<ul>节点中，使之能在网页中显示 或者 
$parent.append($li_1);
$("ul").append($li_2);        
// 添加到<ul>节点中，使之能在网页中显示 或者 $parent.append($li_2);

```

### DOM删除

- removeChild()

```
由父元素调用，删除一个子节点。
注意是直接父元素调用，删除直接子元素才有效，
删除孙子元素就没有效果了。

<div id="div1"> 
<p id="p1">我是第一个P</p> 
<p id="p2">我是第二个P</p> 
</div> 
window.onload = function () { 
var div1 = document.getElementById("div1"); 
div1.removeChild(document.getElementById("p2")); } 

```
    
- Jquery删除

```
empty()  
删除所有匹配元素的内容,只是内容,还剩自己这个架子
remove(expr)  
删除所有匹配的DOM元素，包括自己...


```

### DOM 属性样式操作

- 样式增删查改

```
var div = document.getElementById("div1")
div.style.backgroundColor = "yellow"; 
```

- 元素属性的增删查改

```
通用属性操作：
  obj.name=‘123’
alert（obj.name）
obj.setAttribute(属性的名字，属性的值)
obj.getAttribute(属性的名字)
class操作：obj.className=” “;
img的src的操作：imgobj.src=” “;
input的值操作：inputobj.value

```

- 元素内容增删查改

innerHTML与innerText

```
innerHTML与innerText的区别：
就是对HTML可以放置html代码，Text不会输出HTML代码 
Text只有IE支持，不建议使用
alert(document.getElementById("p1").innerText); 
alert(document.getElementById("p2").innerHTML); 


jquery的html方法解决了各个浏览器的兼容性
如果我们自己写这个函数需要研究各个浏览器的差别

```

- jquery：属性attr

```
attr(attributeName)
 获取第一个元素属性值
attr(attribute, value) 
设置每一个元素属性
 attr(attributeObject) 
设置每一个元素的多个属性
attr(attributeName, function(index, oldAttributeName){}) 
为每一个元素设置属性
```

- jquery：表单元素值val

```
val() 
获取第一个元素值
val(value) 
设置每一个元素值
val(function(index, oldValue){})
 设置每一个元素的值
```

- jquery：样式css

```
 css(cssName) 
获取第一个元素css属性值
 css(cssNameArray) 
获取多个css属性值
css(name, value) 
设置每一个元素css属性
css(cssObject) 
设置每一个元素的多个css属性
css(cssName, function(index, oldCssName){}) 
为每一个元素设置css属性
```
- jquery：hasClass、addClass、removeClass

```
 hasClass() 判断元素是否拥有某类
addClass() 为每一个元素添加类
removeClass() 为每一个元素删除类
```

注意，**addClass为例**，其实要想掌握，还是得留心的：

```
$("p").addClass("selected");
// 加两个类名
$("p").addClass("selected1 selected2");
// 回调函数形式
$('ul li:last').addClass(function() {
  return 'item-' + $(this).index();
});
```

还有就是，**jQuery如何动态生成DOM元素**：

```
$('<div></div>')
```

结合以上两个就是：

`$('<div></div>').addClass("selected1 selected2");`

- jquery：height与width

```
width() 获取第一个元素宽度值
width(value) 设置每一个元素宽度值
width(function(index, oldValue){}) 设置每一个元素的宽度值
height() 获取第一个元素高度值
height(value) 设置每一个元素高度值
height(function(index, oldValue){}) 设置每一个元素的高度值
```

- jquery：坐标值offset

```
offset() 
获取第一个元素坐标值
offset(value) 
设置每一个元素坐标值
offset(function(index, oldValue){}) 
设置每一个元素的坐标值
```

- jquery：position

**理解jQuery的offset和position**

![](http://on9plnnvl.bkt.clouddn.com/17-3-24/18950684-file_1490344435426_101db.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        #box1 {
            position: relative;
            left: 100px;
            width: 100px;
            height: 100px;
            background-color: pink;
        }
        #box2 {
            width: 10px;
            height: 10px;
            background-color: grey;
            position: relative;
            left: 10px;
        }
    </style>
    <script src="http://libs.baidu.com/jquery/1.10.2/jquery.min.js"></script>
</head>
<body>
<div id="box1">
    <div id="box2">
        <div id="box3"></div>
    </div>
</div>
</body>
</html>
```


## 最后

各个对象都有自己的API，理解，做备忘录小项目时候应该会用到。


## 几个面试题

```
以下哪些是javascript的全局函数：（）

A. escape
B. parseFloat
C. eval
D. setTimeout
E. alert

ABC


关于IE的window对象表述正确的有：（）
A. window.opener属性本身就是指向window对象
B. window.reload()方
C. window.location=”a.h法可以用来刷新当前页面tml”和window.location.href=”a.html”的作用都是把当前页面替换成a.html页面
D. 定义了全局变量g；可以用window.g的方式来存取该变量

ACD
B ：应该是location.reload或者window.location.reload


列举浏览器对象模型BOM里常用的至少4个对象，并列举window对象的常用方法至少5个 （10分）

对象：Window document location screen history navigator

方法：Alert() confirm() prompt() open() close() 



怎样添加、移除、移动、复制、创建和查找节点
```







