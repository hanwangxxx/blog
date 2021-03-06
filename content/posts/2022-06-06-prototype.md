---
layout: blog
title: 原型，原型链以及继承
date: 2022-06-06T20:56:31.290Z
description: 深入探讨原型链和继承
slug: "/prototype/"
code:
  code: "function "
  lang: javascript
tags:
image: https://camo.githubusercontent.com/9a69b0f03116884e80cf566f8542cf014a4dd043fce6ce030d615040461f4e5a/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f6d717971696e6766656e672f426c6f672f496d616765732f70726f746f74797065352e706e67
---
### 1. 原型

每一个JavaScript对象(null除外)在创建的时候就会与之关联另一个对象，这个对象就是我们所说的原型，每一个对象都会从原型"继承"属性。

### 2. 原型链

**原型链的本质是拓展原型搜索机制。**

每个实例对象都有一个私有属性 \_\_proto\_\_（隐式原型）。该属性指向它的构造函数的原型对象 prototype（显式原型）。该原型对象的 \_\_proto\_\_ 也可以指向其他构造函数的 prototype。当试图访问一个对象的属性时，它不仅仅在该对象上搜寻，还会搜寻该对象的原型，以及该对象的原型的原型，依次层层向上搜索，直到找到一个名字匹配的属性或直到一个对象的 \_\_proto\_\_ 指向 null。根据定义，null 没有原型，并作为这个原型链中的最后一个环节。

![](https://camo.githubusercontent.com/9a69b0f03116884e80cf566f8542cf014a4dd043fce6ce030d615040461f4e5a/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f6d717971696e6766656e672f426c6f672f496d616765732f70726f746f74797065352e706e67)

### 3. 原型链继承

```js
function SuperType() {
  this.b = \[1, 2, 3];
}

function SubType() {}

SubType.prototype = new SuperType();
SubType.prototype.constructor = SubType;

var sub1 = new SubType();
var sub2 = new SubType();

// 这里对引用类型的数据进行操作
sub1.b.push(4);

console.log(sub1.b); // \[1,2,3,4]
console.log(sub2.b); // \[1,2,3,4]
console.log(sub1 instanceof SuperType); // true
```

### 构造函数继承

[](http://febook.hzfe.org/awesome-interview/book2/js-inherite#3-%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0%E7%BB%A7%E6%89%BF "Direct link to heading")构造函数继承的思想：**子类型构造函数中调用父类的构造函数，使所有需要继承的属性都定义在实例对象上**。

```
function Parent () {
    this.names = ['kevin', 'daisy'];
}

function Child () {
    Parent.call(this);
}

var child1 = new Child();

child1.names.push('yayu');

console.log(child1.names); // ["kevin", "daisy", "yayu"]

var child2 = new Child();

console.log(child2.names); // ["kevin", "daisy"]
```

### 组合继承（伪经典继承）

组合继承的思想：**使用原型链实现对原型属性和方法的继承，借用构造函数实现对实例属性的继承**。

```
function SuperType(name) {
  this.name = name;
  this.a = "HZFE";
  this.b = [1, 2, 3, 4];
}

SuperType.prototype.say = function () {
  console.log("HZFE");
};

function SubType(name) {
  SuperType.call(this, name); // 第二次调用 SuperType
}

SubType.prototype = new SuperType(); // 第一次调用 SuperType
SubType.prototype.constructor = SubType;
```



###  寄生组合式继承

寄生组合式继承的思想：**借用构造函数来继承属性，使用混合式原型链继承方法**。

```
// 在函数内部，第一步创建父类原型的一个副本，第二部是为创建的副本添加 constructor 属性，
// 从而弥补因重写而失去的默认的 constructor 属性。最后一步，将新创建的对象（即副本）赋值给予类型的原型。
function inheritPrototype(subType, superType) {
  var prototype = Object.create(superType.prototype); // 创建对象
  prototype.constructor = subType; // 增强对象
  subType.prototype = prototype; // 指定对象
}

function SuperType(name) {
  this.name = name;
}

SuperType.prototype.sayName = function () {
  console.log(this.name);
};

function SubType(name, num) {
  SuperType.call(this, name);
  this.num = num;
}

inheritPrototype(SubType, SuperType);

SubType.prototype.sayNum = function () {
  console.log(this.num);
};
```

### Reference

JavaScript深入之从原型到原型链  https://github.com/mqyqingfeng/Blog/issues/[](https://github.com/mqyqingfeng/Blog/issues/16#)

JavaScript深入之继承的多种方式和优缺点 https://github.com/mqyqingfeng/Blog/issues/16

重新认识JavaScript面向对象: 继承 https://coffe1891.gitbook.io/frontend-hard-mode-interview/1/1.2.1

ES5、ES6 如何实现继承 http://febook.hzfe.org/awesome-interview/book2/js-inherite