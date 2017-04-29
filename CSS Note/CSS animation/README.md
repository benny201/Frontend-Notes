# CSS动画
> http://www.zhangxinxu.com/wordpress/2010/11/css3-transitions-transforms-animation-introduction/

CSS3动画相关的几个属性是：transition, transform, animation
* transition指过渡
* transform指变换,与transition结合使用
* animation自成一家，最先出现于Safari
* 尽可能的让动画元素不在文档流中，以减少重排

动画例子:
> http://www.zhangxinxu.com/study/201011/css3-transition-animate-demo-14.html

## transition过渡

* transition-property :* //指定过渡的性质，比如transition-property:backgrond 就是指backgound参与这个过渡
* transition-duration:*//指定这个过渡的持续时间
* transition-delay:* //延迟过渡时间
* transition-timing-function:*//指定过渡类型，有ease | linear | ease-in | ease-out | ease-in-out | cubic-bezier
```css
ease-in表示先慢后快, ease-out表示先快后慢, ease-in-out表示由慢到快在到慢
transition: background-color 0.3s ease;
transition:all... all表示所有的属性都有过度效果。
```


## transform
* rotate()表示旋转，rotatex() 和 rotatey() 。。。
* skew()表示倾斜: `skew(20deg)`
* translate()表示变动，位移`:translate(120px,0)`
* 一个元素通过translate3d右移500px的动画流畅度会明显优于使用left属性,left会额外触发repaint



## animations
```css
animation-name: 规定 @keyframes 动画的名称。
animation-duration: 规定动画完成一个周期所花费的秒或毫秒。默认是 0。;
animation-iteration-count: 规定动画被播放的次数。默认是 1。;
animation-direction: 规定动画是否在下一周期逆向地播放。默认是 "normal", "alternate": 动画应该轮流反向播放。;
animation-delay: 规定动画何时开始。默认是 0;
animation-timing-function: 规定动画的速度曲线。默认是 "ease"。;
```
### @keyframes规则
```css
@keyframes myfirst
{
from {background: red;}
to {background: yellow;}
}
当您在 @keyframes 中创建动画时，请把它捆绑到某个选择器，否则不会产生动画效果。
通过规定至少以下两项 CSS3 动画属性，即可将动画绑定到选择器：
规定动画的名称
规定动画的时长
```
* 请用百分比来规定变化发生的时间，或用关键词 "from" 和 "to"，等同于 0% 和 100%, `应该始终定义 0% 和 100% 选择器`
```css
@keyframes myfirst
{
0%   {background: red;}
25%  {background: yellow;}
50%  {background: blue;}
100% {background: green;}
}
```
* 绑定元素
```css
div
{
animation: myfirst 5s;
-moz-animation: myfirst 5s; /* Firefox */
-webkit-animation: myfirst 5s;  /* Safari 和 Chrome */
-o-animation: myfirst 5s;   /* Opera */
}
```
## 兼容性
* firefox: -moz-
* webkit: -webkit-
* opera: -o-