# 一、引出生命周期

为了引出生命周期的概念，完成这个案例。  

要求：
> 1. 让指定的文本做显示/隐藏的渐变动画
> 2. 从完全可见，到彻底消失，耗时2s
> 3. 点击不活了，按钮从界面中卸载组件

效果图：  

![引出组件生命周期](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/%E5%BC%95%E5%87%BA%E7%BB%84%E4%BB%B6%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F.gif?Expires=1651418148&OSSAccessKeyId=TMP.3KgvhCFZZSmzq5QQq3ryaCqkAXrRyugLy9JNicBndPn1Rdbato2Sdy4aYTQvxWZyxxgeUxHWajQyC7ZhxaMaTacRBSHzT3&Signature=u55UBCRlXzFBMk01v8WrKxCmTDA%3D&versionId=CAEQHRiBgMCmxp75gxgiIDEyYTUwMGY4ZDljNTRkN2FiY2I1MGEzZjM1OTkxZmNk)

## 1、对生命周期的简单理解

组件从创建到死亡它会经历一些特定的阶段  

React组件从中包含一系列钩子函数（生命周期回调函数），会在特定的时刻调用。
我们在定义组件时，会在特定的生命周期回调函数中，做特定的工作。  

两个名词要了解：挂载和卸载
1. 挂载：将组件渲染到页面，我们以后都叫挂载`ReactDOM.render()`方法就是挂载
2. 卸载，将组件从页面中移出，叫做卸载。react给我们提供了一个卸载的方法`React.unComponentAtNode()`，用法和挂载一样。

## 2、实现案例，引出生命周期

```html
    <!-- 创建一个容器 -->
    <div id="test"></div>
    <!-- 引入react核心库 -->
    <script src = '../../js/react.development.js'></script>
    <!-- 引入react-dom，用于让react操作DOM -->
    <script src = '../../js/react-dom.development.js'></script>
    <!-- 引入babel，为了将jsx转为js -->
    <script src = '../../js/babel.min.js'></script>
    <!-- 引入prop-types，用于做标签属性类型和必要性以及默认值的限制 -->
    <script src = '../../js/prop-types.js'></script>
    <script type = 'text/babel'>
        // 创建类式组件
        class Life extends React.Component{
            state = {opacity:1};
            //点击按钮出发的函数
            death = ()=>{
                //卸载组件
                ReactDOM.unmountComponentAtNode(document.getElementById('test'));
            }
            //组件完成挂载，加载定时器，触发页面加载时的动画效果
            componentDidMount(){
                this.timer = setInterval(()=>{
                    let {opacity} = this.state;
                    opacity-=0.1;
                    if(opacity<=0){
                        opacity = 1;
                    }
                    this.setState({opacity});
                },100)
            }
            render(){
                const {opacity} = this.state;
                return(
                    <div>
                        <h1 style = {{opacity:opacity}}>React学不会怎么办？</h1>
                        <button onClick = {this.death}>不活了</button>
                        </div>
                )
            }
            // 组件将要卸载,清除定时器
            componentWillUnmount(){
                clearInterval(this.timer);
            }
        }
        //将组件渲染到页面
        ReactDOM.render(<Life/>,document.getElementById('test'));
    </script>
```

说明：
在案例的实现过程中，我们不能在render()函数中定义定时器。一旦定义在render中，就会频繁触发render()方法和定时器回调函数，导致效果执行的越来越频繁，这是因为这样做引发了一个无限的递归。render是在第一次挂载的时候调用的，只要修改了状态,render会再次调用，而定时器中恰好修改了state，因此这个render的调用次数会成指数级增长，导致系统负荷过载。

为解决这样的问题，react提供了一系列的生命周期方法（钩子方法），举例如：
1. `componentDidMount`方法，只要组件挂载到页面上就去调用这个方法。且这个方法只会执行一次。这个方法和render一样，是通过组件实例.的方式调用的。
2. react除了提供了`componentDidMount`方法，还提供了像`componentWillUnMount`等方法。都和render一样通过组件实例.的方式调用。  

经上述案例，总结如下：
`render`调用的时机是：初始化渲染、状态更新之后。  
`componentDidMount`调用的时机是：组件挂载完毕时调用。  
`componentWillUnMount`调用的时机是组件将要卸载时调用。  

理解：
组件的一生也好比人的一生
```shell
人  将要出生====》起名字                  组件
    出生了=====》婴儿用品   =======> `componentDidMount`
    会说话了====》记录一下
    会走路了====》记录一下
    上小学了====》记录一下
    病危了======》交代后事  ========》`componentWillUnmount`
```
组件的生命周期其实就像人的一生，在关键的时间点，帮你去调用一些函数，让你在这个函数里面，完成一些特殊的事情  

生命周期标准来讲叫做【生命周期回调函数】，也叫【生命周期钩子函数】【生命周期钩子】，这些都是一个说法。

# 二、生命周期（旧）

为了分析完整的生命周期流程，将借助一个案例完成整个分析

效果图：

![生命周期流程案例](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E6%B5%81%E7%A8%8B%E5%88%86%E6%9E%90%E6%A1%88%E4%BE%8B.gif?Expires=1651418193&OSSAccessKeyId=TMP.3KgvhCFZZSmzq5QQq3ryaCqkAXrRyugLy9JNicBndPn1Rdbato2Sdy4aYTQvxWZyxxgeUxHWajQyC7ZhxaMaTacRBSHzT3&Signature=B8%2Brp25bNPCwnaa8ZSiL%2F8xw3Jg%3D&versionId=CAEQHRiBgMDK1PP_gxgiIDI1MzhhMTE2NzBhZjQwZGI5Yjc2ZGE2MDIwNDU0MDRj)


## 1、生命周期流程图（旧）

![生命周期流程图](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/%E7%BB%84%E4%BB%B6%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E6%B5%81%E7%A8%8B%E5%9B%BE.png?Expires=1651418227&OSSAccessKeyId=TMP.3KgvhCFZZSmzq5QQq3ryaCqkAXrRyugLy9JNicBndPn1Rdbato2Sdy4aYTQvxWZyxxgeUxHWajQyC7ZhxaMaTacRBSHzT3&Signature=Jwg3E1LFUYDuPCOg7Jb9vwwEtwg%3D&versionId=CAEQHRiBgID50vP_gxgiIDc1NjRjOTJiYjhhMTRlMTQ4ZDkxZjU3MmNjYTUwZWFj)

下下面将从旧的生命周期流程这四条路线进行分析

![生命周期流程案例划分](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/%E7%BB%84%E4%BB%B6%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E6%B5%81%E7%A8%8B%E5%9B%BE%E5%88%92%E5%88%86.png?Expires=1651418243&OSSAccessKeyId=TMP.3KgvhCFZZSmzq5QQq3ryaCqkAXrRyugLy9JNicBndPn1Rdbato2Sdy4aYTQvxWZyxxgeUxHWajQyC7ZhxaMaTacRBSHzT3&Signature=v0rzgogZgwEPeBvt15sDZv2bGCw%3D&versionId=CAEQHRiBgICF0_P_gxgiIGMyOTMxOWQ5MjdhMzQ2ZWU4NTA3NDYxMGFlMmFmNDgy)


## 2、生命周期（旧）组件挂载流程

为了验证生命周期流程图中第一条线的情况，通过下列代码示例进行检验：组件挂载流程。
```javascript
class Count extends React.Component {

            constructor(props){
                super(props);
                this.state = {count:0}//由于使用了构造器，所以先把state定义在构造器中
                console.log('Count---constructor---组件第一次挂载我第一个执行')
            }
            //组件将要挂载的钩子
            componentWillMount(){
                console.log('Count---componentWillMount---组件挂载之前就执行')
            }
            add = ()=>{
                const {count} = this.state;
                this.setState({count:count+1})
            }
            death = ()=>{
                ReactDOM.unmountComponentAtNode(document.getElementById('test'));
            }
            //组件挂载
            render() {
                console.log('Count---render---组件挂载时我执行');
                const {count} = this.state;
                return (
                    <div>
                        <h1>当前求和为：{count}</h1>
                        <button onClick = {this.add}>点我+1</button>
                        <button onClick = {this.death}>卸载组件</button>
                    </div>
                )
                
            }
            //组件挂载完要加载的钩子
            componentDidMount(){
                console.log('Count---componentDidMount---组件挂载完之后我执行');
            }
            //组件将要卸载的钩子
            componentWillUnmount(){
                console.log('操作---------------点击了卸载组件按钮');
                console.log('Count---componentWillUnmount---组件将要卸载时执行');

            }
            
        }
        ReactDOM.render(<Count />, document.getElementById('test'));
```

验证结果：
![组件挂载时流程](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/%E7%BB%84%E4%BB%B6%E6%8C%82%E8%BD%BD%E6%B5%81%E7%A8%8B%E7%9A%84%E6%89%A7%E8%A1%8C%E7%BB%93%E6%9E%9C.png?Expires=1651418275&OSSAccessKeyId=TMP.3KgvhCFZZSmzq5QQq3ryaCqkAXrRyugLy9JNicBndPn1Rdbato2Sdy4aYTQvxWZyxxgeUxHWajQyC7ZhxaMaTacRBSHzT3&Signature=PLxPRZ6odqiY0Sp%2Ftje57wWO2lQ%3D&versionId=CAEQHRiBgMCC0vP_gxgiIDFkOGY2YmNhODZkNjRjZmRiMTFiOTU2ZTQyNTQwMmM0)

## 3、生命周期（旧）setState流程

提前说明：
`shouldComponentUpdate()`这个方法的意思是：组件是否应该被更新，相当于一个阀门。这个钩子如果不写，底层也会给你补一个，而且补的那个钩子默认返回true。如果自己写了这个方法，就必须亲自写一个返回值，返回值必须是布尔值。布尔值为真，阀门开启，可以继续向下执行。布尔值为假，阀门关闭不可以向下走。  


验证生命周期流程的第二条线：setState流程
```javascript
class Count extends React.Component {

            constructor(props){
                super(props);
                this.state = {count:0}//由于使用了构造器，所以先把state定义在构造器中
                console.log('Count---constructor---组件第一次挂载我第一个执行')
            }
            //组件将要挂载的钩子
            componentWillMount(){
                console.log('Count---componentWillMount---组件挂载之前就执行')
            }
            add = ()=>{
                const {count} = this.state;
                this.setState({count:count+1})
            }
            death = ()=>{
                ReactDOM.unmountComponentAtNode(document.getElementById('test'));
            }
            //控制组件更新的阀门
            shouldComponentUpdate(){
                console.log('操作-----------------------------------------------更新操作');
                console.log('Count---shouldComponentUpdate---组件更新时先执行我，如果我是true，可以继续向下执行，如果我是false，呵呵呵---很幸运我今天是true');
                return true;
            }
            //组件将要更新的钩子
            componentWillUpdate(){
                console.log('Count---componentWillUpdate---组件将要更新之前我执行');
            }
            //组件完成更新的钩子
            componentDidUpdate(){
                console.log('Count---componentDidUpdate---组件更新完成时我执行');
            }
            //组件挂载
            render() {
                console.log('Count---render---组件挂载时(或者更新时)我执行');
                const {count} = this.state;
                return (
                    <div>
                        <h1>当前求和为：{count}</h1>
                        <button onClick = {this.add}>点我+1</button>
                        <button onClick = {this.death}>卸载组件</button>
                    </div>
                )
                
            }
            //组件挂载完要加载的钩子
            componentDidMount(){
                console.log('Count---componentDidMount---组件挂载完之后我执行');
            }
            //组件将要卸载的钩子
            componentWillUnmount(){
                console.log('操作-------------------------------------------------点击了卸载组件按钮');
                console.log('Count---componentWillUnmount---组件卸载之前我执行');
            }
            
        }
        ReactDOM.render(<Count />, document.getElementById('test'));
```
验证结果：
![组件setState流程](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/%E7%BB%84%E4%BB%B6setState%E6%B5%81%E7%A8%8B.png?Expires=1651418292&OSSAccessKeyId=TMP.3KgvhCFZZSmzq5QQq3ryaCqkAXrRyugLy9JNicBndPn1Rdbato2Sdy4aYTQvxWZyxxgeUxHWajQyC7ZhxaMaTacRBSHzT3&Signature=n%2Bc7SBs%2FtpLUJBYkSklOnFSQuN8%3D&versionId=CAEQHRiBgIDv0vP_gxgiIDc1ZmJiMGM2Mjk1YTQ0MmY4NzZjNTNhMzkyYjA2YWZk)

## 4、生命周期（旧）forceUpdate流程

首先要明确的是什么是强制更新？：
- 强制更新就是对状态里的属性不做任何更改的情况下进行更新。

其次要知道如何强制更新？
- 像使用`setState()`一样使用`forceUpdate()`进行强制更新

那么我们继续使用如下代码验证生命周期流程的第三条线：forceUpdate流程
```javascript
        class Count extends React.Component {

            constructor(props){
                super(props);
                this.state = {count:0}//由于使用了构造器，所以先把state定义在构造器中
                console.log('Count---constructor---组件第一次挂载我第一个执行')
            }
            //组件将要挂载的钩子
            componentWillMount(){
                console.log('Count---componentWillMount---组件挂载之前就执行')
            }
            add = ()=>{
                const {count} = this.state;
                this.setState({count:count+1})
            }
            death = ()=>{
                ReactDOM.unmountComponentAtNode(document.getElementById('test'));
            }
            force = ()=>{
                console.log('操作-----------------------------------------------强制更新');
                this.forceUpdate();
            }
            //控制组件更新的阀门
            shouldComponentUpdate(){
                console.log('操作-----------------------------------------------更新操作');
                console.log('Count---shouldComponentUpdate---组件更新时先执行我，如果我是true，可以继续向下执行，如果我是false，呵呵呵---很幸运我今天是true');
                return true;
            }
            //组件将要更新的钩子
            componentWillUpdate(){
                console.log('Count---componentWillUpdate---组件将要更新之前我执行');
            }
            //组件完成更新的钩子
            componentDidUpdate(){
                console.log('Count---componentDidUpdate---组件更新完成时我执行');
            }
            //组件挂载
            render() {
                console.log('Count---render---组件挂载时(或者更新时)我执行');
                const {count} = this.state;
                return (
                    <div>
                        <h1>当前求和为：{count}</h1>
                        <button onClick = {this.add}>点我+1</button>
                        <button onClick = {this.death}>卸载组件</button>
                        <button onClick = {this.force}>强制更新</button>
                    </div>
                )
                
            }
            //组件挂载完要加载的钩子
            componentDidMount(){
                console.log('Count---componentDidMount---组件挂载完之后我执行');
            }
            //组件将要卸载的钩子
            componentWillUnmount(){
                console.log('操作-------------------------------------------------点击了卸载组件按钮');
                console.log('Count---componentWillUnmount---组件卸载之前我执行');

            }
            
        }
        ReactDOM.render(<Count />, document.getElementById('test'));
```

验证结果：  
![组件forceUpdate流程](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/%E7%BB%84%E4%BB%B6forceUpdate%E6%B5%81%E7%A8%8B.png?Expires=1651418308&OSSAccessKeyId=TMP.3KgvhCFZZSmzq5QQq3ryaCqkAXrRyugLy9JNicBndPn1Rdbato2Sdy4aYTQvxWZyxxgeUxHWajQyC7ZhxaMaTacRBSHzT3&Signature=LaooK74CZraqRdfGjMxtM%2FQCzV0%3D&versionId=CAEQHRiBgMDH0vP_gxgiIDc1ODAzOGEwY2VmODRhOGI4ZGI2ZmM1NDQ1Yzg2NzE5)

## 5、生命周期（旧）父组件render流程 

第一次听说过父组件。既然有父组件就一定有子组件。为了能更好的理解组件之间的父子关系，下面通过一个关于父子组件的案例来了解父组件render的流程。这里就不再参照上述案例来验证父组件的render流程了。

提前说明：  
`componentWillReceiveProps()`这个钩子的意思是：组件将要接收新的props钩子，这个钩子有一个坑，父组件第一次渲染，子组件第一次接收属性是不执行的。之后更新接收新的值才会执行。

先看案例效果：  
![关于父子组件的案例]()

代码示例：
```javascript
 //定义一个父组件
        class A extends React.Component{
            state = {carName : '奔驰'};
            changeCar = ()=>{
                const {carName} = this.state;
                this.setState({carName:'本田'});
                console.log(`操作------------------------------------------父组件第2次render，第一次render为页面加载`);
            }  
            render(){
                const {carName} = this.state;  
                return(
                    <div>
                        <div>我是A组件（父组件）</div>    
                        <button onClick = {this.changeCar}>换车</button>
                        {/*在A中调用B组件，A是父组件，B是子组件。并且可以把A中的状态传递给子组件*/}
                        <B carName= {carName}/>
                    </div>
                )
            }
        }
        // 定义一个子组件
        class B extends React.Component{
            //组件将要接收新的props钩子
            componentWillReceiveProps(props){
                console.log('B---componentWillReceiveProps---在父组件A首次渲染页面的时候，虽然传递过来了参数，但是我是不会执行的，只有之后传递来新的参数，我才会执行。');
            }
            //控制组件更新的阀门
            shouldComponentUpdate(){
                console.log('B---shouldComponentUpdate---组件更新时先执行我，如果我是true，可以继续向下执行，如果我是false，呵呵呵---很幸运我今天是true')
                return true;
            }
            //组件将要更新的钩子
            componentWillUpdate(){
                console.log('B---componentWillUpdate---组件更新时我执行');
            }
            death= ()=>{
                console.log('操作--------------------------------------------------------卸载组件');
                //卸载组件
                ReactDOM.unmountComponentAtNode(document.getElementById('test'));
            }
            render(){
                return(
                    <div>
                        {/*用props接收父组件传递过来的值属性*/}
                        <div>我是B组件（子组件），我接受到的车是：{this.props.carName}</div>
                        <button onClick= {this.death}>卸载组件</button>    
                    </div>
                )
            }
            //组件更新完毕的钩子
            componentDidUpdate(){
                console.log('B---componentDidUpdate---组件更新完我执行');
            }
            //组件将要卸载
            componentWillUnmount(){
                console.log('B---componentWillUnMount---组件卸载时我执行');
            }
        }
        // 挂载父组件
        ReactDOM.render(<A/>,document.getElementById('test'));
```

验证结果：
![父组件render流程]()



## 6、生命周期总结（旧）
生命周期的三个阶段

1. 初始化阶段：由ReactDOM.render()触发---初次渲染
> - `constructor()`
> - `componentWillMount()`
> - `render()`
> - **`componentDidMount()`** ======>常用,一般在这个钩子做一些初始化的事，例如：开启定时器、发送网络请求、订阅消息

2. 更新阶段：有组件内部this.setState()或父组件重新render触发
> - `shouldComponentUpdate()`
> - `componentWillUpdate()`
> - **`render()`** =================>必须用的一个
> - `componentDidUpdate()`

3. 卸载组件：由ReactDOM.unmountComponentAtNode()触发
- **`componentWillUnmount()`**========>常用,一般在这个钩子中做一些收尾的事，例如：关闭定时器、取消订阅消息
# 三、生命周期（新）

## 1、新版本生命周期图

![新版本生命周期图](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/%E6%96%B0%E7%89%88%E6%9C%AC%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E5%9B%BE.png?Expires=1651418329&OSSAccessKeyId=TMP.3KgvhCFZZSmzq5QQq3ryaCqkAXrRyugLy9JNicBndPn1Rdbato2Sdy4aYTQvxWZyxxgeUxHWajQyC7ZhxaMaTacRBSHzT3&Signature=BYwrQnLAH5AC1eTo3qYW7L90VDw%3D&versionId=CAEQHRiBgMDV1vP_gxgiIGM5YWY3YjI1NmVlNDQ1MmU4NGY2ZWM1ZjUyMWRlYzJi)

## 2、新旧版本生命周期对比

在react17版本中用下面旧版本的三个钩子会出现警告,在react18版本中直接旧废弃掉了。
1. `componentWillMount`，
2. `componentWillReceiveProps`，
3. `componentWillUpdate`

这是为什么呢？官方的解释是这样的：
因为这些生命周期方法经常被误解和滥用；在react将来的版本中，可能推出异步渲染的特性，在一部渲染中，这些钩子潜在的误用问题可能更大。所以，react在新版本中为这些生命周期添加`UNSAFE_`前缀。（这里的UNSAFE_不是指安全性，而是表示使用这些生命周期的代码在React未来版本中更有可能出现bug，尤其是在启用异步渲染之后）  

总之：新的生命周期和旧的生命周期相比废弃了三个钩子`componentWillMount`，`componentWillReceiveProps`，`componentWillUpdate`。新增了两个钩子`getDerivedStateFromProps`，`getSnapshotBeforeUpdate`

## 3、新版本生命周期的挂载流程

提前说明：
在新版本的挂载流程中，发现新增了一个钩子。那么接下来我们说说这个钩子有什么用处。  

`getDerivedStateFromProps`：字面上理解是从props获取派生的state。这个方法有如下几个特点：
1. 这个方法必须是静态的
2. 这个方法必须有返回值：可以返回一个状态对象，也可以返回一个null。
3. 这个方法可以接受两个参数：state和props  

什么情况下会使用这个钩子呢？
在一般开发中，使用这个钩子的情况是非常罕见的，所以一般不用。只有在state值在任何时候都取决于props，才可以使用。派生状态会导致代码冗余，并使组件难以维护。

由于在新版本中三个生命周期钩子将被废弃，所以在代码中就不体现这三个钩子了。

下面通过代码验证新版本生命周期的挂载流程
```javascript
        class Count extends React.Component {

            constructor(props){
                super(props);
                this.state = {count:0}//由于使用了构造器，所以先把state定义在构造器中
                console.log('Count---constructor---组件第一次挂载我第一个执行')
            }
            //若state的值在任何时候都取决于props,那么可以使用。
            static getDerivedStateFromProps(props,state){
                console.log('Count---getDerivedStateFromProps---组件挂载前我执行');
                console.log(props,state);
                return null;
            }
            add = ()=>{
                const {count} = this.state;
                this.setState({count:count+1})
            }
            death = ()=>{
                ReactDOM.unmountComponentAtNode(document.getElementById('test'));
            }
            //组件挂载
            render() {
                console.log('Count---render---组件挂载时我执行');
                const {count} = this.state;
                return (
                    <div>
                        <h1>当前求和为：{count}</h1>
                        <button onClick = {this.add}>点我+1</button>
                        <button onClick = {this.death}>卸载组件</button>
                    </div>
                )  
            }
            //组件挂载完要加载的钩子
            componentDidMount(){
                console.log('Count---componentDidMount---组件挂载完之后我执行');
            }
            //组件将要卸载的钩子
            componentWillUnmount(){
                console.log('操作---------------点击了卸载组件按钮');
                console.log('Count---componentWillUnmount---组件将要卸载时执行');
            }   
        }
        ReactDOM.render(<Count />, document.getElementById('test'));
```

验证结果：
![新版本生命周期挂载流程](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/%E6%96%B0%E7%89%88%E6%9C%AC%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E6%8C%82%E8%BD%BD%E6%B5%81%E7%A8%8B.png?Expires=1651418346&OSSAccessKeyId=TMP.3KgvhCFZZSmzq5QQq3ryaCqkAXrRyugLy9JNicBndPn1Rdbato2Sdy4aYTQvxWZyxxgeUxHWajQyC7ZhxaMaTacRBSHzT3&Signature=98hUaP45MN%2BpoVZBJNbLGbptLOo%3D&versionId=CAEQHRiBgMC91PP_gxgiIDQ2YmU1YmY5NmRlODRkNTI4MjkwNGQzZTgwZDU4YmM1)

## 4、新版本生命周期更新流程

提前说明：
新版本生命周期更新流程又新增了一个钩子，`getSnapshotBeforeUpdate`这个钩子相对于鸡肋的`getDerivedStateFromProps`来说，意义更大一些。

`getSnapshotBeforeUpdate`，从字面上理解是更新之前获取快照，这个钩子有如下特点：
1. 必须有返回值，返回值可以是`null`，也可以是一个快照对象，什么是快照对象呢？就是页面在更新之前的某个特征：比如说：页面更新前滚轮的位置、容器的高度，颜色，等等诸如此类。
2. 可接受props和state作为参数（顺序不可变）。也就是说更新前可以将props参数和state参数作为快照对象返回
3. 返回值可以作为`componentDidUpdate`的第三个参数，交由`componentDidUpdate`处理。此外，`componentDidUpdate`的前两个参数可以是preProps和preState(顺序不可变)，即更新前的state和props

`getSnapshotBeforeUpdate`在开发中也是基本用不到，了解即可

下面通过代码验证新版本生命周期的挂载流程：
```javascript
        class Count extends React.Component {

            constructor(props){
                super(props);
                this.state = {count:0}//由于使用了构造器，所以先把state定义在构造器中
                console.log('Count---constructor---组件第一次挂载我第一个执行')
            }
            //若state的值在任何时候都取决于props,那么可以使用。
            static getDerivedStateFromProps(props,state){
                console.log('操作-----------------------------------------更新组件,第一次更新是页面加载，不是手动更新');
                console.log('Count---getDerivedStateFromProps---组件挂载前我执行');
                // console.log(props,state);
                return null;
            }
            add = ()=>{
                const {count} = this.state;
                this.setState({count:count+1})
            }
            death = ()=>{
                ReactDOM.unmountComponentAtNode(document.getElementById('test'));
            }
            //组件挂载
            render() {
                console.log('Count---render---组件挂载时我执行');
                const {count} = this.state;
                return (
                    <div>
                        <h1>当前求和为：{count}</h1>
                        <button onClick = {this.add}>点我+1</button>
                        <button onClick = {this.death}>卸载组件</button>
                    </div>
                )
                
            }
            //获取更新之前的快照
            getSnapshotBeforeUpdate(props,state){
                console.log('Count---getSnapshotBeforeUpdate---在页面更新完成前我执行');
                console.log(props,state);
                return 'atguigu';
            }
            //组件更新完要加载的钩子
            componentDidUpdate(preProps,preState,snapshotValue){
                console.log('Count---componentDidMount---组件挂载完之后我执行');
                console.log(preProps,preState,snapshotValue);
            }
            //组件将要卸载的钩子
            componentWillUnmount(){
                console.log('操作---------------点击了卸载组件按钮');
                console.log('Count---componentWillUnmount---组件将要卸载时执行');

            }  
        }
        ReactDOM.render(<Count count={199}/>, document.getElementById('test'));
```

验证结果：
![新版本生命周期更新流程](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/%E6%96%B0%E7%89%88%E6%9C%AC%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E6%9B%B4%E6%96%B0%E6%B5%81%E7%A8%8B.png?Expires=1651418368&OSSAccessKeyId=TMP.3KgvhCFZZSmzq5QQq3ryaCqkAXrRyugLy9JNicBndPn1Rdbato2Sdy4aYTQvxWZyxxgeUxHWajQyC7ZhxaMaTacRBSHzT3&Signature=rIIL65qtVHRNRFLmBFSAZkYq3yw%3D&versionId=CAEQHRiBgMDC1PP_gxgiIDcyYjVlM2YwOWViNzRmMzFiNDA0YzNmOTBmYTBmNGFm)

## 5、`getSnapshotBeforeUpdate`举例

正在更新中......

## 6、总结新版生命周期

1. 初始化阶段：由ReactDOM.render()触发---初次渲染
> - constructor()
> - getDerivedStateFromProps()
> - render()
> - componentDidMount()  

2. 更新阶段：由组件内部this.setState()或父组件重新render触发。
> - getDerivedStateFromProps()
> - shouldComponentUpdate()
> - render()
> - getSnapshotBeforeUpdate()
> - componentDidUpdate()
3. 卸载组件：由ReactDOM.unmountComponentAtNode()触发
> - componentWillUnmount()

