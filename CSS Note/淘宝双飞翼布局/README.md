# 双飞翼布局

html：
```HTML
<!--自适应的主要元素应放在文档流前面优先渲染,双飞翼适合各类布局，三列能自由分布-->
<div id="div-middle-02">
  <div id="middle-wrap-02"><span>divdi</span>
  </div>
</div>
<div id="div-left-02"><span>div-left</span></div>
<div id="div-right-02"><span>div-right</span></div>
```

CSS:
```css

* {
  padding: 0;
  margin: 0;
}
span {
    color: blue;
}
/*双飞翼布局*/
#div-middle-02 {
    float: left;
    background-color: #fff9ca;
    width: 100%;
    height: 50px;
}

#div-left-02 {
    float: left;
/*     position: relative; */
    background-color: red;
    width: 150px;
    margin-left: -100%;
    height: 50px;

}

#div-right-02 {
    float: left;
/*     position: relative; */
    background-color: yellow;
    width: 200px;
    margin-left: -200px;
    height: 50px;
}

#middle-wrap-02 {
/*   margin: 0 150px 0 200px; */
  margin-left: 150px;
  margin-right: 200px;
  word-break: break-all;
}
```

资料：
* http://www.cnblogs.com/honoka/p/5161836.html -> 没加word-break: break-all;
* http://www.cnblogs.com/imwtr/p/4441741.html
* https://alistapart.com/article/holygrail