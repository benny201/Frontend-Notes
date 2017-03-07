# 继承

### 伪类
通过prototype添加继承。
待续，看得蒙蔽

### 原型
原型模式中，抛弃类的定义，基于原型的继承：一个新对象可以继承一个旧对象的属性。
```JavaScript
if (typeof Object.beget !== 'function') {
    Object.beget = function(o) {
        var F = function() {};
        F.prototype = o;
        return new F();
    };
}
```
原型继承：
```JavaScript
var women = {

}

var myWomen = Object.beget(women);
```


### 函数化
以上方法的弱点是：所有属性都是可见的。
