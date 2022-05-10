# 一、验证diffing算法

什么是DOM的diffing算法？  
>当状态中数据发生变化时，react会根据新数据生成新的虚拟DOM，然后将新虚拟DOM和旧虚拟DOM进行diff比较，如果内
>没有变化，就直接使用之前的真实DOM，如果有变化，就根据新虚拟DOM生成新的真实DOM，然后将新的真实DOM渲染到页面
>中替换旧真实DOM。  

为了验证diffing算法的存在，我们使用如下案例进行验证： 

随着时间的变化我们在第一个文本框中输入内容，如果文本框中的内容随着时间一闪一闪的刷新，则证明diffing算法是无效的。反之，则证明diffing算法是有效的

测试代码：
```javascript
class Time extends React.Component {
            state = { date: new Date() };
            componentDidMount(){
                    setInterval(()=>{
                        this.setState({date:new Date()});
                    },1000)
                }
            render() {
                const {date} = this.state;
                return(
                    <div>
                        <h1>Hello</h1>
                        <input type="text" />
                        <span>现在是：{date.toTimeString()}</span>
                    </div>
                )
            }
        }
        ReactDOM.render(<Time/>, document.getElementById('test'));
```

验证结果：  

![验证diffing算法](https://gitee.com/Jeren/cloudimages/raw/master/img/验证diffing算法.gif)

理解：由于定时器中更新了state中的数据，所以会一遍一边的调用render，调用一次render会形成新的虚拟DOM树，然后会与前一次生成的虚拟DOM树进行比较。对比过程中发现h1还是之前的h1，input还是之前的input。所以说h1和input对应的真实DOM在页面上没有发生变化。经过比较，还是直接放在页面上。而变的是span标签。

Diffing算法不是对比一层，而是逐层对比，对比最小的力度是标签。比如：在span标签中再嵌套一个输入框，在其中输入内容，看其是否改变？

如果不变，则证明Diffing算法对比不是对比一层，而是逐层对比。

验证结果：  

![验证diffing算法2](https://gitee.com/Jeren/cloudimages/raw/master/img/验证diffing算法2.gif)


# 二、key的作用

在说key的作用之前，先提出一个经典的面试题：
>react/vue中的key有什么作用？（key的内部原理是什么？）
>为什么遍历列表时，key最好不要用index?

带着这两个问题，继续思考......

## 1、虚拟DOM中key的作用
1. 简单的说：key是虚拟DOM对象的标识，在更新显示时key起着及其重要的作用
2. 详细的说：当状态中的数据发生变化时，react会根据句【新数据】生成【新的虚拟DOM】,随后React进行【新虚拟DOM】与【旧虚拟DOM】的diff比较，比较规则如下：
> 旧虚拟DOM中找到了与新虚拟DOM相同的key：
>> 若虚拟DOM中内容没变，直接使用之前的真实DOM
>> 若虚拟DOM中内容变了，则生成新的真实DOM，随后替换掉页面中之前的真实DOM     

> 旧虚拟DOM中未找到与新虚拟DOM相同的key
>> 根据数据创建新的真实DOM，随后渲染到页面

## 2、用index作为key可能会引发的问题
1.   若对数据进行：逆序添加、逆序删除等破坏顺序操作：会产生没有必要的真实DOM更新===》界面效果没问题，但效率低。
2.   如果结构中还包含输入类的DOM：会产生错误DOM更新====》界面有问题
3.   **注意！** 如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示，使用index作为key是没有问题的

下面通过两个案例来说明用id和index作为key的区别：
1. 对数据进行逆序添加这种破坏顺序的操作，导致界面效果没有问题，但使用index会比使用id效率要低

代码示例：
```javascript
        class Person extends React.Component {
            state = {persons:[
                    {id:1,name:'小李',age:18},
                    {id:2,name:'小张',age:23},
                ]
            }
            add = ()=>{
                const {persons} = this.state;
                const newPerson = {id:persons.length+1,name:'小王',age : Math.floor(Math.random()*99)}
                this.setState({persons:[newPerson,...persons]});
            }
            render() {
                const {persons} = this.state;
                return (
                    <div>
                        <h1>展示人员信息</h1>
                        <button onClick= {this.add}>添加一个小王</button>
                        <h2>使用index(索引值)作为key</h2>
                        <ul>
                            {
                                persons.map((per,index)=>{
                                    return <li key={index}>{per.name}---{per.age}</li>
                                })
                            }
                        </ul>
                        <hr/>
                        <hr/>

                        <h2>使用id（数据的唯一标识）作为key</h2>
                        <ul>
                            {
                                persons.map((per)=>{
                                    return <li key = {per.id}>{per.name}---{per.age}</li>
                                })
                            }
                        </ul>
                    </div>
                )
            }
        }
        ReactDOM.render(<Person />,document.getElementById('test'));
```

效果展示：  

![key的作用1](https://gitee.com/Jeren/cloudimages/raw/master/img/key的作用1.gif)

通过上面案例，我们发现无论是使用index作为key，还是使用id作为key，实现的效果是一样的。
但是考虑到性能，就大有不同了。使用index作为key，每次更新state的时候，每个人的index都更新了，key也就更新了。这导致进行diffing比较的时候，虚拟DOM有变化，生成新的真实DOM，替换原来的之前DOM。而使用id作为key则不会，这在效率和性能上有很大的不同。如下两图：  

![使用index作为key](https://gitee.com/Jeren/cloudimages/raw/master/img/使用index作key.png)

![使用id作为key](https://gitee.com/Jeren/cloudimages/raw/master/img/使用id作为key.png)

2. 下面这个案例演示当结构中有输入类DOM使用index作为key会导致页面出现问题

在上面代码的基础上，在li标签中加一个输入框，像这样，做添加操作的时候就会发生错误

代码就沿用上面代码，稍作改动即可。

效果图：  

![key的作用2](https://gitee.com/Jeren/cloudimages/raw/master/img/key的作用2.gif)


从这张图中，可以看出很明显的错误。



## 3、开发中如何选择key?
1.   最好使用每条数据的唯一标识作为key，比如id、手机号、身份证号、学号等唯一值。
2.   如果确定只是简单的展示数据，用index也是可以的。
