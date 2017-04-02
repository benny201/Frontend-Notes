#chapter 4


## Node类型

### childNodes属性
它是一个包含全部子元素的数组:
```javascript
element.childNodes
```
#### length属性
childNodes.length

### nodeType
由childNodes返回的数组不仅包含element节点，而且空格和换行符都会被解析为节点。
所以用nodeType来判断在于哪个节点打交道是必要的。
```javascript
node.nodeType

1. 元素节点：nodeTyep ＝ 1；
2. 属性节点：nodeType ＝ 2；
3. 文本节点：nodeType ＝ 3；
```

### nodeValue属性
想改变一个文本节点的值，那就使用DOM提供的nodeValue属性！
但是非`文本节点`的nodeValue很可能是空值。比如`<p>`的nodeValue属性就是null，因为真正存文本的是它的儿子`文本节点`

### firstChild和lastChild
比`childNodes[0]`和`childNodes[childNodes.length - 1]`的可读性好!