## 一、类型声名
> - 类型声名是TS非常重要的一个特点。
> - 通过类型声名可以已制定TS中变量、函数形参、函数返回值的类型
> - 指定类型后，当为变量赋值时，TS编译器会自动检查值是否符合类型声明，符合则赋值，否则报错
> - 简而言之，类型声明给变量设置了类型，使得变量只能存储某种类型的值。

语法：这里分为三种情况说明类型声名的语法
1. 对变量进行类型声明
```typescript
//基本语法：
// let 变量: 类型;
let a:number;
//a = 'hello';//这样就会报错

//也可以直接在声名类型的时候赋值
// let 变量 :类型 = 值
let b:string = 'hello';
//b=123;//b指定为其他类型就会报错

//如果不显示指定类型，而直接赋值，TS是可以自动对变量进行类型检测
let c = 12;
//c = 'hello'//这样会报错
```

2. 对函数形参进行类型声名
```typescript
//对函数参数进行类型声名
function sum(a:number,b:number){
    return a+b;
}

sum(12,23);//35
//sum('12','23'）//会报错，因为参数限定为数值类型
//sum(12,23,34);//参数数量不一致也会报错
```
3. 对函数返回值进行类型限制
```typescript
//对函数返回值进行限制
function sum2(a:number,b:number):number{
    //return a+'hello';//返回值类型不是number会报错
    return a+b;
}
```
## 二、自动类型判断
- TS拥有自动的类型判断机制
- 如果不显示指定类型，而直接赋值，TS编译器会自动判断变量的类型。
- 所以如果你的变量的声名和赋值是同时进行的，可以省略掉类型声名。

## 三、类型
|类型|例子|描述|
|:---:|:---:|:---:|
|number|1,-33,2.5|任意数字|
|string|'hi',"hi",hi|任意字符串|
|boolean|true、false|布尔值true或false|
|字面量|其本身|限制变量的值就是该字面量的值|
|any|*|任意类型|
|unknown|*|类型安全的any|
|void|空值（undefined）|没有值（或undefined）|
|never|没有值|不能是任何值|
|object|{name:'孙悟空'}|任意的JS对象|
|array|[1,2,3]|任意JS数组|
|tuple|[4,5]|元素，TS新增类型，固定长度数组|
|enum|enum{A,B}|枚举，TS中新增类型|

### 1、number
```typescript
let decimal :number = 6;
let hsx:number = 0xf00d;
let binary:number = 0b1010;
let octal:number = 0o744;
let big:bigint = 100n; 
```

### 2、boolean
```typescript
let isDone:boolean = false;
```

### 3、string
```typescript
let color:string = 'blue';
color:red;

let fullName:string = `Bob Bobbington`;
let age:number =37;
let sentence:string = `Hello,my name is ${fullName}

I'll be ${age+1} years old next month`;
```

### 4、字面量

```typescript
//直接使用字面量进行类型声名
let a : 10;
a = 10;
//a= 20;//会报错
```
### 5、any
```typescript
//any表示的是任意类型，一个变量设置为any后相当于对该变量关闭了TS的类型检测
//使用TS时，不建议使用any类型
let d:any;
d = 10;
d = 'hello';
d = false;
//声名变量如果不指定类型，则TS解析器会自动判断变量的类型为any（隐式any）
//比如：
let d;//这样d的类型就为any
```
### 6、unknow

```typescript
//unknown，表示未知类型的值
let e :unknown;
e = 10;
e = 'hello';
e = true;
//目前看来，unknown和any没有任何区别

// unknown和any的区别如下：
//d的类型是any，它可以赋值给任意变量
let s : string;
let d : any;
s = d;

//unknown实际上就是一个类型安全的any
//unknown类型的变量，不能直接赋值给其他变量
e = 'hello';
//s = e;//这样就会报错
```

当遇到一个类型不确定的变量时，能用unknown用unknown，能不用any就不用any。 

### 7、void
```typescript
//void用来表示空，以函数为例，就表示没有返回值的函数
function fn():void{
    //return true;//如果有返回值就会报错
}

function fn2():void{
    console.log('123');//没有返回值就不会报错
    // return ;
    // return null;
    return undefined;
    //返回空、null或者undefined都不会报错。
}
```

### 8、never
```typescript
//never表示永远不会返回结果
//never和void的区别在于：void可以返回null和undefined
//但是never连undefined都不可以返回。
// 那么never类型的作用是什么呢？在js中有这么一种函数，；连undefined都不返回
//它是用来报错的，当程序运行出现错误了，就可以用这种函数报错
//fn3只要一调用就报错，程序一旦报错，代码就立即结束了，就没有返回值了
function fn3():never{
    throw new Error('报错了');
}
```

### 9、object
```typescript
//object表示一个js对象
//object并不实用，因为js中一切皆对象
let a: object;
a = {};
a = function (){

} 
```
#### （1）对对象中属性的类型进行限制

其实，限制一个对象的时候，我们更想限制的是对象包含哪些属性，而不是限制它是不是一个对象。

```typescript
//那么我们可以这么写，这样写也表示变量b存储的也是一个对象

let b:{}
//{}用来指定对象中可以包含哪些属性
//语法：{属性名:属性值，属性名:属性值}
// 但是这种方式和上面方式是有区别的，我们可以指定对象中属性的类型
let c:{name:string,age?:number}
c = {name:'孙悟空',age:18};

//属性名后面+一个?是什么意思呢？表示该属性是可选的
c = {name:'猪八戒'};//不会报错

//还有一点需要注意：
//按照上面的写法，对象中属性的数量就固定了，我们就不能随意再添加其他属性了。
// 为了解决这个问题：可以像下面这样写
let d :{name:string,[propName:string]:any};
d= {name:'沙和尚',age:18,gender:'男',address:'流沙河'}//这样就仅会限制name为字符串类型而不会限制属性数量了
//[propName:string]:any 表示任意类型的属性
```
#### （2）设置函数结构的类型声名

```typescript
/*
设置函数结构的类型声名
语法：（形参:类型,形参:类型...）=>返回值类型
*/
let e :(a:number,b:number) =>number;
e = function(n1:number,n2:number):number{
    return n1+n2;
}
// 下面这个就会报错
// e = function(n1:string,n2:string):number{
//     return 10;
// }
```

### 10、array

原生的js中，我们发现数组中什么都能存，string,number,boolean都可以混着存。
然而实际开发中我们要求对数组中的类型进行限制，不能什么都存，可以像下面这样做：
```typescript
//string[] 表示字符串数组
let f :string[];
f:['a','b','c'];
// 第二种表示方式
let g:Array<string>;
g=['a','b','c'];
```

### 11、tuple元组
首先要知道什么是元组：元组就是固定长度的数组。
```typescript
/*
语法：[类型,类型,类型]
*/
let h :[string,number];
h = ['hello',123];
// h = ['hello',123,true]//这样写就会报错
```

### 12、enum枚举

```typescript
enum Gender{
    Male,
    Female
}
let i: {name:string,gender:Gender}
i = {
    name:'孙悟空',
    gender:Gender.Female
}
```

### 13、联合类型
```typescript
//联合类型
//可以使用 | 链接多个类型（联合类型）
let b :'male' | 'false';
b = 'male'
//b = 'hello'//'hello'既不属于'male'也不属于'female'，所以会报错
//这种联合类型对于其他类型也一样有效
let c :boolean | string;
c = true;
c = 'hello';
//c= 123;//123既不属于boolean类型也不属于string类型，所以会报错
```

### 14、类型断言

```typescript
//类型断言，可以用来告诉解析器变量的实际类型
/*
语法：
变量 as 类型
<类型>变量
这两种效果一样，都可以
*/ 
let s :string;
let e : unknown;
s = e as string;//告诉解析器e的实际类型为字符串类型
s = <string>e;//告诉解析器e的实际类型为字符串类型
```

### 15、&表示同时
```typescript
// let j :number & string;//这样使用并没有什么意义，一个变量怎么可能既是string类型又是number类型呢

//但是我们可以这么用
let j :{name:string} & {age:number};

```
###  16、类型的别名
```typescript
//类型的别名
// 当一个类型特别难记的时候，为了之后再写这个类型省事，我们可以为一个类型设置一个别名。像下面这样。
type myType = 1 | 2 | 3 | 4 | 5; 
let k:myType;
//然而，我们我string,number，boolean等这种类型设置别的别名就没有什么意义了
```







