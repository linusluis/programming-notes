## 1、CSS简介
CSS(Cascading Style Sheet)：层叠样式表

- 网页实际上是一个多层的结构，通过CSS可以分别为网页的每一个层来设置样式。而最终我们能够看到的只是网页的最上边一层
- 总之一句话，CSS用来设置网页中元素的样式
## 2、CSS编写位置
### 2-1 第一种方式（内联样式，行内样式）

- 在标签内部通过style属性来设置元素的样式
- 问题：
   - 使用内联样式，样式只能对一个标签生效，如果希望影响到多个元素必须在每一个元素中都复制一遍。并且当样式发生变化时，我们必须要一个一个的修改，非常的不方便
- **注意：**开发时绝对不要使用内联样式
### 2-2 第二种方式（内部样式表）

- 将样式编写到head中的style标签里。然后通过CSS的选择器来选中元素并为其设置各种样式。可以同时为多个标签设置样式，并且修改时只需要修改一处即可全部应用
- 内部样式表更加方便对样式进行复用
- 问题：
   - 我们的内部样式表只能对一个网页起作用，它里边的样式不能跨页面进行复用
### 2-3 第三种方式（外部样式表）最佳实践

- 可以将CSS样式编写到一个外部的CSS文件中,然后通过link标签来引入外部的CSS文件
- 外部样式表需要通过link标签进行引入，意味着只要想使用这些样式的网页都可以对其进行引用。使样式可以在不同页面之间进行复用
- 将样式编写到外部的CSS文件中，可以使用到浏览器的缓存机制，从而加快网页的加载速度，提高用户的体验
## 3、CSS基本语法

- 选择器 声明块
- 选择器，通过选择器可以选中页面中的指定元素
   - 比如 p 的作用就是选中页面中所有的p元素
- 声明块，通过声明块来指定要为元素设置的样式
   - 声明块是由一个一个的声明组成
   - 声明时一个名值对结构
   - 一个样式名对应一个样式值，名和值之间以：连接，以；结尾


## 4、CSS选择器
### 4-1常用选择器
#### （1）元素选择器

- 作用：根据标签名来选中指定的元素
- 语法：标签名{}
- 例子：p{}   h1{}    div{}
#### （2） id选择器

- 作用：根据元素的id属性值选中一个元素
- 语法：#id属性值{}
- 例子：#box{}   #red{}
#### （3） 类选择器

- 作用：根据元素的class属性值选中一组元素
- 语法：.class属性值
- ①class是一个标签的属性，它和id类似，不同的是class可以重复使用。
②可以通过class属性来为元素分组。
③可以同时为一个元素指定多个class属性
#### （4） 通配选择器

- 作用：选中页面中的所有元素
- 语法：*{}
### 4-2复合选择器
#### （1） 交集选择器

- 作用：选中同时符合多个条件的元素
- 语法：选择器1选择器2选择器3选择器n{}
- 注意点：交集选择器如果有元素选择器，必须使用元素选择器开头
#### （2） 选择器分组（并集选择器）

- 作用：同时选择多个选择器对应的元素
- 语法：选择器1，选择器2，选择器3，选择器n{}
- ,叫做结合符
### 4-3关系选择器
#### （1） 元素之间的关系

- 父元素
   - 直接包含子元素的元素叫做父元素
- 子元素
   - 直接被父元素包含的元素是子元素
- 祖先元素
   - 直接或间接包含后代元素的元素叫做祖先元素
   - 一个元素的父元素也是它的祖先元素
- 后代元素
   - 直接或间接被祖先元素包含的元素叫做后代元素
   - 子元素也是后代元素
- 兄弟元素
   - 拥有相同父元素的元素是兄弟元素
#### （2） 子元素选择器

- 作用：选中指定父元素的指定子元素
- 语法：父元素 > 子元素
#### （3） 后代元素选择器

- 作用：选中指定元素内的指定后代元素
- 语法 祖先 后代
#### （4） 兄弟选择器

- 选择下一个兄弟
   - 语法：前一个+下一个
   - 要求紧挨！！！
- 选择下边所有的兄弟
   - 语法：兄~弟
### 4-4属性选择器

- [属性名] 选择含有指定属性的元素
- [属性名=属性值]选择含有指定属性和属性值的元素
- [属性名^=属性值]选择属性值以指定值开头的元素
- [属性名$=属性值]选择属性值以指定值结尾的元素
- [属性名*=属性值]选择属性值中含有某值的元素
### 4-5伪类选择器

- 伪类（不存在的类，特殊的类）
   - 比如：第一个子元素、被点击 的元素、鼠标移入的元素。。。。。。
   - 伪类一般都是用:开头
      - :first-child 第一个子元素
      - :last-child 最后一个子元素
      - :nth-child() 选中第n个子元素
      - 特殊值：
         - n 第n个 n的范围0到正无穷
         - 2n 或 even 表示选中偶数位的元素
         - 2n+1 或 odd 表示选中奇数位的元素

   - 以上这些伪类都是根据所有的子元素进行排序
      - :first-of-type
      - :last-of-type
      - :nth-of-type()
      - 这几个伪类的功能和上述的类似，不同点是他们是在同类型元素中进行排序
   - :not() 否定伪类
      - 将符合条件的元素从选择器中去除
   - :empty
      - 内容必须是空的，有空格都不行，有属性没关系
### 4-6超链接的伪类

- :link 用来表示没访问过的链接（正常的链接）
- :visited 用来表示访问过的链接
   - 由于隐私的原因，所以visited这个伪类只能修改链接的颜色
- :hover 用来表示鼠标移入的状态
- :active 用来表示鼠标点击

在页面中写超链接伪类的时候，一定要遵循上述的顺序，否则，:hover和:active将不会生效

- :target 代表一个特殊的元素，它的ID是URI的片段标识符
### 4-7伪元素

- 伪元素表示页面中一些特殊并不真实存在的元素（特殊的位置）
- 伪元素使用::开头
- ::first-letter 表示第一个字母
- ::first-line 表示第一行
- ::selection 表示选中的内容
- ::before 元素的开始 
- ::after 元素的最后
   - before 和 after 必须结合content属性来使用
   - 注意：input标签使用伪元素不生效
### 4-8选择器的权重

- 样式的冲突：当我们通过不同的选择器，选中相同的元素，并且为相同的样式设置不同的值时，此时就发生了样式的冲突。
- 发生样式冲突时，应用哪个样式由选择器的权重（优先级）决定
- 选择器的权重
   - 内联样式              1,0,0,0
   - id选择器               0,1,0,0
   - 类和伪类选择器   0,0,1,0
   - 元素选择器          0,0,0,1
   - 通配选择器           0,0,0,0
   - 继承的样式           没有优先级
- 比较优先级时，需要将所有的选择器的优先级进行相加计算，最后优先级越高，则越优先显示（分组选择器是单独计算的）,选择器的累加不会超过其最大的数量级，类选择器再高也不会超过id选择器。
- 如果优先级计算后相同，此时则优先使用靠下的样式
- 可以在某一个样式的后边添加 !important ，则此时该样式会获取到最高的优先级，甚至超过内联样式，**注意：**在开发中这个玩意一定要慎用！

## 5、继承

- 样式的继承，我们为一个元素设置的样式同时也会应用到它的后代元素上
- 继承是发生在**祖先和后代**之间的
- 继承的设计是为了方便我们的开发，利用继承我们可以将一些通用的样式统一设置到共同的祖先元素上，这样只需设置一次即可让所有的元素都具有该样式
- **注意：**并不是所有的样式都会被继承：
   - 比如 背景相关的，布局相关等的这些样式都不会被继承。
## 6、单位
### 6-1 像素
#### pc端的像素

- 屏幕（显示器）实际上是由一个一个的小点点构成的，这一个个的小点就是像素
- 分辨率1920*1080说的就是屏幕中小点的数量
- 在前端开发中像素要分成两种情况讨论：**CSS像素** 和 **物理像素**
- 物理像素：上述所说的小点点就属于物理像素
- CSS像素：编写网页时，我们所用像素都是CSS像素
- **浏览器在显示网页时，需要将CSS像素转换为物理像素然后再呈现**

一个CSS像素最终由几个物理像素显示，由浏览器或电脑的缩放比例决定
默认情况下在pc端：一个CSS像素 = 一个物理像素
#### 移动端的像素
在不同的屏幕，单位像素的大小是不同的，像素越小屏幕会越清晰
计算机 	24寸  1920*1080
iphone6	7寸    750*1334
智能手机的像素点远远小于计算机的像素点

问题：一个宽度为900px的网页在iphone6中要如何显示呢？，答案是完整显示，而且还有空缺部分
默认情况下，移动端的网页都会将视口设置为980像素（CSS像素），以确保pc端网页可以在移动端正常访问，但是如果网页的宽度超过了980，移动端的浏览器会自动对网页缩放以完整显示网页。

多以基本大部分的PC端网站都可以在移动端中正常浏览，但是往往都不会有一个好的体验，为了解决这个问题，大部分网站都会专门为移动端设计网页。

### 6-2 视口
视口就是屏幕中用来显示网页的区域
可以通过查看视口的大小。来观察CSS像素和物理像素的比值
默认情况下：
视口宽度 1920px（CSS像素）
 1920px（物理像素）
此时，css像素和物理像素的比是1:1
放大两倍的情况
视口宽度 960px（CSS像素）
 1920px（物理像素）
此时，css像素和物理像素的比是1:2
因此，我们可以通过改变视口的大小，来改变css像素和物理像素的比值

#### 完美视口
移动端默认的视口大小是980px(css像素)
默认情况下，移动端的像素比就是980/移动端宽度	（980/750）
如果我们直接在网页中编写移动端代码，这样在980的视口下，像素比是非常不好，导致网页中的内容非常非常的小
编写移动端页面时，必须要确保有一个比较合理的像素比：
1css像素 对应 2个物理像素
1css像素 对应 3个物理像素
可以通过meta标签来设置视口大小

每一款移动设备设计时，都会有一个最佳的像素比。一般我们只需要将像素比设置为该值即可得到一个最佳效果。将像素比设置为最佳像素比的视口大小我们称其为完美视口。

将网页的视口设置为完美视口
`<meta name="viewpoint" content="width=device-width,initial-scale=1.0">`

结论：以后再写移动端的页面，就把上边这个玩意先写上。

### 6-3vw(viewpoint width) 视口宽度
不同设备完美视口的大小是不一样的
iphone6 --- 375
iphone6plus --- 414
由于不同设备视口和像素比不同，所以同样的375个像素在不同设备下意义是不一样的，比如在iphone6中375就是全屏，而到了plus中375就会缺一块
所以在移动端开发时，就不能再使用px来进行布局了
vw表示的是视口的宽度（viewpoint width）
100vw = 一个视口的宽度
1vw=1%视口的宽度
vw这个单位永远相当于视口宽度进行计算
例如：创建一个48px*35px大小的元素
100vw = 750px（设计图的像素） 0.1333333333vw = 1px
6.4vw = 48px
4.667vw = 35px
但是，上述计算很麻烦。
我们可以使用rem来代替上述方式。

- 首先需要给html用vw单位设置一个字体大小，但是网页中字体大小最小是12px，不能设置一个比12像素还小的字体。如果我们设置了一个小于12px的字体，则字体自动设置为12px
- 所以我们给html用vw单位设置一个大于12px的字体，京东设置的是`font-size:5.3333vw;`，即1rem=5.3333vw=40px（设计图像素）
- 然后在应用的时候自己算就OK了

### 6-4 百分比

- 也可以将属性值设置为相对于其父元素属性的百分比
- 优点：设置百分比可以使子元素跟随父元素的改变而改变
```css
.box2{
            width: 50%;
            height: 50%;
            background-color:aqua; 
        }
```
### 6-5 em和rem

- em是相对于元素的字体大小来计算的,网页中默认字体大小为16px
- 1em = 1font-size
- em会根据字体大小的改变而改变

rem是相对于根元素的字体大小来计算,也就是`<html>`元素，如果不指定的话，根元素默认字体大小也为16px

## 7、颜色
### 7-1 RGB值

- 在CSS中可以直接使用颜色名来设置各种颜色
   - 比如：red、orange、yellow、blue、green ... ...
   - 但是在css中直接使用颜色名是非常的不方便
- RGB值：
   - RGB通过三种颜色的不同浓度来调配出不同的颜色
   - R red，G green ，B blue
   - 每一种颜色的范围在 0 - 255 (0% - 100%) 之间
   - 语法：RGB(红色,绿色,蓝色)
- RGBA:
   - 就是在rgb的基础上增加了一个a表示不透明度
   - 需要四个值，前三个和rgb一样，第四个表示不透明度
      - 1表示完全不透明   0表示完全透明  .5半透明
- 十六进制的RGB值：
   - 语法：#红色绿色蓝色
   - 颜色浓度通过 00-ff
   - 如果颜色两位两位重复可以进行
      - 简写 :#aabbcc --> #abc

### 7-2 HSL值

- H 色相(0 - 360)
- S 饱和度，颜色的浓度 0% - 100%
- L 亮度，颜色的亮度 0% - 100%

## 8、文档流（normal flow）

- 网页是一个多层的结构，一层摞着一层
- 通过CSS可以分别为每一层来设置样式
- 作为用户来讲只能看到最顶上一层
- **这些层中，最底下的一层称为文档流，文档流是网页的基础**
- 我们所创建的元素默认都是在文档流中进行排列
- 对于我们来元素主要有两个状态
   - 在文档流中
   - 不在文档流中（脱离文档流）
- 元素在文档流中有什么特点：
   - 块元素:
      - 块元素会在页面中独占一行(自上向下垂直排列)
      - 默认宽度是父元素的全部（会把父元素撑满），也可以说成是auto 
      - 默认高度是被内容撑开（子元素）
   - 行内元素
      - 行内元素不会独占页面的一行，只占自身的大小
      - 行内元素在页面中左向右水平排列，如果一行之中不能容纳下所有的行内元素则元素会换到第二行继续自左向右排列（书写习惯一致）
      - 行内元素的默认宽度和高度都是被内容撑开
      - 行内元素不能设置上下内外边距是无效的。

## 9、盒子模型
### 9-1 盒模型
盒模型、盒子模型、框模型（box model）

- CSS将页面中的所有元素都设置为了一个矩形的盒子
- 将元素设置为矩形的盒子后，对页面的布局就变成将不同的盒子摆放到不同的位置
- 每一个盒子都由以下几个部分组成：
   - 内容区（content）
   - 内边距（padding）
   - 边框（border）
   - 外边距（margin）
### 9-2 盒模型-内容区
 内容区（content），元素中的所有的子元素和文本内容都在内容区中排列

- 内容区的大小由width 和 height两个属性来设置
   - width 设置内容区的宽度（默认值是auto）
   - height 设置内容区的高度
### 9-3 盒子模型-边框
边框（border），边框属于盒子边缘，边框里边属于盒子内部，出了边框都是盒子的外部

- **边框的大小会影响到整个盒子的大小**
- 要设置边框，需要至少设置三个样式：
   - 边框的宽度 border-width
   - 边框的颜色 border-color
   - 边框的样式 border-style
- border-width：
   - border-width如果不写则有默认值：一般是3像素
   - border-width可以用来指定四个方向的边框的宽度
      - 值的情况：
      - 四个值：上  右  下  左
      - 三个值：上  左右 下
      - 两个值：上下  左右
      - 一个值：上下左右
   - 除了border-width还有一组 border-xxx-width（xxx可以是 top right bottom left），用来单独指定某一个边的宽度
```css
border-top-width:10px;
border-right-width:20px;
border-bottom-width:30px;
border-left-width:40px;
```

- border-color:
   - border-color用来指定边框的颜色，同样可以分别指定四个边的边框
   - 规则和border-width一样
   - border-color也可以省略不写，如果省略了则自动使用color的颜色值。color是前景色，一般指定字体，边框等的颜色。而background-color是背景色
```css
color:red;
/*此时，如果不指定border-color,则border-color会有默认值，为red*/
```

- border-style ：
   - border-style指定边框的样式
      - solid 表示实线
      - dotted 点状虚线
      - dashed 虚线
      - double 双线
   - border-style的默认值是none 表示没有边框
- border简写属性，通过该属性可以同时设置边框所有的相关样式，并且没有顺序要求
```css
border:10px red solid;
```

- 除了border以外还有四个border-xxx
   - border-top
   - border-right
   - border-bottom
   - border-left
### 9-4 盒子模型-内边距

- 内边距（padding）是内容区和边框之间的距离！
- 一共有四个方向的内边距：
   - padding-top
   - padding-right
   - padding-bottom
   - padding-left
- **内边距的设置会影响到盒子的大小**
- 背景颜色会延伸到内边距上
- 一个盒子的可见框大小，由内容区、内边距和边框共同决定，所以在计算盒子大小时，需要将这三个区域加到一起计算。
### 9-4 盒子模型-外边距

- 外边距（margin）
   - 外边距不会影响盒子可见框的大小
   - 但是外边距会影响盒子的位置
- 一共有四个方向的外边距：
   - margin-top
      - 上外边距，设置一个正值，元素会向下移动
   - margin-right
      - 默认情况下设置margin-right不会产生任何效果
   - margin-bottom
      - 下外边距，设置一个正值，下边的元素会向下移动
   - margin-left
      - 左外边距，设置一个正值，元素会向右移动
- margin也可以设置负值，如果是负值则元素会向相反的方向移动
- 元素在页面中是按照自左向右的顺序排列的，所以默认情况下如果我们设置的左和上外边距则会移动元素自身。而设置下和右外边距会移动其他元素
- margin的简写属性
   - margin可以同时设置四个方向的外边距，用法和padding一样
- **margin不会影响盒子可见框的大小，但是会影响盒子实际占用空间**
### 9-5行内元素的盒模型

- 行内元素不支持设置宽、高
- 但是支持设置padding、margin、border，但是垂直方向上padding、margin、border不会影响页面的布局，也就是说对元素在页面中的位置不会有影响。
- display用来设置元素显示的类型
   - 可选值：
      - inline 将元素设置为行内元素
      - block 将元素设置为块元素
      - inline-block行内块元素，兼具行内元素和块元素的优点既不会独占一行，也可以设置宽和高。但是也兼具行内元素和块元素的缺点。如果是两个相邻的行内块元素，则会有一个空隙，是空格导致的。如果把空格删掉，就不会有空隙了。尽量不用
      - table 将元素设置为一个表格
      - none 元素不在页面中显示
- visibility 用来设置元素的显示状态
   - 可选值： 
      - visible 默认值，元素在页面中正常显示
      - hidden 元素在页面中隐藏 不显示，但是依然占据页面的位置



## 10、布局
### 10-1盒模型布局
#### ★★★盒子模型水平方向的布局

- 元素在其父元素中水平方向的位置由以下几个属性共同决定
   - margin-left
   - border-left
   - padding-left
   - width
   - padding-right
   - border-right
   - margin-right
- 一个元素在其父元素中，水平布局必须要满足以下的等式：
   - margin-left+border-left+padding-left+width+padding-right+border-right+margin-right=其父元素内容区的宽度（必须满足）
   - 以上等式必须满足，如果相加结果使等式不成立，则称为过渡约束，则等式会自动调整
   - 调整的情况：
      - 如果这七个值中没有auto的情况，则浏览器会自动调整margin-right值以使等式满足
      - 这七个值中有三个值可以设置为auto:
         - width
         - margin-left
         - margin-right
      - 如果某个值为auto，则会自动调整为auto的那个值以使等式成立
      - 如果将一个宽度和一个外边距设置为auto，则宽度会调整到最大，设置为auto的外边距会自动为0
      - 如果将三个值都设为auto，则外边距都是0，宽度最大
      - 如果将两个外边距设置为auto，宽度固定值，则会将外边距设置为相同的值
         - 所以我们经常利用这个特点来使一个元素在其父元素中水平居中
         - 实例：
```css
width:20px;
margin:0 auto;
```
#### 盒子模型垂直方向的布局

- 默认情况下父元素的高度被内容撑开
- 子元素时再父元素的内容区中排列的，如果子元素的大小超过了父元素，则子元素会从父元素中溢出
- 使用 overflow 属性来设置父元素如何处理溢出的子元素
- 可选值：
   - visible，默认值 子元素会从父元素中溢出，在父元素外部的位置显示
   - hidden 溢出内容将会被裁剪不会显示
   - scroll 生成两个滚动条，通过滚动条来查看完整的内容
   - auto 根据需要生成滚动条
- 除此之外，还可以设置overflow-x,overflow-y
#### ★★垂直外边距的重叠
相邻的垂直方向外边距会发生重叠现象

- 兄弟元素
   - 兄弟元素间的相邻垂直外边距会取两者之间的较大值（两者都是正值）
   - 特殊情况：
      - 如果相邻的外边距一正一负，则取两者的和
      - 如果相邻的外边距都是负值，则取两者中绝对值较大的
   - 兄弟元素之间的外边距的重叠，对于开发是有利的，所以我们不需要进行处理
- 父子元素
   - 父子元素间相邻外边距，子元素的会传递给父元素（上外边距）
   - 父子外边距的折叠会影响到页面的布局，必须要进行处理
   - 暂时有两种处理方法：
      - 1、不使用margin;使用padding。将子元素向下挤，然后修改父元素内容的高度height
      - 2、使父元素和子元素的外边界不一致，通过增加border的方式，使的父元素和子元素的外边界不一致。
### 10-2浮动布局    
#### ★★★浮动的简介
通过浮动可以使一个元素向其父元素的左侧或右侧移动

- 使用 float 属性来设置于元素的浮动
- 可选值：
   - none:默认值 ，元素不浮动
   - left 元素向左浮动
   - right 元素向右浮动
- **注意**：
   - 元素设置浮动以后，水平布局的等式便不需要强制成立。
   - 元素设置浮动以后，会完全从文档流中脱离，不再占用文档流的位置，所以元素下边的还在文档流中的元素会自动向上移动
- 浮动的特点：
   - 1、浮动元素会完全脱离文档流，不再占据文档流中的位置
   - 2、设置浮动以后元素会向父元素的左侧或右侧移动
   - 3、浮动元素默认不会从父元素中移出
   - 4、浮动元素向左或向右移动时，不会超过它前边的其他浮动元素
   - 5、如果浮动元素的上边是一个没有浮动的块元素，则浮动元素无法上移
   - 6、浮动元素不会超过它上边的浮动的兄弟元素，最多最多就是和它一样高
- 简单总结：浮动目前来讲它的主要作用就是让页面中的元素可以水平排列， 通过浮动可以制作一些水平方向的布局  
#### ★★★浮动的其他特点

- 1、浮动元素不会覆盖住文字，文字会自动环绕在浮动元素的周围，所以我们可以利用浮动来设置文字环绕图片的效果。
设计浮动的初衷就是制作文字环绕图片的效果
- 2、元素设置浮动以后，将会从文档流中脱离，从文档流中脱离后，元素的一些特点也会发生变化
   - 脱离文档流的特点：
      - 块元素：
         - 1、块元素不在独占页面的一行
         - 2、脱离文档流以后，块元素的宽度和高度默认都被内容撑开
      - 行内元素：
         - 行内元素脱离文档流以后会变成块元素，特点和块元素脱离文档流一样
   - 总之，脱离文档流后就不再区分行内和块了，脱离文档流后都会不再独占一行，宽高都被内容撑开。
### 10-3定位布局
#### （1） 定位的简介

- 定位是一种更加高级的布局手段
- 通过定位可以将元素摆放到页面的任意位置
- 使用position属性来设置定位
   - 可选值：
      - static 默认值，元素是静止的没有开启定位
      - relative 开启元素的相对定位
      - absolute 开启元素的绝对定位
      - fixed 开启元素的固定定位
      - sticky 开启元素的粘滞定位
#### （2） 相对定位
当元素的position属性值设置为relative时则开启了元素的相对定位

- 相对定位的特点：
   - 元素开启相对定位以后，如果不设置偏移量元素不会发生任何的变化
   - 相对定位是参照于元素在文档流中的位置进行定位的
   - 相对定位会提升元素的层级
   - 相对定位不会使元素脱离文档流
   - 相对定位不会改变元素的性质块还是块，行内还是行内
- 偏移量（offset）：当元素开启了定位以后，可以通过偏移量来设置元素的位置
   - top：定位元素和定位位置上边的距离
   - bottom：定位元素和定位位置下边的距离
- 定位元素垂直方向的位置由top和bottom两个属性来控制。通常情况下我们只会使用其中一。top值越大，定位元素越向下移动。bottom值越大，定位元素越向上移动
   - left：定位元素和定位位置的左侧距离
   - right：定位元素和定位位置的右侧距离
- 定位元素水平方向的位置由left和right两个属性控制。通常情况下只会使用一个。left越大元素越靠右，right越大元素越靠左
#### （3） 绝对定位
当元素的position属性值设置为absolute时，则开启了元素的绝对定位

- 绝对定位的特点：
   - 1、开启绝对定位后，如果不设置偏移量元素的位置不会发生变化
   - 2、开启绝对定位后，元素会从文档流中脱离
   - 3、绝对定位会改变元素的性质，行内变成块，块的宽高被内容撑开
   - 4、绝对定位会使元素提升一个层级
   - 5、绝对定位元素是相对于其包含块进行定位的
- 包含块（containing block）
   - 正常情况下：包含块就是离当前元素最近的祖先块元素
```html
<div> <div></div> </div>
<div><span><em>hello</em></span></div>
```

   - 绝对定位的包含块:包含块就是离它最近的开启了定位的祖先元素，如果所有的祖先元素都没有开启定位可以看做根元素就是它的包含块。但是实际上，它的包含块叫做初始包含块，是一个视窗大小的矩形。
      - html（根元素）
#### (4) 固定定位

- 将元素的position属性设置为fixed则开启了元素的固定定位
- 固定定位也是一种绝对定位，所以固定定位的大部分特点都和绝对定位一样
- 唯一不同的是固定定位永远参照于浏览器的视口进行定位固定定位的元素不会随网页的滚动条滚动
#### (5) 粘滞定位

- 当元素的position属性设置为sticky时则开启了元素的粘滞定位
- 粘滞定位和相对定位的特点基本一致，不同的是粘滞定位可以在元素到达某个位置时将其固定
```css
position: sticky;
top: 10px;
```
#### （6）★★★绝对定位元素的位置
水平布局：
left + margin-left + border-left + padding-left + width + padding-right + border-right + margin-right + right = 包含块的内容区的宽度

- 当我们开启了绝对定位后:水平方向的布局等式就需要添加left 和 right 两个值
- 此时规则和之前一样只是多添加了两个值：
- 当发生过度约束：如果9个值中没有 auto 则自动调整right值以使等式满足。如果有auto，则自动调整auto的值以使等式满足
- 可设置auto的值：margin width left right
- 因为left 和 right的值默认是auto，所以如果不指定left和right。则等式不满足时，会自动调整这两个值

垂直方向布局的等式的也必须要满足：top + margin-top/bottom + padding-top/bottom + border-top/bottom + height = 包含块的高度

- ★★★水平垂直居中：
```html
position:absolute;
margin:auto;
top:0;
right:0;
bottom:0;
left:0;CSS
```
#### （7）元素的层级

- 对于开启了定位元素，可以通过z-index属性来指定元素的层级
- z-index需要一个整数作为参数，值越大元素的层级越高。元素的层级越高越优先显示
- 如果元素的层级一样，则优先显示靠下的元素
- 祖先的元素的层级再高也不会盖住后代元素
### 10-4 flex布局（弹性盒、伸缩盒）

- flex是CSS中的又一种布局手段，它主要用来代替浮动来完成页面的布局
- flex可以使元素具有弹性，让元素可以跟随页面的大小的改变而改变
- **弹性容器：**要使用弹性盒，必须先将一个元素设置为弹性容器

可以通过display来设置弹性容器
`display:flex;`设置为块级弹性容器
`display:inline-flex;`设置为行内的弹性容器

- **弹性项目：**

弹性容器的**子**元素是弹性项目（弹性项）
弹性项目可以同时是弹性容器

- **弹性容器的样式**

**justify开头的样式都是主轴上的样式，align开头的样式都是侧轴上的样式**

1. `flex-direction`：指定容器中弹性项目的排列方式

可选值：
row，默认值，弹性项目在容器中水平排列（自左向右） 主轴：自左向右
row-reverse，弹性项目在容器中反向水平排列（自右向左） 主轴：自右向左
column，弹性项目纵向排列（自上向下）  主轴：自上向下
column-reverse，弹性项目反向纵向排列（自下向上）  主轴：自下向上

主轴：弹性项目的排列方向称为主轴
侧轴：与主轴垂直方向的称为侧轴

2. `flex-wrap`：设置弹性项目是否在弹性容器中自动换行。相当于控制侧轴的方向

可选值：
nowrap	默认值，项目不会自动换行
wrap	项目沿着辅轴方向自动换行
wrap-reverse	项目沿着辅轴方向反向换行

3. `flex-flow`：flex-wrap和flex-direction的简写属性

`flex-flow:wrap row;`

4. `justify-content`：如何分配主轴上的空白空间（主轴上的项目如何排列）

可选值：
flex-start	项目沿着主轴起边排列
flex-end	项目沿着主轴终边排列
center	项目居中排列
space-around	空白分布到项目两侧
space-between	空白均匀分布到项目间
space-evenly	空白分布到项目的单侧

5. `align-items`：项目在辅轴上如何对齐

可选值：
stretch	默认值。将同一行项目的长度设置为相同的值
flex-start	项目不会拉伸，沿着辅轴起边对齐
flex-end	沿着辅轴的终边对齐
center	居中对齐
baseline	基线对齐

6. `align-content`：辅轴空白空间的分布，可选值和justify-content一样

- align-content和align-items的对比：
   1. align-items对于一行/一列元素的侧轴对齐方式起作用
   1. align-content对于多行/多列元素的侧轴对齐方式起作用
#### 第四种水平垂直居中的方法
```html
<!--HTML文件-->
<div class="outer">
	<div class="box1">
  </div>
</div>
```
```css
/*CSS文件*/
.outer{
	width:800px;
  height:800px;
  background-color:yellow;
  display:flex;
  justify-content:center;
  align-items:center;
}
.box1{
	width:200px;
  height:200px;
  background-color:green;
}
```

- **弹性项目的样式**

**flex-basis，flex-grow，flex-shrink就像弹簧的三种状态**

1. `flex-grow`：指定弹性项目的伸展系数(1,2,3...)

当父元素有多余空间的时候，子元素如何伸展？父元素的剩余空间会按照比例进行分配

2. `flex-shrink`：指定弹性项目的收缩系数(1,2,3...)

当父元素中的空间不足以容纳所有的子元素时，如何对子元素进行收缩
缩减系数的计算方式比较复杂
缩减多少是根据 **缩减系数 **和 **项目大小 **来计算的

- 收缩的计算方法

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2960726/1647354842061-48056c0e-3b98-427f-aabb-9e778ae8b735.png#clientId=u905abbaa-00c0-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=420&id=ue7a69601&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1706&originWidth=1280&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2763850&status=done&style=none&taskId=ufe123094-ef84-423c-8dce-de97538c55f&title=&width=315)

3. `align-self`：用来覆盖当前弹性项目上的align-items
3. `flex-basis`：指定的是项目在主轴上的基础长度

如果主轴是横向的 则 该值指定的就是项目的宽度
如果主轴是纵向的 则 该值指定的就是项目的高度
默认值是auto,表示参考项目自身的高度或宽度
如果传递了一个具体的数值，则以该值为准

5. `flex`可以设置弹性项目所有的三个样式，默认值initial

语法：`flex:flex-grow flex-shrink flex-basis/auto/initial/inherit;`
其中，`initial`相当于`flex:0 1 auto;`
`auto`相当于`flex:1 1 auto;`
`none`相当于`flex 0 0 auto;`（即弹性项目没有弹性）
`flex:1;`相当于`flex: 1 1 0%;`

6. order决定弹性项目的排列顺序
- order的默认值为0，因此order数值大于0的项目将会显示在那些未指定order值的项目之后
- order还可以指定负值，这很有用。如果要优先显示一个项目，并保持所有其他项目的顺序不变，则可以将该项目的顺序设置为-1，由于该值小于0，因此始终会优先显示该项目
```css
.box1{
	order:2;
}
.box3{
	order:1;
}
.box2{
	order:3;
}
```
## 11、浏览器的默认样式

- 通常情况，浏览器都会为元素设置一些默认样式
- 默认样式的存在会影响到页面的布局
   - 通常情况下编写网页时必须要去除浏览器的默认样式（PC端的页面）
###  重置样式表

- 重置样式表：专门用来对浏览器的样式进行重置的
   - reset.css 直接去除了浏览器的默认样式
   - normalize.css 对默认样式进行了统一

## 12、盒子的大小

- 默认情况下，盒子可见框的大小由内容区、内边距和边框共同决定
- box-sizing 用来设置盒子尺寸的计算方式（设置width和height的作用）
   - 可选值：
      - content-box 默认值，宽度和高度用来设置内容区的大小
      - border-box 宽度和高度用来设置整个盒子可见框的大小
         - width 和 height 指的是内容区 和 内边距 和 边框的总大小

## 13、轮廓、阴影和圆角
### 13-1 轮廓

- 用outline来设置元素的轮廓线。用法和border一模一样
- 和border不同的是，outline不会影响元素可见框的大小，也可以是说不会影响其他元素的位置和页面布局。而border设置边框，整个可见框的大小就会改变，会影响其它元素的位置和页面的布局
### 13-2 阴影

- 用box-shadow属性来设置元素的阴影效果，阴影一般不会影响页面布局
- 属性值：
   - 第一个值：水平偏移量，阴影在水平方向上的位置，正值向右移动，负值向左移动
   - 第二个值：垂直偏移量，阴影在垂直方向上的位置，正值向下移动，负值向左移动
   - 第三个值：阴影的模糊半径
   - 阴影的颜色：可以使用rgba来设置带透明度的颜色
### 13-3 圆角

- 用border-radius来设置圆角
- 可以分别为每一个角设置圆角：（一个值，圆角是以圆形为半径，两个值，圆角是以椭圆为半径）
   - border-top-left-radius:设置左上角
   - border-top-right-radius:设置右上角
   - border-bottom-left-radius:设置左下角
   - border-bottom-right-radius:设置右下角
- 也可以有简写形式：border-radius可以分别指定四个角的圆角（以椭圆为半径连个值之间需要以/分隔）
   - 四个值：左上 右上  右下  左下
   - 三个值：左上     右上左下    右下
   - 两个值：左上右下   左下右上
- 将元素设置为一个圆形或者椭圆形
   - `border-radius:50%;`
## 14、高度塌陷和BFC
### 14-1 高度塌陷的问题
在浮动布局中，父元素的高度默认是被子元素撑开的，当子元素浮动后，其完全脱离文档流，子元素从文档流中脱离，将会无法撑起父元素的高度，导致父元素的高度丢失。
父元素的高度丢失后，其下面的元素会自动上移，导致页面的布局混乱。
所以高度塌陷是浮动布局中比较常见的一个问题，这个问题我们必须要进行处理！
### 14-2 BFC(Blocking Formatting Context)块级格式化环境

- BFC是一个CSS中的一个隐含的属性，可以为一个元素开启BFC
- 开启BFC该元素会变成一个独立的布局区域
- 元素开启BFC后的特点：
   - 1、开启BFC的元素不会被浮动元素所覆盖
   - 2、开启BFC的元素子元素和父元素外边距不会重叠
   - 3、开启BFC的元素可以包含浮动的子元素
- 可以通过一些特殊方式开启元素的BFC：
   - 1、设置元素的浮动（不推荐）
   - 2、将元素的display设置为inline-block、table-cell、table-caption、flex、inline-flex（不推荐）
   - 3、position为absolute或fixed
   - 4、将元素的overflow设置为一个非visible的值
      - 常用的方式为元素设置overflow:hidden 开启bFC 以使其元素可以包含浮动元素。
### 14-3 ★★★clear
由于box1的浮动，导致box3位置上移，也就是box3受到了box1浮动的影响，位置发生了改变

- 如果我们不希望某个元素因为其他元素浮动的影响而改变位置，可以通过clear属性来清除浮动元素所产生的影响
- clear
   - 作用：清除浮动元素对当前元素所产生的影响
   - 可选值：
      - left 清除左侧浮动元素对当前元素的影响
      - right 清除右侧浮动元素对当前元素的影响
      - both 清除两侧中最大影响的那侧
- 原理：设置清除浮动以后，浏览器会自动为元素添加一个上外边距， 以使其位置不受其他元素的影响
### 14-4 使用after伪类解决高度塌陷
```css
.box1::after{
            content: '';
            display: block;
            clear: both;
        }
```
### 14-5 clearfix

- clearfix 这个样式可以同时解决高度塌陷和外边距重叠的问题，当你在遇到这些问题时，直接使用clearfix这个类即可
```css
.clearfix::before,
        .clearfix::after{
            content: '';
            display: table;
            clear: both;
        }
```
## 15、字体
### 15-1 字体族
字体相关的样式 

- color 用来设置字体颜色
- font-size 字体的大小
   - 和font-size相关的单位：
em 相当于当前元素的一个font-sizerem 相对于根元素的一个font-size
- font-family 字体族（字体的格式）
   - 可选值：
      - serif  衬线字体
      - sans-serif 非衬线字体
      - monospace 等宽字体
      - 指定字体的类别，浏览器会自动使用该类别
   - font-family 可以同时指定多个字体，多个字体间使用,隔开
   - 字体生效时优先使用第一个，第一个无法使用则使用第二个 以此类推
- @font-face可以将服务器中的字体直接提供给用户去使用     问题：        1.加载速度        2.版权        3.字体格式

```css
@font-face {
/* 指定字体的名字 */
font-family:'myfont' ;
/* 服务器中字体的路径 */
src: url('./font/ZCOOLKuaiLe-Regular.ttf') format("truetype");
        }
```
### 15-2 图标字体简介
图标字体（iconfont）

- 在网页中经常需要使用一些图标，可以通过图片来引入图标。但是图片大小本身比较大，并且非常的不灵活
- 所以在使用图标时，我们还可以将图标直接设置为字体，然后通过font-face的形式来对字体进行引入
- 这样我们就可以通过使用字体的形式来使用图标
### 15-3 fontawesome使用步骤

1. 下载 [https://fontawesome.com/](https://fontawesome.com/)
1. 解压
1. 将css和webfonts移动到项目中
1. 将all.css引入到网页中
1. 使用图标字体
   - 直接通过类名来使用图标字体class="fas fa-bell"class="fab fa-accessible-icon"
```html
<i class="fas fa-bell-slash"></i>
<i class="fab fa-accessible-icon"></i>
```
### 15-4图标字体的其他使用方式

- 通过伪元素来设置图标字体
   1. 找到要设置图标的元素通过before或after选中
   1. 在content中设置字体的编码
   1. 设置字体的样式
```css
li::before{
            content: '\f1b0';
            font-family: 'Font Awesome 5 Free';
            font-weight: 900; 
            color: blue;
            margin-right: 10px;
        }
```

- 通过实体来使用图标字体：&#x图标的编码;
```html
<span class="fas">&#xf0f3;</span>
```
### 15-5阿里字体图标库 iconfont
[https://www.iconfont.cn/?spm=a313x.7781069.1998910419.d4d0a486a](https://www.iconfont.cn/?spm=a313x.7781069.1998910419.d4d0a486a)
### 15-6 行高

- 行高指的是文字占有的实际高度
- 可以通过line-height来设置行高
   - 行高可以直接指定一个大小（px em）也可以直接为行高设置一个整数。如果是一个整数的话，行高将会是字体的指定的倍数。默认行高是1.33倍
- 行高经常还用来设置文字的行间距
   - 行间距 = 行高 - 字体大小
- 字体框：字体框就是字体存在的格子，设置font-size实际上就是在设置字体框的高度
- 行高会在字体框的上下平均分配
### 15-7 字体的简写属性

- font 可以设置字体相关的所有属性
- 语法：font: 字体大小/行高 字体族
   - 行高 可以省略不写 如果不写使用默认值
   - 可以在字体大小和字体族前面增加font-weight和font-style
      - font-weight 字重 字体的加粗 可选值：
 normal 默认值 不加粗 bold 加粗 100-900 九个级别（没什么用）
      - font-style 字体的风格normal 正常的italic 斜体

font: bold italic 50px/2  微软雅黑, 'Times New Roman', Times, serif;
## 16、文本样式
### 16-1文本的水平和垂直对齐
（1）文本的水平对齐

- text-align 文本的水平对齐
- 可选值：    left 左侧对齐    right 右对齐    center 居中对齐    justify 两端对齐
- text-align是在块元素中设置的，作用给文本元素的
- text-align也能指定容器内的图片对齐方式

（2）文本的垂直对齐

- vertical-align 设置元素垂直对齐的方式
- 可选值：    baseline 默认值 基线对齐    top 顶部对齐    bottom 底部对齐    middle 居中对齐
- 注意：图片在块元素中会有一个px的空白，所以这种情况使用top或者bottom来处理
### 16-2 其他的文本样式

- text-decoration 设置文本修饰
- 可选值：
						none 什么都没有                        underline 下划线                        line-through 删除线                        overline 上划线
```css
text-decoration: underline red dotted;
```

- white-space 设置网页如何处理空白
- 可选值：
						normal 正常                        nowrap 不换行                        pre 保留空白
```css
/*文本溢出添加省略号效果*/
white-space: nowrap;
overflow: hidden;
text-overflow: ellipsis;
```

- text-indent

作用：设置文本块中首行文本的缩进。
默认行高1.33
## 17、背景相关样式
### 17-1background-color
### 17-2background-image:url("")
背景图片和背景颜色同时设置，背景颜色会成为背景图片的背景
边框会盖住图片
### 17-3background-repeat
可选值：no-repeat    repeat-x    repeat-y    repeat
### 17-4background-position
方位：top left right bottom center
偏移量：水平    垂直
### 17-5background-clip
设置背景的范围
可选值：padding-box  border-box  content-box
### 17-6background-origin
设置背景图片偏移量的起点
可选值：和上面属性相同
### 17-7background-size
设置背景图片的大小
可以用像素作为单位  水平 垂直
也可以使用cover和contain
cover：图片比例不变，图片将元素填满
contain：图片比例不变，图片将元素填满
### 17-8background-attachment
设置背景图片是否跟随元素滚动
scrool：默认值，背景图片会跟随所在元素移动
fixed:背景图片会跟随所在元素移动，此时背景图片相对于视口进行定位
### 17-9简写属性background
简写属性
对于顺序没有要求
但是background-clip要写在background-origin后面
background-size要写在background-position后面，而且用/分隔

## 18、渐变
渐变是图片，需要通过background-image来设置
### 18-1线性渐变
颜色沿着一条直线发生变化
background-image:linear-gradient（方向（to right\度数123deg\.5turn圈），颜色1 渐变开始位置1，颜色2 渐变开始位置2，颜色3 渐变开始位置3...）
渐变可以同时指定多个颜色，多个颜色默认情况下平均分布
也可以手动指定渐变的分布情况

background-image:repeat-linear-gradient()：重复线性渐变，可以平铺的线性渐变
### 18-2径向渐变(放射性效果)
background-image:radial-gradient(渐变大小 at 位置，颜色1 位置1，颜色2 位置2)
默认情况下径向渐变是根据元素的形状来计算的
长方形--->椭圆形
正方形--->圆形
我们也可以自己手动指定径向渐变的大小：circle、elipse、closest-side(近边)、closest-corner(近角)、farthest-side(远边)、farthest-corner(远角)
位置：top、bottom、left、right、center、以及偏移量均可表示
## 19、过渡（transition）

- 作用：通过过渡可以指定一个属性发生变化时的切换方式
           通过过渡可以创建一些非常好的效果，提升用户的体验
- transition-property：指定要执行过渡的属性。多个属性间是用,隔开。如果所有属性都需要过渡，则使用all关键字。大部分属性都支持过渡效果，注意过渡时必须是从一个有效数值向另外一个有效数值进行过渡。display不支持过渡
- transition-duration：指定过渡效果的持续时间。

时间单位：s 和 ms
可以指定多个时长，每个时长会被应用到由transition-property指定的对应属性上。如果指定的时长小于属性个数，那么时长列表会重复。如果时长列表更长，那么列表会被裁减。

- transition-timing-function：过渡的时序函数。指定过渡的执行方式。

可选值：
ease：默认值，慢速开始，先加速，后减速
linear：匀速运动
ease-in：加速运动
ease-out：减速运动
ease-in-out：先加速后减速，但是没有ease平滑
cubic-bezier()：贝塞尔曲线来指定时序函数。
[https://cubic-bezier.com/](https://cubic-bezier.com/)
steps()：分步执行过渡效果。
可以设置一个第二个值：
end，在时间结束时执行过渡（默认值）
start，在时间开始时执行过渡
step-start：等同于steps(1,start)
step-end：等同于steps(1,end)

- transition-delay：过渡效果的延迟，等待一段时间后再执行过渡
- 注意：上述每一个属性都是可以指定多个属性值的，当属性值列表长度不一致时（也就是不能对应）。

超出的情况下是会被全部裁掉的。
不够的时候，关于时间的会重复列表。transition-timing-function的时候使用的是默认值ease

- transition：过渡的简写属性，可以同时设置过渡相关的所有属性，只有一个要求，如果要写延迟，则两个时间中第一个是持续时间，第二个时间是延迟时间。多个过渡效果可以用“,”分隔

## 20、动画(animation)

- 作用：动画和过渡类似，都是可以实现一些动态的效果，不同的是过渡需要在某个属性发生变化时才会触发。动画可以自动触发动态效果。
- 设置动画效果必须先要设置一个关键帧，关键帧设置了动画执行每一个步骤
```css
@keyframes test {
            /* from表示动画的开始位置 也可以使用 0% */
            from{
                margin-left: 0;
                background-color: orange;
            } 
            /* to动画的结束位置 也可以使用100%*/
            to{
                background-color: red;
                margin-left: 700px;
            }
        }
```

- animation-name：要对当前元素生效的关键帧的名字
- animation-duration：动画的执行时间
- animation-delay：动画的延时
- animation-timing-function：动画的时序函数，和transition一样。

此外，这个属性作用于两个关键帧之间，而不是整个动画。是从from{}到to，不是整个animation

- animation-iteration-count：动画的执行次数

可选值：
次数
infinite无限执行

- animation-direction：指定动画运行的方向

可选值：
normal：默认值 从 from向 to运行
reverse：从to向from运行 每次都是这样
alternate 从from向to运行 重复执行动画时反向执行
alternate-reverser：从to向from运行 重复执行动画时反向执行

- animation-play-state：设置动画的执行状态

可选值：
running：默认值 动画执行
paused：动画暂停

- animation-fill-mode：动画的填充模式

可选值：
none：默认值 动画执行完毕元素回到原来位置
forwards：动画执行完毕元素会停止在动画结束的位置
backwards：动画延时等待时，元素就会处于开始位置
both：结合了forwards和backwards

- animation：简写属性，和过渡差不多
## 21、变形

- 作用：变形是指通过CSS来改变元素的形状或位置

变形不会影响到页面的布局

- transform用来设置元素的变形效果
- transform不能设置给行内元素，但是对图片元素是有用的。

平移：
translateX()：沿着X轴方向平移
translateY()：沿着y轴方向平移
translateZ()：沿着Z轴方向平移
translate()：二维平移，设置两个值，朝xy轴的夹角方向平移
平移元素，百分比是相对于自身计算的

- 利用平移可以做元素水平垂直居中效果

之前我们学过两种水平垂直居中的方式，其中有一个是通过给元素定位的方式来确定的，但是只能针对于宽高确定的元素。针对宽高不确定，宽高被内容撑开的元素，我们可以使用第三种元素水平居中的方式
```html
<!-- HTML代码 -->
<div class="box1">1222345</div>
```
```css
/*CSS代码*/
.box1{
  position：absolute;
  left:50%;
  top:50%;
  transform:translateX(-50%) translateY(-50%);
}
```

- z轴平移：调整元素在z轴的位置，正常情况就是调整元素和人眼之间的距离，距离越大，元素离人越近

z轴平移属于立体效果（近大远小），默认情况下网页时不支持透视，如果需要看见效果，必须要设置网页的视距。使用perspective设置，一般都设置给body。例如：perspective:800px;
## 22、旋转

- 作用：通过旋转可以使元素沿着x y或z旋转指定的角度

rotateX
rotateY
rotateZ
值：可以是xxxdeg，可以是xxxturn

- backface-visibility：是否显示元素的背面

visible：背面是可见的
hidden：背面是不可见的

## 23、缩放

- 对元素进行缩放的函数

scale()：
一个值：同时作用于X轴和Y轴的缩放系数
2个值：第一个值作用域x轴的缩放系数，第二个值是作用于y轴的缩放系数
3个值：第一个值作用域x轴的缩放系数，第二个值是作用于y轴的缩放系数，第三个值作用于z轴的缩放系数，相当于一个scale3d()函数
scaleX()：水平方向的缩放
scaleY()：垂直方向的缩放
scaleZ()：双方向的缩放

- 关于变形的一些其他样式
   - `transform-origin:20px 20px`变形的原点 默认值center（即50% 50% 0），2d变形2个值，3d变形三个值
   - opacity：为整个元素设置透明效果
   - `transform-style:preserve-3d`

作用：营造有层级的3d舞台，作用于子元素，而不是后代元素。让3D变形有效果

   - 无论平移、旋转、还是缩放，想要看到效果，都要设置transform-style
## 24、less
### less简介
less是一门css的预处理语言

- css本身有它的不足之处，因此出现了less
- less是一个css的加强版，通过less可以编写更少的代码实现更强大的样式
- 在less中添加了许多的新特性：像对变量的支持、对mixin的支持......
- less的语法大体上和css语法一致，但是less中增添了许多对css的扩展，所以浏览器无法直接执行less代码，要执行必须将less转换为css,然后再由浏览器执行。在VScode需要安装一个easy-less插件，保存时自动将less编译为css文件

css原生也支持变量的设置，以及calc()计算函数,但是不兼容IE
```css
html{
            /* css原生也支持变量的设置 */
            --color:#ff0;
            --length:200px;
        }
```
```css
.box1{
            /* calc()计算函数 */
            width: calc(200px*2);
            height: var(--length);
            background-color: var(--color);
        }
```
### less语法
#### 1、less中的注释
`// 注释内容`less中的单行注释，注释中的内容不会被解析到css文件中
`/* 注释内容 */`在less中也可以写css中的注释，注释内容会被解析到css文件中
#### 2、less中的变量
变量：在变量中可以存储一个任意的值，并且我们可以在需要时，任意的修改变量中的值
变量的语法：`@变量名`

- 使用变量时，如果是直接使用则以`@变量名`的形式使用即可
```less
@a:200px;
@b:yellow;
.box1{
	width:@a;
  color:@b
}
```

- 变量作为类名或者一部分值使用时必须以@{变量名}的形式使用
```less
@c:box2;
.@{c}{
	background-image:url("@c/1.png");
}
```

- 变量发生重名时，会优先使用比较近的变量
```less
@d:200px;
@d:300px;
div{
	@d:115px;
  /*这里的width值将会是距离width最近的115px*/
  width:@d;
}
```

- 可以在变量声名之前就使用变量
```less
div{
  /*这里的width值是335px*/
	width:@e;
}

@e:335px;
```

- 可以使用`$`把属性当作变量
```less
@a:100px;
.box1{
	width:@a;
  /*这里的height值和width值一样都是100px*/
  height:$width;
}
```
#### 3、less中的父元素
&就表示外层的父元素
```less
/*例如为box1设置一个hover*/
.box1{
  &:hover{
  	color:red;
  }
}
```
#### 4、扩展

- `:extend()`对当前选择器扩展指定选择器的样式（生成css文件中就相当于选择器分组）
```less
.p1{
	width:100px;
  height:200px;
  
  /*p2在继承p1样式的基础之上，又添加了color:red的样式*/
  .p2:extend(.p1){
  	color:red;
  }
}
```

- 另外使用mixin混合的方式也可以实现扩展，但是这种方式和`:extend()`方式不同的是，生成的css文件不是选择器分组的形式，而是相当于将样式复制
```less
.p1{
	width:100px;
  height:200px;
}
/*直接对指定的样式进行引用，这里就相当于将p1的样式在这里进行了复制*/
.p3{
	.p1();
}
```
#### 5、混合函数

- 定义混合函数：`.函数名（变量1(:默认值),变量2(:默认值),变量3(:默认值)）{样式}`
- 调用混合函数：需要传递参数。传递参数有两种方式：

①按顺序传递参数：`.函数名(参数1,参数2,参数3);`
②按变量名传递参数：`.函数名(变量2:参数2,变量3:参数3,变量1:参数1);`
```less
/*定义混合函数*/
.test(@w:100px,@h:200px,@bg-color:red){
  width:@w;
  height:@h;
  border:1px solid @bg-color; 
}
/*调用混合函数，按顺序传递参数*/
div{
  .test(200px,300px,#bfa);
}

```
其他混合方式：

- 不带输出的混合

像下面这样定义就是会输出的混合，这样的混合会造成代码冗余
```css
/*下面test就是混合函数，这样定义会在编译后的css文件中输出*/
.test{
    width:100px;
    height:100px;
    background-color: red;
}
.box1{
    .test;
}
```
要是想定义一个不带输出的混合，就得在混合函数后面加上括号或者像一开始定义的混合那样有参数也不会输出到编译后的css文件中。

- **匹配模式**

有时我们需要根据要求展现同一个元素的不同效果，那么我们为每一个元素的不同效果写代码，会有很多重复代码。例如我们需要三角形的不同方向效果。这是，我们就会用到匹配模式。
代码：
```html
<!--html代码-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>匹配模式</title>
    <link rel="stylesheet" href="./css/style2.css">
</head>
<body>
    <div class="box1"></div>
</body>
</html>
```
```less
/*业务代码，负责Html页面的样式*/
@import "./匹配模式.less";	
.box1{
  /*这里根据参数匹配不同的三角形的样式*/
    .triangle(R,100px,purple);
}
```
```less
/*功能代码*/
/*这里使用@_作用是匹配不同的关键字，然后有不同的三角形样式。这个代码在应用的同时，
会同时应用下面的同名代码。
*/
.triangle(@_,@w,@c){
    width:0;
    height:0; 
}
.triangle(T,@w,@c){
    border:@w solid;
    border-top: none;
    border-color: transparent transparent @c transparent;
}
.triangle(L,@w,@c){
    border:@w solid;
    border-left: none;
    border-color: transparent @c transparent transparent ;
}
.triangle(R,@w,@c){
    border:@w solid;
    border-right: none;
    border-color: transparent transparent transparent @c;
}
.triangle(B,@w,@c){
    border:@w solid;
    border-bottom: none;
    border-color: @c transparent transparent transparent;
}
```

- **arguments变量**
```less

.style(@1,@2,@3){
    width:200px;
    height:200px;
    background-color: red;
    border:@arguments;
}
.box1{
    .style(1px,solid,red);
}
```
#### 6、less继承
语法：`:extends(要继承的类名,all);`
all关键字是为了继承该类所有状态的样式，比如这个类有:hover，:focus样式，也都能继承过来
#### 7、其他语法

- `import`用来将其他的less引入到当前的less
```less
@import "syntax22.less"
```

- 在less中所有的数值都可以直接进行计算，计算双方有一方带单位就可以了
```less
.box1{
	width:100px+200px;
  height:100px/2;
  background-color:#bfa;
}
```
**8、避免编译**
在需要不编译的语句前加上~，并且用""包裹
就能在编译成css文件时，不编译该语句。
例如：
```less
.box1{
	~"width:calc(100px/10)";
}
```


## 25、媒体查询
### 响应式布局
网页可以根据不同的设备或窗口大小呈现出不同的效果
响应式布局，可以使一个网页适用于所有设备
响应式布局的关键就是 **媒体查询**
通过媒体查询，可以为不同的设备，或设备的不同状态来分别设置样式
### 媒体查询
如何使用媒体查询
语法：`@media 查询规则{}`
**媒体类型：**
all	所有设备
print	打印设备
screen	带屏幕的设备
speech	屏幕阅读器
**媒体特性：**
width：视口的宽度
height：视口的高度

min-width：视口的最小宽度（视口大于指定宽度时生效）
max-width：视口的最大宽度（视口小于指定宽度时失效）

举例：
```css
@media only screen and (min-width:600px) and (max-width:800px){
  body{
    /*只有当视口宽度为600-800之间，背景颜色才会变为黄色*/
  	background-color:yellow
  }
}
```
**常用分界点**
样式切换的分界点，我们称其为断点，也就是网页的样式会在这个点时发生变化。一般比较常用的断点有：
小于768	超小屏幕 max-width=768px
大于768	小屏幕	min-width=768px
小于992	中性屏幕	min-width=992px
大于1200	大屏幕	min-width=1200px
**操作符&关键字**

- **only:**

可以在媒体类型前添加一个only,表示只有。only的使用主要是为了兼容一些老版本浏览器

- and：

连接媒体类型、媒体属性
对于所有的连接选项都要匹配成功才能应用规则

- or(,)

和and相似
连接多个媒体类型，这样他们之间就是一个或的关系。也就是说对于所有的连接选项只要匹配成功一个就能应用规则。

- not：取反


