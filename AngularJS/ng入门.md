# 是什么

前端框架

![](http://i4.buimg.com/567571/20c1687fc288991f.png)

# 有什么用

## 特点：

    MVC
    
    模块化
    
    自动化双向数据绑定
    
    指令系统

# 怎么用？ -- ng语法

ng-app

ng-model -- 跟value和innerHTML有关


模型（Model）数据是要展示到视图（View）上的，所以需要将控制器（Controller）关联到视图（View）上，通过为HTML标签添加ng-controller属性并赋值相应的控制器（Controller）的名称，就确立了**关联关系**。

 

所有需要ng管理的代码必须被包裹在一个有ng-app指令的元素中

ng-app是ng的入口，表示当前元素的所有指令都会被angular管理（对每一个指令进行分析和操作）

![](http://on9plnnvl.bkt.clouddn.com/17-3-30/89835574-file_1490844836213_e9b8.png)

## 安装

无论是bower还是npm，都是安装，只是工具安装，更方便简洁。

用CDN方式也可以：http://apps.bdimg.com/libs/angular.js/1.4.6/angular.min.js

总之，在创建了一个项目以后，你要想使用angular，那你就得引包（上面几种方式）。

演示bower引包方式：

```
bower init

bower install angular
```

### 百度静态资源库

http://cdn.code.baidu.com/

为什么使用别人的CDN：

客户端登录你的网站，从别的地方下载angular，快，降低自身带宽、流量，明白了吧。

![](http://on9plnnvl.bkt.clouddn.com/17-3-30/92184328-file_1490849045286_5c43.png)


## 初使用

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<div ng-app>
    <input type="text" placeholder="输入" ng-model="user.name">
    <p>hello <strong>{{user.name}}</strong></p>
</div>

<script src="bower_components/angular/angular.js"></script>
</body>
</html>
```

![](http://on9plnnvl.bkt.clouddn.com/17-3-30/90734133-file_1490845018584_165ac.png)

## 上面案例分析

当网页加载完毕，AngularJS 自动开始执行；

HTML 页面中 ng-xxx **的属性称之为指令**（Directive）；

ng-app 指令告诉 AngularJS，<div> 元素是 AngularJS 应用程序**管理的边界**；

ng-model 指令把文本框的值绑定到变量 name 上 -- 双向数据绑定的指令

![](http://on9plnnvl.bkt.clouddn.com/17-3-30/97733821-file_1490847268312_744.png)

{{ name }} 表达式就是把应用程序变量 name 绑定到某个段落的 **innerHTML**。


解放了传统js中频繁的DOM操作，让js更专注业务逻辑


## 事例：登录界面 -- 业务逻辑

![](http://on9plnnvl.bkt.clouddn.com/17-3-30/85178552-file_1490847484634_a630.png)

### js逻辑：

![](http://on9plnnvl.bkt.clouddn.com/17-3-30/52285355-file_1490847682475_6875.png)

1. 给按钮注册点击事件
2. 拿到文本框1/2
3. 判断值是否合法 -- 邮箱、密码

### 业务逻辑 -- 校验表单数据是否合法：

给两个值，判断是否合理

![](http://on9plnnvl.bkt.clouddn.com/17-3-30/76307044-file_1490847783819_2365.png)

依赖程度低、耦合度低；关联更少；

## 可以启动Chrome时候，让本地打开的file文件支持ajax请求...

## npm自带的httpserver启动静态服务器

hs -o [-p 8888]

![](http://on9plnnvl.bkt.clouddn.com/17-3-30/53263982-file_1490848099345_1662b.png)

## 模块Module

angular.module('')

模型和控制器

注册模块 通过module函数，
 
第一个参数是这个模块的名字

!!! 第二个参数是这个模块所依赖的模块,

如果不依赖任何模块也必须传递第二个参数，如果没有传递第二个参数，angular.module就不是创建一个模块

angular.module 返回 刚刚创建的模块对象

```
var app = angular.module('myApp',[]);
```

app.controller 方法用于创建一个控制器，所创建的控制器属于myApp模块

// app.controller('DemoCtrl');

控制器函数的参数中有一个`$scope`

```
angular.module('myApp').controller('DemoController', function($scope) {
// 当控制器执行时会自动执行的函数
$scope.user = {};
$scope.user.name = '张三';
// $scope不仅仅可以往视图中暴露数据，还可以暴露行为
$scope.show = function() {
 console.log($scope.user);
    };
});
```

### 案例

![](http://on9plnnvl.bkt.clouddn.com/17-3-30/62462004-file_1490850954538_696b.png)

```

<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <title>Angular 模块</title>
</head>

<body>
  <div ng-app="myApp" ng-controller="DemoController">
    <h1>使用NG实现双边数据绑定</h1>
    <input type="text" placeholder="请输入你的姓名" ng-model="user.name">
    <p>hello <strong>{{user.name}}</strong></p>
    <input type="button" ng-click="show()">
  </div>
  <script src="bower_components/angular/angular.js"></script>
  <script>
    // 注册模块 通过module函数，
    // 第一个参数是这个模块的名字
    // !!! 第二个参数是这个模块所依赖的模块, 如果不依赖任何模块也必须传递第二个参数，如果没有传递第二个参数，angular.module就不是创建一个模块
    // angular.module 返回 刚刚创建的模块对象
   var app=  angular.module('myApp',[]);
    // app.controller 方法用于创建一个控制器，所创建的控制器属于myApp模块
//     app.controller('DemoCtrl');
    // 控制器函数的参数中有一个$scope
     angular.module('myApp').controller('DemoController', function($scope) {
    //   // 当控制器执行时会自动执行的函数
       $scope.user = {};
       $scope.user.name = '张三';
    //   // $scope不仅仅可以往视图中暴露数据，还可以暴露行为
       $scope.show = function() {
         console.log($scope.user);
       };
     });
  </script>
</body>

</html>

```

## 控制器

### 语法

```
<body ng-app="myModule" ng-controller="HelloController">
  <script src="bower_components/angular/angular.js"></script>
  <script>
    // 由于控制器是必须出现在某个模块下的，想创建一个控制器必须先创建模块
    var module = angular.module('myModule', []); // 返回的就是模块对象

    // angular在执行控制器函数时，
    // 会根据参数的名字（$scope）去自动的注入对象
    // 根据参数名称传递对应对象，所以必须要写正确的参数名称
    // module.controller('HelloController', function($scope) {
    //   console.log($scope);
    // });
    //
    // 由于压缩代码会改变参数名称，注册控制的标准方式就是通过第二个参数传递数组的方式（数组的成员最后一个就是原本的控制器函数，前面的成员都是需要注入的对象名称）
    module.controller('HelloController', ['$scope','$http', function(a,b) {
      console.log(a);
    }]);
  </script>
</body>
```

### controller职责

1. 为应用中的**模型model设置初始状态**

2. 通过$scope对象把数据**模型model**或函数行为**暴露给视图view**

3. 监视模型model的变化，做出相应的动作

### 使用

![](http://on9plnnvl.bkt.clouddn.com/17-3-30/45362946-file_1490853916346_3c82.png)

```
<!DOCTYPE html>
<html lang="en" ng-app="myApp">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<table border='1' ng-controller="myController">
    <tr>
        <td>用户名</td>
        <td>
            <input type="text" ng-model='user.username'>
        </td>
    </tr>
    <tr>
        <td>密码</td>
        <td>
            <input type="password" ng-model='user.password'>
        </td>
    </tr>
    <tr>
        <td>{{user.username}}</td>
        <td>
            <input type="button" value='show' ng-click="click()">
        </td>
    </tr>
</table>

<script src="bower_components/angular/angular.js"></script>

<script>
    // 创建一个模块
    var app = angular.module('myApp', []);
    // 为这个模块创建一个控制器
    app.controller('myController', ['$scope', function ($scope) {
        // 数据
        $scope.user = {
            username: '',
            password: ''
        };
        // 行为数据
        $scope.click = function () {
            // 因为数据的变化时双向的同步，所以界面上的值变化会同步到$scope.user上
            console.log($scope.user);
        }
    }])
</script>
</body>
</html>
```

## $scope（上下文模型）

1. 视图view和控制器controller之间的桥梁
2. 用于在视图和控制器之间传递数据
3. 利用$scope暴露数据模型（数据，行为）

![](http://on9plnnvl.bkt.clouddn.com/17-3-30/32650853-file_1490855300783_1157d.png)


## $watch

![](http://on9plnnvl.bkt.clouddn.com/17-3-30/83160666-file_1490854735064_8593.png)

![](http://on9plnnvl.bkt.clouddn.com/17-3-30/63669661-file_1490854742234_92dd.png)

![](http://on9plnnvl.bkt.clouddn.com/17-3-30/11632930-file_1490854750352_2dc8.png)

```
<!DOCTYPE html>
<html lang="en" ng-app="myApp">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<table border='1' ng-controller="myController">
    <tr>
        <td>用户名</td>
        <td>
            <input type="text" ng-model='user.username'>
        </td>
    </tr>
    <tr>
        <td>密码</td>
        <td>
            <input type="password" ng-model='user.password'>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>
            <input type="button" value='show' ng-click="click()">
        </td>
    </tr>
    <tr>
        <td></td>
        <td>{{message}}</td>
    </tr>
</table>

<script src="bower_components/angular/angular.js"></script>

<script>
    // 创建一个模块
    var app = angular.module('myApp', []);
    // 为这个模块创建一个控制器
    app.controller('myController', ['$scope', function ($scope) {
        // 数据
        $scope.user = {
            username: '',
            password: ''
        };
        $scope.message = '请输入'
        // 行为数据
        $scope.click = function () {
            // 因为数据的变化时双向的同步，所以界面上的值变化会同步到$scope.user上
            console.log($scope.user);
        }
        // 官方的API中提供了一个$scope.$watch方法，
        $scope.$watch('user.username', function (now, old) {
            // 当user.username发生变化时触发这个函数
            // console.log('now is ' + now);
            // console.log('old is ' + old);
            if (now) {
                if (now.length < 5) {
                    $scope.message = '用户名太短'
                }
                else {
                    $scope.message = 'ok'
                }
            }
        })

        // angular 基本不用操作DOM，如果必要，可以使用angular提供的jqlite
        //
        // angular.element('body')
    }])
</script>
</body>
</html>
```

## 表达式（Expression）

作用：

使用 表达式 把数据绑定到 HTML。

语法：

表达式写在双大括号内：{{ expression }}
。
比较：

表达式作用类似于ng-bind指令

建议更多的使用指令


```
数字	{{ 100 + 100 }}
字符串	{{ 'hello' + 'angular' }}
对象	{{ zhangsan.name }}
数组	{{ students[10] }}

```

### 对比 JavaScript 表达式

相同点：

AngularJS 表达式可以包含字母，操作符，变量。

不同点：

AngularJS 表达式可以写在 HTML 中。

AngularJS 表达式不支持条件判断，循环及异常。

AngularJS 表达式支持过滤器。


## 单向数据绑定

模型变化过后，自动同步到界面上；

一般纯展示型的数据会用到单项数据绑定；

使用表达式的方式都是单向的

## 双向数据绑定

两个方向的数据自动同步：

模型发生变化自动同步到视图上；

视图上的数据发生变化过后自动同步到模型上；
