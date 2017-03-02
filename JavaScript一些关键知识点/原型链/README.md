# 原型链

为了属性的重用
```
var newObject = Object.create(obejct);
```
通过原型链实现继承。

## new运算符的缺点
用构造函数生成实例对象，有一个缺点，那就是无法共享属性和方法。

```JavaScript
function DOG(name){
　　　　this.name = name;
　　　　this.species = '犬科';
　　}
然后，生成两个实例对象：
　　var dogA = new DOG('大毛');
　　var dogB = new DOG('二毛');
这两个对象的species属性是独立的，修改其中一个，不会影响到另一个。
　　dogA.species = '猫科';
　　alert(dogB.species); // 显示"犬科"，不受dogA的影响
```

## prototype属性的引入
实例对象一旦创建，将自动引用prototype对象的属性和方法。也就是说，实例对象的属性和方法，分成两种，一种是本地的，另一种是引用的。
```JavaScript
function DOG(name){
　　　　this.name = name;
　　}
　　DOG.prototype = { species : '犬科' };

　　var dogA = new DOG('大毛');
　　var dogB = new DOG('二毛');

　　alert(dogA.species); // 犬科
　　alert(dogB.species); // 犬科
```