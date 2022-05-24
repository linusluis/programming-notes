# 内置对象 Object

## 属性

## 方法

### Object.freeze()

作用：冻结数据的结构

严格模式会报错，正常模式不起作用

```js
const foo = Object.freeze({});
foo.name = 'luis';
console.log(foo.name);//undefined
```

除了将对象本身冻结，对象的属性也应该冻结。下面是一个将对象彻底冻结的函数。

```js
varconstantize =(obj)=>{Object.freeze(obj);Object.keys(obj).forEach((key,i)=>{if(typeofobj[key]==='object'){constantize(obj[key]);}});};
```

### Object.keys(obj)


作用：方法会返回一个由一个给定对象的自身可枚举属性组成的数组，数组中属性名的排列顺序和正常循环遍历该对象时返回的顺序一致 。
