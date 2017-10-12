---
title: angular学习总结
date: 2017-10-12 10:31:41
author: 鸿基梦
categories: 学习
tags: angular
---
1.定义：Google开源的前端JS结构化框架

  作用：动态展示页面数据，并与用户交互

  指令：nagular定义的属性/标签/样式/注释

  -- ng-app(指令):告诉angular管理当前标签声明所在的整个标签都由angular来解析管理

  -- ng-model:将当前输入框的值与谁关联(属性名：属性值),并作为跟作用域对象($rootScope)的属性

    将当前输入框的值关联到内存的$rootScope对象的指定属性(username)上

  -- {{表达式}}:显示数据，从作用域对象的指定属性名上取 显示作用域对象($rootScope)上的属性值上

  -- ng-inint: 初始化

  特性：双向数据绑定、声明式依赖注入、解耦应用逻辑，数据模型和试图、完善的页面指令、定制表单验证、Ajax封装、测试更方便

2.angular是支持双向数据绑定的

  View(视图):页面(标签、指令、表达式)；Model(模型):作用域对象(属性、方法)；

  数据绑定： 数据从一个地方流向另一个地方，数据从一个位置自动流向另一个位置

  单项数据绑定：只支持一个方向;

  View --> Model  : ng-init

  Model --> View  : {{name}}

  双向数据绑定：

  Model <--> View : ng-model
  
3.作用域：是一个js实例对象

  这个对象的属性、方法，页面都可以直接引用、操作

  ng-app指令: 内部创建一个根作用域($rootScope),是所有其它作用域的父对象

4.控制器：

  也是一个对象，是我们View与Model之间的桥梁

  当我们使用了ng-controller指令，内部就会创建控制器对象

  但我们同时的提供控制器的构造函数(必须定义一个$scope的形参)

  每定义一个ng-controller指令，内部就会创建一个新的作用域对象输入构造函数中
    
5.依赖注入：

  依赖的对象被别人(调用者)自动注入(传参)

  注入的方式： 内部注入:不动态

  全局变量：污染全局环境

  形参： 动态  这种最好

  angular就是通过声明式依赖注入，得到作用域对象

  形参名不能随便定义(只是针对当前这种写法)
  
6.模块：

  也是一个对象；

  创建模块对象：angular.module('模块名', [依赖的模块])

  通过模块添加控制器：

    module.controller('MyController', function($scope){操作$scope的语句}

  angular的整体设计也是多模块的

    核心模块：angular.js

    扩展模块：angular-router.js angular-message.js angular-animate.js

7.表达式：

  {{js表达式}}

  从作用域对象中读取对应的属性数据来显示数据

  不支持if/for/while

  支持三目表达式
    
8.Angular指令：指令(标签、标签属性、类、注释)

  Angular与Angular的Model交互，扩展页面的动态表现力

  --常用的内置指令：

    ng-app：指定模块名，angular管理的区域

    ng-model：双向绑定，输入相关标签（常用于input）

    ng-init： 初始化数据

    ng-click：调用作用域对象的方法(点击时)

    ng-controller：指定控制器构造函数名，内部会自动创建一个新的作用域(外部的)

    ng-bind：解决使用{{}}显示数据的闪屏(在很短时间内显示{{}})

    ng-repeat：遍历数组显示数据，数组有几个元素就会产生几个新的作用域('item in arr');

        -- 属性： $index、$first、$last、$middle、$odd、$even

    ng-show：布尔类型，如果为true才会显示；false不显示隐藏

    ng-hide：布尔类型，如果为false才会显示；true不显示隐藏
  
9.过滤器：

  在显示数据时可以对数据进行格式化或过滤

    单个-->格式化(将别的类型的数据转化为特定格式的字符串)

    多个-->过滤(内部的个数变化，但类型不变) -- 不会真正改变被操作数据
  ```bash
  语法：{{express | 过滤器名:补充说明}}
  ```
  --常用内置过滤器：

    currentcy:货币格式化(文本)

    number：数值格式化(文本)

    date：将日期对象格式化(文本)

    json：将js对象格式化为json(文本)

    lowercase：将字符串格式化为全小写(文本)

    uppercasw：将字符串格式化为全大写(文本)

    limitTo：从一个数组或字符串中过滤出一个新的数组或字符串(根据下标过滤)

    orderBy:根据指定作用域属性对对象进行排序

    filter：从数组中过滤返回一个新数组(根据数据过滤)
      
10.自定义过滤器：

   内置过滤器有限，不能满足页面显示数据的需求

   语法：

   ``` bash
    module.filter('myLimitTo', function(){
      return function(value, startIndex, endIndex){
        // 对value进行过滤处理，并return处理的结果
        // 不要修改value本身
      }
    });

    ```   
11.编写Angular应用的基本步骤：

  -- 编写基本静态页面；

  -- 将angular.js引入工程中，并在页面中引入

  -- 在页面中指定ng-app, ng-controller

  -- 在js中定义model和controller

  -- 在controller中初始化数据($scope)

  -- 在页面中通过表达式或指令来显示数据

  -- 在页面中使用ng-click添加点击监听，并定义对应的方法进行操作
    
12.服务：

  为所有(angular)的应用提供特定功能服务的对象(单例),具有特定的功能可以是Object对象、函数、数组和基本类型

  Augular内置多个服务(都以$开头),在controller函数中可以声明注入服务并直接使用

  也可以自定义服务，但不要以$开头  

  -- 常用的内置服务：

    $rootScope与$scope（作用域）

    $filter（自定义）

    $http（数据交互）

    $timeout与$interval

  当一个非angular调用的回调函数执行后，不会进行脏数据检查，即使数据变化也不会改变

  显示、更新界面的基本步骤

    1):  进行脏数据检查

    2):  如果有变化，就去更新对应处
      
13.自定义服务：

  factory():  可以自定义 对象 函数 。。。   -- 最常用

  service():  只能是对象

  provider():

  value():

  constant():
      
14.指令：（angular中最常用，用在html页面中）

  内置指令：

    ng-click:点击事件

    ng-blur:失去焦点

    $event: 事件参数

    ng-class: 值是一个对象 {}

    ng-style: 值是一个对象 {}

    ng-include: 动态插入一个模板页面(不是完整的html的页面，可以有表达式)

  自定义指令：

    module.directive('指令名', function(){})

    restrict : 'ECMA', 默认'A' --> E(element:标签)，C(class:类)，M(mement:属性)，A(attribute:属性)

    template : '简单的html标签',（常用）  

    templateUrl : '包含模板标签结构的页面',-->内部会通过ajax请求得到其html片段模板（常用）

    replace : true/false, //是否替换指令所在的标签  默认false 若为true,模板就会完全替换标签，否则是插入其标签体（常用）

    scope: （常用）

    使用什么作用域，默认为false，直接使用外部作用域作为当前作用域

    如果为true,代表创建一个作用域继承自外部作用域

    如果是{},代表创建一个隔离作用域，不从外部作用域继承

    --> {}  隔离作用域的绑定策略： 

      1.基于字符串的绑定  使用  "@"  操作符，绑定的是指定标签属性的字符串

      2.基于变量的绑定，使用  "="  操作符，绑定的是外部作用域的变量

      3.基于方法的绑定，使用  "&"  操作符，绑定的是外部作用域的方法  

    transclude:嵌入转换，默认false;  如果为true,需要与作用域和ng-transclude指令配合使用（常用）

    controller:引用某个Controller或定义一个新的controller（常用）

      -->function($scope, $element, $attrs, $transclude)  

    compile:指定编译期执行的函数； 对模板DOM进行处理

    ``` bash
      -->function(){
        return  pre:function preLink(scope, element, attributes){...}
        post:function postLink(scope, element, attributes){...}  可以覆盖link的显示
      }   
    link :  指定链接期执行的函数； 将作用域和DOM进行链接（常用）
      -->function(scope, elements,attrs,contrller){
        // scope是作用域的对象，通过它可以操作该作用域中的所欲的属性和方法
      }
    require: 指定一个指令的名称（常用）
      "^xxx": 查找外部指令的控制器
      "?xxx": 在当前指令中查找控制器，如果没有为null
      "xxx": 在当前标签中查找指令的控制器注入到当前指令的link函数中
      "?^xxx": 两种情况都会查找
    priority: 优先级，默认是0，最大是1000  优先级高的指令总是优先解析执行； 
      -->   ng-repeat的优先级是最高的
    terminal: 是否终止优先级较低的指令执行，默认是false
    })

   ```   
15.依赖注入(DI: Dependency Injection)：依赖的对象被自动注入进来   

  依赖对象：完成特定功能的函数需要某个对象才能实现, 这个对象就是依赖对象

  引入依赖对象：

    方式一: 内部自己创建 : 不动态

    方式二: 全局变量 : 污染全局命名空间

    方式三: 形参引入依赖 : 依赖注入使用的方式

  定义：

    1). 定义函数时, 使用形参声明依赖对象变量, 在函数体中使用依赖对象(我们实现)

    2). 函数调用时, 自动将创建好的依赖对象动态传入(框架实现)

    3). 例子: 事件监听就使用了依赖注入, event就是依赖对象(event可以是任意名称)

  angular的依赖引入：形参必须是特定的名称, 否则Angular无法注入抛异常
  
16.$apply和$watch方法：

  $apply():

    1). 当scope中的数据发生了改变, angular会将数据同步显示到页面, 这一操作称为"脏数据检查"

    2). angular在它的方法执行完后, 都会进行脏数据检查,

    3). 在原生JS函数中改变作用域数据, angular是不会进行脏数据检查的

    4). 使用$scope的$apply函数可以解决此问题

      $scope.$apply(function(){
      //在这里更新scope数据, angular会同步更新其页面数据
      });

    5). $apply()的本质是调用$digest()去进行脏数据检查更新页面的

    $scope.$digest()

    6). $apply()虽然也能实现页面更新, 但建议使用$apply()

  $watch():

    1). angular是双向数据绑定的, Scope中的属性数据发生了改变, 会自动更新页面中对应的数据

    2). 但有时, 我们想监视数据的变化情况, 来实现特定的功能

    3). Angular提供了$watch()来实现

    var unWatch = $scope.$watch('propertyName', function(newValue, oldValue){}, deepWatch)

    参数一: 指定监视属性的属性名

    参数二: 发现数据发生改变时的回调函数

    参数三: 是否深度监视, 默认是false, 代表只是监视属性本身, 而不监视其内部数据

    返回值: 用于取消监视的函数, 调用unWatch()取消监视

17.视图和路由

  SPA:(simple page application) 单页应用

  对单页应用来讲，视图和路由的作用可以从一个视图跳转到另外一个视图,可以合理管理用户在使用过程中看到的界面

  -- 引入：将angular-route.js添加到项目中-->在页面中引入此文件-->创建应用module时加载此模块

  -- 实例：

  主页面：

   ``` bash
    <div ng-controller="MyController">
      <ul>
        <li><a href="#/a">click a</a></li>
        <li><a href="#/b">click b</a></li>
      </ul>
      <ng-view></ng-view>
    </div>
   ``` 
  模板页面a:

   ``` bash
   <div style="height:500px;width:100%;background-color:green;">{{hello}}</div>
   ``` 
  模板页面b: 

  ``` bash
  <div style="height:2500px;width:100%;background-color:blue;">{{hello}}</div>
  ``` 
  JS实现：

   ``` bash
    angular.module('myApp',['ngRoute'])
    .config(function ($routeProvider) {
    $routeProvider
      .when('/a', {
        templateUrl : 'a.html', //加载指定template页面替换 <ng-View>
        controller : 'AController'
      })
      .when('/b', {
        templateUrl : 'b.html',
        controller : 'BController'
      })
      .otherwise({
        redirectTo : '/a'
      });
    })
    .controller('AController', function ($scope) {
      $scope.hello = "this is a.html";
    })
    .controller('BController', function ($scope) {
      $scope.hello = "this is b.html";
    })
    .controller('MyController', function($scope){
      //$scope.hello = "this is xxx.html";
    });
    ```      
18.表单验证：

  使用angular-messages扩展库

  安装Chorme插件：AngularJS Baterarang  可以查看作用域对象中的属性变化情况

  表单：当前$scope下会有对应的属性对象, 属性名为form的name属性

  表单对象包含以下重要属性:

    1). $dirty : 表示用户是否输入过数据, 初始值为false, 一旦用户输入数据就会为true

    2). $valid : 表示整个表单是否是合法的, 一旦有一个表单项不合法,就会为false

    3). $invalid : 与$valide值相反        

    4). 表单项属性: 保存表单项的验证相关信息

  表单项：form属性对象下有对应的属性对象, 属性名为表单项的name属性，表单项对象包含以下重要属性

    1). $dirty : 表示用户是否输入过数据, 初始值为false, 一旦用户输入数据就会为true

    2). $valid : 表示整个表单是否是合法的, 一旦有一个表单项不合法,就会为false

    3). $invalid : 与$valide值相反

    4). $error : 包含错误名称的对象, 属性名为特定的验证名称, 值为true: {require : true}

  编码：

  在表单字段上定义验证指令： 

    ng-required = "true" 必填项； ng-minlength ng-maxlength

    ng-pattern="/^[a-zA-Z]$/"  type="email/url"      min max

  提示信息：

    ng-messages: 读取表单项中的$error对象  ng-messages="nameForm.username.$error"

    ng-message: 读取$error对象中验证名称属性，如果为true才会显示当前标签  ng-message="minlength"

    ng-show: 控制包含提示信息的标签是否显示 ng-show="nameForm.username.$dirty&&nameForm.username.$invalid"

    ng-bind: 指定提示信息文本字符串 ng-bind="字符串最少为4"

    ng-class: 避免出现红色提示区域闪烁的情况 ng-class="'alert alert-danger help-block'"

  实例：

   ``` bash
    <div ng-show="myForm.username.$dirty&&myForm.username.$invalid" ng-messages="myForm.username.$error" class="alert alert-danger help-block">
      <span ng-message="required" ng-bind="'必填项'"></span>
      <span ng-message="minlength" ng-bind="'字符太短小于4'"></span>
      <span ng-message="pattern" ng-bind="'开头必须是字母'"></span>
    </div>
   ```   
19.MVC与MVVM:

  通用：

    模型Model: 存储数据的实体模型，操作数据的业务模型

    视图View: 显示数据，响应用户操作，与用户进行交互

    控制器Controller:操作模型数据，更新视图，View与Model之间的桥梁

  angular中的MVC:

    模型Model: scope 存储数据的容器 提供操作数据的方法

    视图View: html/css/directive/expression 显示Model的数据，将数据同步到Model 与用户交互

    控制器Controller： controller 初始化Ｍodel的数据  为Model添加行为方法 

  MVVM： View <--> ViewModel <--> Model

  MVVM是MVC的进化版，Angular使用的是MVVM  双向数据绑定

----------------------------------------------------------------------------------------------------

备注：如有错误与不全面的地方希望大牛补充，谢谢！！！！！！

更多内容请访问：        
angular中的自定义过滤器使用：http://git.oschina.net/hjm100/codes/nr9vfgxh3tzajiswl6omd34

angular中的服务使用：http://git.oschina.net/hjm100/codes/6scz41ryv9xf70gtbowkh50

angular总结学习：http://git.oschina.net/hjm100/codes/uohp5vsbljqyr1298eixn92

angular中的tab切换：http://git.oschina.net/hjm100/codes/q1csxnui6thoda8melzjf29