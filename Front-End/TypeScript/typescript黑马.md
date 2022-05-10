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

除此之外，Vue3源码使用TS重写、Angular默认支持TS、React与TS完美配合，Typescript已成为大中型前端项目的首选编程语言。

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

解释：`|`（竖线）在ts中叫做联合类型（由两个或多个 	其他类型组成的类型，表示可以是这些类型中的任意一种）。

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

![贪吃蛇案例](https://gitee.com/Jeren/cloudimages/raw/master/img/20220508201411.png)

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

## 2、Class 类

TypeScript全民支持ES2015中引入的class关键字，并为其添加了类型注解和其他语法（比如，可见性修饰符等）

class基本使用，如下：

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220508202413.png)



解释：

1. 根据TS中的类型推论，可以知道Person类的实例对象p的类型是Person.
2. TS中的class，**不仅提供了class的语法功能，也作为一种类型存在。**

### （1）实例属性初始化

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220508202701.png)

解释：

1. 声名成员age，类型为number(没有初始值)
2. 声名成员为gender，并设置初始值，此时，可省略类型注解（TS类型推论为string类型）。

### （2）构造函数

 ```typescript
 class Person{
     name:string;
     age:number;
     gender:string;
     constructor(name:string,age:number,gender:string){
         this.name = name;
         this.age = age;
         this.gender = gender;
     }
 }
 
 const p = new Person('luis',22,'男');
 ```



解释：

1. 成员初始化（比如，age:number）后，才可以通过this.age来访问实例成员
2. 需要为构造函数指定类型注解，否则会被隐式推断为any；构造函数不需要返回值类型。

### （3）class的实例方法

```typescript
class Point{
    x = 3;
    y = 10;
    scale = (n:number):void=>{
        this.x*=n;
        this.y*=n;
    } 
}
const p = new Point();
p.scale(10);
console.log(p.x);//30
```



解释：方法的类型注解（函数和返回值）与函数用法相同

### （4）class的继承

类继承的两种方式：

1. extends（继承父类）
2. implements（实现接口）

说明：JS中只有extends，而implements是TS提供的

```typescript

class Animal{
    name:string;
    age:number;
    constructor(name:string,age:number){
        this.name = name;
        this.age = age
    }
    run(){
        console.log('跑啊跑');
    }
}
enum Gender{男,女};
class Dog extends Animal{
    gender:Gender;
    constructor(name:string,age:number,gender:Gender){
        super(name,age);
        this.gender = gender
    }
    bark(){
        console.log('汪汪汪');
    }
}
const dog = new Dog('大黄',12,Gender.男);
dog.run();
dog.bark();
```



解释：

1. 通过extends 关键字实现继承
2. 子类Dog类继承父类Animal，则Dog的实例对象dog就同时具有了父类Animal和子类的所有属性和方法了

### （5）class的实现接口

```typescript
interface Singable{
    sing():void;
}
class Person implements Singable{
    sing(): void {
        console.log('I can sing a song');
    }
}
```



解释：

1. 通过implements关键字让class实现接口
2. Person类实现接口Singable意味着，Person类中必须提供Singable接口中指定的所有方法和属性。

### （6）类成员可见性

可以使用TS来控制class的方法或属性对于class外的代码是否可见

可见性修饰符包括：

1. public（公有的）
2. protected（受保护的）
3. private（私有的）

#### <1> public 

`public`：表示公有的、公开的，公有成员可以被任何地方访问，默认可见性

```typescript
class Animal{
    public move(){
        console.log('moving along');
    }
}
const dog = new Animal();
dog.move();
```



解释：

1. 在类属性或方法前面添加public关键字，来修饰该属性或方法是共有的。
2. 因为public是默认可见性，所以直接省略。

#### <2>protected

`protected`表示受保护的，仅对其声名所在类和子类中（非实例对象）可见。



```typescript
class Animal{
    protected move(){
        console.log('moving along');
    }
}
class Dog extends Animal{
    bark(){
        console.log('汪汪汪!');
        this.move();//父类中受保护的方法
    }
}
const dog = new Animal();
//dog.move();//实例不能直接访问。
const dog2 = new Dog();
dog2.bark();//两个方法都能访问到
```



解释：

1. 在类属性或方法前面添加protected关键字，来修饰该属性或方法是受保护的。
2. 在子类的方法内部可以通过this来访问父类中受保护的成员，但是，对实例不可见。



####  <3>private

`private`表示私有的，只在当前类中可见，对实例对象以及子类也是不可见的。

```typescript
class Animal{
    protected move(){
        console.log('moving along');
        this.run();//在当前类中可以访问private的属性
    }
    private run(){
        console.log('run run run ...');
    }
}
class Dog extends Animal{
    bark(){
        console.log('汪汪汪!');
        this.move();
        // this.run(); 在子类中不能访问到run方法
    }
}
const dog = new Animal();

const dog2 = new Dog();
dog2.bark();
// dog2.run();//在实例对象中也不能访问run方法
```





解释：

1. 在类属性或方法前面添加private关键字，来修饰属性或方法是私有的。
2. 私有的属性或方法只在当前类中可见，对子类和实例对象也都是不可见的。



### （7）只读修饰符

除了可见性修饰符之外，还有一个常见的修饰符就是：readonly（只读修饰符）。

readonly：表示只读，用来防止在构造函数之外对属性进行赋值。

```typescript
class Person{
    //注意：只要是readonly来修饰的属性，必须手动提供明确的类型
    readonly age:number = 18;
    constructor(age:number){
        this.age = age;
    }
}
const  p = new Person(23);
p.age = 33;//不能修改
```



解释：

1. 使用readobly关键字修饰概属性是只读的没注意**只能修饰属性不能修饰方法**
2. 注意：属性age后面的类型注解（比如，此处的number）如果不加，则age的类型为18（字面量类型）
3. 接口或者{}表示的对象类型，也可以使用readonly。

```typescript
//比如接口中
interface IPerson{
    name:string;
    readonly age:number
}

const person:IPerson = {
    name:'luis',
    age:23
}
// person.age = 33;//不能更改，因为age是只读的

//比如对象中
const computer:{readonly type:string,size:number} = {
    type:'BenQ300',
    size:23
}

computer.type = 'Huawei';//不能更改，因为type是只读的。
```

## 2、类型兼容性

两种类型系统：

1. Structural Type System（结构化类型系统）
2. Nominal Type System（标明类型系统）

TS采用的是结构化类型系统，也叫做duck typing（鸭子类型），**类型检查关注的是值所具有的形状。**

也就是说，在结构类型系统中，如果两个对象具有相同的形状，则认为他们属于同一类型。

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220508233702.png)

解释：

1. Point和Point2D是两个名称不同的类。
2. 变量p的类型被显示标注为Point类型，但是，它的值却是Point2D的实例，并且没有类型错误。
3. 因为TS是结构化类型系统，只检查Point和Point2D的结构是否相同（相同，都具有x和y两个属性，属性类型也相同）。
4. 但是，如果在Nominal Type System中（比如，C#、Java等），它们是不同的类，类型无法兼容。

如下代码也属于类型兼容性

```typescript
let arr= ['a','b','c'];
arr.forEach(value=>{})
arr.forEach((value,index)=>{})
arr.forEach((value,index,array)=>{})
```

### （1）对象之间的类型兼容性

注意：在结构化类型系统中，如果两个对象具有相同的形状，则认为它们属于同一类型，这种说法并不准确。

更准确的说法：对于对象类型来说，y的成员至少与x相同，则x兼容y（**成员多的可以赋值给少的**）。

```typescript
class Point{x:number;y:number}
class Point3D{x:number;y:number;z:number}
const p:Point = new Point3D();
//const p2:Point3D = new Point();//少的复制给多的就会报错
```

解释：

1. Point3D的成员至少与Point相同在则Point兼容Point3D.
2. 所以，成员多的Point3D可以赋值给成员少的Point

### （2）接口兼容性

除了class之外，TS中的其他类型也存在互相兼容的情况，包括：①函数兼容性 ②函数兼容性等。

接口之间的兼容性，类似于class。并且，class和interface之间也可以兼容。

- 接口之间的兼容性

```typescript
interface Point{
    x:number
    y:number
}
interface Point2D{
    x:number
    y:number
}
let p1:Point;
let p2:Point2D = p1;
interface Point3D{
    x:number
    y:number
    z:number
}
let p3:Point3D;
p2 = p3;
```

- 接口与类之间的兼容性

```typescript
interface Point{
    x:number
    y:number
}
interface Point2D{
    x:number
    y:number
}
let p1:Point;
let p2:Point2D = p1;
class Point3D{
    x:number
    y:number
    z:number
}
const p3:Point2D = new Point3D();
```

### （3）函数之间的兼容性——函数参数个数

函数之间兼容性比较复杂，需要考虑：①参数个数  ②参数类型 ③返回值类型



参数对的兼容参数少的（或者说，参数少的可以赋值给多的）

```typescript
//参数个数：参数少的可以赋值给参数多的
type F1 = (a:number) =>void;
type F2 = (a:number,b:number) =>void;

let f1:F1;
let f2:F2;
f2 = f1;//少的赋值给多的
// f1 = f2;//多的赋值给少的，会报错。
```

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220509114247.png)

解释：

1. 参数少的可以赋值给参数多的，所以f1可以赋值给f2
2. 数组forEach方法的第一个参数是回调函数，该示例中类型为：
3. 在JS中省略用不到的函数参数实际上是很少见的，这样的使用方式，促成了TS中函数类型之间的兼容性。
4. 并且因为回调函数是有类型的，所以，TS会自动推出参数item、index、array

### （4）函数之间的兼容性——函数参数类型

参数类型，相同位置的参数类型要相同（原始类型）或兼容（对象类型）

- 简单：参数类型是原始类型的情况---要求参数类型相同

 ```typescript
 type F1 = (a:number)=>string;
 type F2 = (a:number)=>string;
 let f1:F1;
 let f2 :F2 = f1;
 ```

解释：函数类型F2兼容函数类型F1，因为F1和F2的第一个参数类型相同。

- 复杂：参数类型包括对象类型的情况

参数类型，相同位置的参数类型要相同或者兼容。

```typescript
//对象类型
interface Point2D{
    x:number
    y:number
}
interface Point3D{
    x:number
    y:number
    z:number
}
type F2 = (p:Point2D)=>void;
type F3 = (p:Point3D)=>void;

let f2:F2;
let f3:F3 = f2;
```



解释：

1. 注意，此处与前面讲到的接口兼容性冲突
2. 技巧：将对象拆开，把每个属性看做一个个参数，则参数少的（f2）可以赋值给参数多的（f3）



### （5）函数之间的兼容性——函数返回值

返回值类型，只关注返回值类型本身即可：

```typescript
type F5 = () =>string;
type F6 = ()=>string;

let f5:F5;
let f6:F6 = f5;
f5 = f6;
```

```typescript
type F7 = ()=>{name:string}
type F8 = ()=>{name:string,age:number}
let f7 : F7;
let f8 : F8;
f7 = f8;
//f8 = f7;//成员少的不能赋值给成员多的。
```



解释：

1. 如果返回值类型是原始类型，此时两个类型要相同，比如，第一段代码类型F5和F6
2. 如果返回值类型是对象类型，此时成员多的可以赋值给成员少的，比如，第一段代码类型F7和F8

## 3、交叉类型

交叉类型（&）：功能类似于接口继承（extends），用于组合多个类型为一个类型（常用于对象类型）

比如，

```typescript
interface Person{
    name:string;
    say():number
}
interface Contact{
    phone:string;
}

type PersonDetail = Person & Contact;
let obj :PersonDetail = {
    name:'jack',
    phone:'133...',
    say(){
        return 1;
    }
```



解释：使用交叉类型之后，新的类型personDetail就同时具备了person和Contact的所有属性类型

相当于，

```typescript
type PersonDetail = {name:string;phone:string}
```

### （1）交叉类型(&)和接口继承（extends）的对比

- 相同点：都可以实现对象类型的组合。
- 不同点：两种方式实现类型组合时，对于同名属性之间，处理类型冲突的方式不同。

```typescript
//接口继承
interface A{
    fn:(value:number)=>void;
}
interface B extends A{
    fn:(value:string)=>void
}
```

```typescript
//交叉类型
interface A{
    fn:(value:number) =>void
}
interface B{
    fn:(value:string)=>void
}

type C = A & B;
let c:C={
    fn(value:number | string){
        return ''; 
    }
}
```

说明：以上代码，接口继承会报错（类型不兼容）；交叉类型没有错误，可以简单的理解为：

```typescript
fn:(value:string | number)=>void
```

## 4、泛型

泛型时可以在保证类型安全前提下，让函数等与**多种类型**一起工作，从而**实现复用**，常用于**函数、接口、class中**。

需求：创建一个id函数，传入什么数据就返回该数据本身（也就是说，参数和返回值类型相同）。

```typescript
function id(value:number):number{return value};
```



比如：id(10)调用以上函数就会直接返回10本身。但是，该函数只接受数值类型，无法用于其他类型。

为了能让函数能够接受任意类型，可以将参数类型修改为any。但是，这样就失去了TS的类型保护，类型不安全。

```typescript
function id(value:any):any{return value};
```



泛型在保证类型安全（不丢失类型信息）的同时，可以让函数等与多种不同的类型一起工作，灵活可复用。

实际上，在C#和java等编程语言中，泛型都是用来实现可复用组件功能的主要工具之一。



### （1）创建泛型函数

```typescript
function id<Type>(value:Type):Type{
    return value;
}
```



解释：

1. 语法：在函数名称的后面添加`<>`（尖括号），尖括号中添加类型变量，比如此处的Type
2. 类型变量Type，是一种特殊类型的变量，它处理类型而不是值。
3. 该类型变量想相当于一个类型容器，能够捕获用户提供的类型（具体是什么类型由用户调用该函数时指定）。
4. 因为Type是类型，因此可以将其作为函数参数和返回值的类型，表示参数和返回值具有相同的类型。
5. 类型变量Type，可以是任意合法的变量名称。

### （2）调用泛型函数

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220509134250.png)

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220509134350.png)

解释：

1. 语法：在函数名称后面添加<>（尖括号），尖括号中指定具体的类型，比如，此处的number。
2. 当传入类型number后，这个类型就会被函数声名时指定的类型变量Type捕获到
3. 此时，Type的类型就是number，所以，函数id参数和返回值的类型也都是number。

同样，如果传入类型string，函数id参数和返回值的类型就都是string。

这样，通过泛型就做到了让id函数与多种不同的类型一起工作，实现了复用的同时保证了类型安全。

### （3）简化调用泛型函数

```typescript
function id<Type>(value:Type):Type{
    return value
}
//正常写法
let num = id<number>(3)
//简写形式，利用推断
let num2 = id(3);
```



解释：

1. 在调用泛型函数时，**可以省略<类型>来简化泛型函数的调用。**
2. 此时，TS内部会采用一种叫做类型参数推断的机制，来根据传入的实参自动推断出类型变量Type的类型。
3. 比如：传入实参10，TS会自动推断出变量num的类型number，更易于阅读。

推荐：使用这种简化的方式调用泛型函数吗，使代码更短，更易于阅读

说明：当 型参数。

### （4）泛型约束

默认情况下，泛型函数的类型变量Type可以代表多个类型，这导致无法访问任何属性。

比如：`id('a')`调用函数时获取参数的长度：

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220509142036.png)

解释：Type可以代表任意类型，无法保证一定存在length属性，比如numbers类型就没有length。此时，就需要为泛型添加约束来收缩类型（缩窄类型取值范围）



添加泛型约束收缩类型，主要有以下两种方式：①指定更加具体的类型②添加约束

#### <1> 指定更加具体的类型

```typescript
function id<Type>(value:Type[]):Type[]{
    console.log(value.length);
    return value;
}
```



比如，将类型修改为Type[]（Type类型的数组），因为只要是数组就一定存在length属性，因此就可以访问了。

#### <2> 添加约束

```typescript
interface ILength{
    length:number
}
function id<Type extends ILength>(value:Type):Type{
    console.log(value.length);
    return value;
}
// id(12);//number类型不具有length属性
id('hello');
```



解释：

1. 创建描述约束的接口ILength，该接口要求提供length属性。
2. 通过extends关键字使用该接口，为泛型（类型变量）添加约束。
3. 该约束表示：传入的类型必须具有length属性。

注意：传入的实参（比如，数组、字符串）只要有length属性即可，这也符合前面讲到的接口的类型兼容性。

### （5）多个泛型变量的情况

泛型的类型变量可以有多个，并且类型变量之间还可以约束（比如，第二个类型变量受第一个类型变量约束）。

比如：创建一个函数来获取对象中属性的值：

```typescript
function getProps<Type,Key extends keyof Type>(obj:Type,key:Key){
    return obj[key];
}
let person = {
    name:'luis',
    age:23
}
getProps(person,'age');
console.log(getProps('hello',2));//l
console.log(getProps(['one','two','three'],'length'));//3
```



解释：

1. 添加了第二个类型变量key，两个类型变量之间使用(,)逗号分隔。
2. keyof关键字接收一个对象类型，生成其键名称（可能是字符串或数字）的联合类型。
3. 本示例中keyof Type实际上获取的是person对象所有键的联合类型，也就是`'name'|'age' `
4. 类型变量Key受Type约束，可以理解为Key只能是Type所有键中的任意一个，或者说只能访问对象中存在的属性。

### （6）泛型接口

接口也可以配合泛型来使用，以增加其灵活性，增强其复用性。

```typescript
interface IDFunc<Type>{
    id:(value:Type)=>Type;
    ids:()=>Type[]
}

let obj:IDFunc<number> ={
    id(value){
        return value
    },
    ids(){
        return [1,2]
    }
} 
```



解释：

1. 在接口名称的后面添加`<类型变量>`，那么，这个接口就变成了泛型接口。
2. 接口的类型变量，对接口找那个所有其他成员可见，也就是接口中所有成员都可以使用类型变量
3. 使用泛型接口时，需要显示指定具体的类型（比如，此处的IdFunc<number>）
4. 此时，id方法的参数和返回值类型都是number；ids方法的返回值类型是number[]。

### （7）数组就是一个泛型接口

实际上，JS中的数组在TS中就是一个泛型接口。

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220509154218.png)

解释：当我们在使用数组时，TS会根据数组的不同类型，来自动将类型变量设置为相应的类型。

技巧：可以通过Ctrl+鼠标左键来查看具体的类型信息

### （8）泛型类

class也可以配合泛型来使用

比如，React的class组件的基类Component就是泛型类，不同的组件有不同的props和state。

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220509154642.png)

解释：React.Component泛型类两个类型变量，分别指定props和state类型

#### <1> 创建泛型类

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220510083101.png)

解释：

1. 类似于泛型接口，在class名称后面添加<类型变量>，这个类就变成了泛型类。
2. 此处的add方法，采用的是箭头函数形式的类型书写方式。

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220510112627.png)

类似于泛型接口，在创建class实例时，在类名后面通过<类型>来指定明确的类型。

### （9）泛型工具类型

TS内置了一些常用的工具类型，来简化TS中的一些常见操作。

说明：它们都是基于泛型实现的（泛型适用于多种类型，更加通用，并且是内置的），可以直接在代码中使用

这些工具类型有很多，主要学习以下几个：

1. Partial<Type>
2. Readonly<Type>
3. Pick<Type,Keys>
4. Record<Keys,Type>

#### <1> `Partial<Type>`

泛型工具类型 - **Partial<Type> 用来构造（创建）一个类型，将 Type 的所有属性设置为可选。**

```typescript
interface Props{
    id:string;
    children:number[];
}

type PartialProps = Partial<Props>
const p1:Props= {
    id:'',
    children:[12,23]
}
const p2:PartialProps = {
    //属性是可选的
}
```



解释：构造出来的新类型 PartialProps 结构和 Props 相同，但所有属性都变为可选的。

#### <2>`Readonly<Type>`

泛型工具类型 - Readonly<Type> 用来构造一个类型，将 Type 的所有属性都设置为 readonly（只读）.

![image-20220510090407517](https://gitee.com/Jeren/cloudimages/raw/master/img/20220510112549.png)

解释：构造出来的新类型 ReadonlyProps 结构和 Props 相同，但所有属性都变为只读的。

当我们想重新给 id 属性赋值时，就会报错：无法分配到 "id" ，因为它是只读属性。

#### <3>`Pick<Type,Keys>`

泛型工具类型 - Pick 从 Type 中选择一组属性来构造新类型

```typescript
interface Props{
    id:string,
    title:string,
    children:number[]
}

type PickProps = Pick<Props,'id' | 'title'>

const p:PickProps = {
    id:'002',
    title:'hello'
}
```



解释：

1. Pick 工具类型有两个类型变量：1 表示选择谁的属性 2 表示选择哪几个属性。 
2. 其中第二个类型变量，如 果只选择一个则只传入该属性名即可。 
3. 第二个类型变量传入的属性只能是第一个类型变量中存在的属性。 
4. 构造出来的新类型 PickProps，只有 id 和 title 两个属性类型。

#### <4>  `Record<Keys,Type>`

泛型工具类型 - Record 构造一个对象类型，属性键为 Keys，属性类型为 Type

```typescript
type RecordObj = Record<'a' | 'b' | 'c',string[]>
let obj:RecordObj = {
    a:['h','e'],
    b:['l','l'],
    c:['o']
}
```

解释： 

1. Record 工具类型有两个类型变量：1 表示对象有哪些属性 2 表示对象属性的类型。 
2. 2. 构建的新对象类型 RecordObj 表示：这个对象有三个属性分别为a/b/c，属性值的类型都是 string[]。

## 5、索引签名类型

暂未学习。。。。

## 6、映射类型

暂未学习。。。

# 五、typescript类型声明文件

今天几乎所有的 JavaScript 应用都会引入许多第三方库来完成任务需求。

这些第三方库不管是否是用 TS 编写的，最终都要编译成 JS 代码，才能发布给开发者使用。 我们知道是 TS 提供了类型，才有了代码提示和类型保护等机制。

但在项目开发中使用第三方库时，你会发现它们几乎都有相应的 TS 类型，这些类型是怎么来的呢？类型声明文件 类型声明文件：用来为已存在的 JS 库提供类型信息。 

这样在 TS 项目中使用这些库时，就像用 TS 一样，都会有代码提示、类型保护等机制了。 

1. TS 的两种文件类型
2. 类型声明文件的使用说明

## 1、TS中的两种文件类型

TS 中有两种文件类型：1 .ts 文件 2 .d.ts 文件。

- .ts 文件：

  1. 既包含类型信息又可执行代码。 

  2. 可以被编译为 .js 文件，然后，执行代码。 

  3. 用途：编写程序代码的地方。

     

- .d.ts 文件：
  1. 只包含类型信息的类型声明文件。 
  2. 不会生成 .js 文件，仅用于提供类型信息。 
  3. 用途：为 JS 提供类型信息。 

总结：.ts 是 implementation（代码实现文件）；.d.ts 是 declaration（类型声明文件）。 如果要为 JS 库提供类型信息，要使用 .d.ts 文件

## 2、类型声明文件的使用说明

在使用 TS 开发项目时，类型声明文件的使用包括以下两种方式：

1. 使用已有的类型声明文件 
2. 创建自己的类型声明文件 

学习顺序：先会用（别人的）再会写（自己的）。

### （1）使用已有的类型声明文件

使用已有的类型声明文件：1 内置类型声明文件 2 第三方库的类型声明文件。

 内置类型声明文件：TS 为 JS 运行时可用的所有标准化内置 API 都提供了声明文件。 比如，在使用数组时，数组所有方法都会有相应的代码提示以及类型信息： 

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220510112645.png)



实际上这都是 TS 提供的内置类型声明文件。 

可以通过 Ctrl + 鼠标左键（Mac：option + 鼠标左键）来查看内置类型声明文件内容。 

比如，查看 forEach 方法的类型声明，在 VSCode 中会自动跳转到 lib.es5.d.ts 类型声明文件中。

当然，像 window、document 等 BOM、DOM API 也都有相应的类型声明（lib.dom.d.ts）

### （2）第三方库的类型说明文件

第三方库的类型声明文件：目前，几乎所有常用的第三方库都有相应的类型声明文件。 第三方库的类型声明文件有两种存在形式：1 库自带类型声明文件 2 由 DefinitelyTyped 提供。 

1. 库自带类型声明文件：比如，axios

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220510212524.png)

解释：这种情况下，正常导入该库，TS 就会自动加载库自己的类型声明文件，以提供该库的类型声明。

2. 由 DefinitelyTyped 提供。 

[DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped/) 是一个 github 仓库，用来提供高质量 TypeScript 类型声明。 

可以通过 npm/yarn 来下载该仓库提供的 TS 类型声明包，这些包的名称格式为：@types/*。 

比如，@types/react、@types/lodash 等。 

说明：在实际项目开发时，如果你使用的第三方库没有自带的声明文件，VSCode 会给出明确的提示。

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220510212849.png)

解释：当安装 @types/* 类型声明包后，TS 也会自动加载该类声明包，以提供该库的类型声明。 

补充：TS 官方文档提供了一个[页面](https://www.typescriptlang.org/dt/)，可以来查询 @types/* 库。

## 3、创建自己的类型声名文件

暂未学习。。。。





# 六、在react中使用typescript

现在，我们已经掌握了 TS 中基础类型、高级类型的使用了。但是，如果要在前端项目开发中使用 TS，还需要掌握 React、Vue、Angular 等这些库或框架中提供的 API 的类型，以及在 TS 中是如何使用的。 接下来，我们以 React 为例，来学习如何在 React 项目中使用 TS。包括以下内容： 

1. 使用 CRA 创建支持 TS 的项目 
2. TS 配置文件 tsconfig.json 
3. React 中的常用类型

## 1、使用CRA创建支持TS的项目

React 脚手架工具 create-react-app（简称：CRA）默认支持 TypeScript。 创建支持 TS 的项目命令：npx create-react-app 项目名称 --template typescript。 当看到以下提示时，表示支持 TS 的项目创建成功：

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220510112517.png)

更多：[在已有项目中使用 TS](https://create-react-app.dev/docs/adding-typescript/)

## 2、React支持的项目目录结构说明

相对于非 TS 项目，目录结构主要由以下三个变化：

1. 项目根目录中增加了 tsconfig.json 配置文件：指定 TS 的编译选项（比如，编译时是否移除注释）。
2. React 组件的文件扩展名变为：*.tsx。
3. src 目录中增加了 react-app-env.d.ts：React 项目默认的类型声明文件。

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220510174155.png)

有必要详细说明一下这个react-app-env.d.ts

react-app-env.d.ts：React 项目默认的类型声明文件

三斜线指令：指定依赖的其他类型声明文件，types 表示依赖的类型声明文件包的名称

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220510185326.png)

解释：告诉 TS 帮我加载 react-scripts 这个包提供的类型声明。

react-scripts 的类型声明文件包含了两部分类型：

1. react、react-dom、node 的类型
2. 图片、样式等模块的类型，以允许在代码中导入图片、SVG 等文件。



TS 会自动加载该 .d.ts 文件，以提供类型声明（通过修改 tsconfig.json 中的 include 配置来验证）

## 3、TS配置文件tsconfig.json的说明

tsconfig.json 指定：项目文件和项目编译所需的配置项。

注意：TS 的配置项非常多（100+），以 CRA 项目中的配置为例来学习，其他的配置项用到时查[文档](https://www.typescriptlang.org/zh/tsconfig)即可。

tsconfig.json 文件所在目录为项目根目录（与 package.json 同级）。

tsconfig.json 可以自动生成，命令：`tsc --init`。

```typescript
{
  //编译选项
  "compilerOptions": {
    //生成代码的语言版本
    "target": "es5",
    //指定要包含在编译中的library
    "lib": [
      "dom",
      "dom.iterable",
      "esnext"
    ],
    //允许ts编译器编译js文件
    "allowJs": true,
    //跳过声名文件的类型检查
    "skipLibCheck": true,
    //es模块化操作，屏蔽ESModule和CommonJS之间的差异
    "esModuleInterop": true,
    //允许通过import x from y，即使模块没有显示指定default导出
    "allowSyntheticDefaultImports": true,
    //开启严格模式
    "strict": true,
    //对文件名强制区分大小写
    "forceConsistentCasingInFileNames": true,
    //为switch语句启用错误报告
    "noFallthroughCasesInSwitch": true,
    //生成代码的模块化标准
    "module": "esnext",
    // 模块解析（查找）策略
    "moduleResolution": "node",
    // 允许导入扩展名为.json的模块
    "resolveJsonModule": true,
    // 是否将没有import/export的文件视为旧（全局而非模块化）脚本文件。
    "isolatedModules": true,
    //编译时 不生成任何文件（只进行类型检查）
    "noEmit": true,
    // 指定将JSX编译成什么形式
    "jsx": "react-jsx"
  },
  //指定允许ts处理目录
  "include": [
    "src"
  ]
}
```

### （1）通过命令行方式使用编译配置

除了在 tsconfig.json 文件中使用编译配置外，还可以通过命令行来使用

使用演示：tsc hello.ts --target es6

注意：

1. tsc 后带有输入文件时（比如，tsc hello.ts），将忽略 tsconfig.json 文件。 
2. tsc 后不带输入文件时（比如，tsc），才会启用 tsconfig.json。 

推荐使用：tsconfig.json 配置文件。



## 4、React中的常用类型

前提说明：现在，基于 class 组件来讲解 React+TS 的使用（最新的 React Hooks，在后面讲解）。

 在不使用 TS 时，可以使用 prop-types 库，为 React 组件提供类型检查。

 说明：TS 项目中，推荐使用 TypeScript 实现组件类型校验（代替 PropTypes）。 不管是 React 还是 Vue，只要是支持 TS 的库，都提供了很多类型，来满足该库对类型的需求。 

注意： 

1. React 项目是通过 @types/react、@types/react-dom  类型声明包，来提供类型的。
2. 这些包 CRA 已帮我们安装好（react-app-env.d.ts），直接用即可。 
3. 参考资料：[React文档-静态类型检查](https://reactjs.org/docs/static-type-checking.html) 、[React+TS备忘单](https://github.com/typescript-cheatsheets/react)

### （1）React函数组件的类型1——组件和属性的类型

函数组件的类型以及组件的属性

```typescript
import { FC } from "react"

interface Props{
    name:string,
    age?:number
}
const Demo:FC<Props> = ({name,age})=>{
    return <div>你好，我叫{name},我{age}岁了</div>
}
export default Demo;
```

实际上，还可以完全简化为（完全按照函数在TS中的写法）

```typescript
const Demo = ({name,age}:Props)=>{
    return (
        <div>你好，我叫{name}，我{age}岁了</div>
    )
}
```

### （2）React函数组件的类型2——事件绑定和事件对象

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220510205057.png)

技巧：在 JSX 中写事件处理程序（e => {}），然后，把鼠标放在 e 上，利用 TS 的类型推论来查看事件对象类型。

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220510205610.png)

### （3）class组件的类型1——组件的类型

class 组件，主要包括以下内容： 

1. 组件的类型、属性、事件 

2. 组件状态（state）

class组件的类型

```typescript
import {Component} from 'react';
interface IProps{
    message:string
}
interface IState{
    count:number
}
class Demo1 extends Component{}
class Demo2 extends Component<IProps>{}
class Demo3 extends Component<{},IState>{}
class Demo4 extends Component<IProps,IState>{}
```

### （4）class组件状态（state）和事件

![](https://gitee.com/Jeren/cloudimages/raw/master/img/20220510212055.png)
