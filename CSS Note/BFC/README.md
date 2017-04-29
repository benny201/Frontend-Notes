# BFC
> http://www.cnblogs.com/lhb25/p/inside-block-formatting-ontext.html

## BFC是什么?
BFC: Block fomatting context

### FC
Formatting context 是 W3C CSS2.1 规范中的一个概念。它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用

最常见的 Formatting context 有 Block fomatting context (简称BFC)和 Inline formatting context (简称IFC)


## BFC规则
BFC布局规则：
* 内部的Box会在垂直方向，一个接一个地放置。
* Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠
* 每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
* BFC的区域不会与float box重叠。
* BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
* `计算BFC的高度时，浮动元素也参与计算` -> 为什么BFC能解决高度塌陷的原因

## 生成BFC的元素
* 根元素
* float属性不为none
* position为absolute或fixed
* display为inline-block, table-cell, table-caption, flex, inline-flex
* overflow不为visible

## 解决的实际问题

### 1. 自适应两栏布局

* 所应用的规则：
```
1. 每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
2. BFC的区域不会与float box重叠。
3. BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
```

### 2. 清除内部浮动

* 所应用的规则:
```
1. 计算BFC的高度时，浮动元素也参与计算
2. BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
```

### 3. 防止垂直 margin 重叠
* 所应用的规则：
```
1. Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠
2. BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
```
