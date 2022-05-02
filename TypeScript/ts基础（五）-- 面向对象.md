
面向对象是程序中一个非常重要的思想，它被很多人理解成了一个比较难，比较深奥的东西，其实不然。面向对象很简单，简而言之就是程序之中所有的操作都需要通过对象来完成。  

举例来说：
- 操作浏览器要使用window对象
- 操作网页要使用document对象
- 操作控制台要使用console对象

一切操作都要通过对象，也就是所谓的面向对象，那么对象到底是什么，计算机程序的本质就是对现实事物的抽象，抽象的反义词是具体，比如：照片是对一个具体的人的抽象，汽车模型是对具体汽车的抽象等等。程序也是对事物的抽象，在程序中我们可以表示一个人、一条狗、一把枪、一颗子弹等等所有的事物。一个事物到了程序中就变成了一个对象。  

在程序中所有的对象都被分成了两个部分：数据和功能，以人为例，人的姓名、性别、年龄、身高、体重等属于数据，人可以说话、走路、吃饭、睡觉这些属于人的功能。数据在对象中被称为属性，而功能就被称为方法。所以简而言之，在程序中一切皆对象。
## 1、类
要想面向对象，操作对象，首先便要拥有对象。  

要创建对象，必须要先定义类，所谓的类可以理解为对象的模型。

程序中可以根据类创建指定类型的对象。

举例来说：
可以通过Person类来创建人的对象，通过Dog类创建狗逇对象，不同的类可以用来创建不同的对象。

### （1）定义类

直接定义的属性是实例属性，需要通过对象的实例去访问：
```javascript
const per = new Person();
per.name
```

使用static开头的属性是静态属性（类属性），可以直接通过类去调用

```javascript
Person.age
```

readonly开头的属性表示一个只读的属性，无法修改
```javascript
static readobly age:number = 18
```

如果方法以static开头则方法就是类方法或者叫静态方法，可以直接通过类去调用

示例：
```typescript
    class Person{
    //定义实例属性
    name:string = '孙悟空';
    // age:number = 18;
    //在属性前使用static关键字可以定义类属性（静态属性）
    static age:number = 18;
    //定义实例方法，该类的所有实例都可以调用
    fun(){
        console.log('fun');
    }
    //定义静态方法，只有类可以调用
    static fun2(){
        console.log('staticfun2');
    }
}
const per = new Person();
console.log(per.name);
console.log(Person.age);
Person.fun2();
per.fun();
```
### （2）构造函数

可以使用constructor定义一个构造器方法；  

> 注1：在TS中只能有一个构造器方法！
```typescript
class Dog{
    //要提前声名变量的类型，否则会报错
    name:string;
    age:number;
    // constructor被称为构造函数
    // 构造函数会在对象创建时调用
    constructor(name:string,age:number){
        //在实例方法中，this就表示当前的实例
        // 在构造函数中当前对象就是当前新建的那个对象
        // 可以通过this向新建的对象中添加属性
        this.name = name;
        this.age = age;
        console.log(this);
    }

    bark(){
        // alert('汪汪汪');
        //在方法中可以通过this来表示当前调用方法的对象
        console.log(this.name);
    }
}
const dog = new Dog('小黑',2);
const dog2 = new Dog('小白',3);
const dog3 = new Dog('小花',5);
console.log(dog);
dog2.bark();
```
同时也可以将属性的类型在构造函数中声名
```typescript
class Dog{
    constructor(public name:string, public age:number){
            //在实例方法中，this就表示当前的实例
            // 在构造函数中当前对象就是当前新建的那个对象
            // 可以通过this向新建的对象中添加属性
            this.name = name;
            this.age = age;
            console.log(this);
        }
}
```
上面两种定义方法是完全相同的！

### （3）继承

>注意：子类继承父类时，必须调用父类的构造方法，使用super（如果子类中也定义了构造方法）

继承的代码举例：
```typescript
 // 定义一个动物类
    class Animal{
        name:string;
        age:number;
        constructor(name:string,age:number){
            this.name = name;
            this.age = age;
        }
        sayHello(){
            console.log(this.name);
        }
    }

    /*
    Dog extends Animal
    此时，Animal被称为父类，Dog被称为子类
    使用继承后，子类将会拥有父类所有的方法和属性
    通过继承可以将多个类中共有的代码写在一个父类中，这样
    只需要写一次即可让子类同时拥有父类中的属性和方法
    如果希望在子类中添加一些父类总没有的属性或方法直接加就行
    如果在子类中添加了和父类相同的方法，则子类方法会覆盖掉父类的方法
    这种子类覆盖掉父类方法的形式，称为方法重写
    */
    // 定义一个表示狗的类
    // 使Dog继承Animal类
    class Dog extends Animal{
        gender:string;
        constructor(name:string,age:number,gender:string){
            //如果子类中写了构造函数，在子类构造函数中必须对父元素的构造函数进行调用
            super(name,age);//调用父类的构造函数
            this.gender = gender;
        }

        run(){
            console.log(this.name+'在跑');
        }
        sayHello(){
            // 在类的方法中，super就表示当前类的父类
            super.sayHello();
        }
    }
    // 定义一个表示猫的类
    //使Cat类继承Animal类
    class Cat{

    }
    const dog = new Dog('旺财',5,'male');
    const cat = new Dog('猫咪',3,'female');
    console.log(dog);
    dog.sayHello();
    dog.run();
    console.log(cat);
    cat.sayHello();
```


## 2、抽象类
1. 抽象类
>以`abstract`开头的类是抽象类，抽象类和其他类区别不大，只是不能用来创建对象。
>抽象类就是专门用来被继承的类
>抽象类中可以添加抽象方法

2. 抽象方法
>抽象方法使用abstract开头，**没有方法体**。
>抽象方法只能定义在抽象类中，子类必须对抽象方法进行重写。

抽象类举例：
```typescript
//定义了一个抽象类
//开头的类是抽象类，抽象类和其他类区别不大，只是不能用来创建对象。
//抽象类就是专门用来被继承的类
// 抽象类中可以添加抽象方法
abstract class Animal{
    name:string;
    constructor(name:string){
        this.name = name;
    }
    // 抽象方法使用abstract开头，**没有方法体**
    // 抽象方法只能定义在抽象类中，子类必须对抽象方法进行重写。
    abstract sayHello():void;
}

class Dog extends Animal{
    sayHello(): void {
        console.log('汪汪汪');
    }
}
const dog = new Dog('旺财');
```

## 3、接口（Interface）

接口的作用类似于抽象类，不同点在于：接口中的所有方法和属性都是没有实值的，换句话说接口中的所有方法都是抽象方法。

接口主要有两个作用：
1. 接口可以用来描述一个对象的类型：对象只有包含接口中定义的所有属性和方法才能匹配接口

在之前的ts类型的学习中，我们知道通过起别名的方式，可以给变量指定一种类型，如下列代码：将obj指定为myType类型
```typescript
// 描述一个对象的类型
type myType = {
    name:string,
    age:number
}
const obj:myType = {
    name:'hello',
    age:19
}
```

此外，通过接口可以实现和上述代码相同的功能

```typescript
//可以使用接口实现和上述代码一样的功能，即也能为obj指定一个类型
interface myInterface{
    name:string;
    age:number;
}
//此外，接口可重复定义，而起别名的方式则不能。
//重复定义的接口会合并，如下：
interface myInterface{
    gender:string;
}
const obj:myInterface = {
    name:'hello',
    age:19,
    gender:'male'//如果不指定gender会报错
}
```

2. 接口主要负责定义一个类的结构，可以让一个类去实现接口，实现接口时必须把接口中的所有属性和所有的方法在类中实现。

```typescript
//定义一个接口
interface myInter{
    name:string;
    sayHello():void;
}

//定义类式，可以使类去实现一个接口,
//实现接口就是使类去满足接口的要求
class MyClass implements myInter{
    name: string;
    constructor(name:string){
        this.name = name;
    }
    sayHello(): void {
        console.log('大家好');
    }  
}
```

## 4、属性的封装


对象实质上就是属性和方法的容器，它的主要作用就是存储属性和方法，这就是所谓的封装。

默认情况下对象的属性是可以任意的修改的，为了确保数据的安全性，在TS中可以对属性的权限进行设置
- 静态属性（static）
    - 声名为static的属性或方法不在属于实例，而是属于类的属性。
- 只读属性（readonly）：
    - 如果在声明属性时添加一个readonly，则属性便成了只读属性无法修改
- TS中属性具有三种修饰符：
    - public（默认值），可以在类、子类和对象中修改
    - protected，可以再类、子类中修改
    - private，可以在类中修改

- 示例：

public
```typescript
class Person{
    public name: string; // 写或什么都不写都是public
    public age: number;

    constructor(name: string, age: number){
        this.name = name; // 可以在类中修改
        this.age = age;
    }

    sayHello(){
        console.log(`大家好，我是${this.name}`);
    }
}

class Employee extends Person{
    constructor(name: string, age: number){
        super(name, age);
        this.name = name; //子类中可以修改
    }
}

const p = new Person('孙悟空', 18);
p.name = '猪八戒';// 可以通过对象修改
```

protected

```typescript
class Person{
    protected name: string;
    protected age: number;

    constructor(name: string, age: number){
        this.name = name; // 可以修改
        this.age = age;
    }

    sayHello(){
        console.log(`大家好，我是${this.name}`);
    }
}

class Employee extends Person{

    constructor(name: string, age: number){
        super(name, age);
        this.name = name; //子类中可以修改
    }
}

const p = new Person('孙悟空', 18);
p.name = '猪八戒';// 不能修改
```

private
```typescript
class Person{
    private name: string;
    private age: number;

    constructor(name: string, age: number){
        this.name = name; // 可以修改
        this.age = age;
    }

    sayHello(){
        console.log(`大家好，我是${this.name}`);
    }
}

class Employee extends Person{

    constructor(name: string, age: number){
        super(name, age);
        this.name = name; //子类中不能修改
    }
}

const p = new Person('孙悟空', 18);
p.name = '猪八戒';// 不能修改
```


对于类中一些不希望被修改的属性，可以将其设置为private。

直接将其设置为private将导致无法再通过对象修改其中的属性。

我们可以在类中定义一组读取、设置属性的方法，这种对属性读取或设置的属性被称为属性的存取器

读取属性的方法叫做setter方法，设置属性的方法叫做getter方法。

在ts中也可以像java一样定义和调用getName,setName。此外，在ts中我们通过get和set关键字来定义这两种方法，调用的时候，也很方便，代码示例如下：

示例：
```typescript
class Person{
    private _name: string;

    constructor(name: string){
        this._name = name;
    }

    get name(){
        return this._name;
    }

    set name(name: string){
        this._name = name;
    }
}
const p1 = new Person('孙悟空');
// 实际通过调用getter方法读取name属性
console.log(p1.name);
// 实际通过调用setter方法修改name属性 
p1.name = '猪八戒'; 
```

## 5、泛型

定义一个函数或类时，有些情况下无法确定其中要使用的具体类型（返回值、参数、属性的类型不能确定）
此时，泛型便能够发挥作用；
举个例子：
```typescript   
function test(arg: any): any{
    return arg;
}
```

上例中，test函数中有一个参数类型不确定，但是能确定的是其返回值的类型和参数的类型是相同的。

由于类型不确定所以参数和返回值均使用了any，但是很明显这样做是不合适的：

首先使用any会关闭TS的类型检查，其次这样设置也不能体现出参数和返回值是相同的类型。

### （1）泛型函数

创建泛型函数  
```typescript
function test<T>(arg: T): T{
    return arg;
}
```

这里的<T>就是泛型。

T是我们给这个类型起的名字（不一定非叫T），设置泛型后即可在函数中使用T来表示该类型。

所以泛型其实很好理解，就表示某个类型

那么如何使用上边的函数呢？

使用泛型函数

方式一（直接使用）：
```typescript
test(10);
```
使用时可以直接传递参数使用，类型会由TS自动推断出来，但有时编译器无法自动推断时还需要使用下面的方式。

方式二（指定类型）：

```typescript
test<number>(10);
```
也可以在函数后手动指定泛型

函数中声名多个泛型

可以同时指定多个泛型，泛型间使用逗号隔开：
```typescript   
function test<T, K>(a: T, b: K): K{
  return b;
}

test<number, string>(10, "hello");
```
使用泛型时，完全可以当成是一个普通的类去使用

### （2）泛型类
类中同样可以使用泛型

```typescript
class MyClass<T>{
  prop: T;

  constructor(prop: T){
      this.prop = prop;
  }
}
```

### (3)泛型继承
除此之外，也可以对泛型的范围进行约束

```typescript
class MyClass<T>{
  prop: T;

  constructor(prop: T){
      this.prop = prop;
  }
}
```

使用T extends MyInter表示泛型T必须是MyInter的子类。
