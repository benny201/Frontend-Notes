#数组
JavaScript的数组允许混合类型。
```JavaScript
var empty = [];
empty.length;
```

## 长度
每个数组都有一个length属性。但是这个length没有上界，数组可以无限扩展。
可以通过两种方式尾部加元素：
```JavaScript
1. numbers[numbers.length] = 1;
2. numbers.push(1);
```

## 删除
```JavaScript
arrayObject.splice(index,howmany,item1,.....,itemX)
index   必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。
howmany 必需。要删除的项目数量。如果设置为 0，则不会删除项目。
item1, ..., itemX   可选。向数组添加的新项目。
```

## 枚举
* 因为数组其实是对象，可以用for in来遍历。但是for in无法保证属性的顺序。
* 还是用for循环好。