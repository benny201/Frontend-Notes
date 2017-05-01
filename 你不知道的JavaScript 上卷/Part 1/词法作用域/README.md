# chapter 2: 词法作用域

JavaScript采用了`词法作用域模型`, 另外如Bash，Perl则使用了动态作用域。

* `词法作用域`: 就是书写代码时将变量和块作用域写在哪里决定的。
* `遮蔽效应`: 作用域查找会在找到第一个匹配的标识符时停止。
* `全局变量`: 全局变量都会变成全局对象，如浏览器中的window对象的属性，e.g. : window.a.

## 1. 欺骗词法
欺骗词法会使性能下降。
* 使用eval()。 但是在`"use strict";`情况下无用。
* with关键字。
```javascript
var obj = {
    a: 1,
    b: 2,
    c: 3
}

with(obj) {
    a = 3;
    b = 4;
    c = 5;
}

出现欺骗词法的情况：
function foo(bj) {
    with (obj) {
        a = 2;
    }
}
obj2 = {
    b: 1
}
foo (obj2);
这个时候obj2并没有a这个属性，所以自动为全局创建了一个a ＝ 2...
```

严格模式下，with被完全禁止。eval()会受限制。
最好不要使用这两个东西。


