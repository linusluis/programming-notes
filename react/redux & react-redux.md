

# 一、redux

## 1、redux是什么？

1. redux是一个专门用于做状态管理的js库（不是react插件库）

2. 它可以用在react,angular,vue等项目中，但基本与react配合使用

3. 作用：集中式管理,react应用中多个组件共享的状态

## 2、什么情况下需要使用redux

1. 某个组件的状态，需要让其他组件可以随时拿到（共享）

2. 一个组件需要改变另一个组件的状态（通信）

3. 总体原则：能不用就不用，如果不用比较吃力才考虑使用

## 3、redux原理图

![redux原理图](https://gitee.com/Jeren/cloudimages/raw/master/img/redux原理图.png)

## 4、redux的三个概念

### （1）action
1. 动作的对象
2. 包含两个属性
- type：标识属性，值为字符串，唯一，必要属性
- data：数据属性，值类型任意，可选属性
3. 举例：
```jsx
{type:'ADD STUDENT',data:{name:'tom',age:18}}
```

### （2）reducer
1. 用于初始化状态、加工状态
2. 加工时，根据旧的state和action，产生新的state的纯函数
3. 初始化状态时：previousState为undefined，action中的type是`@@init@@`

### （3）store

1. 将state、action、reducer联系在一起的对象

2. 如何得到此对象？
```jsx
import {createStore} from redux;
import reducer from './reducers';
const store = createStore(reducer);
```

3. 此对象的功能？
- getState()：得到state

- dispatch(action)：分发action，当触发reducer调用，产生新的state。

- subscribe(listener)：注册监听，当产生了新的state时，自动调用。

## 5、求和案例_纯react版

后面所有redux的知识都围绕这个求和案例完成

效果图：

![redux案例](https://gitee.com/Jeren/cloudimages/raw/master/img/redux案例.gif)


- `src/index.js`

```js
//src/index.js

import React from 'react';
import ReactDOM from 'react-dom';

import App from './App';
ReactDOM.render(<App/>,document.getElementById('root'));
```

- `src/App.js`

```jsx
//src/App.js
import {Component} from 'react';

import Count from './components/Count';
export default class App extends Component{
    render(){
        return(
            <Count/>
        )
    }
}
```

- `src/components/Count/index.jsx`

```jsx
//src/components/Count/index.jsx
import {Component} from 'react';
export default class App extends Component{
    state = {count:0}
    increment = ()=>{
        const {count} = this.state;
        const value = this.selectNumber.value*1;
        this.setState({count:count+value});          
    }
    decrement = ()=>{
        const {count} = this.state;
        const value = this.selectNumber.value*1;
        this.setState({count:count-value}); 
    }
    incrementIfOdd = ()=>{
        const {count} = this.state;
        const value = this.selectNumber.value*1;
        if(count%2 !== 0){
            this.setState({count:count+value}); 
        }

    }
    incrementAsync = ()=>{
        const {count} = this.state;
        const value = this.selectNumber.value*1;
        setTimeout(()=>{
            this.setState({count:count+value});
        },1000)
    }
    render(){
        const {count} = this.state;
        return (
            <div>
                <h1>{count}</h1>
                <select ref = {(c)=>{this.selectNumber = c}}>
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                </select>
                <button onClick = {this.increment}>+</button>
                <button onClick = {this.decrement}>-</button>
                <button onClick = {this.incrementIfOdd}>奇数+</button>
                <button onClick = {this.incrementAsync}>异步+</button>
            </div>
        )
    }
}
```
## 6、求和案例_redux精简版

第一次使用redux，要安装redux：`npm i redux`；

步骤：
1. 去除Count组件自身的状态。

2. src下建立：
>src/redux/store.js
>src/redux/reducer.js

3. store.js
- 引入redux中的createStore函数，创建一个store
- createStore调用时要传入一个为其服务的reducer
- 记得暴露store对象

4. count_reducer.js
- reducer的本质是一个函数，接收:`preState`，`action `，返回加工后的状态。
- rudecer有两个作用：初始化状态，加工状态
- reducer被第一次调用时，是store自动触发的，传递的preStore是undefined，传递的action是：`{type:'@@REDUX/INIT_a.2.b.4'}`

5. 在index.js中监测store中状态的改变，一旦发生改变重新渲染。
- 使用`store.subscribe()`
- 备注：redux只负责管理状态，至于状态的改变驱动着页面的展示，要靠我们自己写。

代码：
- `src/index.js`

```js
//src/index.js
import React from 'react';
import ReactDOM from 'react-dom';

import store from './redux/store';
import App from './App';
ReactDOM.render(<App/>,document.getElementById('root'));

//store.subscribe()用于检测redux中状态的变化，只要变化，就调用render
store.subscribe(()=>{
    ReactDOM.render(<App/>,document.getElementById('root'));
})
```

- `src/App.jsx`

```js
//src/App.jsx
import {Component} from 'react';

import Count from './components/Count';
export default class App extends Component{
    render(){
        return(
            <Count/>
        )
    }
}
```

- `src/components/Count/index.jsx`

```jsx
//src/components/Count/index.jsx
import React,{Component} from 'react';
//引入store，用于获取redux中保存状态
import store from '../../redux/store';
export default class Count extends Component{
    myRef = React.createRef();
    increment = ()=>{
        const {value} = this.myRef.current;
        //通知redux+value
        store.dispatch({type:'increment',data:value*1});
    }
    decrement = ()=>{
        const {value} = this.myRef.current;
        // 通知redux-value
        store.dispatch({type:'decrement',data:value*1});
    }
    incrementIfOdd = ()=>{
        const count = store.getState();
        if(count%2!==0){
            const {value} = this.myRef.current;
            store.dispatch({type:'increment',data:value*1});
        }
    }
    incrementAsync = ()=>{
        setTimeout(()=>{
            const {value} = this.myRef.current;
            store.dispatch({type:'increment',data:value*1});
        },1000)
    }
    render(){
        const count = store.getState();
        return(
            <div>
                <h1>{count}</h1>
                <select ref = {this.myRef}>
                    <option>1</option>
                    <option>2</option>
                    <option>3</option>
                </select>
                <button onClick = {this.increment}>+</button>
                <button onClick = {this.decrement}>-</button>
                <button onClick = {this.incrementIfOdd}>奇数+</button>
                <button onClick = {this.incrementAsync}>异步+</button>
            </div>
        )
    }
}
```

- `src/redux/store.js`

```js
//src/redux/store.js
//该文件专门用于暴露一个store对象，整个应用只有一个store

//引入createStore，专门用于创建redux中最为核心的store对象
import {createStore} from 'redux';
//引入为Count服务的reducer
import countReducer from './count_reducer';

export default createStore(countReducer);

```

- `src/redux/count_reducer.js`

```js
//src/redux/count_reducer.js
//该文件是用于创建一个为Count组件服务的reducer，reducer的本质就是一个函数
//reducer函数会接到两个参数，分别为：之前的状态（preState），动作对象（action）
const initState = 0;//初始化状态
export default function countReducer(prevState = initState,action){
    //从对象中获取：type、data
    const {type,data} = action;
    // 根据type决定如何加工数据
    switch(type){
        case 'increment'://如果是加
            return prevState + data;
        case 'decrement'://如果是减
            return prevState - data;
        default:
            return prevState;
    }
}
```

## 7、求和案例redux完整版

在精简版的基础上增加了两个文件：
- `count_action.js`：专门用于创建action对象
- `constant.js`：放置容易写错的type值

代码：

- `src/index.js`

```js
//src/index.js
import React from 'react';
import ReactDOM from 'react-dom';

import store from './redux/store';
import App from './App';
ReactDOM.render(<App/>,document.getElementById('root'));

store.subscribe(()=>{
    ReactDOM.render(<App/>,document.getElementById('root'));
})
```

- `src/App.jsx`

```jsx
//src/App.jsx

import {Component} from 'react';

import Count from './components/Count';
export default class App extends Component{
    render(){
        return(
            <Count/>
        )
    }
}
```

- `src/components/Count/index.jsx`

```js
//src/components/Count/index.jsx

import React,{Component} from 'react';

import store from '../../redux/store';
import { createIncrementAction,createDecrementAction } from '../../redux/count_action';
export default class Count extends Component{
    myRef = React.createRef();
    increment = ()=>{
        const {value} = this.myRef.current;
        store.dispatch(createIncrementAction(value*1));
    }
    decrement = ()=>{
        const {value} = this.myRef.current;
        store.dispatch(createDecrementAction(value*1));
    }
    incrementIfOdd = ()=>{
        const count = store.getState();
        if(count % 2 !== 0){
            const {value} = this.myRef.current;
            store.dispatch(createIncrementAction(value*1));
        }
    }
    incrementAsync = ()=>{
        setTimeout(()=>{
            const {value} = this.myRef.current;
        store.dispatch(createIncrementAction(value*1));
        },1000)
    }
    render(){
        const count = store.getState();
        return (
            <div>
                <h1>{count}</h1>
                <select ref = {this.myRef}>
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                </select>
                <button onClick = {this.increment}>+</button>
                <button onClick = {this.decrement}>-</button>
                <button onClick = {this.incrementIfOdd}>奇数+</button>
                <button onClick = {this.incrementAsync}>异步+</button>
            </div>
        )
    }
}
```

- `src/redux/store.js`

```js
//src/redux/store.js
import {createStore} from 'redux';

import countReducer from '../redux/count_reducer';

export default createStore(countReducer);
```

- `src/redux/contant.js`

```js
//src/redux/contant.js
// 该模块是用于定义action对象中type类型的常量值
//目的只有一个，便于管理的同时防止程序员单词写错

export const INCREMENT = 'increment';
export const DECREMENT = 'decrement';
```

- `src/redux/count_action.js`

```js
//src/redux/count_action.js
/*该文件专门为Count组件生成action对象 */
import { INCREMENT,DECREMENT } from "./contant";
export const createIncrementAction = data=>({type:INCREMENT,data})
export const createDecrementAction = data=>({type:DECREMENT,data})
```



- `src/redux/count_reducers.js`

```js
//src/redux/count_reducers.js
import { INCREMENT,DECREMENT } from "./contant";
const initState = 0;
export default function countReducer(prevState = initState,action){
    const {type,data} = action;
    switch(type){
        case INCREMENT:
            return data + prevState;
        case DECREMENT:
            return prevState - data;
        default:
            return prevState;
    }
}
```

## 8、求和案例_redux异步action版

### （1）同步action和异步action
action分为两种，同步action和异步action
- 同步action是指，action的值为Object类型的一般对象
- 异步action是指，action的值为函数，异步action中一般都会调用同步action，异步action不是必须要用的

### （2）求和案例redux异步action版
1. 明确：延迟的动作不想交给组件自身，想交给action
2. 何时需要异步action：想要对状态进行操作，但是具体的数据靠异步任务返回。（以后可能会通过调用接口改变redux中的状态，就得写到异步action里面）。
3. 使用异步中间件。
安装redux-thunk：`npm install --save redux-thunk`
使用：
```js
import {createStore,applyMiddleWare} from 'redux';
import thunk from 'redux-thunk' //在store中引入redux-thunk，用于支持异步action
export default createStore (countReducer,applyMiddleWare(thunk));//applyMiddleWare接收thunk作为参数，而且必须自身作为createStore自身的第二个参数，不能是第一个参数也不能是第二个参数
```
4. 备注：异步action不是必须要写的，完全可以自己等待异步任务的结果再去 分发同步action 

代码实现：

- `src/index.js`

```js
//src/index.js
import React from 'react';
import ReactDOM from 'react-dom';

import store from './redux/store';
import App from './App';
ReactDOM.render(<App/>,document.getElementById('root'));

store.subscribe(()=>{
    ReactDOM.render(<App/>,document.getElementById('root'));
})
```
- `src/App.jsx`
```jsx
//src/App.jsx
import {Component} from 'react';

import Count from './components/Count';
export default class App extends Component{
    render(){
        return(
            <Count/>
        )
    }
}
```
- `src/index/components/Count/index.jsx`

```jsx
//src/index/components/Count/index.jsx
import React, { Component } from 'react'

import { createIncrementAction,createDecrementAction,createIncrementAsyncAction } from '../../redux/count_action';
import store from '../../redux/store';
export default class Count extends Component {
    myRef = React.createRef();
    increment = ()=>{
        const {value} = this.myRef.current;
        store.dispatch(createIncrementAction(value-0));
    }
    decrement = ()=>{
        const {value} = this.myRef.current;
        store.dispatch(createDecrementAction(value-0));
    }
    incrementIfOdd = ()=>{
        const count = store.getState();
        if(count % 2 !== 0){
            const {value} = this.myRef.current;
            store.dispatch(createIncrementAction(value-0));
        }
    }
    incrementAsync = ()=>{
        const {value} = this.myRef.current;
                    //使用异步action
        store.dispatch(createIncrementAsyncAction(value-0,1000));
    }
  render() {
      const count = store.getState();
    return (
      <div>
        <h1>{count}</h1>
        <select name="" id="" ref = {this.myRef}>
            <option value="1">1</option>
            <option value="1">2</option>
            <option value="1">3</option>
            <option value="1">4</option>
        </select>
            <button onClick = {this.increment}>+</button>
            <button onClick = {this.decrement}>-</button>
            <button onClick = {this.incrementIfOdd}>奇数+</button>
            <button onClick = {this.incrementAsync}>异步+</button>
      </div>
    )
  }
}

```

- `src/redux/store.js`

```js
//src/redux/store.js

import {createStore,applyMiddleware} from 'redux';

import countReducer from './count_reducer';
//引入redux-thunk，用于支持异步action
import thunk from 'redux-thunk';

//applyMiddleWare		接收thunk作为参数，而且必须自身作为createStore自身的
//第二个参数，不能是第一个参数也不能是第二个参数
export default createStore(countReducer,applyMiddleware(thunk));
```

- `src/redux/contant.js`

```js
//src/redux/contant.js
export const INCREMENT = 'increment';
export const DECREMENT = 'decrement';
```

- `src/redux/count_reducer.js`

```js
//src/redux/count_reducer.js
import { INCREMENT,DECREMENT } from "./contant";
const initState = 0;
export default function countReducer(prevState = initState,action){
    const {type,data} = action;
    switch(type){
        case INCREMENT:
            return prevState+data;
        case DECREMENT:
            return prevState - data;
        default:
            return prevState;
    }
}
```

- `src/redux/count_action.js`

```js
//src/redux/count_action.js

import { INCREMENT,DECREMENT } from "./contant"
//同步action，就是指action的值为Object类型的一般对象
export const createIncrementAction = (data)=>({type:INCREMENT,data}); 
export const createDecrementAction = (data)=>({type:DECREMENT,data}); 

//异步action，就是指action的值为函数，异步action中一般都会调用同步action，异步action不是必须要用
export const createIncrementAsyncAction = (data,time)=>{
    return (dispatch)=>{
        setTimeout(()=>{
            dispatch(createIncrementAction(data));
        },time)
    }
}
```



# 二、react-redux

## （1）对react-redux的理解

1. 一个插件库（与redux不同，redux是一个专门用于做状态管理的js库）

2. 专门用来简化react应用中使用redux

## （2）react-redux原理图

![react-redux原理图](https://gitee.com/Jeren/cloudimages/raw/master/img/react-redux原理图.png)

## （3）react-redux将所有组件分成两大类

1. UI组件
- 只负责UI的呈现，不带有任何业务逻辑
- 通过props接收数据（一般数据和函数）
- 不使用redux的API
- 一般保存在components文件夹下
2. 容器组件
- 负责管理数据和业务逻辑
- 使用Redux的API
- 一般保存在containers文件夹下

## （4）react-redux的基本使用

使用之前要先安装react-redux：`npm i react-redux`

使用react-redux完成上面的求和案例

代码
- `src/index.js`

```js
//src/index.js
import React from 'react';
import ReactDOM from 'react-dom';

import store from './redux/store'
import App from './App';
ReactDOM.render(<App/>,document.getElementById('root'));

store.subscribe(()=>{
    ReactDOM.render(<App/>,document.getElementById('root'));
})
```

- `src/App.jsx`

```jsx
//src/App.jsx
import {Component} from 'react';

import Count from './containers/Count'; 
import store from './redux/store';
class App extends Component{
    render(){
        return(
            /* 给容器组件传递store */
            <Count store = {store}/>
        )
    }
}

export default App;
```

- `src/components/Count.jsx`(UI组件)

```jsx
//src/components/Count.jsx
import {Component} from 'react';

class Count extends Component{
    
    increment = ()=>{
        const {value} = this.selectNumber;
        this.props.jia(value-0);
    }
    decrement = ()=>{
        const {value} = this.selectNumber;
        this.props.jian(value-0);
    }
    incrementIfOdd = ()=>{
        const {count} =this.props;
        if(count % 2 !== 0){
            const {value} = this.selectNumber;
            this.props.jia(value-0);
        }
    }
    incrementAsync = ()=>{
        const {value} = this.selectNumber;
        this.props.asyncjia(value-0,1000);
    }
    render(){
        const {count} = this.props;
        return(
            <div>
                <h1>{count}</h1>
                <select name="" id="" ref = {c=>{this.selectNumber = c}}> 
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                </select>
                <button onClick = {this.increment}>+</button>
                <button onClick = {this.decrement}>-</button>
                <button onClick = {this.incrementIfOdd}>奇数+</button>
                <button onClick = {this.incrementAsync}>异步+</button>
            </div>
        )
    }
}
export default Count
```

- `src/containers/Count.jsx`（容器组件）

```jsx
//src/containers/Count.jsx
//引入Count的UI组件
import CountUI from '../../components/Count';
//引入action
import { createIncrementAction,
    createDecrementAction,
    createIncrementAsyncAction } from '../../redux/count_action';
//引入connect用于连接UI组件与redux
import {connect} from 'react-redux';

//mapStateProps函数返回的是一个对象
//返回的对象中的key就作为传递给UI组件props的key，value就作为传递给UI组件props的value
//mapStateProps用于传递状态

function mapStateProps(state){
    return{count:state};
}
//mapDispatchProps函数返回的是一个对象
//返回的对象中的key就作为传递给UI组件props的key，value就作为传递给UI组件props的value
//mapStateProps用于传递操作状态的方法
function mapDispatchProps(dispatch){
    // 通知redux执行加法和减法操作
    return{
        jia:number=>dispatch(createIncrementAction(number)),
        jian:number=>dispatch(createDecrementAction(number)),
        asyncjia:(number,time)=>dispatch(createIncrementAsyncAction(number,time))
    }
}// 使用connect()()创建并暴露一个Count容器组件
export default connect(mapStateProps,mapDispatchProps)(CountUI)
```

- `src/redux/store.js`

```js
//src/redux/store.js
import {createStore,applyMiddleware} from 'redux';
import countReducer from '../redux/count_reducer';
import thunk from 'redux-thunk';
export default createStore(countReducer,applyMiddleware(thunk));
```

- `src/redux/contant.js`

```js
//src/redux/contant.js
export const INCREMENT = 'increment';
export const DECREMENT = 'decrement';
```

- `src/redux/count_action.js`

```js
//src/redux/count_action.js
import { INCREMENT,DECREMENT } from "./contant"

export const createIncrementAction = data =>({type:INCREMENT,data});
export const createDecrementAction = data =>({type:DECREMENT,data});
export const createIncrementAsyncAction = (data,time)=>{
    return (dispatch)=>{
        setTimeout(()=>{
            dispatch(createIncrementAction(data));
        },time)
    } 
}
```

- `src/redux/count-reducer.js`

```js
//src/redux/count-reducer.js
import { INCREMENT,DECREMENT } from "./contant";
const initState = 0;
export default function countReducer(prevState=initState,action){
    const{type,data} = action;

    switch(type){
        case INCREMENT:
            return prevState+data;
        case DECREMENT:
            return prevState-data;
        default:
            return prevState;
    }
}
```

## 5、react-redux求和案例优化





