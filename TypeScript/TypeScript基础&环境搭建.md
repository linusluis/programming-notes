## 1、TypeScript是什么？

> 1. 以javaScript为基础构建的语言
> 2. 一个javaScript的超集
> 3. 可以在任何平台上支持javaScript的平台中执行
> 4. TypeScript扩展了javaScript，并添加了类型
> 5. TS不能被JS解析器直接执行，需要先编译成JS

## 2、TypeScript增加了什么？
> - 类型
> - 支持ES的新特性
> - 添加ES不具备的新特性：抽象类、接口、装饰器等
> - 丰富的配置选项：严格和松散可以相互切换
> - 强大的开发工具
> - 可以被编译成任何一个版本的js,以解决兼容性问题

## 3、TS开发环境搭建

### （1）下载Node.js

- https://nodejs.org/zh-cn/download/

### （2）安装Node.js

### （3）使用npm全局安装typescript

- 进入命令行
- 输入：`npm i -g typescript`

### （4）创建一个ts文件

### （5）使用tsc对文件进行编译

- 进入命令行
- 进入ts文件所在目录
- 执行命令`tsc xxx.ts`