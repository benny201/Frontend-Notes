# chapter 9

## 网页的三层信息
* 结构层
* 表示层
* 行为层

### 结构层
类似HTML／XTHML等组成了结构层

### 表示层
presentation layer由CSS负责完成。

### 行为层
behavior layer负责内容应该如何响应事件这个问题。

### 潜在的重叠区域
JS可以操作HTML，改变HTML／CSS
CSS的伪类也有类似DOM的功能

## style属性
每个元素节点都有一个`style属性`。style属性包涵着元素的样式。
```javascript
element.style.property

e.g.
p.style.color
遇到front－family等中间带有横岗的，可以用驼峰法书写：frontFamily
```

### style属性的局限性
style属性只能返回内嵌样式！！！换句话说只有把CSS style属性插入到标记里，才可以用DOM style属性去查询这些信息！！！

## 何时用DOM设置CSS

### 根据元素在节点树里的位置设置样式
css2中的位置选择器：
```javascript
:first-child, :last-child
```
css3中新增的：
```javascript
:nth-child(), :nth-of-type()
```
有些位置不好设置，但是DOM中的previousSibling、nextSilbling、parentNode、firstChild和lastChild就可以很好的处理位置。

### 何时用css而不用js设置一些动作

如果仅仅是改变颜色，应该就用更简单的css

## className属性
改变class的方法：
```javascript
element.className = value;
或者追加class
element.className += " vaule";
```
追加时：
* 先判断className是否为空
* 如果是直接赋值不用追加
* 如果不是，则追加

## abtraction
抽象：就是让函数更加通用！！！

