# Angular

## Angular vs jQuery
- 提高了dom操作的效率
- 不推崇dom操作

- angular.element, 使用方式和jquery非常像,jqLite对象
    + 可以把angular.element当作jQuery的$来用，
    + 注意*angular.element 要求传入的参数是一个原生的dom对象，而不是选择器*

### 回顾并总结Angular开发流程
- 1.在html中引入angular.js文件
- 2.在html中加上ng-app指令，告诉angular要管理页面哪一部分代码
- 3.在js中创建模块`angular.module('myApp',[])`,给ng-app指令一个值，
- 这个值就是这个模块的模块名:myApp
- 4.在js中创建控制器`xxx.controller('控制器名字',function($scope){})`,我们需要在页面上加上ng-controller指令，指令的值为控制器的名字
  `ng-controller="控制器名字"`
- 5.建模:根据页面结构，抽象出具体的js对象.
- 6.通过$scope做一些初始化操作`$scope.username="小明"`
- 7.通过`ng-model , ng-click , {{}}` 把$scope的属性在页面展示出来
- 8.在js写一些具体的逻辑

### MVC
- MVC只是一种思想，只是约定了我们代码应该如何去组织
- 让我们代码的每一部分都有一个明确的职责
- 用利于后期的维护性(并不是提高了代码的执行性能,有可能10行代码放到10个方法里,
- 10方法再放到10文件去.)


### $scope

- 视图和控制器之间的数据桥梁
- 用于在视图和控制器之间传递数据
- 用来暴露数据模型（数据，行为）

![$scope](./scope.png)

### ViewModel

- $scope 实际上就是MVVM中所谓的VM（视图模型）
- 正是因为$scope在Angular中大量使用甚至盖过了C（控制器）的概念，所以很多人（包括我）把Angular称之为MVVM框架
- 这一点倒是无所谓，具体看怎么用罢了

## Angular 模块
- angular.module('模块名',[])

### Angular中模块的划分方式
- 1.按照项目的功能去划分模块
- 2.按照项目中文件的类型去划分模块

## Angular 控制器
### 传统的方式创建控制器

```javascript
    // 创建控制器(1.2.x版本)
    // angular会把全局的函数当作控制器
    function demoController($scope){
      $scope.name = '小明'
    }

    function xxx($scope){
      $scope.age = 18
    }
```

### 面向对象的方式创建控制器
```html
<!-- 这里的obj 代表控制器中回调函数new 出的对象 -->
<div ng-controller="demoController as obj">
  <p>{{myname}}</p>
  <p>{{obj.name}}</p>
</div>
```
```javascript
    // 1.创建模块
    var app = angular.module('myApp', [])

    // 2.创建控制器
    // angular会把这二个参数当作构造函数使用
    app.controller('demoController', function($scope){
      $scope.myname='小红'
      this.name = '小明'
    })
```

### 安全的方式创建控制器
- 就是为了避免压缩后代码无法运行

```javascript
    // 把第二个参数改为一个数组,在数组把我们需要的参数的名字写上
    // 回调函数就写在数组的最后一个元素上
    // *注意*：数据中传入的元素的顺序,要和function的中顺序一一对应
    app.controller('demoController',['$scope','$log',function($scope,$log){
      $scope.msg = 'hello World!'
      $log.log('哈哈哈哈！')
    }])
```

## 指令

### ng-bind
- 可以解决表达式闪烁问题:
- `<p ng-bind="msg"> </p>` 浏览器不会把标签的属性显示出来!
- 效果：angular会把ng-bind对应的数据显示到所在标签中间

### ng-cloak
- 可以解决表达闪烁问题:
- `<div class="ng-cloak"><p>{{msg}}</p></div>` 先隐藏后显示
- angular在解析表达式之后会把页面上的ng-cloak样式移除,
     这样ng-cloak对应的样式就不生效了,我们就先给ng-cloak设置display:none;

### ng-repeat
- 能够把一组数据直接渲染到页面上，不需要我们拼接字符串
- 我们希望重复的是哪个元素就把ng-repeat指令加在哪个元素上，不一定是li上
- ng-repeat="item in users" , item对应是遍历users时的第一条数据，users是我们
- 要遍历的数据(是一个数组)

```html
    <!-- ng-repeat 遍历生成数据，类似for in 循环的语法 -->
      <li ng-repeat="item in users" >
        {{item.name}} , {{item.age}}
      </li>
```

#### ng-repeat补充
- ng-repeat 在遍历时会提供以下值:
    + $odd : 为true时，表明当前数据是否是第[奇]数条
    + $even: 为true时，表明当前数据是否是第[偶]数条
    + $first: 为true时，表明当前数据是否是第1条
    + $last: 为true时，表明当前数据是否是最后一条
    + $middle: 为true时，表明当前数据是否是中间的数据

```html
    <!--  $odd, ng-repeat在每次遍历时都提供这样的值，为true表明当前数据是否第奇数条,从索引为0开始判断的 -->
    <!--  $even, ng-repeat在每次遍历时都提供这样的值，为true表明当前数据是否第偶数条,从索引为0开始判断的 -->
      <li class="{{ $odd ?'red':'green'}}" ng-repeat="item in data">
        {{item.name}},{{item.age}}
      </li>
```

### ng-class
- ng-class 可以帮助我们控制元素的class样式，
- ng-class 可以独立在其他元素上使用，并非一定要和ng-repeat结合

```html
    <!--  ng-class,动态的添加class样式,
      以对象的形式书写，angular会把属性值为true的属性名当作样式添加到class
      class="green" -->
    <li ng-class="{red:item.age>=20, green:item.age>=10&&item.age<20,blue:item.age<10}" ng-repeat="item in data">
      {{item.name}},{{item.age}}
    </li>
```

### ng-show/ng-hide
- 控制元素的显示与否,ng-show与ng-hide作用是相反的(只是设置display:none来隐藏元素)

```html
    <!-- ng-show,控制元素的显示或隐藏,值为true时显示，为false隐藏-->
    <p ng-show="isShowing">我是中国人，我爱自己的祖国!</p>
    <!-- ng-hide 值为true时，隐藏当前元素 -->
    <p ng-hide="true">我是小明!</p>
```

### ng-if
- 控制元素的显示与否:*值为false时，元素会从dom移除*

```html
    <!-- ng-if，也能控制元素的显示或隐藏,为true时显示,为false时【会将当前dom元素移除】 -->
    <p ng-if="true">我是中国人，我爱自己的祖国!</p>
    <h1>ng-if="false"</h1>
    <p ng-if="false">我是中国人，我爱自己的祖国!</p>
```

### ng-switch
- 当ng-switch-when 对应的值等于ng-switch对应值时，当前dom元素就显示

```html
    <div ng-switch="name">
      <div ng-switch-when="小明">
        我是小明，我在这里！
      </div>
      <div ng-switch-when="小红">
        我是小红!
      </div>
    </div>
```

### 其他常用指令
- ng-checked： 
  + 单选/复选是否选中,（单向数据绑定:界面操作不会影响数据模型的值）   ng-model:双向数据绑定
- ng-selected：
  + 是否选中
- ng-disabled：
  + 是否禁用
- ng-readonly：
  + 是否只读

### 常用事件指令

不同于以上的功能性指令，Angular还定义了一些用于和事件绑定的指令：

- ng-blur：失去焦点
- ng-focus： 获得焦点
- ng-change：内容改变
- ng-copy：复制
- ng-click: <div ng-click="aa()"></div>
- ng-dblclick：双击
- ng-submit：  form表单提单

### 指令的其他使用方式

data-xxx,在使用angular指令时，只需要在原先的指令前加上data-前缀。
如: data-ng-app,data-ng-click
x-ng-app,x-ng-click