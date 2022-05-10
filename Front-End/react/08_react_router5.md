
# 一、相关理解

## 1、SPA理解

1. 单页Web应用（Single page web application ,SPA）
2. 整个应用只有一个完整的页面
3. 点击页面中的链接不会刷新页面，只会做局部的更新
4. 数据都需要通过ajax请求获取，并在前端异步展现

## 2、对路由的理解

### （1）什么是路由

1. 一个路由就是一个映射关系（key:value）
2. key为路径，value可能是function或component

### （2）路由分类

1. 后端路由
> 理解：value是function，用来处理客户端提交的请求
> 注册路由：router.get(path,function(req,res));
> 工作过程：当node接收到一个请求时，根据请求路径找到匹配的路由，调用路由中的函数来处理请求，返回响应数据。
2. 前端路由：
> 浏览器端路由，value是 component，用于展示页面内容
> 注册路由：`<Router path="/test" component = {Test}>`
> 工作过程：当浏览器的path变为/test时，当前路由组件就会变为Test组件

## 3、react-router-dom的理解

1. react的一个插件库
2. 专门用来实现SPA应用
3. 基于react的项目基本都会用到此库

react-router有三种实现，分别给三种平台去用：第一个就是web：网页开发人员，也就是react-router-dom，第二个是native，给写react原生应用的人用的，还有一个是anywhere ：在哪都能用

## 4、react-router-dom相关API
- 内置组件
    - `<BrowserRouter>`
    - `<HashRouter>`
    - `<Route>`
    - `<Redirect>`
    - `<Link>`
    - `<NavLink>`
    - `<Switch>`
- 其他
    - history对象
    - match对象
    - withRouter函数

# 二、路由的基本使用

使用路由完成如下案例

![路由的案例](https://gitee.com/Jeren/cloudimages/raw/master/img/路由的基本使用.gif)

## 1、准备工作

1. 下载`react-router-dom`：`npm i react-router-dom@5`
2. 由于这个案例用到bootstrap.css，所以需要引入
3. class改成className

## 2、实现过程

之前，我们都知道原生html中要靠`<a>`跳转不同的页面

```html
<a className="list-group-item" href="./about.html">About</a>
<a className="list-group-item active" href="./home.html">Home</a>
```

然而在react中要靠路由链接切换组件

### （1）编写路由链接

1. 引入`Link组件`和 `BrowserRouter组件`

`import {Link,BrowserRouter} from 'react-router-dom'`

说明：
`Router`(路由器)分为两种：`BrowserRouter`（对应`History.createBrowserHistory()`，H5推出的history身上的API，用于创建一个history对象）和`HashRouter`（对应`History.createHashHistory()`，类似锚点定位，也是用于创建一个history对象）。如果使用`BrowserRouter`，那么路径中就不会出现“#”号了，如果使用`HashRouter`，路径中就会出现“#”号

2. 使用Link组件代替页面中的`a标签`。并且使用`<BrowserRouter></BrowserRouter>`包裹起来。并且指定to属性，to属性指定的就是路径中的查询字符串
```jsx
             <BrowserRouter>
                <Link class="list-group-item active" to='/about'>About</Link>
                <Link class="list-group-item" to='/home'>Home</Link>
                {/* 使用Link标签to后面的路径不能写成"./home"，一般用小写 */}
              </BrowserRouter>
```

3. 注册路由

引入`Route`组件  

`import { Link, BrowserRouter ,Route} from 'react-router-dom';`

```jsx
                {/* 注册路由 */}
                <BrowserRouter>
                  <Route path='/about' component={About}></Route>
                  <Route path='/home' component={Home}></Route>
                </BrowserRouter>
```
但是这样并不能完成效果，原因在于注册路由和编写路由链接用的是不同的BrowserRouter(路由器)，导致两个路由器之间不能传递信息。

解决办法：在编写路由链接和注册路由时，都不再使用`<BrowserRouter>`，而是将`<BrowserRouter>`组件用在index.jsx中包裹App组件，同时不要忘记在index.jsx中引入`BrowserRouter`组件

最终代码：

```js
//src/index.js
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter } from 'react-router-dom';

import APP from './App';
ReactDOM.render(
<BrowserRouter>
    <APP/>
</BrowserRouter>
,document.getElementById('root'));
```

```jsx
//src/App.jsx
import React, { Component } from 'react'
import { Link, BrowserRouter ,Route} from 'react-router-dom';
import Home from './pages/Home'
import About from './pages/About'
export default class App extends Component {
  render() {
    return (
      <div>
        <div class="row">
          <div class="col-xs-offset-2 col-xs-8">
            <div class="page-header"><h2>React Router Demo</h2></div>
          </div>
        </div>
        <div class="row">
          <div class="col-xs-2 col-xs-offset-2">
            <div class="list-group">
              {/* <a class="list-group-item active" href="./about.html">About</a>
              <a class="list-group-item" href="./home.html">Home</a> */}
              {/* 编写路由链接 */}
                <Link class="list-group-item active" to='/about'>About</Link>
                <Link class="list-group-item" to='/home'>Home</Link>
                {/* 使用Link标签to后面的路径不能写成"./home"，一般用小写 */}

            </div>
          </div>
          <div class="col-xs-6">
            <div class="panel">
              <div class="panel-body">
                {/* 注册路由 */}
                  <Route path='/about' component={About}></Route>
                  <Route path='/home' component={Home}></Route>
              </div>
            </div>
          </div>
        </div>
      </div>
    )
  }
}

```

## 3、路由基本使用小总结

1. 明确好界面中的导航区、展示区
2. 导航区的a标签改为Link标签
`<Link to='/xxxxx'>Demo</Link>`
3. 展示区写Route标签进行路径的匹配
4. `<App/>`的最外侧包裹一个`<BrowserRouter>`或`<HashRouter>`

# 三、路由组件与基本组件的区别
1. 写法不同
>- 一般组件：`<Demo/>`
>- 路由组件：`<Route path="/about" component={About}></Route>`

2. 存放位置不同
>一般组件：components
>路由组件:pages
3. 接收到的props不同
> 一般组件：写组件标签时传递了什么，就能收到什么
> 路由组件：接收到三个固定的属性
> - history:
>   - go: ƒ go(n)
>   - goBack: ƒ goBack()
>   - goForward: ƒ goForward()
>   - push: ƒ push(path, state)
>   - replace: ƒ replace(path, state)
>  - location:
>    - pathname: "/about"
>    - search: ""
>    - state: undefined
>  - match:
>    - params: {}
>    - path: "/about"
>    - url: "/about"

# 四、NavLink的基本使用

NavLink可代替Link实现路由链接高亮的效果  

需要引入NavLink组件 `import { NavLink, Route } from 'react-router-dom'`

代码演示：
```html
<NavLink activeClassName='demo' class ='list-group-item' to='/about'>About</NavLink>
<NavLink activeClassName='demo' class ='list-group-item a' to='/home'>Home</NavLink>
```

实现原理：

使用`<NavLink>`组件就意味着，点谁就给谁加了一个名为：active的class
而且`<NavLink>`组件 可以多传递一个属性 ，这个属性的名字就叫做`activeClassName`，就是当你点击NavLink的时候，加哪个类的类名，不写这个属性，默认就是，就默认指定为active。

例如：

```css
/*demo样式，定义在public/index.html中*/
.demo{
        background-color: orange!important;
        color:brown!important;
      }
```

```jsx
{/* 编写路由链接 */}
{/* 使用NavLink，activeClassDemo指定要用的高亮样式，定义在src/App.js */}
<NavLink activeClassName='demo' className ='list-group-item' to='/about'>About</NavLink>
<NavLink activeClassName='demo' className ='list-group-item a' to='/home'>Home</NavLink>
```
这样就实现了点击高亮的效果。
![点击路由组件高亮效果](https://gitee.com/Jeren/cloudimages/raw/master/img/路由高亮.png)

# 五、封装NavLink组件

先看封装代码吧：

```jsx
//定义在src/components/MyNavLink中,封装了NavLink
import React, { Component } from 'react'
import {NavLink} from 'react-router-dom';
export default class MyNavLink extends Component {
  render() {
    return (
        <NavLink activeClassName='demo' className="list-group-item" {...this.props}/>
    )
  }
}
```

```jsx
//MyNavLink的使用，写在App.jsx
<MyNavLink to="/home" children= 'Home'/>
<MyNavLink to="/About" children= 'About'/>
```

说明：
**标签体内容是一个特殊的标签属性**
1. `<MyNavLink to="/About">About</MyNavLink>`  

当写这种标签的时候，props中会有一个children属性，children属性的value就是标签体的内容，在这条语句中，标签体内容就是About。这样接收者就会通过`props.childrens`中拿到`children`属性

2. `<MyNavLink to="/home" children= 'Home'/>`

当写自闭和标签的时候，我们可以自己指定标签体内容，就是通过传递children属性，接收者就会自动在props属性中找到children属性的内容

## NavLink小总结

1. `NavLink`组件可以实现路由链接的高亮，通过`activeClassName`指定样式名
2. 组件标签体内容是一个特殊的标签属性
3. 通过`this.props.children`可以获取组件标签体内容

# 六、Switch的使用

当我们为同一个路由路径匹配多个组件，哪个会生效呢？比如说，下列代码，同时为/home路径，匹配了两个路由，结果是二者都生效了
```jsx
<Route path="/about" component={About}></Route>
<Route path="/home" component={Home}></Route>
<Route path="/home" component={Test}></Route>
```
![Switch的使用1](https://gitee.com/Jeren/cloudimages/raw/master/img/Switch的使用.png)

那么我们只想让同一个路径匹配的多个组件只生效一个，我们可以使用`Switch`组件  

需要导入`Switch`组件  

`import { Switch, Route } from 'react-router-dom';`

使用Switch

```jsx
                <Switch>
                  <Route path="/about" component={About}></Route>
                  <Route path="/home" component={Home}></Route>
                  <Route path="/home" component={Test}></Route>
                </Switch>

```

这样就只生效一个Home组件了。
![Switch的使用2](https://gitee.com/Jeren/cloudimages/raw/master/img/Switch的使用2.png)

switch小总结：
1. 通常情况下，path和component是一一对应的关系
2. Switch可以提高路由匹配效率（单一匹配）

# 七、解决样式丢失问题

现在我们有一个需求：我们希望在我们编写路由链接的时候前面加上项目或者公司的名称：比如说下面这种形式：

```jsx
{/* 在React中靠路由链接切换组件 */}
<MyNavLink to="avepoint/home" children= 'Home'/>
<MyNavLink to="/avepoint/About" children= 'About'/>
  {/* 注册路由 */}
<Switch>
  <Route path="/avepoint/about" component={About}></Route>
  <Route path="/avepoint/home" component={Home}></Route>
</Switch>
```
这样写第一次进入页面没有什么样式问题，但是刷新之后，样式就会消失了  

![样式丢失问题](https://gitee.com/Jeren/cloudimages/raw/master/img/样式丢失问题.png)

原因是因为在刷新之前样式的加载路径是这样的：`Request URL: http://localhost:3000/css/bootstrap.css`，这个地址是能够成功请求到bootstap的。

刷新之后呢，会发现样式的加载路径是这样的：`Request URL:http://localhost:3000/avepoint/css/bootstrap.css`。会默认为/avepoint也是路径的一部。如果请求了不存在的资源。就会用public/index.html兜底，所以样式会消失，进显示index.html

解决办法有三种

1. 第一种：在public/index.html中，引入样式的时候，把前面的点去掉，如果加.的话，失去当前路径下去找样式文件，这样就把avepoint也带着了，根本就没有这个路径。如果不加.的话失去根路径下找样式文件，就可以找得到

```html
<link rel="stylesheet" href="/css/bootstrap.css">
```

2. 第二种：%PUBLIC_URL%代表的就是public文件夹的根路径

```html
 <link rel="stylesheet" href="%PUBLIC_URL%/css/bootstrap.css">
```

3. 第三种：不去掉引入样式的.，而是修改路由器，使用`<HashRouter>`，不使用`<BrowserRouter>`，因为`<HashRouter>`会把#后的路径看作前端的路径。

第三种方法很少见。

解决多级路径刷新叶念，样式丢失问题的小总结：
三种解决办法要知道。
1. public/index.html中 引入样式时不写 ./写 / （常用）
2. public/index.html中引入样式时不写 ./写`%PUBLIC_URL%`（只在脚手架里这么写）（常用）
3. 使用HashRouter

# 八、路由的模糊匹配与严格匹配

## 1、模糊匹配

匹配失败情况（不是模糊匹配）----->这种情况会匹配失败，要避免这么写

```jsx
//编写路由链接
<MyNavLink to="/home" children= 'Home'/>
//注册路由
<Route path="/home/a/b" component={Home}></Route>
```

模糊匹配，下面这种情况才叫模糊匹配，会匹配成功

```jsx
//编写路由链接
<MyNavLink to="/home/a/b" children= 'Home'/>
//注册路由
<Route path="/home" component={Home}></Route>
```

![模糊匹配](https://gitee.com/Jeren/cloudimages/raw/master/img/模糊匹配.png)
## 2、严格匹配

严格匹配要求编写的路由链接和注册路由的路径需要一模一样
可以通过exact属性开启精准匹配，注册路由时添加`exact ={true}`或者`exact`。

```jsx
{/*编写路由链接*/}
<MyNavLink to="/home/a/b" children= 'Home'/>
<MyNavLink to="/about" children= 'About'/>
{/* 注册路由 */}
<Switch>
 <Route exact = {true} path="/about" component={About}></Route>
 <Route exact path="/home" component={Home}></Route>
</Switch>
```

![严格匹配](https://gitee.com/Jeren/cloudimages/raw/master/img/严格匹配.png)

## 3、模糊匹配与严格匹配小总结

1. 默认使用的是模糊匹配（简单记【输入的路径】必须包含要【匹配的路径】，且顺序要一致）
2. 开启严格匹配：`<Route exact = {true} path="/about" component={About}></Route>`
3. 严格匹配不要随便开启，需要再开，有些时候开启会导致无法继续匹配二级路由

# 九、Redirect的使用

一般写在所有路由注册的最下方，当所有路由都无法匹配时，跳转到Redirect指定的路由

需要引入`Redirect组件`
```jsx
import { Switch, Route ,Redirect} from 'react-router-dom';
```

使用注意：`Redirect`的属性是`to`而不是`path`
```jsx
<Switch>
  <Route path="/about" component={About}></Route>
  <Route path="/home" component={Home}></Route>
  <Redirect to='/home'></Redirect>
</Switch>
```

## 十、嵌套路由的使用

### （1）使用嵌套路由要完成的效果

![嵌套路由的效果](https://gitee.com/Jeren/cloudimages/raw/master/img/嵌套路由的实现案例.gif)

### （2）思路

路由的匹配都是按照注册顺序来的
比如说编写路由链接`<MyNavLink to='/home/news' children='News'></MyNavLink>`，先是去和注册路由时的/home去匹配的，因为，模糊匹配的存在，所以匹配成功了，Home组件成功展示，然后再和/news去匹配，发现/news也注册路由了，匹配成功了，则News组件也成功展示了

### （3）实现过程

在一级路由的基础上进行扩展

在Home组件中新增Message组件和News组件，当点击News链接，跳转到News组件

Message组件代码

```jsx
import React, { Component } from 'react'

export default class Message extends Component {
    render() {
        return (
            <div>
                <ul>
                    <li>
                        <a href="/message1">message001</a>&nbsp;&nbsp;
                    </li>
                    <li>
                        <a href="/message2">message002</a>&nbsp;&nbsp;
                    </li>
                    <li>
                        <a href="/message/3">message003</a>&nbsp;&nbsp;
                    </li>
                </ul>
            </div>
        )
    }
}
```

News组件代码

```jsx
import React, { Component } from 'react'

export default class News extends Component {
    render() {
        return (
            <ul>
                <li>news001</li>
                <li>news002</li>
                <li>news003</li>
            </ul>
        )
    }
}
```

Home组件代码

```jsx
import { Component } from 'react';
import { NavLink,Route,Redirect } from 'react-router-dom';

import News from './News';
import Message from './Message';
export default class Home extends Component {
    render() {
        return (
            <div>
                <h1>我是Home组件中的内容</h1>
                
                <ul class="nav nav-tabs">
                    <li>
                    <NavLink className="list-group-item " to =  '/home/news' >News</NavLink> 
                    </li>
                    <li>
                    <NavLink className="list-group-item " to =  '/home/message' >Message</NavLink>
                    </li>
                </ul>
                <Route path = '/home/news' component={News}></Route>
                <Route path = '/home/message' component={Message}></Route>
                <Redirect to = '/home/news'></Redirect>
            </div>
        )
    }
}
```

# 十一、向路由组件传递参数

通过完成下列案例，向路由组件传递参数，一共有三种传递参数的方式。

若想完成案例需要在`src/pages/Home/Message`文件夹下新建Detail文件夹。

![向路由组件传递参数的案例](https://gitee.com/Jeren/cloudimages/raw/master/img/传递参数的案例.gif)

## 1、向路由组件传递params参数

总共分为3个步骤：
1. 编写路由链接时：向路由组件传递params参数==>以`<Link to = 'home/message/detail/001/消息1'></Link>`这种方式传递params参数
2. 注册路由时：声名接收参数==>以`<Route path = '/home/message/detail/:id/:title' component={Detail}></Route>`这种方式声名接收参数

第一步和第二步在同一个文件中，所以放在一起写

```jsx
//src/pages/Home/Message/index.jsx
import { Component } from 'react';
import { NavLink,Route } from 'react-router-dom';

import Detail from './Detail';
export default class Message extends Component {
    state = {
        messageArr: [
            { id: '001', title: '消息1' },
            { id: '002', title: '消息2' },
            { id: '003', title: '消息3' },
        ]
    }
    render() {
        const { messageArr } = this.state;
        return (
            <div>
                <ul>
                    {
                        messageArr.map(msg => {
                            return<li key={msg.id}>
                                {/* 向路由组件传递params参数 */}
                                <NavLink to={`/home/message/detail/${msg.id}/${msg.title}`}>{msg.title}</NavLink>&nbsp;&nbsp;
                            </li>
                        })
                    }
                </ul>
                {/* 声名接收params参数 */}
                <Route path = '/home/message/detail/:id/:title' component={Detail}></Route>
            </div>
        )
    }
}
```

3. 正式接收==>通过`const {id,title} = this.props.match.params`这种方式正式接收
```jsx
//src/pages/Home/Message/Detail/index.jsx
import {Component} from 'react';

const Detaildata = [
    {id:'001',content : '我爱你中国'},
    {id:'002',content : '我爱你长春'},
    {id:'003',content : '我爱你长沙'},
]
export default class Detail extends Component{
    render(){
        // 接收params参数
        const {id,title} = this.props.match.params;
        const findResult = Detaildata.find((detailObj)=>{
            return detailObj.id === id
        })
        return (
            <ul>
                <li>ID:{id}</li>
                <li>Title:{title}</li>
                <li>Content:{findResult.content}</li>
            </ul>
        )
    }
}
```

params参数小总结：
1. 路由链接（携带参数）：<Link to = '/demo/test/tom/18'>详情</Link>
2. 注册路由（声名接收）：<Route path="demo/test/:nam/:age" component={Test}/>
3. 接收参数：const {id,title} = this.props.match.params

## 2、向路由组件传递search参数

同样，总共分为3步。案例和上述的一样，这里就仅将变化的数据写下来，其余的和上述的一样。

1. 向路由组件传递search参数 ==>以`key=value&key=value`这种方式传递search参数。

```jsx
{/* 向路由组件传递search参数 */}
<NavLink to={`/home/message/detail/?id=${msg.id}&title=${msg.title}`}>{msg.title}</NavLink>&nbsp;&nbsp;
```
2. search参数无需声名接收 ，正常注册路由即可
```jsx
{/* search参数无需声名接收 ，正常注册路由即可*/}
<Route path = '/home/message/detail' component = {Detail}></Route>
```
3. 正式接收search参数==>通过`const search = this.props.location.search`这种方式正式接收参数

此外，这个地方有些特殊，因为传递过来的是urlencoded编码字符串，所以需要处理

- 通过安装一个包：`bom i query-string`，完成将urlencoded转为对象的操作

```jsx
import {Component} from 'react';
import qs from 'query-string';
const Detaildata = [
    {id:'001',content : '我爱你中国'},
    {id:'002',content : '我爱你长春'},
    {id:'003',content : '我爱你长沙'},
]
export default class Detail extends Component{
    render(){
        console.log(this.props);
        // 接收search参数
        const search = this.props.location.search;
        const{id,title} = qs.parse(search.slice(1));
        const findResult = Detaildata.find((detailObj)=>{
            return detailObj.id === id
        })
        return (
            <ul>
                <li>ID:{id}</li>
                <li>Title:{title}</li>
                <li>Content:{findResult.content}</li>
            </ul>
        )
    }
}
```

- 传递比params简单，接收麻烦
- key=value&key=value ===>这叫urlencoded编码
- 小总结：
  - 路由链接（携带参数）：`<Link to='demo/test?name=tom&age=18'>详情</Link>`
  - 注册路由（无需声名，正常注册即可）：`<Route path ='/demo/test' component={Test}/>`
  - 接收参数：`const {search} = this.props.location`
  - 备注：获取到的search是urlencoded编码字符串，需要借助query-string解析，导包`import queryString from 'query-string'`;

## 3、向路由组件中传递state参数

同样，总共分为三步。

1. 向路由组件传递state参数==>以`<Link to={{path:'demo/test'},state:{name:'tom',age:18}}>详情</Link>`这种方式传递state参数
```jsx
{/* 向路由组件传递state参数 */}
<NavLink to={{pathname:'/home/message/detail',state:{id:msg.id,title:msg.title}}}>{msg.title}</NavLink>&nbsp;&nbsp;
```
2. state参数无需声名接收 ，正常注册路由即可
```jsx
{/* search参数无需声名接收 ，正常注册路由即可*/}
<Route path = '/home/message/detail' component = {Detail}></Route>
```
3. 正式接收search参数==>以`const{id,title} = this.props.location.state;`这种方式接收state参数

```jsx
import {Component} from 'react';
const Detaildata = [
    {id:'001',content : '我爱你中国'},
    {id:'002',content : '我爱你长春'},
    {id:'003',content : '我爱你长沙'},
]
export default class Detail extends Component{
    render(){
        console.log(this.props);
        // 接收state参数
        const{id,title} = this.props.location.state;
        const findResult = Detaildata.find((detailObj)=>{
            return detailObj.id === id
        })
        return (
            <ul>
                <li>ID:{id}</li>
                <li>Title:{title}</li>
                <li>Content:{findResult.content}</li>
            </ul>
        )
    }
}
```
向路由中传递state参数小总结：
- 这个state参数不同于组件中的state状态
- 特点：地址栏不显示参数信息
1. 路由链接（携带参数）：<Link to={{path:'demo/test'},state:{name:'tom',age:18}}>详情</Link>
2. 注册路由（无需声名，正常注册即可）：<Route path="/demo/test" component = {Test}>
3. 接收参数：this.props.location.state
4. 备注：当前页面刷新可以保留住参数，强制刷新无法保留参数，可以在接收参数时这么做
```jsx
    //接收state参数
    const {id,title} = this.props.location.state || {};
    const findResult = Detaildata.find((detailObj)=>{
        return detailObj.id === id;
    }) || {};
```

# 十二、路由跳转方式：push方式、replace方式
## 1、push方式