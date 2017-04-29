# 经典的圣杯布局

> https://cnodejs.org/topic/56d70d5f4dfa4031185aabbf

左边栏，右边栏，中间栏，header和footer

所谓液态布局是相对固态布局而言的，固态布局就是固定值不变的布局，液态就好比在容器里到了一杯水，它可以随着容器宽度的变化而自适应宽度。

必须按照源顺序（在 DOM 中表现为先写 Left，然后 Middle，最后，Right）等，它将可能导致代码不够灵活，尤其是从 DOM 的载入顺序上来说，中间的内容不能被首先加载。
因此他给出一个方案，它将：
```
两边带有固定宽度中间可以流动（fluid）；
允许中间一栏最先出现；
允许任意一栏放在最上面；
仅需一个额外的 div 标签
仅需非常简单的 CSS，带上最少的兼容性补丁
```

## 实现

### HTML部分
```HTML
<div id="header">#header</div>

<div id="container">
  <div id="center" class="column">#center</div>
  <div id="left" class="column">#left</div>
  <div id="right" class="column">#right</div>
</div>

<div id="footer">#footer</div>
```
### CSS部分
```css
body {
  min-width: 550px;      /* 2x LC width + RC width */
}
#container {
  padding-left: 200px;   /* LC width */
  padding-right: 150px;  /* RC width */
}
#container .column {
  height: 200px;
  position: relative;
  float: left;
}
#center {
  background-color: #e9e9e9;
  width: 100%;
}
#left {
  background-color: red;
  width: 200px;          /* LC width */
  right: 200px;          /* LC width */
  margin-left: -100%;
}
#right {
  background-color: blue;
  width: 150px;          /* RC width */
  margin-right: -150px;  /* RC width */
}
#footer {
  clear: both;
}
#header,
#footer {
  background-color: #c9c9c9;
}

/*** IE6 Fix ***/
* html #left {
  left: 150px;           /* RC width */
}
```

