#方法

## array.concat(item...)
返回一个新数组,将items附加到数组尾。

## array.join(separator)
以separator链接数组的内容

## array.pop()/array.push()
让array像stack一样工作

## array.reverse()
反转array中的元素的顺序。返回当前array。

## array.shift()
移除并返回一个元素，但是逼pop()慢很多

## array.slice(start,end)
slice方法可以对array做一段浅复制

## arrat.sort()
默认比较时都是字符串，所以比较前都会转换成字符串。
可以自定义比较的回调函数:
如果第一个参数应该排列在前面，则返回一个负数，如果第二个参数应该排列在后面，则返回一个正数。相等则为0.
```javascript
arr.sort(function(a, b) {
    return a - b;
})
```

## array.splice(start, count, item...)
splice函数会从start位置开始移除count个元素，然后插入item。

## array.unshift(item...)
从array头部插入item，并返回array长度。