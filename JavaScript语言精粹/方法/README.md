#方法

## array
### array.concat(item...)
返回一个新数组,将items附加到数组尾。

### array.join(separator)
以separator链接数组的内容

### array.pop()/array.push()
让array像stack一样工作

### array.reverse()
反转array中的元素的顺序。返回当前array。

### array.shift()
移除并返回一个元素，但是逼pop()慢很多

### array.slice(start,end)
slice方法可以对array做一段浅复制

### arrat.sort()
默认比较时都是字符串，所以比较前都会转换成字符串。
可以自定义比较的回调函数:
如果第一个参数应该排列在前面，则返回一个负数，如果第二个参数应该排列在后面，则返回一个正数。相等则为0.
```javascript
arr.sort(function(a, b) {
    return a - b;
})
```

### array.splice(start, count, item...)
splice函数会从start位置开始移除count个元素，然后插入item。

### array.unshift(item...)
从array头部插入item，并返回array长度。

## function.apply(this, args)
可传入任意数组
## Number

### number.toExponential(digits)
转换成指数形式的字符串。可选择digits个位的小数

### number.toFixed(digits)
转换成十进制数形式的字符串。可选择digits个位的小数

### number.toPrecision(Predigits)
转换成一个十进制形式的字符串。一共Predigits位数。

### number.toString(radix)

## Object

### Object.hasOwnProperty()
如果这个object包含了一个名为name，则返回true，原型链不会被检查。

## String

### String.charAt()

### string.charCodeAt()
类似charAt()但是返回ASCii码，超出长度范围则返回NaN
### string.fromCharCode(codes...)
从ascii码中返回一串字符串

### string.concat()
concat方法时链接字符串，然后返回新字符串。

### string.indexof()

### string.lastIndexOf()
从尾部开始搜索。

### string.localeCompare(that)
比较两个字符串。如果比that小，返回负数，大则正数，相等则零。

### string.match(regexp)
### string.search(regexp)

### string.replace(searchValue, replaceValue)
* searchValue可以是字符串，但是这种情况下只会在第一个出现的位置被替换
* searchValue也可以是正则表达式。
* replaceValue可以是一个`函数`，也可以是字符串。

### string.slice(start, end)
start,end都可以是负数，会与string.length相加。

### string.split(separator, limit)
limit可选被分割的片段数。
### string.substring(start, end)
不能处理负数，其他与slice一样。

### string.toUpperCase()/string.toLowerCase()






