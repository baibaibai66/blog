# ng路由、服务

## 介绍

http://www.runoob.com/angularjs/angularjs-routing.html

```
http://runoob.com/#/first

http://runoob.com/#/second

http://runoob.com/#/third
```

当我们点击以上的任意一个链接时，向服务端请的地址都是一样的 (http://runoob.com/)。

因为 # 号之后的内容在向服务端请求时会被浏览器忽略掉。 

所以我们就需要在客户端实现 # 号后面内容的功能实现。

AngularJS 路由 就通过 # + 标记帮助我们区分不同的逻辑页面并将不同的页面绑定到对应的控制器上。

## 关于与单页应用SPA的结合 -- 两种解决方案

![](http://i1.piimg.com/567571/1199ef881ebe25ac.png)

是这样的，就拿之前百度首页的案例来说，当你点击一个button能更换主页内某一块儿区域的时：

`$('#container').innerHTML = str;`

顶部window.loacation区域是不会变的。这里就有一个问题，当你点击一个button出现你想要的内容，当你想要分享出去这个网页的内容的时候，URL只有那一个，当别人点击这个URL时候，并不一定能直接看到你所看到的网页样子。所以，这时候就有一个需求：

点击一个button时候，网页window.location里面URL是变的，同时，**不跳转**到另一个网页、**不刷新**。

这里，就有两种方式了：

1. 锚点，为在location里面加hash -- #

    检测锚点变化 -- 基本逻辑：
    
    ```
    // 监听锚点变化，发送请求
    // hashchange事件监听锚点变化
    window.addEventListener('hashChange', function() {})
    
    // 拿到hash值；锚点
    var hash = window.location.hash;
    处理#号
    hash = hash.slice(1);
    // 实例对象
    var xhr = null;
    // 将锚点作为参数进行传递
    xhr.open('get', 'aaaa.php?hash')
    
    xhr.send()
    
    xhr.onreadystatechange = function() {
        if (xhr.readyState == 400 && xhr.status == 200) {
            xhr.responseText
            // 将返回结果添加页面
        }
    }
    ```

    angularJS就是这种核心思想的封装，进行完善。
    
    对比：
    
    ```
    <script>
		
		$.ajax({
			url: '',
			type: 'get/post',
			dataType: 'jsonp',
			// data: {name: 'itcast', age: 10}, // name=itcast&age=10
			data: 'name=itcast&age=10',
			// 能不能设置请求头？
			success: function (data) {
				// data 返回的数据
			}
		});

		// XMLHttpRequest; 是不能完成跨域访问的

		$http({
			url: 'example.php?call=JSON_CALLBACK',
			method: 'jsonp',
			headers: {}, // 请求头
			data: {}, // post
			params: {
				call: 'JSON_CALLBACK' // angular_callback.0({name: 1})
			}, // get
		}).success(function (info) {
			// 
		});

		function fn(arg) {

			alert(1);
		}
	</script>
    ```

2. H5新特性之操作历史记录 -- window.history.pushState 

    使用之前先进行判断：
    
    ```
    // 操作历史记录
    if (window.history && history.pushState) {
    // 添加一个新的历史记录;1.状态 2.长按回退按钮可以看到的历史记录名字 3.真正URL
    history.pushState(title, 'title没有任何浏览器支持', '?t=' + title);
    } else {
    console.log('不支持');
    }
    ```
    
    关于上面几个参数：
    
    第一个参数，是用在当popstate时候，事件e的state属性 -- e.state
    
    ```
     // 当我们在伪造的访问历史中前进或后退时会执行一个popstate事件
      window.addEventListener('popstate', function(e) {
        content.innerHTML = data[e.state];
      });
    ```
    
    上面就实现了不跳转、不更新，但是URL变化。还有一个问题，当别人点击这个URL时候，呈现相应的内容：
    
    ```
    // window.location = "https://www.baidu.com";
      // 第一次请求过来 获取地址栏中的t参数
      // window.location可以拿到当前网页中跟地址相关的信息
      var search = window.location.search; // ?t=jkaljdksfla
      // 如果地址栏中的地址有中文，会以URL编码方式呈现
      // decodeURI 可以转换到之前中文
      var title = search.split('=')[1]; // ['?t','jkaljdksfla']
      if (title) {
        // 有值 decodeURI作用就是从URL编码转换到之前的状态
        console.log(decodeURI(title));
        content.innerHTML = data[decodeURI(title)];
      }
    ```
    这里就需要获取你pushState()时候设置的URL了。然后对相应的URL展现相应的内容。
    
    
### 使用

1. 引入angular-route.js

![](http://i4.buimg.com/567571/f60181e4ad95f2a4.png)

2. 实例化模块（App）时，当成依赖传进去（模块名称叫ngRoute）

![](http://i4.buimg.com/567571/3ae848506bbaefda.png)

3. 配置路由模块

![](http://i1.piimg.com/567571/a17b25483aa73b68.png)

4. 布局模板

通过ng-view指令布局模板，路由匹配的视图会被加载渲染到些区域。

![](http://i4.buimg.com/567571/12ac55a9aa384482.png)

可能有一个缺点 -- 搜索引擎可能无法抓取ajax页面

### 路由参数
$routParams服务 获取

`/#/index?name=aaa&&password=1`

`/in_theaters:page`

两种传参方式：

：
？

## 一个简单的实例

![](http://i4.buimg.com/567571/7869e3a9b444e134.png) 

```
<!DOCTYPE html>
<html lang="en" ng-app="App">
<head>
	<meta charset="UTF-8">
	<title>AngularJS 路由和多视图</title>
	<style>
		body {
			padding: 0;
			margin: 0;
			background-color: #F7F7F7;
			font-family: Arial;
		}

		.wrapper {
			max-width: 980px;
			margin: 50px auto;
		}

		ul {
			padding: 0;
			margin: 0;
			overflow: hidden;
			list-style: none;
			background-color: #000;
			border-radius: 4px;
		}

		li {
			float: left;
			width: 120px;
			height: 40px;
			text-align: center;
			line-height: 40px;
			font-size: 18px;
		}

		li.active {
			background-color: #333;
		}

		li a {
			display: block;
			color: #FFF;
			text-decoration: none;
		}

		.content {
			margin-top: 30px;
			font-size: 24px;
			padding: 0 20px;
		}
	</style>
</head>
<body>
	<div class="wrapper">
		<!-- 导航菜单 -->
		<ul>
			<li class="active">
				<a href="#/index">Index</a>
			</li>
			<li>
				<a href="#/introduce">Introduce</a>
			</li>
			<li>
				<a href="#/contact">Contact Us</a>
			</li>
			<li>
				<a href="#/list">List</a>
			</li>
		</ul>
		<!-- 内容 -->
		<div class="content">
			<!-- 占位符 -->
			<div ng-view></div>
		</div>

	</div>
	<!-- AngularJS核心框架 -->
	<script src="./libs/angular.min.js"></script>
	<!-- 路由模块理解成插件 -->
	<script src="./libs/angular-route.js"></script>
	<script>
		// 依赖ngRoute模块
		var App = angular.module('App', ['ngRoute']);

		// 需要对路由模块进行配置，使其正常工作
		App.config(['$routeProvider', function ($routeProvider) {

			$routeProvider.when('/index', {
				// template: '<h1>index Pages!</h1>',
				templateUrl: './abc.html'
			})
			.when('/introduce', {
				template: '<h1>introduce Pages!</h1>'
			})
			.when('/contact', {
				// template: '<h1>contact US Pages!</h1>',
				templateUrl: './contact.html',
				controller: 'ContactController' // 定义控制器
			})
			.when('/list', {
				templateUrl: './list.html', // 视图模板
				controller: 'ListController' // 定义控制器
			})
			.otherwise({
				redirectTo: '/index'
			});

		}]);

		// 列表控制器
		App.controller('ListController', ['$scope', '$http', function ($scope, $http) {
			// 模型数据
			// $scope.items = ['html', 'css', 'js'];

			// $http({
			// 	url: '10-02.php',
			// }).success(function (info) {
			// 	// console.log(info);

			// 	$scope.items = info;
			// });
		$scope.content = 'aaaaaaaaaa';

		$scope.items = [
		'aaa', 'bbb', 'ccc'
		]
		}]);

		App.controller('ContactController', ['$scope', '$http', function ($scope, $http) {

			// $http({
			// 	url: 'contact.php'
			// }).success(function (info) {
			// 	$scope.content = info;
			// });
			$scope.content = 'aabbbaaaa';
		}]);

	</script>

</body>
</html>
```