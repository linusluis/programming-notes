
## 1、todolist案例展示

![todolist案例展示]()

## 2、 todolist案例组件拆分

该案例拆分为四个组件
1. Header组件
2. List组件（包裹Item组件）
3. Item组件
4. Footer组件

![todolist组件拆分]()

## 3、todolist文件结构

![todolist文件结构]()

## 4、动态初始化列表

这部分是实现网页的静态效果，并且将数据动态的展示在界面上（真正开发中是向后端发起请求拿数据，目前，就使用对象代替）
关于css样式代码不是我们的重点，所以在这里就不展示了

将页面中所有`class`改为`className`

将`style`用`{{}}`包裹

## 5、功能实现

1. App组件
```javascript
import React, { Component } from 'react'

// 引入Header\List\Footer组件和公共样式
import Header from './components/Header'
import List from './components/List'
import Footer from './components/Footer'
import './App.css';
export default class App extends Component {
  //初始化状态
  state = {
    todos:[
      {id:'001',name:'play basketball',done:false},
      {id:'002',name:'play chess',done:false},
      {id:'003',name:'do homework',done:true},
      {id:'004',name:'play volleyball',done:false},
      {id:'005',name:'play football',done:false},
    ]
  }
  //添加todo的方法
  addTodo = (newTodoObj)=>{
    const {todos} = this.state;
    this.setState({todos:[newTodoObj,...todos]});
  }
  //更新todo的方法
  updateTodo = (id,done)=>{
    const {todos} = this.state;
    const newTodos = todos.map((todoObj)=>{
      if(todoObj.id === id){
        return {...todoObj,done};
      }
      return todoObj;
    })
    this.setState({todos:newTodos});
  }
  //删除todo的方法
  deleteTodo = (id)=>{
    const {todos} = this.state;
    const newTodos = todos.filter((todoObj)=>{
      return todoObj.id !== id;
    })
    this.setState({todos:newTodos});
  }
  //更新所有todo的方法
  updateAllTodos = (done)=>{
    const {todos} = this.state;
    const newTodos = todos.map((todoObj)=>{
      return {...todoObj,done};
    })
    this.setState({todos:newTodos});
  }
  //清除所有做过todo的方法
  clearAllDone = ()=>{
    const {todos} = this.state;
    const newTodos = todos.filter((todoObj)=>{
      return !todoObj.done;
    })
    this.setState({todos:newTodos})
  }
  render() {
    const {todos} = this.state;
    return (
      <div className="todo-container">
        <div className="todo-wrap">
          <Header addTodo = {this.addTodo}/>
          <List todos = {todos} updateTodo = {this.updateTodo} deleteTodo = {this.deleteTodo}/>
          <Footer todos = {todos} updateAllTodos = {this.updateAllTodos} clearAllDone = {this.clearAllDone}/>
        </div>
      </div>
    )
  }
}


```
2. Header组件
```javascript
import React, { Component } from 'react'
import { nanoid } from 'nanoid';

import './index.css';
export default class Header extends Component {
    handleKeyUp = (event)=>{
        const {target,keyCode} = event;
        if(keyCode !== 13) return;
        if(target.value === ''){
            alert('输入的todo不能为空');
            return;
        }
        const newTodo = {id:nanoid(),name:target.value,done:false};
        this.props.addTodo(newTodo);
        
    }
    render() {
        return (
            <div className="todo-header">
                <input type="text" placeholder="请输入你的任务名称，按回车键确认" onKeyUp={this.handleKeyUp}/>
            </div>
        )
    }
}

```
3. List组件
```javascript
import React, { Component } from 'react'

import Item from '../Item';
import './index.css';
export default class List extends Component {
    render() {
        const {todos,updateTodo,deleteTodo} = this.props;
        return (
            <ul className="todo-main">
                {
                    todos.map((todoObj)=>{
                        return <Item key = {todoObj.id} {...todoObj} updateTodo = {updateTodo} deleteTodo = {deleteTodo}/>
                    })
                }
            </ul>
        )
    }
}

```
4. Item组件

```javascript
import React, { Component } from 'react'

import './index.css';
export default class Item extends Component {
    state = {mouse:false};
    handleMouse = (flag)=>{
        return ()=>{
            this.setState({mouse:flag});
        }
    }
    handleCheck = (id) =>{
        return (event)=>{
            this.props.updateTodo(id,event.target.checked);
        }
    }
    handleDelete = (id)=>{
        return ()=>{
            this.props.deleteTodo(id);
        }
    }
    render() {
        const {name,done,id} = this.props;
        const {mouse} = this.state;
        return (
            <li style= {{backgroundColor:mouse?'#ddd':'#fff'}}onMouseEnter={this.handleMouse(true)} onMouseLeave = {this.handleMouse(false)} >
                <label>
                    <input type="checkbox" checked = {done} onChange={this.handleCheck(id)} />
                    <span style = {{textDecoration:done?'line-through':'none'}}>{name}</span>
                </label>
                <button className="btn btn-danger" style={{display:mouse?'block':'none'}} onClick = {this.handleDelete(id)}>删除</button>
            </li>
        )
    }
}

```
5. Footer组件

```javascript
import React, { Component } from 'react'

import './index.css';
export default class Footer extends Component {
    handleCheckAll = (event)=>{
        this.props.updateAllTodos(event.target.checked);
    }
    handleClear = ()=>{
        this.props.clearAllDone();
    }
    render() {
        const {todos} = this.props;
        const allTodos = todos.length;
        const doneTodos = todos.reduce((prev,todoObj)=>{
            return prev+(todoObj.done?1:0);
        },0)
        return (
            <div className="todo-footer">
                <label>
                    <input type="checkbox" checked = {allTodos === doneTodos && allTodos !== 0?true:false} onChange = {this.handleCheckAll}/>
                </label>
                <span>
                    <span>已完成{doneTodos}</span> / 全部{allTodos}
                </span>
                <button className="btn btn-danger" onClick = {this.handleClear}>清除已完成任务</button>
            </div>
        )
    }
}

```