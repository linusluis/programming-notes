## 1、项目打包

使用`npm run build`命令，将项目打包，打包之后，生成一个build文件夹。这个文件夹就是打包之后的文件

## 2、运行打包后的项目

### （1）方式一

使用node或者java自己搭建一台服务器

### （2）方式二：使用serve库

能指定文件夹快速开启一台服务器

安装：`npm i serve -g` 

运行`serve -s build`

运行成功的标志，react dev tools 图标变量