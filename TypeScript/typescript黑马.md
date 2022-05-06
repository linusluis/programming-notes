# 一、typescript介绍
## 1、typescript是什么？
typescript（简称：JS）是JavaScript的超集（JS有的TS都有）
typescript = type + javascript（在js基础之上，为js添加了类型支持）

typescript是微软开发的开源编程语言，可以在任何运行javascript的地方运行
举例：  

![typescript举例](https://gitee.com/Jeren/cloudimages/raw/master/img/typescript代码举例.png)

## 2、typescript为什么要为js添加类型支持？

背景：js的类型系统存在“先天缺陷”，js代码中绝大部分错误都是类型错误（Uncaught TypeError）。
问题：增加了找Bug、改Bug的时间，严重影响开发效率。

从编程语言的动静来区分，typescript属于静态类型的编程语言。js属于动态类型的编程语言。

静态类型：编译期做类型检查  
动态类型：执行器做类型检查。

代码编译和代码的执行顺序：1 编译 2执行

对于js来说，需要等到代码真正去执行的时候才能发现错误（晚）
对于TS来说，在代码编译的时候（代码执行前）就可以发现错误（早）
并且，配合VSCode等开发工具，TS可以提前到在编写代码的同时就发现代码中的错误，减少找Bug、改Bug的时间

## 3、typescript相比js的优势
1. 更早（写代码的同时）发现错误，减少找Bug、改Bug时间，提升开发效率。
2. 程序中任何位置的代码都有代码提示，随时随地的安全感，增强了开发体验。
3. 强大的类型系统提升了代码的可维护性能，使得重构代码更加容易。
4. 支持最新的ECMAScript语法，优先体验最新的语法，让你走在前端技术最前沿。
5. TS类型推断机制，不需要在代码中的每个地方都显示标注类型，让你在享受优势的同时，尽量降低了成本。

除此之外，Vue3源码使用TS重写、Angular默认支持TS、React与TS完美配合，Typescript于成为大中型前端项目的首选编程语言。

# 二、typescript初体验

## 1、安装编译TS的工具包

问题：为什么要安装TS的工具包？

回答：Node.js、浏览器，只认识js代码，不认识ts代码。需要先将TS转化为js代码，然后才能运行。

安装命令：`npm i -g typescript`

typescript包：用来编译ts代码的包，提供了tsc命令，实现了ts->js的转化。

验证是否安装成功：`tsc-v`（查看typescript的版本）

![ts的编译运行流程](https://gitee.com/Jeren/cloudimages/raw/master/img/20220507001947.png)

## 2、编译并运行ts代码
1. 创建`Hello.ts`文件（注意：TS文件的后缀名为.ts）

2. 将TS编译为js：在终端输入命令，`tsc hello.ts`（此时，在同级目录中会出现一个同名的js文件）

3. 执行js代码：在终端中输出命令，`node hello.js`

![ts初体验](https://gitee.com/Jeren/cloudimages/raw/master/img/20220507002014.png)

说明：所有合法的js代码都是ts代码，有js基础只需要学习ts的类型即可。
注意：由TS编译生成的js文件，代码中就没有类型信息了。

## 3、简化运行ts的步骤

问题描述：每次修改代码后，都要重复执行两个命令，才能运行ts代码，太繁琐。

简化方式：使用ts-node包，直接在Node.js中执行ts代码

安装命令：`npm i -g ts-node`（ts-node包提供了ts-node命令）

使用方式：`ts-node hello.ts`

解释：`ts-node`命令在内部偷偷的将ts->js，然后，再运行js代码。

# 三、typescript常用类型

## 1、概述
typescript是js的超集，ts提供了js的所有功能，并且额外的增加了：**类型系统**
- 所有的js代码都是ts代码
- js有类型（比如：number/string等），但是js不会检查变量的类型是否发生变化。而ts会检查。typescript类型系统的主要优势：可以显示编辑出代码中的意外行为，从而降低了发生错误的可能性。

## 2、类型注解

示例代码：
```typescript
let age:number = 18;
```

说明：代码中的`:number`就是类型注解

作用：为变量添加**类型约束**。比如：上述代码中，约定变量age的类型为number（数值类型）

解释：约定了什么类型，就只能给变量赋值该类型的值，否则，就会报错。

![类型注解发生错误的情况](https://gitee.com/Jeren/cloudimages/raw/master/img/20220507002123.png)



## 3、常用基础类型

### （1）常用基础类型概述
可以将ts中的常用基类型细分为两类：
1. js已由类型
- 原始类型：number/string/boolean/null/undefined/symbol

特点：简单。这些类型，完全按照js中类型的名称来书写。

- 对象类型：object（包括数组、对象、函数等对象）

特点：对象类型，在TS中更加细化，每个具体的对象都有自己的类型语法。

2. ts新增类型
- 联合类型、自定义类型（类型别名）、接口、元组、字面量类型、枚举、void、any等

### （2）原始类型

原始类型：number/string/boolean/null/undefined/symbol



```typescript
let age:number = 18;
let myName :string = '刘老师';
let isLoading: boolean = false;
let a : null = null;
let b :undefined = undefined;
let s:symbol = Symbol();
```

### （3）数组类型

数组类型的两种写法：（推荐使用number[]写法）

```typescript
let numbers :number[] = [1,2,3,4,5];
let strings :Array<string> = ['a','b','c'];
```

### （4）联合类型
需求：数组中既有number类型，又有string类型，这个数组的类型该如何写？

```typescript
//添加小括号，表示：首先是数组，然后这个数组中能够出现number或string类型的元素
let arr:(number | string)[] = [1,'a','c',2];
//不添加小括号，表示：arr1既可以是number类型，又可以是string[]类型。
let arr1:number | string[] = ['a','b'];
let arr3:number | string[] = 23;
let arr2:Array<string|number> = [1,'s',2,'d'];
```

解释：`|`（竖线）在ts中叫做联合类型（由两个或多个其他类型组成的类型，表示可以是这些类型中的任意一种）。

注意：这是TS中联合类型的语法，只有一根竖线，不要与JS中的或（||）混淆了。

### （5）类型别名

类型别名（自定义类型）：为任意类型起别名。

使用场景：当同一类型（复杂）被多次使用时，可以通过类型别名，简化该类型的使用。
```typescript
type CustomArray = (number | string)[];
let arr1:CustomArray = [1,2,'a','c'];
let arr2: CustomArray = [2,5,'b',4,'r'];
```

解释：
1. 使用type关键字来创建类型别名。

2. 类型别名（比如：此处的CustomArray），可以是任意合法的变量名称。

3. 创建类型别名后，直接使用该类型别名作为变量的类型注解即可。

### （6）函数类型

函数的类型实际上指的是：函数**参数**和**返回值**的类型
为函数指定类型的两种方式：
1. 单独指定参数、返回值的类型。
```typescript
function add(num1:number,num2:number):number{
    return num1+num2;
}
const add2 =(num1:number,num2:number):number=>{
    return num1+num2;
}
console.log(add(12,2));
console.log(add2(23,3));
```

2. 同时指定参数、返回值的类型。

```typescript
const add3:(num1:number,num2:number)=>number = (num1,num2) =>{
    return num1+num2;
}
console.log(add3(2,5));
```
注意：要单独把`:(num1:number,num2:number)=>number`这部分拿出来看，这就是一个类型，这个类型同时指定了参数和返回值。

解释：当函数作为表达式时，可以通过类似箭头函数形式的语法来为函数添加类型
注意：这种形式只适用于函数表达式

3. void类型  

如果函数没有返回值，那么，函数返回值类型为：`void`

```typescript
function greet(name:string):void{
    console.log('hello',name);
}
```

4. 函数可选参数

使用函数实现某个功能时，参数可以传也可以不传。这种情况下，在给函数参数指定类型时，就用到可选参数。

比如，数组的slice方法，可以slice()也可以slice(1)还可以slice(1,3)

```typescript
function mySlice(start?:number,end?:number):void{
    console.log('起始索引',start,'结束索引',end);
}
```

可选参数：在可传可不传的参数名称后面添加 `?`（问号）。

注意：**可选参数只能出现在参数列表的最后**，也就是说可选参数后面不能再出现必选参数。

### （7）对象类型


JS中的对象是由属性和方法构成的，而TS中对象的类型就是在描述对象的结构（有什么类型的属性和方法）

#### <1> 对象类型的写法：
```typescript
const person:{name:string,age:number,sayHi:()=>void} = {
    name:'jack',
    age:19,
    sayHi(){}
}
```
解释：
1. 直接使用{}来描述对象结构。属性采用`属性名:类型`的形式；方法采用`方法名():返回值类型`的形式。
2. 如果方法有参数，就在方法名后面的小括号中指定参数（比如：`greet(name:string):void`）。
3. 在一行代码中指定对象的多个属性类型时，使用;（分号）来分隔。
- 如果一行代码只指定一个属性类型（通过换行来分隔多个属性类型），可以去掉;（分号）。
- **方法的类型也可以使用箭头函数形式（比如：`{sayHi:()=>void}`）**

#### <2> 对象类型的可选属性

对象的属性或方法也是可选的，此时就用到了可选属性了。

比如，我们在使用axios({...})时，如果发送GET请求，method属性就可以省略。

```typescript
function myAxios(config:{url:string,method?:string}){
    console.log(config);
}
myAxios({
    url:''
})
```

可选属性的语法与函数可选参数的语法一致，都使用`?`（问号）来表示

### （8）接口

#### <1> 接口的基本使用
当一个对象类型被多次使用时，一般会使用接口（interface）来描述对象的类型，达到复用的目的。

```typescript
interface IPerson{
    name:string,
    age:number,
    sayHi:()=>void
}

let person:IPerson = {
    name:'jar',
    age:19,
    sayHi(){}
}
```

解释：
1. 使用interface关键字来声名接口
2. 接口名称（比如，此处的Iperson）,可以是任意合法的变量名称。
3. 声名接口后，直接使用接口名称作为变量的类型。
4. 因为每一行只有一个属性类型，因此，属性类型后没有;（分号）

#### <2> 接口 vs 类型别名
interface（接口）和type（类型别名）的对比：
- 相同点：都可以给对象指定类型
- 不同点：
    - 接口，只能为对象指定类型
    - 类型别名，不仅可以为对象指定类型，实际上可以为任意类型指定别名。例如：`type NumStr = number | string`

#### <3> 接口继承 

如果两个接口之间有相同的属性或方法，可以将公共的属性或方法抽离出来通过继承来实现复用。

比如：这里两个接口都用x、y两个属性，重读写两次，可以，但很繁琐。

```typescript
interface Point2D{x:number,y:number};
interface Point3D{x:number,y:number,z:number};
```

更好的方式：
```typescript
interface Point2D{x:number,y:number};
//使用 继承 实现复用
interface Point3D extends Point2D{z:number}
```

解释：
1. 使用extends（继承）关键字实现了接口point3D继承point2D

2. 继承后，Point3D就有了Point2D的所有属性和方法（此时，Point3D同时有x、y、z三个属性）

### （9）元组

场景：在地图中，使用经纬坐标来标记位置信息

可以使用数组来记录坐标，那么，该数组中只有两个元素，并且这两个元素都是数值类型。

```typescript
let position:number[]=[102.4,100.3,122.4];
```
使用numberp[]的缺点：不严谨，因为该类型的数组中可以出现任意多个数字。

更好的方式：元组（Tuple）

```typescript
let position:[number,number] = [22.44,33.55];
```
元组类型是另一种类型的数组，它确切的知道包含多少个元素，以及特定索引对应的类型。

解释：
1. 元组类型可以确切地标记出有多少个元素，以及每个元素的类型。
2. 该实例中，元素有两个元素，每个元素的类型都是number。

### （10）类型推论

在TS中，某些没有明确指出类型的地方，TS的类型推论机制会帮助提供类型。

换句话说：由于推论的存在，这些地方，类型注解可以省略不写！
发生类型推论的两种场景：
1. 声名变量并初始化时
如果声名变量但没有立即初始化值，此时，还必须手动添加类型注解。
2. 决定函数返回值时

![类型推断变量声名初始化时](https://gitee.com/Jeren/cloudimages/raw/master/img/20220507002218.png)

![类型推断决定函数返回值时](https://gitee.com/Jeren/cloudimages/raw/master/img/20220507002247.png)

注意：这两种情况下，类型注解可以省略不写！



推荐：能省略类型注解的地方就省略（充分利用TS类型推断的能力，提升开发效率）

技巧：如果不知道类型，可以通过鼠标放在变量名称上，利用VSCode的提示来查看类型。

### （11）类型断言

有时候你会比TS更加明确一个值的类型，此时，你可以使用类型断言来指定更具体的类型。

比如，

![类型断言](https://gitee.com/Jeren/cloudimages/raw/master/img/20220507002516.png)

注意：getElementById方法返回值的类型是HTMLElement，该类型只包含所有标签公共的属性或方法，不包含a标签特有的href等属性。

因此，这个类型太宽泛（不具体），无法操作href等a标签特有的属性或方法。

解决方式：这种情况下就需要使用类型断言指定更加具体的类型

使用类型断言：
![使用类型断言](https://gitee.com/Jeren/cloudimages/raw/master/img/20220507002557.png)

解释：
1. 使用as关键字实现类型断言。
2. 关键字as后面的类型是一个更加具体的类型（HTMLAnchorElement是HTMLElement的子类型）。
3. 通过类型断言，aLink的类型变得更加具体，这样就可以访问a标签特有的属性或方法了。

另一种语法，使用<>语法，这种形式不常用知道即可：

![类型断言的另一种语法](https://gitee.com/Jeren/cloudimages/raw/master/img/20220507002637.png)

**技巧：在控制台，通过console.dir打印DOM元素，在属性列表的最后面，即可看到该元素的类型。**

### （12）字面量类型

思考以下代码，两个变量的类型分别是什么？

![字面量类型](https://gitee.com/Jeren/cloudimages/raw/master/img/20220507002737.png)


通过TS类型推论机制，可以得到答案：
1. 变量str1的类型为：`string`。
2. 变量str2的类型为：`Hello TS`。

解释：
1. str1是一个变量（let），它的值可以是任意字符串，所以类型为：string。
2. str2是一个常量（const），它的值不能变化只能是'Hello TS'，所以，它的类型为`'Hello TS'`

注意：此处的'Hello TS'，就是一个字面量类型。也就是说某个特定的字符串也可以作为TS中的类型。除字符串外，任意的JS字面量（比如：对象、数字等）都可以作为类型使用。

使用模式：字面量类型配合联合类型一起使用

使用场景：**用来表示一组明确的可选值列表**
比如，在贪吃蛇游戏中，游戏的方向的可选值只能是上、下、左、右中的任意一个。

![贪吃蛇案例](../AppData/Roaming/Typora/typora-user-images/image-20220507002815304.png)

解释：参数`direction`的值只能是up/down/left/right中的任意一个。

优势：相比于string类型，使用字面量类型更加精确、严谨。

### （13）枚举类型

#### <1> 访问枚举
枚举的功能类似于字面量类型+联合类型组合的功能，也可以**表示一组明确的可选值**

枚举：定义一组命名常量。它描述一个值，该值可以是这些命名常量中的一个。

```typescript
enum Direction {Up,Down,Left,Right};

function changeDirection(direction:Direction){
    console.log(direction);
}
```

解释：
1. 使用`enum`关键字定义枚举
2. 约定枚举名称、枚举的值以大写字母开头。
3. 枚举中的多个值之间，通过，（逗号）分隔
4. 定义好枚举后，直接使用枚举名称作为类型注解

注意：形参direction 的类型为枚举Direction，那么，实参的值就应该是枚举Direction成员的任意一个。

#### <2> 访问枚举成员

```typescript
enum Direction {Up,Down,Left,Right};

function changeDirection(direction:Direction){
    console.log(direction);
}

changeDirection(Direction.Right);
```

解释：类似于JS中的对象，直接通过点（.）语法访问枚举的成员。

#### <3> 枚举成员的值

问题：我们把枚举成员作为了函数的实参，它的值是什么呢？

![枚举成员是有值的](https://gitee.com/Jeren/cloudimages/raw/master/img/20220507003047.png)

解释：通过将鼠标移入Direction.Right，可以看到枚举成员的值为3。

注意：枚举成员是有值的，默认为：从0开始自增的数值

我们把，枚举成员的值为数字的枚举，称为数字枚举

当然，也可以给枚举中的成员初始化值

```typescript
//Down->11、Left->12、Right->13
enum Direction{Up =10,Down,Left,Right}
```

```typescript
enum Direction{Up =2,Down = 4,Left = 6,Right = 8}
```

#### <4> 字符串枚举

字符串枚举：枚举成员的值是字符串

```typescript
enum Direction{
    Up = 'UP',
    Down = 'DOWN',
    Left = 'Left',
    Right = 'Right'
}
```
注意：字符串枚举没有自增长行为，因此，字符串枚举的每个成员必须有初始值

#### <5> 枚举的特点及原理

枚举是TS为数不多的非javascript类型级扩展（不仅仅是类型）的特性之一。

因为：其他类型仅仅被当做类型，而枚举不仅用作类型，还提供值（枚举成员都是有值的）。

也就是说，其他的类型会在编译为JS代码时自动移出。但是，枚举类型会被编译为JS代码。

![枚举类型会被编译为JS代码](https://gitee.com/Jeren/cloudimages/raw/master/img/20220507002844.png)

说明：枚举与前面讲到的字面量类型+联合类型组合的功能类似，都用来表示一组明确的可选值列表。

一般情况下，**推荐使用字面量类型+联合类型组合的方式**，因为相比枚举，这种方式更加直观、简洁、高效。


### 14、any类型

原则：**不推荐使用any!**这会让Typescript变为“AnyScript”（失去类型保护的优势）。
因为当值的类型为any时，可以对该值进行任意操作，并且不会有代码提示。

```typescript
let obj:any = {x:0};
obj = 'hello';
obj.bar =100;
obj();
const n:number = obj;
```
解释：以上操作都不会有任何类型错误提示，即使肯能存在错误！

尽可能的避免使用any类型，除非**临时使用any**来“避免”书写很长、很复杂的类型！

其他隐式具有any类型的情况：
1. 声名变量不提供类型也不提供默认值
2. 函数参数不加类型

注意：因为不推荐使用any，所以，这两种情况下都应该提供类型！

### 15、typeof运算符

众所周知，JS中提供了typeof操作符，用来在JS中获取数据的类型。

```javascript
console.log(typeof 'Hello world')//string
```

实际上，TS也提供了typeof操作符：可以在**类型上下文**中引用变量或属性的类型（类型查询）

使用场景：根据已有变量的值，获取该值的类型，来简化类型书写。

```typescript
let p = {a : 1, b : 2};
function formatPoint(point:{a:number,b:number}){};
formatPoint({a:23,b:32})
```

```typescript
let p = {a : 1, b : 2};
function formatPoint(point:typeof p){};
formatPoint({a:123,b:234}) 

```

这两种写法是等价的。

解释：
1. 使用typeof操作符来获取变量p的类型，结果与第一种（对象字面量形式的类型）相同。
2. typeof出现在类型注解的位置（参数名称的冒号后面）所处的环境加载类型上下文（区别于JS代码）
3. 注意：typeof只能用来查询变量或属性的类型，无法查询其他形式的类型（比如，函数调用的类型）。
例如：
```typescript
let p = {a : 1, b : 2};

let str :string;
function formatPoint(point:{a:number,b:number}){};
formatPoint({a:23,b:32});

//查询属性的类型
let num:typeof p.a;//num就是和p.a的类型一样为number类型
//查询变量的类型
let str2:typeof str;//str2就是和str一样为string类型
```

# 四、typescript高级类型

## 1、高级类型概述

TS中的高级类型又很多，重点学习一下高级类型
1. class类
2. 类型兼容性
3. 交叉类型
4. 泛型和keyof
5. 索引签名类型和索引查询类型
6. 映射类型



