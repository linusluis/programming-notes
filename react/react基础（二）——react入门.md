# 一、React入门

## 1、官网

英文官网：[https://reactjs.org/](https://reactjs.org/)  
中文官网：[https://react.docschina.org/](https://react.docschina.org/)

## 2、React高效的原因

1. 使用虚拟（Virtual）DOM，不总是直接操作真实DOM。（在操作真实DOM之前，会把两个不同的虚拟DOM进行比较，比较出有差异的那一部分，再去更新页面）  
2. DOM Diffing算法，最小化页面重绘  

## 3、React的基本使用

### （1）实现Hello React 

第一次使用react，当然是要完成helloreact的效果啦，效果图：

![image.png](https://gitee.com/Jeren/cloudimages/raw/master/img/Hello_react.png)

 

react依赖包结构:
>- `babel.min.js`：学习React,写的不是原生的js，是jsx（jsx在js的基础上提出了一些要求和新的语法）。我们写的jsx语法，但是浏览器只认识js，所以需要babel。babel总共有两个作用：①是将ES6转换为ES5②是将jsx转换为js   
>- `react.development.js`：React的核心库  
>- `react-dom-development.js`：React的扩展库    
>- `prop-types`：用于对prop的类型和默认值做限制  
  
步骤：
>1. 引入依赖包：`react-development.js`要在`react-dom-development.js`之前引入
>1. 准备好一个容器
>1. 在script标签中编写jsx代码，注意：一定要将type类型设置为`type='text/babel'`
>1. 创建虚拟DOM。一定不要把标签当作字符串，一定不要写引号
>1. 渲染虚拟DOM到页面 ，使用`ReactDOM.reander(虚拟DOM,容器)`  

代码  

```html
<body>
    <!-- 准备好一个容器 -->
    <div id="test"></div>

    <!-- 引入react核心库 -->
    <script src="../../js/react.development.js"  ></script>
    <!-- 引入react-dom，用于支持react操作DOM -->
    <script src = "../../js/react-dom.development.js"></script>
    <!-- 引入babel，用于将jsx转为js -->
    <script src = "../../js/babel.min.js"></script>

    <script type="text/babel"> /* 此处一定要写babel */
    // 1. 创建虚拟DOM
        const VDOM = <h1>Hello,React</h1>;//此处一定不要写引号
    //2、渲染虚拟DOM到页面
        ReactDOM.render(VDOM,document.getElementById("test"));
    </script>
</body>
```
### （2）创建虚拟DOM的两种方式

**纯JS方式（实际开发不用，了解即可）**  

代码演示：  

```html
<body>
    <!-- 准备好一个容器 -->
    <div id="test"></div>
    <!-- 引入react核心库 -->
    <script src = '../../js/react.development.js'></script>
    <!-- 引入react-dom库，用于支持react操作DOM -->
    <script src = '../../js/react-dom.development.js'></script>
    <!-- 用原生的js创建虚拟DOM可以不使用babel -->

    <script type = 'text/javascript'>
        //1、创建虚拟DOM
        const VDOM = React.createElement('h1',{id:'title'},React.createElement('span',{},'Hello React'));
        //2、渲染虚拟DOM到页面
        ReactDOM.render(VDOM,document.getElementById('test'));
    </script>
</body>
```

说明
>原生js中有`createElement()`方法，React中也有这个方法。`React.createElement(标签名,标签属性,标签内容)`
>弊端：当发生标签嵌套的时候需要多次调用`React.createElement()`，比如上述代码在p标签中嵌入一个span标签，这样写就非常麻烦了  

**JSX方式：就是上面实现reacthello的代码，这里不再重新写了**  

>和原生js创建虚拟DOM的方式相比，可见jsx的好。jsx来到这个世界上它只为解决一个问题，就是使用原生js创建虚拟DOM太繁琐了，有了jsx可以让编码人员更加简单的创建虚拟DOM
>而且用小括号包起来，可以缩进。  
   
### （3）虚拟DOM与真实DOM

关于虚拟DOM
>本质是Object类型的对象（一般对象）
>虚拟DOM比较“轻”，真实DOM比较“重”，因为虚拟DOM是React内部在用，无需真实DOM上那么多的属性（使用debugger;在控制台可以查看节点属性）
>虚拟DOM最终会被React转化为真实DOM，呈现在页面上
>我们编码时基本只需要操作react 的虚拟DOM相关数据，react会自动转换为真实DOM  

## 4、jsx语法规则  

### （1）jsx介绍  

>1. 全称：JavaScript XML
>1. react定义的一种类似于XML的JS扩展语法：JS+XML 。本质是`React.createElement(component,props,...children)`方法的语法糖
>1. 作用：用来简化创建虚拟DOM
>>写法：`var ele = <h1>Hello JSX!</h1>`  
>>注意1：它不是字符串，也不是HTML、XML标签  
>>注意2：它最终产生的就是一个JS对象  
>4. 标签名任意：HTML标签或其他标签  
>4. 标签名属性任意：HTML标签属性或其他  
>4. 基本语法规则：  
>>遇到<开头的代码，以标签的语法解析：html同名标签转换为html同名元素，其它标签需要特别解析    
>>遇到以{开头的代码，以JS语法解析：标签中的js表达式必须用{ }包含  
>7. babel.js的作用
>>浏览器不能直接解析jsx代码，需要babel转译为纯js的代码才能运行  
>>只要用了jsx，都要加上`type='text/babel'`，声名需要babel来处理
>8. jsx的注释方式`{/*<input ref = {this.saveInput} type="text" /><br/><br/>*/}`  

### （2）jsx语法规则

>1. 定义虚拟DOM时，不要写引号
>1. 标签中混入JS表达式时要用{}。（一定要注意区分【js语句】和【js表达式】）
>1. 样式的类名指定不要用class，要用className。这是因为class是ES6中class类的关键字。为了避免混淆，所以使用className
>1. 内联样式，要用`style = {{key:value}}`的形式去写（外层{}是语法规定，内层{}意思是一个对象，可以传递多个属性键值对）如果属性名为font-size这种的，使用“小驼峰”命名法。
>1. 只有一个根标签
>1. 标签必须闭合，如果是自闭和标签，加一个“/”
>1. 标签首字母
>>- 若小写字母开头，则将标签转为html中同名元素，若html中无该标签对应的同名元素，则报错。
>>- 若大写字母开头，react就去渲染对应的组件，若组件没有定义，则报错

### （3）jsx的小练习

要求动态展示如下列表

![image.png](https://gitee.com/Jeren/cloudimages/raw/master/img/jsx的小练习.png)

代码实现：
```html
<body>
    <!-- //创建一个容器 -->
    <div id="test"></div>
    <!-- 引入react核心库 -->
    <script src = '../../js/react.development.js'></script>
    <!-- 引入react-dom库，为了让react可以操作DOM -->
    <script src = '../../js/react-dom.development.js'></script>
    <!-- 引入babel，为了将jsx转为js -->
    <script src = '../../js/babel.min.js'></script>
    <script type = 'text/babel'>
        //模拟一些数据
        const data = ['Angular','React','Vue'];
        //1、创建虚拟DOM
        const VDOM = (
            <div>
                <h1>前端js框架列表</h1>
                <ul>
                    {
                        data.map((value,index)=>{
                            return <li key = {index}>{value}</li>
                        })
                    }
                </ul>    
            </div>
        )
        //将虚拟DOM渲染至页面
        ReactDOM.render(VDOM,document.getElementById('test'));
    </script>
</body>
```

### （4）小总结
如果给react虚拟DOM一个数组，react会帮你遍历，如果给react虚拟DOM一个函数，react则不会帮你遍历  
一定要注意区分：【js语句（代码）】与【js表达式】  
>表达式：一个表达式会产生一个值，可以放在任何一个需要值的地方  
>下面这些都是表达式：  
>>a  
>>a+b  
>>demo(1)  
>>arr.map()  
>>dunction test() { }  
   
>语句（代码）：下面这些都是语句（代码）    
>>f(){}  
>>for(){}  
>>switch(){case:xxxx}  
>>  
## 5、模块与组件、模块化与组件化的理解  

### （1）模块  

理解：向外提供特定功能的js程序，一般就是一个js文件    
为什么要拆成模块：随着业务逻辑的增加，代码越来越多越复杂  
作用：复用js，简化js的编写，提高js运行效率  

### （2）组件

理解：用来实现局部功能的代码和资源的合集（html/css/jsimage等）  
为什么要用组件：一个界面的功能更复杂  
作用：复用编码，简化项目编码，提高运行效率  

![image.png](https://gitee.com/Jeren/cloudimages/raw/master/img/组件.png)
### （3）模块化

当应用的js都以模块来编写的，这个应用就是一个模块化的应用  

### （4）组件化

当应用是以多组件的方式实现，这个应用就是一个组件化的应用  

![image.png](https://gitee.com/Jeren/cloudimages/raw/master/img/组件化.png)
