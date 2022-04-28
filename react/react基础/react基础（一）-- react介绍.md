- # 一、React介绍
  ## 1、React是什么？

  - 一句话是一个将数据渲染为HTML视图的开源JavaScripy库
  ## 2、谁开发的？
  由Facebook开发，且开源

  1. 起初由Facebook的软件工程师Jordan Walke创建

  ↓

  2. 于2011年部署于Facebook的newsfeed

  ↓

  3. 随后在2012年部署于Instagram

  ↓

  4. 2013年5月宣布开源

  .......

  5. 近十年“陈酿”React正在被腾讯、阿里等一线大厂广泛使用
  ## 3、为什么要学

  1. 原生JavaScript操作DOM繁琐、效率低（DOM-API操作UI）。
  1. 使用JavaScript直接操作DOM，浏览器会进行大量的重绘重排。
  1. 原生JavaScript没有组件化编码方案，代码复用率低
  ## 4、React的特点

  1. 采用组件化模式、声名式编码，提高开发效率及组件复用率。（与声名式对应的就是命令式编码操作。直接操作DOM就是命令式编码）
  1. 在React Native中可以使用React语法进行移动端开发（用js编写ios和Android应用）
  1. 使用虚拟DOM+优秀的Diffing算法，尽量减少与真实DOM交互（虚拟DOM没在页面上，而是代码运行时的内存里）
  - 不使用React

  ![image.png](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/%E4%BD%BF%E7%94%A8react%E7%9A%84%E6%83%85%E5%86%B5.png?Expires=1651117815&OSSAccessKeyId=TMP.3KdPGs9eyfp1x8jbNccCgWEUsYnp25cJS7SQCNBW3hghEJe2w783Wp8earitkf9CLWrEbXcQ6Xgf7weioyraQqj8NwY7Gt&Signature=GyPuy4LH8uo%2F6YqGpYzw4r5d5SU%3D&versionId=CAEQHRiBgMDZj6a4gxgiIGUzYTQ4OTJjMmU2NTQ0ZmZiZTNlMGNjN2RhMWYyZDBm)

  - 使用React

  ![image.png](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/react/react%E5%9F%BA%E7%A1%80/%E4%BD%BF%E7%94%A8react%E7%9A%84%E6%83%85%E5%86%B5.png?Expires=1651117883&OSSAccessKeyId=TMP.3KdPGs9eyfp1x8jbNccCgWEUsYnp25cJS7SQCNBW3hghEJe2w783Wp8earitkf9CLWrEbXcQ6Xgf7weioyraQqj8NwY7Gt&Signature=YrI3lMBviaCbDMp9%2Fe9Nmt6wj7w%3D&versionId=CAEQHRiBgMDZj6a4gxgiIGUzYTQ4OTJjMmU2NTQ0ZmZiZTNlMGNjN2RhMWYyZDBm)
  ## 5、学习React之前要掌握的js基础知识

  - 判断this的指向
  - class（类）
  - ES6语法规范
  - npm包管理器
  - 原型、原型链
  - 数组常用方法
  - 模块化