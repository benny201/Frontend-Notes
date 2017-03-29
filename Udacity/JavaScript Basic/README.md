# JavaScript Basic

##Dev-tool
* DON'T FORGET THE semicolon ！！！

## Jquery
* append(): 在被选元素的结尾插入内容
```JavaSript
$(selector).append(content)
```
* prepend(): 在被选元素的开头插入内容

## Data type
### number
* all are 64 bits
### String
* replace()
```JavaScript
var email = "447093943@qq.com"
email.replace("qq", "gmail");
```
* slice(start, end); 截取start／end，并返回(不包括end的位置).
* toUpperCase();

### Truthy
* true
* non-zero
* String
* object
* array
* function

### Falsy
* false
* 0
* ""
* undefined: 变量不存在，编译器不知道你指的啥
* null: 变量存在，但没值，占位符
* NaN

### Array
* var arrayName = [];
* slice() in array!
```JavaScript
var newArray = array.slice(0);
```
* pop(); operation like a stack!
* push();
* join("string"): 以string为间隔合并

### Object
* not classes
* 对象字面值
```JavaScript
var bio = {
    'name' : "Zhibin Wu",

}
```
* property: object.propertyName = "hi" to get a new property for the object;

## JSON
Json stands for JavaScript Object Notation.

### Json Format
```JavaScript
var education = {
    "schools": [
        {
            "school": "UCSC",
            "schools'cities": "first class",
            "majors": "CE",
            "minors": "EE",
            "graduation_year": "2018",
            "course_info": "JS Basic"
        }
    ]
}
```


### Json validator
* www.jsonlint.com

## Evaluators
* ==
* ===(最保险)
* <, > , <= ,>=
```JavaScript
严格相等 (===) 对比宽松相等 (==)

当连用三个等号 === 时，在执行比较之前， 不进行任何类型转换。如果两值属于不同类型，例如， 字符串和数字，则二者永远也不能相等。 仅当数值相等且类型相同时， 才返回 true。

宽松相等 == 会检查两值是否属于同一 类型，如果类型不同，则会先转换为相同类型，然后再进行比较。如果 类型相同，则 === 和 == 的结果 完全一致。如果不同，则可能会产生 意外结果。
```

## loop
### for-in loop
* like the for-each loop in JAVA
```JavaScript

var works = ["a", "b", "c"];
for (work in works) {
    console.log(work); -> this will just get the index of the array, FALSE!!!
    console.log(works[work]); -> True!!!
}
```
* 不要使用for－in循环

## JavaScript Scoping
* not**block-level scope**, but**function-level scope**
* Blocks, such as if statements, do not create a new scope. Only functions create a new scope.
