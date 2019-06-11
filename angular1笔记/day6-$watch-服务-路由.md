# Angular

## todomvc使用filter过滤器来切换不同状态任务的显示
- arr=[{a:3,b:4},{a:5}]
- 数据模型 | filter : {a:3}

## $watch 监视数据模型的变化

```javascript
    $scope.name = '小明'
      $scope.age = 18

      // $watch可以用来监视数据模型的变化
      // 第一个参数: 数据模型对应的名字(字符串形式)
      // 第二个参数: 相应的数据模型变化就会调用 这个函数
      // 默认会直接执行一次回调函数
      $scope.$watch('name',function(now,old){
        // 第一个参数是变化后的值
        // 第二个参数是变化前的值
        // console.log(now,old)
      })
```
- 也可以监视方法的返回值

```javascript
    $scope.getAge = function(){
        return $scope.age
      }
      
      // 也能够监视$scope.属性中的方法的返回值
      $scope.$watch('getAge()',function(now,old){
        console.log(now,old)
      })
```

## 服务
- 创建服务

```javascript
    // 1.创建服务模块
  var app = angular.module('service',[])

  // 2.创建服务
  // 第一个参数：服务的名字
  // 第二个参数里的function: 
  //    angular会把这个function当作构建函数，angular会帮助我们new这个构建函数，然后得到一个对象。A,B
  app.service('MyService', [function(){
    this.name = '小明'
  }])
```

- 使用服务

```javascript
    // 1.创建模块
  var app = angular.module('todosApp', ['service'])
  // 2.创建控制器
  app.controller('todosController', [
    'MyService'
    , function(MyService){
    // 这个MyService就是，对应的'MyService'时的回调函数new出的对象
    console.log(MyService)
}])
```

## 路由
- 根据url中不同的锚点值，在页面显示不同的内容！

### 路由使用

```javascript
    // 1.创建模块
    var app = angular.module('myApp', ['ngRoute'])

    // 2.配置路由规则(约定什么样的锚点值，对应什么样的内容)
    // 第一个参数与controller第二个参数类似
    app.config(['$routeProvider',function($routeProvider){
      
      // 第一个参数：对应的url中锚点值
      // 当angular检测到url中锚点变为/ali里，就会把template对应的内容插入到页面拥有ng-view指令的标签中
      $routeProvider.when('/ali',{
        template:'<div>阿里在二楼!</div>',
        // 指定一个控制器的名字,
        // 当前url中锚点值为/ali时就会执行控制器中的回调函数
        // 我们可以直接在template/templateUrl对应的模板中使用该控制器中对应的$scope属性值
        controller:'demoController'
        //templateUrl
      })
      .when('/baidu',{
        template:'<div>百度在1楼</div>'
      })
    }])
```

### 路由参数
- 在原有规则中可以加冒号:,
- 表示:号后的内容是可以变的(但是必须要有)
    + 如果加上问号，就能够匹配到了
- 在控制器中可以通过$routeParams得到myname对应的值

```javascript
    $routeProvider.when('/company/:myname？')
```

### otherwise
- 当不匹配when方法对应的规则时，就会匹配otherwise对应的规则


## webapi
- I/O
-  // url

## api
- 
- console.log('小明') //小明
- I/O     docuemnt.getGetElementById('')

## 豆瓣API

- ng-src 指令: 用来取代src

### $http
- 发请求

```javascript
    http.get('./in_theaters/data.json')
      .then(function(res){
        // 成功的回调函数
        // console.log(res.data)
        $scope.data = res.data
      })
```