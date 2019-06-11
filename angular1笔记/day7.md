# Angular

## 跨域
- img  src可以指向一个跨域的资源
- link
- video audio .

- script: src 一般指向一个js文件
- a.com 请求b.com/tmp.js文件

-A 版本：
- 假设tmp.js 内容为: var data = 123
<script src="b.com/tmp.js"></script>
<script>
    console.log(data)
</script>

-B 版本
- 假设tmp.js 内容为: var data = {name:'小明',age:18}
<script src="b.com/tmp.js"></script>
<script>
    console.log(data)
</script>

-C 版本
- 假设tmp.js 内容为:  test({name:'小明',age:18})
<script>
    function test(data){
        console.log(data)
    }
</script>
<script src="b.com/tmp.js"></script>

## 正在热映

## 分页

## 即将上映

## Top250


## 合并重复的功能





## loading

## 导航焦点切换
## 搜索模块
## 详细页
