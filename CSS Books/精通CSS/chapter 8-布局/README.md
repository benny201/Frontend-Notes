# chapter 8 布局
所有的css布局技术的根本都是3个基本概念：定位，浮动，外边距操纵。

## em/rem
* em: 1em 等于当前的字体尺寸
* rem: REM表示“Root EM”,字面上指的是根元素的em大小。在Web文档的上下文中，根元素就是你的html元素。如果没有重置，html默认font-size:16px。

### chrome的font－size问题
当样式设定font-size<12px时，chrome浏览器里字体显示仍为12px；
* 解决方案，添加一个私有属性到html选择器: `html{-webkit-text-size-adjust: none;}`


## 1.设置基本结构
经典的三列布局，左栏，右栏，中间content

### 水平居中的div
* 一种典型的布局
```css
<body>
    <div class="wrapper"></div>
</body>

.wrapper {
    width: 920px;
    margin: 0 auto;
}
也可以设置宽度为主体的百分之几，活着是用em相对于文本字号设置宽度。
```
* 怎么让外层div水平居中
```
1、不能使用float（无论float:left和float:right都不能使用）
2、对body设置text-align:center，以便兼容低版本和高版本浏览器
3、对最外层DIV设置margin:0 auto，兼容各大浏览器水平居中样式
```

### 一种IE的hack
在IE中`text-align: center`误解为让所有东西居中，不只是文本。


## 2.基于浮动的布局
最常见的用法是`浮动几乎所有东西，然后再整个文档的例如页脚`上进行一次或者两次清理。

### 2.1 两列浮动布局
html布局如下：
```html
<div class="container">
    <div class="content"></div>
    <div class="secondary"></div>
</div>
```
为什么content的div需要放在前面呢？
* 主要的内容在文档中先出现。
* 方便屏幕阅读起用去，先看到主要内容

css如下：
```css
.container .content {
    display: inline; //解决IE的双外边距浮动产生的BUG
    float: right;
    width: 600px;
}
.container .secondary {
    display: inline;
    float: left;
    width: 200px;
}
```
让左栏向左浮动，内容栏向右浮动是为了：不让元素太挤，左右浮动创建视觉上的隔离。

### 2.2 三列布局
类似两列布局

## 3.固定宽度／流式／弹性布局
固定布局对于分辨率变化无能为力。可以使用`流式布局`和`弹性布局`解决这个问题。

### 3.1流式布局
流式布局中，尺寸是`百分比`而不是具体的像素大小，这样可以使布局相对于浏览器窗口进行伸缩。
* 缺点： 在窗口宽度较小时，行变得非常窄。
* 解决方案： 添加min-width，以px或者em为单位。但是min－width设置大了面临跟固定布局一个窘境。
* 使用liquidfold.net计算百分比，其实自己算就行啦。。。吐槽一下。
```html
<div class="content">
    <div class="primary">
        <div class="primary"></div>
        <div class="secondary"></div>
    </div>

    <div class="secondary"></div>
</div>
```
对应的样式：
```css
.content {
    width: 76.8%;
    margin: 0 atuo;
    text-align: left;
}

.cotent .primary {
    width: 72.82%;
    float: right;
    display: inline:
}

.content .secondary {
    width: 25%;
    float: left;
    displayL inline;
}

.content .primary .primary {
    width: 59.7%;
    float: left;
    display: inline;
}

.content .primary .secondary {
    width: 34.33%;
    padding-right: 2.63%;
    float: right;
    display: inline;
}
```
为了确保文本行的长度，所以应该加个max－width和min－width;

### 3.2 弹性布局
弹性布局是`相对于字号`布局的，有别于流式布局的相对于`浏览器宽度`, 可以解决行过长文字不方便阅读的问题。
* `修改：` 只需要将容器的宽度改为em为单位，其他仍然用百分比即可。

几个注意点：
* 如果图片跨大区域，可以设置成背景图片。overflow设置为hidden。
* 给img设定百分数宽度，可以相对于周围元素伸缩。





