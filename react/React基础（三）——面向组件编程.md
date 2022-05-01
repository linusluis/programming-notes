
# 一、准备工作——使用react开发者工具调试  

## 1、安装插件  

![react developer tools插件](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/react%20developer%20tools%E6%8F%92%E4%BB%B6.png?Expires=1651387205&OSSAccessKeyId=TMP.3KfNT7MvcaB4FbDQtrM23vHkbL6b6qKp9wu5zKiaafStZnPhoeKzksLjhMM6hzaEwLQ87CYSeJSoDRwixf5mvUxkEX31wk&Signature=UousS3qDrf%2Fi6Cb%2FBklSE%2FQNVtM%3D&versionId=CAEQHRiBgMC8_7jtgxgiIGY1MzdhOWZmZDU0MzQzYzc5M2RiYmEwYWQxNTllMzA0)  

## 2、插件图标状态  

- 红色：插件图标颜色是红色的说明网页是用react写的，但是react没有经过打包。还处于开发者的模式。也就是说网页没有经过打包上线，通过127.0.0.1这个形式去访问的  
- 蓝色：当图标是蓝色的时候，说明是上线发布了的，比如说meituan.com，就是用react写的  

## 3、Components和Profiler选项卡  

添加了这个组件之后，在浏览器的开发者工具中多了两个选项卡Components和Profiler  

>Components这个选项卡可以观察网页是由多少个组件组成的，每一个组件中都有什么属性  
>Profiler用于记录网站的一些性能，比如说渲染用了多久，哪一个组件加载的最慢，慢的原因是什么
## 4、Components控制台  

![Components控制台](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/Components%E6%8E%A7%E5%88%B6%E5%8F%B0.png?Expires=1651386790&OSSAccessKeyId=TMP.3KfNT7MvcaB4FbDQtrM23vHkbL6b6qKp9wu5zKiaafStZnPhoeKzksLjhMM6hzaEwLQ87CYSeJSoDRwixf5mvUxkEX31wk&Signature=KPcvHnSe0xjKDxmGzCGHL3dd4tA%3D&versionId=CAEQHRiBgMC6ibf4gxgiIDliOTdhMDAzNTQ1YjQ2MWM5OGRkZDM4YjI5Mzg5ZTQx) 

- props：是指组件身上的属性
- rendered by：指的是当前这个组件是由哪个版本的react渲染的  


# 二、基本理解和使用

react中有两种创建组件的方式：分别是函数式组件和类式组件  

## 1、函数式组件 

### （1）创建函数式组件 

步骤：  

1. 创建函数式组件
2. 渲染组件到页面

代码示例：  

```html
<!-- 准备一个容器 -->
    <div id="test"></div>
    <!-- 引入react核心库 -->
    <script src = '../../js/react.development.js'></script>
    <!-- 引入react-dom库，用于支持react操作DOM -->
    <script src = '../../js/react-dom.development.js'></script>
    <!-- 引入babel,用于将jsx转为js -->
    <script src = '../../js/babel.min.js'></script>
    <script type="text/babel">
        // 1、创建函数式组件
        function MyComponent(){ //组件名一定要大写
            console.log(this);  //此处的this是undefined，因为babel编译后开启了严格模式
            return <h2>我是用函数定义的组件，（适用于【简单组件】的定义）</h2> //一定要有返回语句
        }
        //22、渲染组件到页面
        ReactDOM.render(<MyComponent />, document.getElementById('test'));//渲染的时候必须以标签的形式写组件
    </script>
```  
### （2）注意

1. 函数式组件的组件名必须要大写
2. 函数必须有返回值
3. 渲染到页面的时候必须要写组件标签

### （3）问题
> 1. 函数式组件中的this是谁？

通过打印会发现，this是undefined。在原生js中，以()调用方法，this就是window。为什么在组建中是undefined呢？是因为babel对jsx进行了翻译，babel翻译完之后，开启了严格模式。而严格模式的最大特点就是禁止这种自定义函数中的this指向window，所以是undefined。  

> 2. 执行了`ReactDOM.render(<MyComponent/>....`之后，发生了什么？  

react解析组件标签找到了`MyComponent`组件。发现组件是使用函数定义的，随后调用该函数，将返回的虚拟DOM转为真实DOM,随后呈现在页面中。

## 2、复习类的知识  

学到这里，类的知识也忘得差不多了，让我们一起回顾一下 

```javascript
        class Person{
            constructor(name,age){
                this.name = name;
                this.age = age;
            }
            speak(){
                console.log(`我叫：${this.name}，今年${this.age}岁了`);
            }
        }
        class Student extends Person{
            constructor(name,age,grade){
                super(name,age);
                this.grade= grade;
            }
            //父类方法的重写,一旦重写子类实例就无法访问到父类中被重写的方法了
            speak(){
                console.log(`我叫：${this.name}，今年${this.age}岁了,${this.grade}年级`);
            }
            slogon='我们都是学生';//slogon类的自身访问不到，但是它的实例可以访问到
            static c = '123';//c是类的静态属性，只有类自身可以访问到
        }
        let stu = new Student('lius',18,8);
        stu.speak();
        console.log(stu.slogon);//我们都是学生
        console.log(stu.c);//undefined
        console.log(Student.c);//123
        console.log (Student.slogon);//undefined
```

总结：
>1. 类中的构造器不是必须写的，要对实例进行一些初始化的操作，如添加指定属性时才写
>1. 如果A类继承了B类，且A类中写了构造器，那么A类构造器中的super是必须要调用的
>1. 类中所定义的方法，都是放在了类的原型对象上，供实例去使用。


## 3、类式组件

### （1）创建类式组件

步骤：
1. 创建类式组件
2. 渲染类式组件到页面  

代码示例：  

```html
<body>
    <!-- 创建一个容器 -->
    <div id="test"></div>
    <!-- 引入react核心库 -->
    <script src = '../../js/react.development.js'></script>
    <!-- 引入react-dom库，为了让react操作DOM -->
    <script src = '../../js/react-dom.development.js'></script>
    <!-- 引入babel，为了将jsx转为js -->
    <script src = '../../js/babel.min.js'></script>
    <script type = text/babel>
        // 1、创建类组件
        class MyComponent extends React.Component{
            render(){
                //render是放在哪里的？——MyComponent的原型对象上，供实例使用
                //render中的this是谁？——MyComponent的实例对象 <=> MyComponent组件实例对象
              	console.log(this);
                return <h2>我是用类定义的组件（适用于【复杂组件】的定义）</h2>
            }
        }
        //2、渲染类组件到页面
        ReactDOM.render(<MyComponent />, document.getElementById('test'));
    </script>
</body>
```
### （2）注意  

1. 一定要继承`React.Component`类  
2. 一定要有`render()`方法  
3. `render()`方法一定要有返回值  

### （3）问题

> 1. render是放在哪里的？
MyComponent的原型对象上，供实例使用。  

> 2. render中的this是谁？  
MyComponent的实例对象 <=> MyComponent组件实例对象。因为在渲染的时候，react会自动new出来一个组件实例，并通过该实例调用render方法，所以this就是组件实例对象 

> 3. 执行了`ReactDOM.render(<MyComponent/>......之后`，发生了什么？
1. React解析组件标签，找到了MyComponent组件。
2. 发现组件是使用类定义的，随后new出来该类的实例，并通过该实例调用到原型上的render方法。
3. 将render返回的虚拟DOM转为真实DOM，随后呈现在页面中。

# 三、组件实例的三大核心属性

既然说到组件实例的三大核心属性，可想而知，这三大属性是针对类式组件来说的。但这种说法不绝对，React新出了一个东西叫做`hooks`，能够让函数式组件操作这三大属性

## 1、简单组件与复杂组件

区分简单组件与复杂组件的区分：
- 复杂组件：如果组件是有状态state（不为null）的就是复杂组件
- 简单组件：如果组件是没有状态（为null）的就是简单组件

## 2、属性1：state

### （1）初步理解

> 什么是状态state：
下面以人的状态为例说明组件的状态  
   - 人   的    状态     影响      行为
   - 组件 的    状态     驱动      页面
总而言之，组件的状态里面存放着数据，数据的改变就会驱动着页面的展示  

### （2）初始化state并使用状态中的数据

我们要使用state完成以下效果，点击`h1`切换文字。

![state案例](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/state%E6%A1%88%E4%BE%8B.gif?Expires=1651387285&OSSAccessKeyId=TMP.3KfNT7MvcaB4FbDQtrM23vHkbL6b6qKp9wu5zKiaafStZnPhoeKzksLjhMM6hzaEwLQ87CYSeJSoDRwixf5mvUxkEX31wk&Signature=Ff890IlxcaGtNtvg%2FmihHtMICUI%3D&versionId=CAEQHRiBgMCnw_r0gxgiIGNlNjVmNmRlOTA3YTQxNWRiYjE2Mzg5ZTUyMTRiMTI5)

首先第一步就是初始化state中的数据。需要使用`constructor`来进行state的初始化。  

代码示例：

```javascript
		//创建一个类式组件
        class Weather extends React.Component {
            constructor(props){ //想让组件有状态就需要使用构造器
                super(props);
              	//初始化状态
                this.state = {isHot:false};//这个this是组件实例对象
            }
            render(){
              	//读取状态
                console.log(this.state);//这个this也是组件实例对象
                return <h1>今天天气很{this.state.isHot?'炎热':'凉爽'}</h1>
            }
        }
        //渲染组件到页面
        ReactDOM.render(<Weather/>,document.getElementById('test'));
```

说明：
1. 简单组件可以不使用constructor构造器，有状态组件需要使用构造器（也可以不使用，下文的简化写法就不需要使用）
2. 当组件实例的状态数据改变时，组件实例会再次调用render()方法重新渲染对应的标记

### （3）react中的事件绑定

首先，我们来总结一下原生js中事件绑定的三种方式：
1. onclick方式
2. addEventListener()方法
3. 绑定给html标签

这三种方式在react中都支持，，但是最好的方式是使用绑定给html标签这种方式，是因为为了减少原生操作DOM元素的代码（像document.getElementById什么的）  

在react中使用事件绑定的代码举例：即下文中的onClick事件

```javascript
 //创建一个类式组件
        class Weather extends React.Component {
            constructor(props){ //想让组件有状态就需要使用构造器
                super(props);
                //初始化状态
                this.state = {isHot:false};//这个this是组件实例对象
            }
            render(){
              	console.log(this.state);//这个this也是组件实例对象
                //读取状态
              	const {isHot} = this.state; //解构赋值
                return <h1 onClick = {changeWeather}>今天天气很{isHot?'炎热':'凉爽'}</h1> //注意不要写成changeWeather()，
                //如果写成changeWeather()，意思就是将changeWeather函数的返回值赋值给onClick事件了，当执行onclick事件时onclick不生效，被赋值为undefined了.
                //而且还要注意事件名称要遵循小驼峰命名方式
            }
            
        }
        //渲染组件到页面
        ReactDOM.render(<Weather/>,document.getElementById('test'));
        function changeWeather(){
            console.log('标题被点击了');
        }
```

注意：
1. 事件名称和原生js中的不一样，要使用小驼峰命名法
2. 绑定事件函数的时候，不要把返回值赋值给事件。像`onclick = {changeWeather()}`这样是不行的，因为这样写的意思是将changeWeather方法的返回值赋值给onclick事件了。当执行onclick事件时onclick不生效，被赋值为undefined了。切记：一定不能加小括号()，除非这个方法中的返回值是一个方法（这涉及到高阶函数，下文会说）。

### （4）类中方法中的this（难点）

#### <1> 分析自定义方法中的this

目前，我们知道`constructor`构造器中的`this`是组件实例。`render`方法中的`this`也是组件实例。那么类中自定义方法的this是什么呢？  

我们在自定义方法中打印this，如下列代码。发现：自定义方法中`this`是`undefined`。  

这是因为changeWeather是作为oncClick的回调，所以不是通过实例调用的，是函数直接调用。这样changeWeather方法中的this指向`window`。而类中的方法默认开启了局部的严格模式，所以changeWeather中的this最终为undefined。  

```javascript
		//创建一个类式组件
        class Weather extends React.Component {
            constructor(props){ //想让组件有状态就需要使用构造器
                super(props);
                //初始化状态
                this.state = {isHot:false};//这个this是组件实例对象
            }
            render(){
                //读取状态
                const {isHot} = this.state; //解构赋值
                console.log(this.state);//这个this也是组件实例对象
                return <h1 onClick = {this.changeWeather}>今天天气很{isHot?'炎热':'凉爽'}</h1> 
            }
            changeWeather(){
                //由于changeWeather是作为oncClick的回调，所以不是通过实例调用的，是函数直接调用
                //类中的方法默认开启了局部的严格模式，所以changeWeather中的this为undefined
            console.log(this);//undefined
        }
            
        }
        //渲染组件到页面
        ReactDOM.render(<Weather/>,document.getElementById('test'));
```

总结：
1. 为了让changeWeather()方法能操作到state中的数据，所以需要把changeWeather方法拿到类中定义。而且绑定事件的时候，要用`this.changeWeather`。然后问题就出现了=====>我们发现changeWeather中的this是undefined，这是为什么呢？目前，类中有三块内容，我们好好梳理一下这三块内容中的this。
1. constructor构造器中的 this：constructor中的this无论继不继承都是当前类的实例对象，在React中，渲染的时候会自动生成实例对象，所以这个this就指向自动生成的实例对象
1. render()方法中的this，在渲染的时候，react自动帮我们创建对应的实例对象，并通过该实例对象调用原型上的render方法，因此，render()方法中的this也是指向自动生成的实例对象
1. changeWeather()方法中的this：首先changeWeather放在哪里？——放在Weather的原型对象上，供实例使用。由于changeWeather是作为onClick的回调，所以不是通过实例调用的，是直接函数形式调用的。按理来说，它的this应该指向window，但是类中的方法默认开启了局部的严格模式，所以changeWeather中的this为undefined  

#### <2> 解决自定义方法中的this指向问题

直接说方法：在构造函数中添加`this.changeWeather = this.changeWeather.bind(this);`，解决changeWeather中this指向问题  

进一步说明这条语句
- 先看右边部分`this.changeWeather.bind(this)`。首先要知道constructor中的this是组件实例对象，然后实例对象沿着原型链找到在类中定义的changeWeather方法，然后调用bind()方法，将实例对象指定为changeWeather方法中的this，并且返回了一个新的changeWeather方法,这个方法中的this是指向组件实例对象的
- 再看左边部分`this.changeWeather`，constructor中的this是组件实例对象，然后定义一个changeWeather属性。然后结合起来看，changeWeather这个属性的值，就是右边返回的那个改变了this指向的新的changeWeather方法。

```javascript
        //创建一个类式组件
        class Weather extends React.Component {
            constructor(props){ 
                super(props);
                //初始化状态
                this.state = {isHot:false};//这个this是组件实例对象
                //解决changeWeather中的this指向问题
                this.changeWeather = this.changeWeather.bind(this);
            }
            render(){
                //读取状态
                const {isHot} = this.state; //解构赋值
                console.log(this.state);//这个this也是组件实例对象
                return <h1 onClick = {this.changeWeather}>今天天气很{isHot?'炎热':'凉爽'}</h1> 
            }
            changeWeather(){
                console.log(this);//此时this为组件实例对象
            }
        }
```



### （5）setState的使用（更改状态中的数据）

状态中的数据不能直接更改。状态必须通过setState进行更新，且更新是一种合并而不是替换。

```javascript
        //创建一个类式组件
        class Weather extends React.Component {
            constructor(props){ //想让组件有状态就需要使用构造器
                super(props);
                //初始化状态
                this.state = {isHot:false,wind:'微风'};//这个this是组件实例对象
                //解决changeWeather中的this指向问题
                this.changeWeather = this.changeWeather.bind(this);
            }

            render(){
                //读取状态
                const {isHot,wind} = this.state; //解构赋值
                console.log(this.state);//这个this也是组件实例对象
                return <h1 onClick = {this.changeWeather}>今天天气很{isHot?'炎热':'凉爽'},{wind}</h1> 
            }

            changeWeather(){
                console.log(this);
                //获取原来的isHot值
                const isHot = this.state.isHot;
                //严重注意：状态必须通过setState进行更新，且更新是一种合并，不是替换。
                this.setState({isHot:!isHot});
                //严重注意：状态(state)不可以直接更改，下面这行就是直接更改！！！
                // this.state.isHot = !isHot;
            }
        }
        //渲染组件到页面
        ReactDOM.render(<Weather/>,document.getElementById('test'));
```

问题：  
1. 状态更新是替换还是合并？ 状态更新是一种合并而非替换
2. 构造器调用几次？构造器调用1次
3. render调用几次？render调用1+n次 。1次是初始化次数 n是状态更新的次数
4. changeWeather调用几次 点击几次调用几次  

setState总结
1. 为什么要写构造器 ？需要在构造器里初始化状态和解决this指向问题
2. 为什么要写render ？从状态里读取数据，根据数据值做展示
3. 为什么要写changeWeather？获取state中的数据，更新数据

### （6）state的简写方式 

在类中写的自定义方法一般有两个用途：
1. 作为事件回调和用户做交互的
2. 作为标签的属性，传递给子组件  

因此，如果不在构造器中指定这些方法的this，这些方法的this就都是`undefined`

然而我们可以通过两处简写，来解决以上的问题。
1. 去掉构造函数。将初始化state语句从原型中拿出来，放到实例自身上，这样其实例都能拿到这个state。
2. 组件中所有的自定义方法都要写成赋值语句+箭头函数这种形式。这种形式将方法放到了实例的自身上，而不是原型对象中，每个实例对象都能拿到，而且通过箭头函数解决了this的指向问题，何乐而不为呢。

```javascript
				// 创建一个组件
        class Weather extends React.Component{
            //简写1：初始化state
            state = {isHot:false,wind:'微风'};
            render(){
                const {isHot,wind} = this.state;
                return <h2 onClick={this.changeWeather}>今天天气很{isHot?'炎热':'凉爽'},{wind}</h2>
            }
            //简写2：自定义方法——要用赋值语句的形式+箭头函数
            changeWeather=()=>{
                const isHot = this.state.isHot;
                this.setState({isHot:!isHot});
            }
        }
        //将组件渲染到页面
        ReactDOM.render(<Weather/>,document.getElementById('test'));
```


### （7）state总结

1. state是组件对象最重要的属性，值是对象（可以包含多个key-value的组合）不能是数组
2. 组件被称为状态机（红绿灯），通过更新组件的state来更新对应的页面显示（重新渲染组件）
3. **强烈注意**：状态数据：不能直接修改或更新

## 3、属性2：props

理解：
1. 每个组件都会有props（properties的简写）属性
2. 组件标签的所有属性都保存在props中

作用：
1. 通过标签属性从组件外向组件内传递变化的数据
2. 注意：组件内部不要修改props数据，只能使用。

我们要使用props完成以下案例：  

- 自定义用来显示一个人员信息的组件
- 姓名必须指定，且为字符串类型
- 性别为字符串类型，如果性别没有指定，默认为男
- 年龄为字符串类型，且为数字型，默认值为18

效果图：
![props案例](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/props%E6%A1%88%E4%BE%8B.png?Expires=1651387348&OSSAccessKeyId=TMP.3KfNT7MvcaB4FbDQtrM23vHkbL6b6qKp9wu5zKiaafStZnPhoeKzksLjhMM6hzaEwLQ87CYSeJSoDRwixf5mvUxkEX31wk&Signature=a55thYVPqcrJkzy%2B4gMNxpb08BA%3D&versionId=CAEQHRiBgMCs26r3gxgiIDE1ZWU2NmYxOTcwZjQzMGE4ZmZlYmY1NmFkZTBhNDNk)

### （1）props基本使用

props的基本使用非常简单，只需要在渲染组件到页面的时候在标签中以key=value的形式传递数据即可。然后在组件中用this接收，即可展示到页面。

参照下列代码：

```javascript
// 创建一个组件
        class Person extends React.Component {
            render(){
                const {name,age,sex} = this.props;
                return (
                    <ul>
                        <li>姓名：{name}</li>
                        <li>年龄：{age}</li>
                        <li>性别：{sex}</li>
                    </ul>
                )
            }
        }
        //将组件渲染到页面上
        ReactDOM.render(<Person name='Tom' age='18' sex='男'/>,document.getElementById('test'));
        ReactDOM.render(<Person name='Jerry' age='24' sex='女'/>,document.getElementById('test2'));
        ReactDOM.render(<Person name='Bili' age='28' sex='男'/>,document.getElementById('test3'));
```

### （2）批量传递props（批量传递标签属性）
如果是真实的项目开发，人的信息是由服务器返回的，得发一个Ajax请求把数据带回来，然后做展示。所以向上面的方法给组件传递属性是非常麻烦的，因此，可以批量传递props。  

批量传递props的方法就是使用扩展运算符。

先简单回顾一下原生js的扩展运算符：  
原生js中不允许使用展开运算符展开一个对象，像这样...person，但是可以像这样拷贝一个对象{...person}。而在react中和这种的不是一回事儿。  

react+babel允许使用展开运算符展开一个对象，即...person。但是我们在实际开发中这个展开运算符不能让你随便去用，仅仅适用于标签属性的传递，别的地方使用都不行。所以在标签中我们要这样写{...person}。切记，这个和原生的扩展运算符拷贝一个对象不是一回事儿。在react中，这个{}只是react的语法规范，作为分隔符使用的。  

**一定切记，在react中允许使用展开运算符展开一个对象，和原生的拷贝对象不是一回事儿。**


### （3）对props进行限制

为了完成需求，我们发现还存在三个问题
1. 对传递的标签属性进行类型的限制
1. 对传递的标签属性进行必要性的设置
1. 给某一个属性指定默认值

React15.xxx之前，使用React.PropTypes.xxx属性对传递的标签属性进行限制。在React16.xxx之后，这个属性通过引入依赖包`prop-types.js`使用   

使用`Person.propType = {}`对标签属性进行类型和必要性的限制   
使用`Person.defaultProps={}`指定标签默认属性值。

代码演示：
```html
  <!-- 创建一个容器 -->
    <div id="test"></div>
    <div id="test2"></div>
    <div id="test3"></div>
    <div id="test4"></div>
    <!-- 引入react -->
    <script src = '../../js/react.development.js'></script>
    <!-- 引入react-dom，为了让react操作DOM -->
    <script src = '../../js/react-dom.development.js'></script>
    <!-- 引入babel,为了将jsx转为js -->
    <script src = '../../js/babel.min.js'></script>
    <!-- 引入prop-types，为了对prop属性进行限制 -->
    <script src ='../../js/prop-types.js'></script>
    <script type = 'text/babel'>
        // 创建一个组件
        class Person extends React.Component {
            render(){
                const {name,age,sex} = this.props;
                return (
                    <ul>
                        <li>姓名：{name}</li>
                        <li>年龄：{age+1}</li>
                        <li>性别：{sex}</li>
                    </ul>
                )
            }
        }
        //对标签属性进行类型、必要性的限制
        Person.propTypes = {
            name:PropTypes.string.isRequired,//限制name必传，且为字符串
            sex:PropTypes.string,//限制sex为字符串
            age:PropTypes.number,//限制age为数值
            // speak:PropTypes
        }
        //指定默认标签属性值
        Person.defaultProps = {
            sex:'男',//sex默认值为男
            age:18//age默认值为18
        }
        //将组件渲染到页面上
        ReactDOM.render(<Person name='Tom' age={18} sex='男'/>,document.getElementById('test'));
        ReactDOM.render(<Person name='Jerry' sex='女'/>,document.getElementById('test2'));
        ReactDOM.render(<Person name='Bili'/>,document.getElementById('test3'));
        const p = {name:'julia',age:32,sex:'男'};
        ReactDOM.render(<Person {...p}/>,document.getElementById('test4'));
```

说明：
1. props是只读的
2. 大写的PropTypes是因为引入了Prop-types.js这个库，全局才出现了PropTypes。至于小写的propTypes，是react里的要求，应该给组件加上这个属性。如果不加这个属性，找不到这个属性，就认为没有任何限制。

### （4）Props的简写方式

目前，对标签属性进行类型、必要性的限制，指定默认标签属性值这些操作都是设置在类的外面的。这样不好。我们希望类中囊括所有和组件相关的东西。  

可以通过为类设置静态变量的方式将这些操作放到类的自身上。


代码演示：
```javascript
 // 创建组件
        class Person extends React.Component {
            render(){
                //获取传过来的props
                const {name,age,sex} = this.props;
                return(
                    <ul>
                        <li>姓名：{name}</li>                        
                        <li>年龄：{age}</li>                        
                        <li>性别：{sex}</li>                        
                    </ul>
                )
            }
            //对标签属性进行类型、必要性的限制
            static propTypes = {
                name:PropTypes.string.isRequired,
                age:PropTypes.number,
                sex:PropTypes.string
            }
            //指定默认标签属性值
            static defaultProps = {
                sex:'男',
                age:18
            }
        }
        //将组件渲染到页面
        ReactDOM.render(<Person name = 'juren' age ={27} sex = '男'/>,document.getElementById('test1'));
        ReactDOM.render(<Person name = 'bingo' age ={19} sex = '女'/>,document.getElementById('test2'));
        ReactDOM.render(<Person name = 'luxu'/>,document.getElementById('test3'));
        const p = {name:'siri',age:33};
        ReactDOM.render(<Person {...p}/>,document.getElementById('test4'));
```

### （5）类式组件中的构造器和props

通常，在React中，构造函数仅用于以下两种情况：（这两种情况前边都有用过）
1. 是通过this.state赋值对象来初始化内部state
2. 是为事件处理函数绑定实例

```javascript
            constructor(props){ //想让组件有状态就需要使用构造器
                super(props);
                //初始化状态
                this.state = {isHot:false};//这个this是组件实例对象
                //解决changeWeather中的this指向问题
                this.changeWeather = this.changeWeather.bind(this);
            }
```

然而，如果我们不使用constructor，以上两种情况也能通过其他方式处理，所以是否使用构造器对我们来说无伤大雅。在开发中基本上就是不用构造器。  

我们发现，如果使用了构造器，不传props也无伤大雅。构造器是否接受props，是否传递给super，取决于：是否希望在构造器中通过this访问props，如果有这种需求的，就必须传递和接收props。但这种需求在开发中，出现的概率基本为零。  

### （6）函数式组件使用props

对于函数式组件，state属性和refs属性，是无法操作的，但是却可以操作props属性。因为函数有一个特点，函数可以接收参数。所以所有传递到函数式组件的标签属性都收集成为一个对象props，作为参数传递进组件中。

代码演示：
```html
 <!-- 创建容器 -->
    <div id="test1"></div>
    <div id="test2"></div>
    <div id="test3"></div>
    <div id="test4"></div>
    <div id="test5"></div>
    <!-- 引入react -->
    <script src = '../../js/react.development.js'></script>
    <!-- 引入react-dom，为了让react操作DOM -->
    <script src = '../../js/react-dom.development.js'></script>
    <!-- 引入babel,为了将jsx转为js -->
    <script src = '../../js/babel.min.js'></script>
    <!-- 引入prop-types，为了对标签属性做限制 -->
    <script src = '../../js/prop-types.js'></script>
    <script type = 'text/babel'>
        //创建函数式组件，使用函数式组件操作props
        function Person(props){
            const {name,age,sex} = props;
            return (
                <ul>
                    <li>名字：{name}</li>    
                    <li>年龄：{age}</li>    
                    <li>性别：{sex}</li>    
                </ul>  
            )
        }
        // 对标签属性进行类型和必要性的限制
        Person.propTypes = {
                name:PropTypes.string.isReauired,
                age:PropTypes.number,
                sex:PropTypes.string
            }
            //指定默认标签属性值
        Person.defaultProps = {
                age:18,
                sex:'男'
            }
        //将组件渲染到页面
        ReactDOM.render(<Person name='pia' age={77} sex ='男'/>,document.getElementById('test1'));
        ReactDOM.render(<Person name='george'/>,document.getElementById('test2'));
        ReactDOM.render(<Person name='paul' age={45} sex ='女'/>,document.getElementById('test3'));
        ReactDOM.render(<Person name='jessa' age={26}/>,document.getElementById('test4'));
        const p = {name:'ria',age:99};
        ReactDOM.render(<Person {...p}/>,document.getElementById('test5'));
    </script>
```

## 4、属性3：refs与事件处理

什么是refs?
- 可以把ref理解成打标识，相当于原生中的id。refs就是保存多个标识的对象。
- 一个ref的key是设置的ref的值，value是ref当前所处的这个节点，这个value不是虚拟DOM，是虚拟DOM转为真实DOM之后的那个真正的节点。

我们要使用refs属性完成下列案例：  

效果图：

![refs案例](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/refs%E6%A1%88%E4%BE%8B.gif?Expires=1651384477&OSSAccessKeyId=TMP.3KfNT7MvcaB4FbDQtrM23vHkbL6b6qKp9wu5zKiaafStZnPhoeKzksLjhMM6hzaEwLQ87CYSeJSoDRwixf5mvUxkEX31wk&Signature=mtbTUjhJDxVWlA20Y2z4hVCQsXw%3D&versionId=CAEQHRiBgIDD2_D3gxgiIGI3NWUzZDM0ODkzMjRlNWFiY2NlOWI0YzAxNjYxMjE2)


### （1）字符串形式的ref

使用字符串形式的ref实现案例

```html
 <!-- 创建容器 -->
    <div id="test"></div>
    <!-- 引入react核心库 -->
    <script src = '../../js/react.development.js'></script>
    <!-- 引入react-dom用于react操作dom -->
    <script src = '../../js/react-dom.development.js'></script>
    <!-- 引入babel ，用于将jsx转为js-->
    <script src = '../../js/babel.min.js'></script>
    <!-- 引入prop-types，用于对标签属性进行限制 -->
    <script src = '../../js/prop-types.js'></script>
    <script  type = 'text/babel'>
        // 创建组件
        class Demo extends React.Component {
            render(){
                return(
                    <div>
                        <input ref = 'input1' type="text" placeholder="点击按钮提示数据"/>&nbsp;
                        <button onClick = {this.showData}>点我提示左侧的数据</button>&nbsp;
                        <input ref = 'input2' onBlur = {this.showData2} type="text" placeholder="失去焦点提示数据"/>&nbsp;
                    </div>  
                )
            }
            showData = ()=>{
                const {input1} = this.refs;
                alert(input1.value);
            }
            showData2 = () =>{
                const {input2} = this.refs;
                alert(input2.value);
            }
        }
        //渲染组件到页面
        ReactDOM.render(<Demo/>,document.getElementById("test")); 
    </script>  
```


### （2）回调形式的ref

字符串形式的ref已经不被react官方推荐使用了。而且以后再更新，很有可能把这种方式废弃掉。因为string类型的refs存在一些效率上的问题

回调函数需要满足三个特定
1. 你定义的函数
2. 你没有调用
3. 但是执行了

使用回调函数形式的ref实现案例
```html
 <div id="test"></div>
    <!-- 引入react核心库 -->
    <script src = '../../js/react.development.js'></script>
    <!-- 引入react-dom，用于让react操作DOM -->
    <script src = '../../js/react-dom.development.js'></script>
    <!-- 引入babel，为了将jsx转为js -->
    <script src = '../../js/babel.min.js'></script>
    <!-- 引入prop-types，为了对标签属性进行限制 -->
    <script src = '../../js/prop-types.js'></script>

    <script type = 'text/babel'>
        class Demo extends React.Component {
            render(){
                return (
                    <div>
                    <input ref = {currentNode=>this.input1 = currentNode} type="text" placeholder='点击按钮提示数据'/>
                    <button onClick = {this.showData}>点我提示左侧的数据</button>    
                    <input ref = {currentNode=>this.input2 = currentNode} onBlur = {this.showData2} type="text" placeholder="失去焦点提示数据"/>
                    </div>
                )
            }
            showData = () =>{
                const {input1} = this;
                alert(input1.value);
            }
            showData2 = ()=>{
                const {input2} = this;
                alert(input2.value);
            }
        }
        ReactDOM.render(<Demo/>,document.getElementById('test'));
    </script>
```

`ref = {currentNode=>this.input1 = currentNode}`这条语句的意思是：为了在页面展示内容，先要创建一个组件实例，react通过组件实例调用render()方法，调用render的时候，执行里面的jsx代码，当执行到这条语句的时候，就直接触发了这个回调函数的执行，而且这个函数中的参数是当前所处的节点，然后把这个节点放到了组件实例自身的input1属性中，这个input1属性名是自己定义的。  
这里的this是箭头函数的this，所以这个this是回调函数作用域的this，是render里的this，就是组件实例对象。  
总之，这么写的意思就是：把ref当前所处的节点挂在了实例自身上，并且取个名字叫input1

### （3）回调ref的调用次数问题

如果ref回调函数是以内联函数方式定义的（就是上述方式），**在更新过程中（指render多次调用）**它会被执行两次，第一次传入参数null。然后第二次会传入参数DOM元素。这是因为在每次渲染时会创建一个新的函数实例，所以React清空旧的ref并且设置新的。通过将ref的回调函数定义成class的绑定函数的方式可以避免上述问题，但是大多数情况下它是无关紧要的。因此，在开发中可直接使用内联函数方式调用就行。   

![回调ref的调用次数问题](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/%E5%9B%9E%E8%B0%83ref%E7%9A%84%E8%B0%83%E7%94%A8%E6%AC%A1%E6%95%B0%E9%97%AE%E9%A2%98.png?Expires=1651385086&OSSAccessKeyId=TMP.3KfNT7MvcaB4FbDQtrM23vHkbL6b6qKp9wu5zKiaafStZnPhoeKzksLjhMM6hzaEwLQ87CYSeJSoDRwixf5mvUxkEX31wk&Signature=BaN1FevzGj%2FnLWESHEl4lGAXu0w%3D&versionId=CAEQHRiBgICInIP4gxgiIDhhMmVhNzU5ZGI5OTQ2NjM4MzMyZmQxMTU1YjI1Nzll)

使用class绑定函数方式就避免了这个问题，如下面代码。但是这个问题无关紧要

```javascript
class Demo extends React.Component{
            state = {isHot:'true'};
            render(){
                const {isHot} = this.state;
                return (
                    <div>
                        <h1>今天天气很{isHot?'炎热':'凉爽'}</h1>
                        <input ref = {this.saveInput} type="text" /><br/><br/>
                        <button onClick={this.showData}>点我提示输入的数据</button>    
                        <button onClick={this.changeWeather}>点我切换天气</button>    
                    </div>
                )
            }
            saveInput = (currentNode)=>{
                this.input = currentNode;
                console.log('@',currentNode);
            }
            showData=()=>{
                const {input1} = this;
                alert(input1.value);
            }
            changeWeather=()=>{
                const {isHot} = this.state;
                this.setState({isHot:!isHot});
            }
        }
        ReactDOM.render(<Demo/>,document.getElementById('test'));
```

### （4）React.createRef()的使用（React最推荐的一种形式）

React.createRef调用后可以返回一个容器，该容器可以存储被ref所标识的节点，该容器是“专人专用”，也就是说这个容器只能一次存储一个ref，如果存储多个，后面的会将前面的覆盖。如果要存储多个ref，就只能多创建几个容器了。  

容器中有一个current属性，这个属性的值就是被ref所标识的节点。    

使用createRef的方式实现案例

```html
    <!-- 创建一个容器 -->
    <div id="test"></div>
    <!-- 引入react核心函数 -->
    <script src = '../../js/react.development.js'></script>
    <!-- 引入react-dom，为了让react操作DOM -->
    <script src = '../../js/react-dom.development.js'></script>
    <!-- 引入babel，为了将jsx转换为js -->
    <script src = '../../js/babel.min.js'></script>
    <!-- 引入prop-types，为了做标签属性的限制 -->
    <script src = '../../js/prop-types.js'></script>
    <script type="text/babel">
        // 创建一个组件
        class Demo extends React.Component {
            myRef = React.createRef();
            myRef2 = React.createRef();
            render(){
                return (
                    <div>
                    {/*这条语句中ref使用的意思就是，把当前ref所在的这个节点，直接存储到了容器里面。*/}
                        <input ref = {this.myRef} type="text" placeholder="点击按钮提示数据"/>
                        <button onClick = {this.showData}>点我提示左侧的数据</button>    
                        <input ref = {this.myRef2} onBlur = {this.showData2} type="text" placeholder="失去焦点提示数据"/>
                    </div>
                )
            }
            showData = ()=>{
                alert(this.myRef.current.value);//myRef中有个current属性
            }
            showData2 = () =>{
                alert(this.myRef2.current.value);
            }
        }
        // 将组件渲染到页面
        ReactDOM.render(<Demo/>,document.getElementById("test"));
    </script>
```

### （5）事件处理
1. 通过onXxx属性指定事件处理函数（注意大小写）
> - React使用的是自定义（合成）事件，而不是使用的原生DOM事件——为了更好的兼容性
> - React中的事件是通过事件委托方式处理的（委托给组件最外层的元素）——为了更高效

2. 通过event.target得到发生事件的DOM元素对象————不要过度使用ref
> - 有时候ref是可以避免的。什么时候可以避免呢？发生事件的元素正好是你要操作的元素就可以省略ref。然后使用event.target得到发生事件的DOM元素对象。
> - 而发生事件的元素和你要操作的元素不是一个的时候，也可拿到你要操作的元素，这个在受控组件和非受控组件部分有说。

举例：就像上面代码中的第二个输入框，就可以不通过ref来拿到要操作的元素，而通过event.target来拿到要操作的元素
代码演示：
```html
<!-- 创建一个容器 -->
    <div id="test"></div>
    <!-- 引入React核心库 -->
    <script src = '../../js/react.development.js'></script>
    <!-- 引入react-dom，为了让react能够操作DOM -->
    <script src = '../../js/react-dom.development.js'></script>
    <!-- 引入babel，为了将jsx转为js -->
    <script src = '../../js/babel.min.js'></script>
    <!-- 引入prop-types为了做标签属性的限制 -->
    <script src = '../../js/prop-types.js'></script>
    <script type = 'text/babel'>
        // 创建一个容器
        class Demo extends React.Component {
            myRef = React.createRef();
            myRef2 = React.createRef();
            render(){
                return (
                    <div>
                        <input ref = {this.myRef} type="text" placeholder="点击按钮提示数据"/>
                        <button onClick = {this.showData}>点我提示左侧的数据</button>    
                        <input ref = {this.myRef2} type="text" onBlur = {this.showData2} placeholder="失去焦点提示数据"/>
                    </div>
                )
            }
            showData = ()=>{
                alert(this.myRef.current.value);
            }
            showData2 = (event)=>{
                alert(event.target.value);
            }
        }
        ReactDOM.render(<Demo/>,document.getElementById('test'));
    </script>
```


# 四、收集表单数据

我们将要运用受控组件和函数柯里化等知识去实现这样一个案例：
要求：定义一个包含表单的组件。输入用户名和密码后，点击登录提示输入信息

效果图：  
![收集表单数据的案例](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/%E6%94%B6%E9%9B%86%E8%A1%A8%E5%8D%95%E6%95%B0%E6%8D%AE%E7%9A%84%E6%A1%88%E4%BE%8B.gif?Expires=1651385822&OSSAccessKeyId=TMP.3KfNT7MvcaB4FbDQtrM23vHkbL6b6qKp9wu5zKiaafStZnPhoeKzksLjhMM6hzaEwLQ87CYSeJSoDRwixf5mvUxkEX31wk&Signature=g3MPAqnI0hLhA%2BuEXMkM41H5Ox4%3D&versionId=CAEQHRiBgMDp0Jn4gxgiIGI4ZmRjNGQwOTM5MDQ4NzQ4YmQxMzJjOTk3MTY3YjNh)

首先我们要知道什么是受控组件什么是非受控组件。  


受控组件与非受控组件的区别：
1. 现用现取的（用的时候通过ref拿）就是非受控组件，随着输入维护状态就是受控组件
2. 受控组件：即通过setState的形式控制输入的值及更新，一般输入框要绑定onChange事件。非受控组件：即通过dom的形式更新值，要获取其值可以通过ref的形式去获取。  

以后在项目中，建议写受控式组件，受控式组件没用ref，非受控组件，有几个输入项，就需要写几个ref

## 1、非受控组件

现用现取的组件叫做非受控组件，非受控组件必须使用ref属性
如下代码就是一个非受控组件
```html
  <!-- 创建容器 -->
    <div id="test"></div>
    <!-- 引入react -->
    <script src = '../../js/react.development.js'></script>
    <!-- 引入react-dom，为了让react操作DOM -->
    <script src = '../../js/react-dom.development.js'></script>
    <!-- 引入babel，为了将jsx转为js -->
    <script src = '../../js/babel.min.js'></script>
    <!-- 引入prop-types，为了做标签属性的限制 -->
    <script src = '../../js/prop-types.js'></script>
    <script type = 'text/babel'>
        //创建一个组件
        class Login extends React.Component{
            render(){
                return (
                    <form action="https://www.atguigu.com" onSubmit = {this.handleSubmit}>
                        用户名：<input ref = {currentNode =>this.username = currentNode} type="text" name = 'username'/>    
                        密码：<input ref={currentNode =>this.password = currentNode} type="password" name = 'password'/>    
                        <button>登录</button>
                    </form>
                )
            }
            //表单提交的回调
            handleSubmit = (event)=>{
                event.preventDefault()//阻止表单提交
                const {username,password} = this;
                alert(`你输入的用户名是：${username.value}，你输入的密码是：${password.value}`);
            }
        }
        //将组件渲染到页面
        ReactDOM.render(<Login/>,document.getElementById('test'));
    </script>
```

## 2、受控组件 

页面中所有输入类的DOM，比如input框就是输入类DOM，随着输入，就把输入的东西维护到状态里去，等状态需要用的时候，就从状态中取出来，这就受控组件：  

如下代码就是有一个非受控组件
```html
    <!-- 创建一个容器 -->
    <div id="test"></div>
    <!-- 引入react核心库 -->
    <script src = '../../js/react.development.js'></script>
    <!-- 引入react-dom，用于让react操作dom -->
    <script src = '../../js/react-dom.development.js'></script>
    <!-- 引入babel，用于将jsx转为js -->
    <script src = '../../js/babel.min.js'></script>
    <!-- 引入prop-types，用于将标签属性做限制 -->
    <script src = '../../js/prop-types.js'></script>
    <script type="text/babel"> 
        class Login extends React.Component{
          //初始化状态
            state = {
                username:'',
                password:''
            }
            render(){
                return (
                    <form action="https://www.atguigu.com" onSubmit={this.handleSubmit}>
                        用户名：<input onChange ={this.saveUsername}  type="text" name='username'/>
                        密码：<input type="text" onChange = {this.savePassword} name='password'/>
                        <button>登录</button>
                    </form>
                )
            }
            //表单提交的回调
            handleSubmit = (event)=>{
                event.preventDefault();
                const {username,password} = this.state;
                alert(`您输入的用户名为：${username}，您输入的密码为：${password}`);
            }
           	//保存用户名到状态中
            saveUsername = (event) =>{
                this.setState({username:event.target.value});
            }
            //保存密码到状态中
            savePassword = ()=>{
                this.setState({password:event.target.value});
            }
        }
        //渲染组件到页面
        ReactDOM.render(<Login/>,document.getElementById('test'));
    </script>
```

## 3、高阶函数和函数柯里化

高阶函数：如果一个函数符合下面两个规范中的任何一个，那该函数就是高阶函数
1. 若A函数，接收的参数是一个函数，那么A就可以称之为高阶函数
2. 若A函数，调用的返回值依然是一个函数，那么A就可以称之为高阶函数
常见的高阶函数：Promise、定时器的回调、arr.map()等等  

函数的柯里化：通过函数调用继续返回函数的方式，实现多次接收参数最后统一处理的函数编码形式。

举例：函数柯里化完成求和案例
```javascript
        function sum(a){
            return (b)=>{
                return (c)=>{
                    return a+b+c;
                }
            }
        }
        let add = sum(1)(2)(3);
        console.log(add);//6
```

使用受控组件+函数柯里化完成案例
```javascript
    <div id="test"></div>
    <script src = '../../js/react.development.js'></script>
    <script src = '../../js/react-dom.development.js'></script>
    <script src = '../../js/babel.min.js'></script>
    <script src = '../../js/prop-types.js'></script>
    <script type = 'text/babel'>
        class Login extends React.Component {
            state = {username:'',password:''};
            handleSubmit = (event)=>{
                // 阻止表单提交
                event.preventDefault();
                const {username,password} = this.state;
                alert(`您输入的用户名是：${username}，您输入的密码是：${password}`);
            }
            saveFormData = (dataType)=>{//使用函数柯里化做优化，将多个函数可以揉为一个函数
                return (event)=>{
                    this.setState({[dataType]:event.target.value});
                }
            }
            render(){
                return (
                    <form action="https://www.baidu.com" onSubmit = {this.handleSubmit}>
                        用户名：<input onChange={this.saveFormData('username')} type="text" name = 'username'/>
                        密码： <input onChange = {this.saveFormData('password')} type="password" name = 'password'/>
                        <button>提交</button>
                    </form>
                )
            }
        }
        //渲染页面
        ReactDOM.render(<Login/>,document.getElementById('test'));
    </script>
```

说明：
![函数柯里化](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/%E5%87%BD%E6%95%B0%E6%9F%AF%E9%87%8C%E5%8C%96.png?Expires=1651386438&OSSAccessKeyId=TMP.3KfNT7MvcaB4FbDQtrM23vHkbL6b6qKp9wu5zKiaafStZnPhoeKzksLjhMM6hzaEwLQ87CYSeJSoDRwixf5mvUxkEX31wk&Signature=Q0JRedRBCSO6prAQ1AiH%2BznCZRs%3D&versionId=CAEQHRiBgMC6uaz4gxgiIDcwM2FkYzQzNzg2ZDQ0OTQ4OTg3OTIzNDhhOGRlN2Vm)

上述代码这部分使用了函数柯里化做了优化，原本是为两个输入框的onChange事件分别绑定saveUsername事件和savePassword属性。但使用了函数柯里化之后，为两个输入框仅绑定一个saveFormData事件，但是能分别处理传入的不同数据。
之前说事件回调函数中不能传递数据，但是这里传了，是因为将数据传递至saveFormData()函数中，而saveFormData()函数返回值是一个函数，所以这个返回的函数作为onChange的回调函数，所以event参数也是传递给这个saveFormData返回值函数的。这种设计非常巧妙。因此标签中的事件回调函数加不加()是看有没有函数柯里化这种情况。

` this.setState({[dataType]:event.target.value});`这条语句中的[dataType]，是获取对象属性的另一种方式，不要感觉陌生。

### 4、不使用函数柯里化完成和使用柯里化一样效果

综合以上分析，只要是给onClick传递一个没有被执行过的函数对象就行，那么我们直接在行内传给它一个没有执行过的过的函数对象就行了`onChange = {event=>this.saveFormData('username',event)}`，使用这种箭头函数的方式，默认返回一个函数对象给onChange作为回调，这个函数对象是saveFormData，定义在外边，所以每次触发事件回调的时候，直接执行这个saveFormData()函数就行了
