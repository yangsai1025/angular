# Angular

## Angular 与 jQuery
- jQuery: 库
    + 提供了一些已有的方法，我们主动调用它。
    + $('.test').val()

- Angular: 框架
    + 框架提供了一种结构或者模式
    + 我们按照它提供这种结构或者模式去书写代码
    + 框架会帮助我们去剩下的事情

### Angular简介
- 一款非常优秀的前端高级 JS 框架
- 最早由 Misko Hevery 等人创建
- 2009 年被 Google 公式收购，用于其多款产品
- 目前有一个全职的开发团队继续开发和维护这个库
- 有了这一类框架就可以轻松构建 SPA 应用程序
- 其核心就是通过指令扩展了 HTML，通过表达式绑定数据到 HTML。

#### 什么是 SPA
- single page application
- 单页应用程序

### 值+1

### 指令
- 在angular中以ng-开头的html标签属性，称之为指令
- ng-app: 选择angular去管理哪一部分的html代码, 管理的是ng-app所在
   元素的子元素及其本身
- ng-click: 也是用来注册点击事件
- ng-model: 可以指定一个属性值，这个属性就表示当前文本框的value值
- ng-init: 可以对数据进行初始化操作，给一个默认值。

### 模块
- 创建模块:`var app = angular.module('模块名',[])`
- *注意* 如果不依赖其他模块，也需要提供一个空的数组
- 需要在ng-app指令的属性值上写我们的模块名(房子)

### 控制器
- 创建控制器:`app.controller('控制器的名字',function($scope){})`
- 如果要改变页面{{testName}}的值，就直接改变$scope.testName值就可以
- *注意* 要显示数据模型的值,就要在它所在标签或者父标签上加上ng-controller指令
  ng-controller的值就是我们想要显示的数据模型所在控制器的名字
  :ng-controller="window"

### 双向数据绑定
- 数据模型($scope.属性)的改变，会影响内容的显示(文本框的值)
- 我们改变了文本框的值，对应的数据模型发生了改变.
- 这种相互影响的关系就称之为双向数据绑定.

### MVC 思想
- M : Model: 存储，获取数据
- V : View 视图，把数据呈现给用户
- C : Controller 做一些控制和调度的操作