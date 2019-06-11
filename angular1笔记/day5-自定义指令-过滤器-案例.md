# Angular

## 自定义指令
- 自定义指令无外乎增强了HTML,提供了额外的功能。
- 内部指令基本能满足我们的需求。
- 少数情况下我们有一些特殊的需要，可以通过自定义指令的方式实现

## 创建自定义指令
- *注意: 名字要符合驼峰合法*

```javascript
    // 1.创建模块对象
    var app = angular.module('directiveApp', [])

    // 2.创建自定义指令
    // 第一个参数：是指令的名字,必须是驼峰命名法
    //             使用时把大写改成小写，在原来大写前加上-
    // 第二个参数：和控制器的第二个参数类似!
    app.directive('myBtn', [function(){
      // 在这里直接return 一个对象就可以了
      return {
        // template属性，是封装的ui
        template:'<div><button>我是按钮</button></div>'
      }
    }])
```

### 自定义指令中回调里返回的对象的属性
- template: 需要提供一个html字符串,最终会被添加到当前页面使用了自定义指令的位置
- templateUrl:需要提供一个html文件路径，angular会发请求，请求对应的文件，
 把文件内容作为模板插入到自定义指令中间
            : 也可以提供一个script标签的id, angular会把script标签中的内容作为
              模板插入到自定义指令中间,*注意* 要改变script标签的type="text/ng-template"

- restrict: 也是需要提供一个字符串，限制自定义指令的使用形式
    + A : Attribute 表示只能以属性的形式使用
    + C : Class     表示只能以类样式名的形式使用
    + E : Element   表示只能以自定义标签的形式使用
    + ACE : 如果希望多种方
    + 式合适，就把对应值组合在一起。

- replace：需要提供一个布尔值，为true时，模板会被用来替换自定义指令所在标签，
        * 否则是插入到自定义指令中间
        
- transclude: 需要一个布尔值, 为true时会将自定义标签中的内容插入到模板中，
        * 拥有ng-transclude 指令的标签中间

- scope：需要一个对象: 可以用来获取自定义指令的属性值,
    -  给当前对象添加一个属性(如:tmp),属性值以@开头，后面跟上自定义指令的属性名
       然后就可以在模板中使用{{tmp}} 来得到对应的属性值
       + `scope: { tmp:'@mystyle'}`  {{tmp}}
       + `scope: { mystyle:'@'}`     {{mystyle}}

- link: 需要一个function 这是function在angular解析到相应指令时就会执行一次,
    + scope      ：类似于$scope,只不过scope的属性只能在模板中使用
    + element    : 自定义指令所在标签对应的对象(jqLite)
    + attributes : 包含了自定义指令所在标签的必有属性

## todomvc案例

### todomvc功能分析
1. 任务的展示
2. 添加任务
3. 删除任务
4. 修改任务内容
5. 切换任务完成与否的状态
6. 批量切换任务完成与否的状态
7. 显示未完成的任务数
8. 清除所有已完成任务
    - 注意： 在循环删除数组长度，会导致循环条件改变，也会导致元素原来的索引改变
9. 切换显示不同状态的任务

## 过滤器(filter)
- 格式化数据
- 过滤数据(filter)

```html
    <ul>
        <!--  如果指定一个布尔值，或者字符串就是全文匹配 -->
      <!-- 会到对应的todos中寻找，如果当前元素有completed属性且值 为true就会被显示出来。（只会到completed属性中寻找） -->
      <li ng-repeat="item in todos | filter : {completed:true} ">
        {{item.name}},{{item.completed}}
      </li>
    </ul>
```


```html
  <h1>currency</h1>
  <!-- 在数据模型后加上|  再加上过滤器的名字 
        也可以在过滤器名字后指定参数，参数是写在冒号后面的-->
  <p>{{money | currency : '￥'}}</p>

  <h1>date</h1>
  <p>{{myDate | date : 'yyyy年MM月dd日 HH:mm:ss'}}</p>
```

- limitTo

```html
    <h1>limitTo</h1>
  <!-- 第一个参数，表明显示多少个字，第二个参数表示，从第几个字开始显示(索引从0开始) -->
  <p>{{msg | limitTo : 5 : 2}}...</p>
```

- orderBy 及 json

```html
<h1>json</h1>
 <!--  格式化显示json数据，参数指定缩近的长度 -->
 <pre>{{myJson | json : 8}}</pre>
  <h1>orderBy</h1>
  <!-- 对数据进行排序，参数，给+号就按正序排，- 就按倒序排 -->
  <span ng-repeat="item in arr | orderBy:'-'">{{item }}，</span>
```

- 在js中使用过滤器

```javascript
    <!-- $filter 需要在控制器的回调中传入 -->
    // 可以调用不同的过滤器得到相应的结果
      // 参数是一个过滤器的名字
      // 返回值是一个方法
      //        : 第一个参数是需要处理的数据
      //        : 后面的参数是当前过滤器本身需要的参数
     $scope.result =  $filter('currency')($scope.money,'￥')
```
