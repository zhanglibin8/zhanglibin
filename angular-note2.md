## 安装nrm工具(切换源)
- mac下安装全局时需要增加sudo
```
npm install -g nrm
```
- 显示所有可用的源
```
nrm ls
```
- 切换源
```
nrm use taobao
```
- 添加张利斌源
```
nrm add zhanglibin http://172.18.0.199
```
- 切换到张利斌源上
```
nrm use zhanglibin
```
- 查看速度
```
nrm test
```

## 组件和装饰 ->directive：指令 (可以复用) 用指令封装功能
> 特点 

- 1.组件式指令 :有模板的

- 2.装饰型指令：增加属性的

- 指令是否依赖于控制器：不依赖

- 组件式 一般采用E
- 装饰型 一般采用A

- 默认指令是不会创建作用域的

> 1.组件

```
<!--元素element  E -->
<zz-xxx></zz-xxx>
<!--属性 attribute  A-->
<div zz-xxx></div>
<!--样式 class   C-->
<div class="zz-xxx"></div>
<!--注释 comment   M-->
<!-- directive:zf-xxx -->
var app = angular.module('appModule',[]);
    //需要转换成驼峰命名法,标签名为-连接
    app.directive('zzXxx',function () {//声明指令后默认返回一个对象
       return {
        //默认支持的只有EA生效
          restrict:'ACME',
          replace:true,
          template:'<div><h1>hello</h1><span>hi</span></div>',//模板中根节点只有一个
          //templateUrl:'xxx/xxx.html',//ajax将文件读取过来插入到模板中
          transclude:true
       }
    });
```
- transclude:true//你想让内容放到什么位置上就要在放置的标签上增加ng-transclude 属性,带有ng-transclude的标签会生成一个作用域
```
<div class="panel panel-info">
    <div class="panel-heading">{{title}}</div>
    <div class="panel-body" ng-transclude></div>
    <div class="panel-footer">{{tail}} <button ng-click="q({a:1,b:2})">say</button></div>
</div>
```


> 2.装饰

- angular唯一可以操作dom的地方

- link

```
var app = angular.module('appModule',[]);
    app.directive('redBorder',function () {
        return {
            restrict:'A',
            link:function (scope,element,attrs) {//链接 视图和作用域的，特点：唯一一个可以操作dom的地方
                //scope:当前指令所在的作用域
                //element 是一个jq对象 ,指向的是当前指令所在的元素
                //attrs： 当前指令的所有属性变成一个对象格式
                //console.log(angular.element(element[0])) dom对象与jq对象互转
                //element.css('border','1px solid red');
                element.css('fontSize','40px'); angular提供一些简单的jq方法
                angular.element(document).on('click',function () {//angular.element()->把原生对象转化为angular对象
                    //alert(21)
                });
                console.log(attrs);//attrs是一个属性集合Attributes
            }
        }
    })
```

## @符、=符、&符

- 用@符取的是当前指令上属性的字符串 （单向）

- 用=取得是当前指令上属性对应的作用域上的变量 （双向）

- &只用于函数

## scope:true 和 scope:{}的区别
- 控制和指令默认不生成私有作用域，但是加上scope:true或者scope:{}就会生成私有的作用域
- scope:true//仍然可以找到上机作用域 父亲和儿子仍然有关系
- scope:{}//断绝父子关系，不能到父级去拿东西.需要通过属性传递props
```

```
 
