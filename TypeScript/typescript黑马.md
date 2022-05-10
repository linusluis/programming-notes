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



解释：

1. 类似于泛型接口，在class名称后面添加<类型变量>，这个类就变成了泛型类。
2. 此处的add方法，采用的是箭头函数形式的类型书写方式。



