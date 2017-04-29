# 对链接应用样式

## 下划线的伪类选择器

选择器的次序非常重要，如果次序反过来，鼠标悬停和激活样式就不起作用了：

* link
* visited
* hover
* focus
* active

## css精灵
合并所有的图像到一张图片上，减少http请求。
通过`background-position: apx bpx`来切换图片位置。

### 应用方法
```css
ul.Sprites li span{ background:url(ico.png) no-repeat} 给span设置css背景图片
再分别对不同span class设置对于图标背景定位具体值
ul.Sprites li span.a1{ background-position: -62px -32px}设置背景图片作为对应盒子对象背景后向左“拖动”62px，向上“拖动”32px开始显示此背景图标
ul.Sprites li span.a2{ background-position: -86px -32px}设置背景图片作为对应盒子对象背景后向左“拖动”86px，向上“拖动”32px开始显示此背景图标
ul.Sprites li span.a3{ background-position: -110px -32px}设置背景图片作为对应盒子对象背景后向左“拖动”110px，向上“拖动”32px开始显示此背景图标
ul.Sprites li span.a4{ background-position: -133px -32px}设置背景图片作为对应盒子对象背景后向左“拖动”133px，向上“拖动”32px开始显示此背景图标
ul.Sprites li span.a5{ background-position: -158px -32px}设置背景图片作为对应盒子对象背景后向左“拖动”158px，向上“拖动”32px开始显示此背景图标
```

### 缺点
* CSS Sprites在维护的时候比较麻烦，如果页面背景有少许改动，一般就要改这张合并的图片
* 在宽屏，高分辨率的屏幕下的自适应页面，你的图片如果不够宽，很容易出现背景断裂




