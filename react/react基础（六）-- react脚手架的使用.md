
# 一、使用`crreate-react-app`创建react应用

## 1、什么是脚手架

xxx脚手架: 用来帮助程序员快速创建一个基于xxx库的模板项目
- 包含了所有需要的配置（语法检查、jsx编译、devServer…）
- 下载好了所有相关的依赖
- 可以直接运行一个简单效果

## 2、react脚手架
react提供了一个用于创建react项目的脚手架库: create-react-app 项目名

项目的整体技术架构为:  react + webpack + es6 + eslint

使用脚手架开发的项目的特点: 模块化, 组件化, 工程化（工程化是指如果在项目中用上了wenpack这种全自动化构建工具。也就是说你写了一段代码，它能够进行自动的代码检查，代码压缩，语法转换，兼容性处理等等一系列自动的处理，那么就可以称之为工程化的项目）

## 3、创建项目并启动
1. 第一步，全局安装：`npm i -g create-react-app`
2. 第二步，切换到想创项目的目录，使用命令：`create-react-app 项目名称`
3. 第三步，进入项目文件夹：`cd hello-react`
4. 第四步，启动项目：`npm start`
创建好项目之后可以执行的一些yarn（npm）命令：
> - yarn start：开启开发者的那个服务器 可以配置一些短命令 输入命令自动打开浏览器，自动打开页面
> - yarn build 把写完的项目最终进行一次打包，整个应用都写完了执行。前端都洗完了交给后端部署，用yarn build
> - yarn test 几乎不用 做测试用的
> - yarn eject react脚手架也得借助webpack去搭建。react脚手架默认把所有webpack相关的配置文件都隐藏了。webpack.config.js，专门用于写webpack配置的。这个文件不能乱改，所以react将类似这样的文件都隐藏了。执行了这个命令就相当于把webpack的所有配置都暴露出来了，就不能再隐藏了

## 4、脚手架的文件结构

![脚手架的文件结构](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/%E8%84%9A%E6%89%8B%E6%9E%B6%E7%9A%84%E6%96%87%E4%BB%B6%E7%BB%93%E6%9E%84.png?Expires=1651562244&OSSAccessKeyId=TMP.3KkF7HmnjGLLU6WjcUPxRguNC5X47w9qF26VZh1ZiDBibkZBmQMobdb4DjMDh6djvunX14h9X5SoAGnt8F7KvGJebjjGXA&Signature=KUsr%2Bo5xrjnwYpwq%2FZ9uY%2B%2BZrus%3D&versionId=CAEQHRiBgICf36CihBgiIGI2ZGFkOThjZjMwYjQyYjRhMDAxNTEzMThlOGU4MzRi)

下面我们介绍一些主要的文件

1. `public/index.html`
```javascript
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <!-- %PUBLIC_URL%代表public文件夹的路径 -->
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <!-- 开启理想视口，用于做移动端网页的适配 -->
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <!-- 用于配置浏览器页签+地址栏的颜色（仅支持安卓手机浏览器） -->
    <meta name="theme-color" content="#000000" />
    <meta
      name="description"
      content="Web site created using create-react-app"
    />
    <!-- 用于指定网页添加到手机主屏幕后的图标 -->
    <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
    <!-- 应用加壳时的配置文件 -->
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    
    <title>React App</title>
  </head>
  <body>
    <!-- 若浏览器不支持js则展示标签中的内容 -->
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
    
  </body>
</html>
```


2.`src\App.js` 
```javascript
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}
//导出App模块
export default App;
```

3. `src\index.js` 入口文件
```javascript
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  //这个是做检查的，检查App组件及其子组件是否合理
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
reportWebVitals();
```

## 5、整个项目的启动过程

执行src下的index.js（入口文件）,引入react核心库，reactDOM，引入样式，引入App组件（App组件中引入的是自己写的组件）===>触发ReactDOM.render。把App组件渲染到root容器。然后public中执行到index.html，找到root节点，渲染到界面。

## 6、功能界面的组件化编码流程（通用） 非常重要 

1. 拆分组件：拆分界面，抽取组件
2. 实现静态组件：使用组件实现静态页面效果
3. 实现动态组件
- 动态显示初始化数据
    - 数据类型
    - 数据名称
    - 保存在哪个组件
- 交互（从绑定事件监听开始）
