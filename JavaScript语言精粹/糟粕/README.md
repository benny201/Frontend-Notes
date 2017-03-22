# 糟粕

## 全局变量
JavaScript中如果不声明var的话会自动变成全局变量。

## 作用域
不提供块级作用域。

## 自动插入分号
JavaScript有一个机制，它试图通过自动插入分毫来修正有缺损的程序。
```JavaScript
return
{
    status: true
}
会被认定为：
return;
{
    status: true
};
这就是undefined了。
```

## 保留字
很多没有使用的变量名都作为了保留字。但是很多在ES6使用了，所以没毛病。

## Unicode


## typeOf
```javascript
typeof null -> object
更好的方法：
valur === null
```

## parseInt
这个函数的缺点是，它虽然是吧字符串转换为整数的，但是遇到非数字时会停止解释：
```javascript
parseInt("16") 和 parseInt("16 tons") 是一样的。
```
它并不会提示出现了额外的文本。

## "+"

## 浮点数

## NaN
它表示不是一个数字。
但是：
```javascript
typeof NaN === 'number' ---> true!!!
```
而且NaN还不是它自己！！！
```javascript
NaN === NaN  //false
```
可以用`isNaN(value)`来判断。
最好判断是不是数字的方法是用isFinite()，它会筛选NaN和Infinity,但是它会把输入转换成一个数字，所以要先判断是不是number类型。
```javascript
function isNumber(value) {
    return typeof value === 'number' && isFinite(value);
}
```

## 伪数组
JavaScript中没有真正的数组。永远不会越界。
要判断一个对象是不是一个数组，要通过constructor中去判断。
```javascript
if (value && typeof value === 'object' && value.constructor === Array) {

}
```
## 假值

## hasOwnProperty

## 对象
