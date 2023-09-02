---
title: 【前端八股文】this,apply,call,bind,作用域链,原型链,闭包
description: 🏃项目经理今天开始赶我走了
mathjax: true
tags:
  - 面试
  - 前端八股文
categories:
  - 前端八股文
abbrlink: 2023627d
swiper_index: 2
date: 2023-06-27 16:38:45
# updated: 2023-06-26 22:00:00
cover: https://imgbed.zshlmy.love/picture/js汽水.jpg
keyword: 前端八股文,this,apply,call,bind,作用域链,原型链,闭包,博客,雨打窗前
---

## 【前端八股文】promise,箭头函数,var,let,const

### this

#### 函数中this的指向问题

谁调用函数，this就指向谁

##### 全局作用域

在全局作用域中，函数没有被绑定到任何对象上，this指向全局对象（浏览器环境下是window，在node.js环境中this指向global）

```javascript
console.log(this)
```

##### 函数调用

当函数作为一个独立函数调用时，函数中this指向全局对象

```javascript
function mythis(){
    console.log(this)
}
```

##### 方法调用

当一个函数作为一个对象的方法时，this指向这个对象

```javascript
const obj={
    name:"jack",
    sayHello:function(){
        console.log('Hello,'+this.name)
    }
}
obj.sayHello()
//this指向obj这个对象
```

##### 构造函数

当一个函数用new关键字作为一个构造函数调用创建一个新实例的时候，this指向这个新的实例

```javascript
function Person(name){
    this.name=name
}
const jack=new Person('jack')
console.log(jack.name)
```

##### 显式绑定

通过call(),apply()，可以显式的指定函数的this值

```javascript
function sayHello(){
    console.log('Hello,'+this.name)
}
const obj1={name:'jack'}
const obj2={name:'john'}
sayHello.apply(obj1)
sayHello.call(obj2)
```

##### 箭头函数

箭头函数的this是在一开始就定义好的，而不是在运行时确定的，他会继承外部作用域的this值

```javascript
const obj={
    name:jack,
    sayHello:()=>{
        console.log('Hello,'+this.name)
    }
}
obj.sayHello()
//箭头函数的this指向外部作用域的this，这里输出Hello，undefined
```

### bind，apply，call

共同点：都是JavaScript内置方法，都改变this指向，都要接收一个要改变为this指向的对象

不同点：

​	bind是返回一个新的已经改变了this指向的函数，不会立即调用，但这会永久改变this指向

​		apply和call都是立即调用，只改变一次this指向

​			call是一个，一个传参数，apply是传一个数组或一个类数组



call和apply第一个参数为null或undefined时，指向全局对象



```javascript
const person = {
  name: 'John',
  greet: function(message) {
    console.log(message + ', ' + this.name);
  }
};

const person2 = {
  name: 'Jane'
};

// 使用 call 方法调用 person 对象的 greet 方法，并将 this 设置为 person2，传递参数 'Hello'
person.greet.call(person2, 'Hello'); 
// 输出: "Hello, Jane"

// 使用 apply 方法调用 person 对象的 greet 方法，并将 this 设置为 person2，传递参数数组 ['Hi']
person.greet.apply(person2, ['Hi']); 
// 输出: "Hi, Jane"

// 使用 bind 方法创建一个新函数，并将 this 设置为 person2
const greetPerson2 = person.greet.bind(person2);
// 调用新创建的函数，并传递参数 'Hola'
greetPerson2('Hola');
// 输出: "Hola, Jane"

```

### 原型链

在某些时候我们可以在构造函数的prototype中添加一些方法，使用这个构造函数创建的实例对象都会带上这个方法，当我们在一个对象上调用方法的时候，如果他在自身上找不到这个方法，他会在原型链上往上找，原型链的顶端是null

在浏览器打印的[[prototype]]和__ _proto_ _ _是等价的

每个JavaScript对象都有原型对象，对象可以通过__ _proto_ _ _来访问他的原型，对象的__ _proto_ _ _指向他的构造函数的prototype

```javascript
// 定义一个构造函数
function Person(name) {
  this.name = name;
}

// 在构造函数的原型上定义一个方法
Person.prototype.sayHello = function() {
  console.log("Hello, my name is " + this.name);
};

// 创建一个实例对象
var person1 = new Person("Alice");

// 调用实例对象的方法
person1.sayHello(); // 输出: Hello, my name is Alice

// 创建另一个实例对象
var person2 = new Person("Bob");

// 调用另一个实例对象的方法
person2.sayHello(); // 输出: Hello, my name is Bob

```

### 作用域链

当JavaScript执行时，每个函数都会创建一个作用域链，包含活跃对象和[[Scope]]

活跃对象包含函数的局部变量和参数

[[Scope]]属性指向当前函数所在作用域上的所有父级作用域

如果要获取一个变量的值没有在活跃对象上找到，他会去[[Scope]]上继续寻找，直到找到该变量或达到全局作用域

### 闭包

#### 闭包的产生

函数嵌套，内部函数可以引用外部函数作用域中的变量

```javascript
function outerFunction() {
  var outerVariable = 'I am from outer function';

  function innerFunction() {
    console.log(outerVariable); // 内部函数引用外部函数的变量
  }

  return innerFunction; // 返回内部函数
}

var closure = outerFunction(); // 调用外部函数，得到内部函数的引用

closure(); // 输出: "I am from outer function"
```

#### 闭包的作用

**保护变量**：闭包可以创建一个私有的作用域，将变量隐藏起来，只能通过内部函数来访问和修改。这样可以防止外部对变量的意外修改和访问，实现了数据的封装和保护。

**实现数据的持久化**：由于闭包的特性，内部函数持有对外部函数作用域的引用，使得外部函数的变量不会在函数执行完毕后被销毁。这样，可以通过闭包将数据持久化，使得数据在函数执行完毕后仍然存在，并可以被后续的操作所使用。

#### 闭包的缺点

会造成内存泄漏，因为被闭包保护的数据仍然被引用，js的v8引擎垃圾回收机制不会去回收内存

#### 闭包的处理

当闭包持有大量数据时，可能会导致内存泄漏。为了避免内存泄漏，应该注意在不需要使用闭包时解除对其的引用，让垃圾回收机制回收不再需要的内存。可以手动解除引用

```javascript
closure = null
```

或者使用一些技术手段如 WeakMap 来解决内存泄漏问题。