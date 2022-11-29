## vue基础

1.  导入vue.js  库
2.  创建 视图容器
3.  创建 vue 实例对象   new Vue({});

##  编程  思想

1. MVC  思想   
   M  model  模型  数据
   V  view   视图
   C  controller  控制器

2. MVVM  思想
   M  model  模型  数据（请求后台的，表单收集的）
   V  view   视图  html+css+js
   VM 虚拟视图  

## vue 实例对象

1. 

```js
            new Vue({
                el:"#app",
                data:{
                    str:"学习vue"
                }
            })
```

2.

```js
new Vue({
            el:document.getElementById("app"),
            data:{
                str:"学习vue"
            }
})
```

3. 

```js
new Vue({
            el:document.getElementById("app"),
            data:function(){
                return {
                    str:"学习vue data是一个函数"
                }
            }
})
```

4. 

```js
new Vue({
            el:document.getElementById("app"),
            data(){   // 用在组件中
                return {
                    str:"学习vue data是一个函数"
                }
            }
        })
```

5. 

```js
new Vue({
            data:{
                str:"学习vue"
            }
        }).$mount("#app");
```


## vue 指令

1. v-text 更新元素的 textContent。
2. v-html 更新元素的 innerHTML。注意：内容按普通 HTML 插入 - 不会作为 Vue 模板进行编译。
3. v-show 根据表达式之真假值，切换元素的 display CSS property。  数据及视图永远在加载
4. v-if   v-else   v-else-if 根据表达式的值的 truthiness 来有条件地渲染元素。在切换时元素及它的数据绑定 / 组件被销毁并重建
5. v-for 
   Array | Object | number | string | Iterable (2.6 新增)
   基于源数据多次渲染元素或模板块。此指令之值，必须使用特定语法 alias in expression，为当前遍历的元素提供别名：
6. v-on   简写：@    绑定事件    v-on:事件名="函数"
   修饰符
   .stop - 调用 event.stopPropagation()。  阻止冒泡
   .self - 只当事件是从侦听器绑定的元素本身触发时才触发回调。
   .prevent - 调用 event.preventDefault()。
   .{keyCode | keyAlias} - 只当事件是从特定键触发时才触发回调。   @keyup.13
   .once   只触发一次回调。
   .left - (2.2.0) 只当点击鼠标左键时触发。
   .right - (2.2.0) 只当点击鼠标右键时触发。
   .middle - (2.2.0) 只当点击鼠标中键时触发。
7. v-bind 简写 :   动态绑定属性值
8. v-model  表单 双向绑定获取表单值
   input   text、number  、password  、url、email、 search、tel  、   radio、  checkbox
   select
   textarea
9. v-pre 跳过这个元素和它的子元素的编译过程。可以用来显示原始 Mustache 标签。跳过大量没有指令的节点会加快编译。
10. v-cloak 这个指令保持在元素上直到关联实例结束编译。和 CSS 规则如 [v-cloak] { display: none } 一起用时，这个指令可以隐藏未编译的 Mustache 标签直到实例准备完毕。
11. v-once 只渲染元素和组件一次。随后的重新渲染，元素/组件及其所有的子节点将被视为静态内容并跳过。这可以用于优化更新性能。

##  vue 实例对象

``` js
    new Vue({
        el:"#app",  //绑定视图
        data:{   //模型数据

        },
        methods:{  //自定义方法  【普通方法】

        },
        computed:{  //计算属性

        },
        watch:{  //监听属性

        },
        directives:{  // 自定义局部指令

        },
        components:{  //注册组件

        },
        template:"",  //模板
        mixins:[],    //混入
        props:[]   //接受外部组件传递的数据
        //8个生命周期钩子函数
    })

```


## vue  methods  【普通方法】

1. 不调用不执行   事件  {{ }}
2. 调用几次就执行几次

## vue computed  【计算属性】

1. 支持缓存，只有依赖数据发生改变，才会重新进行计算
2. 不支持异步，当computed内有异步操作时无效，无法监听数据的变化
3. computed 属性值会默认走缓存，计算属性是基于它们的响应式依赖进行缓存的，也就是基于data中声明过的数据通过计算得到的值
4. 如果一个属性是由其他属性计算而来的，这个属性依赖其他属性，是一个【多对一】或者【一对一】，一般用computed
5. 如果computed属性属性值是函数，那么默认会走get方法；函数的返回值就是属性的属性值；在computed中的，属性都有一个get和一个set方法，当数据变化时，调用set方法。 


## watch  【监听属性   侦听器】

```js
//完整写法
 watch:{  //监听属性   只能监听data中存在的数据
            uname:{
                deep:true,   //深度监视
                immediate:true,   //立即监视
                handler(newValue,oldValue){
                        //当uname数据发生变化的时候，会自动调用
                    console.log("当数据发生变化的时候，handler会自动调用",newValue,oldValue);
                }
            }
 }

 //简写形式
            phone(){  
                //相当于 hanler()
                 console.log("手机号发生变化了");
            }

```


watch    handler[只要数据发生变化，就是自动调用hanler]   deep[深度监视]  immediate[立即监视]
特点：

1. 不支持缓存，数据变，直接会触发相应的操作；
2. watch支持异步；
3. 监听的函数接收两个参数，第一个参数是最新的值；第二个参数是输入之前的值；
4. 当一个属性发生变化时，需要执行对应的操作；一对多；
5. 监听数据必须是data中声明过或者父组件传递过来的props中的数据，当数据变化时，触发其他操作，函数有两个参数，

		　　immediate：组件加载立即触发回调函数执行，
		　　deep: 深度监听，为了发现对象内部值的变化，复杂类型的数据时使用，例如数组中的对象内容的改变，注意监听数组的变动不需要这么做。注意：deep无法监听到数组的变动和对象的新增，参考vue数组变异,只有以响应式的方式触发才会被监听到。 */



## watch 和  computed  对比

computed :  对数据进行计算，有缓存,不支持异步， 多对一/ 一对一。
watch：  对数据进行监听处理，没有缓存，支持异步，一对多。

一般情况下，computed 能做的 watch 都能做，但是 watch 能做的,computed 不一定能做。

##  自定义指令

1. 自定义全局指令

```js
//自定义全局指令   directive("指令名",{配置指令功能})
        Vue.directive("foucs",{
            inserted(el){
                el.focus();
            }
        });
```

2. 自定义局部指令


## 数据代理和数据劫持

vm  实例对象
    $attrs:(...)
    $children:[]
    ....
    uname
    age
    ....
    _data:{
        uname:(...)
        age:(...)
        get age
        set age
        get uname
        set uname
    }
    ....
    get age
    set age
    get uname
    set uname

##  数据代理和数据劫持 总结

1. 数据代理
   目的 ：  在视图中更简单的使用数据  _data.uname  uname
   原理：  使用 Object.defineProperty(); 将数据代理到 vm 身上。
   体现：  修改vm身上的数据，通过 proxyGetter   读取对应_data数据，通过 proxySetter 更新对应_data的数据

2. 数据劫持
   目的 ：  为了监视 _data 中的数据的变化，然后重新渲染视图。
   原理：  使用 Object.defineProperty(); 将数据代理到 vm 身上。
   体现： 修改 _data 中的数据，通过 reactiveGetter 读取 _data数据，通过reactiveSetter  更新_data 中的数据，并重新渲染视图。


##  vue 数组数据更新

为什么不能直接更新数组？  没有 get  set  方法
Vue 将被侦听的数组的变更方法进行了包裹，所以它们也将会触发视图更新。这些被包裹过的方法包括：
    push()
    pop()
    shift()
    unshift()
    splice()
    sort()
    reverse()

##  vue 实例的生命周期

概念：  vue 实例 从创建到销毁的一系列过程，就是生命周期。
在创建到销毁的过程中，会自动一些函数，这些函数就是生命周期钩子函数。

1. 创建  beforeCreate[创建前]   created[创建后]

       beforeCreate: data数据及methods方法都不存在
       
       created:data数据及methods方法此时被创建
       
       创建 数据 data 和 方法 methods

2. 挂载  beforeMount[挂载前]    mounted[挂载后]

   beforeMount:准备虚拟dom,将 data 数据 和 methods方法绑定到虚拟DOM上。但是视图还是展示未编译的dom。$el虚拟dom准备完毕,此时对dom 的操作最终 都不会生效。
       
   mounted:此时会将虚拟dom[$el]渲染到页面中，一般发送ajax请求，发布消息、创建定时器，绑定自定义事件

3. 更新  beforeUpdate[更新前]   updated[更新后]

       beforeUpdate:  数据data会被更新，但是，视图不会被更新,还是老数据
       
       updated:数据data会被更新，此时，视图才被更新,展示新数据

4. 销毁  beforeDestroy[销毁前]  destroyed[销毁后]

       beforeDestroy: data、methods 都可使用，但是，数据只能读，不能更新。methos只能读，调用不执行。做收尾工作。取消定时器，取消订阅，解绑自定义事件
       
       destroyed:销毁虚拟 DOM  完成



## 组件

1. 创建组件    
       使用 Vue.extend()创建组件
       一定在实例之前去创建组件

```js
    //完整写法
    let wangshao = Vue.extend({
            template:"#wangshao",
            data(){
               return{
                    uname:"王少",
                    sex:"男"
               }
            },
            methods:{
                changeWangShao(){
                    console.log(this);
                    this.uname = "今晚的消费，由王公子买单";
                    this.sex = "nan";
                }
            }
    })


    //简写形式
    let App = {
            template:"<div><heshao/><wangshao/></div>",
            components:{  //注册组件
                heshao,
                wangshao
            }
    }


```




2. 注册组件   
       在 vue实例 / 组件中的 components

```js
   //在实例中一般只注册 App  根组件
    new Vue({
            el:"#app",
            components:{  //注册组件
               App
            },
            template:`<App/>`  //模板
    })


    //在组件中注册子组件
     let App = {
            template:"<div><heshao/><wangshao/></div>",
            components:{  //注册组件
                heshao,
                wangshao
            }
    }


```

3. 使用组件
       以标签形式

   

## 组件的特点

1. 组件相当于 vue 实例
2. 组件和组件之间的作用域不互通，组件和vue实例之间的作用域不互通
3. 组件的使用形式 标签


##  vue版本

vue核心代码 最新版 3.x
目前所学  vue 2.x  
vue-cli脚手架  开发平台的最新版  5.0.8


## vue-cli  脚手架 安装

1. npm install -g @vue/cli  全局安装脚手架环境
2. vue create xxxx（项目名）  创建项目
   defalut  vue2
   use  npm
3. npm run serve  启动服务

 npm init  安装模块

 ## vuecli

  main.js  入口文件
  App.vue  根组件

##  vscode  安装 插件

1. Vetur
2. Vue VSCode Snippets

##  vue  单文件组件   .vue 

```js
<template>
    组件的模板  html
</template>

<script>
    逻辑部分   js
</script>

<style>
    css  样式部分
</style>

```



## vue组件命名 

必须严格使用大驼峰
使用 

```html
<DemoCom/>
<DemoCom></DemoCom>
<demo-com></demo-com>

```


## 关闭 vue 语法检查

``` js
//  在 项目的根目录下  vue.config.js  

const { defineConfig } = require('@vue/cli-service')
module.exports = defineConfig({
  transpileDependencies: true,
  //关闭语法检查，必须重启服务器,必须重启服务器,必须重启服务器
  lintOnSave:false
})


```


## style  

1. scoped  样式作用域
2. 一般 App 根组件不写 scoped,公共样式存放在 App组件中


##  diffing算法  和 key作用

key  必须具有唯一性   index(不具备唯一性)   id（具有唯一性）  worddate()
作用: 提高浏览器运行效率
操作虚拟DOM
  mounted  生命周期 钩子 

``` html
    <ul>
        <li>1111</li>
        <li>2222</li>
        <li>3333</li>
    </ul>

    <ul>
        <li>1111</li>
        <li>2222</li>
        <li>3333</li>
        <li>4444</li>
    </ul>

```


```js
let arr = ["aa","bbb","ccc"];
    index:   0     1      2
    id:   0        1      2
           
let arr = ["aa","ddd","bbb","ccc"];
    index:   0     1      2     3
      id:    0     4       1    2
```

## mixin  混入

作用： 进一步封装 组件中的复用的逻辑代码
特点： mixin  相当于 实例(vm) / 组件(vc)

1.  如果自身组件不存在 data / methods  中的方法，就会调用mixins
    如果自身组件存在 data / methods  中的方法，就不会调用mixins,会调用自身的data、methods
2.  生命周期钩子函数,不管是 组件中的还是mixin，都会调用


## 数据来源

1.  整个前端数据来源
    后台API
    表单收集
2.  组件来源
    自身组件中的数据
    外部组件传递的数据

## props 

作用： 接受外部组件传递的数据

```js
    1. //写法
     props:["middleArr","str"],

    2. 
    props:{
        middleArr:Array,
        str:String
    }

    3. 
    props:{
        num:{
                required:true,  //必须接受
                type:Number,  //接受数据类型
                default:100   //默认数据 //默认数据,string,number ,boolean 正常写。如果是array、object，必须是一个函数返回一个array、object
                // default:function(){
                //     return [1,2,3,4,5,6]
                // }
                validator(value){   //自定义验证
                    //必须传递 18 - 65之间  
                    return value >= 18 && value <= 65;
                }
        }
    }

```

