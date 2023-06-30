---
title: 【前端八股文】promise,箭头函数,var,let,const
description: 📚失业了，快复习复习找新工作
mathjax: true
tags:
  - 面试
  - 前端八股文
categories:
  - 前端八股文
abbrlink: 2023626d
sticky: 2
swiper_index: 2
date: 2023-06-25 18:19:03
updated: 2023-06-26 22:00:00
cover: https://imgbed.zshlmy.love/picture/js汽水.jpg
keyword: 前端八股文,promise,箭头函数,var,let,const,博客,雨打窗前
---

## 【前端八股文】promise,箭头函数,var,let,const

### promise

promise是JavaScript中用来处理异步操作的对象，代表了一个异步操作的最终结果

new Promise（（resolve，reject）=>{...}）这里的resolve和inject是等会通过then和catch传入的两个回调函数

```javascript
// 异步函数，返回一个Promise对象
const fetchData = () => {
 return new Promise((resolve, reject) => { 
//这里的resolve是等会通过then传入成功的回调
  setTimeout(() => {
   resolve('Data fetched');
//这里的resolve是调用promise的resolve方法把promise状态设置为成功
  }, 2000);
 });
};

// 使用async关键字定义的异步函数
const getData = async () => {
 try {
  console.log('Fetching data...');
  const result = await fetchData(); // 等待Promise对象的解析
  console.log(result);
  console.log('Data fetched successfully!');
 } catch (error) {
  console.error('Error:', error);
 }
};

// 调用异步函数
getData();
```

promise是用来解决回调地狱问题，promsie可以用来做网络请求，定时器操作，文件读写操作等

```javascript
const delay = (milliseconds) => {
 return new Promise((resolve) => {
  setTimeout(resolve, milliseconds);
 });
};
console.log('开始执行');
delay(2000)
 .then(() => {
  console.log('延迟2秒后执行');
 })
 .catch((err) => {
  console.error('发生错误:', err);
 });
//这个例子中体现了promise可以在执行完后再指定回调
```

#### promise的同步与异步

同步过程：

创建Promise对象：当调用Promise的构造函数时，创建Promise对象是同步执行的。
执行executor函数：executor函数会立即执行，它接收两个参数(resolve和reject)并立即执行其中之一。
返回Promise对象：Promise构造函数返回Promise对象本身，这也是同步操作。
异步过程：

处理.then()和.catch()：通过调用.then()和.catch()方法，可以为Promise对象添加成功和失败的回调函数。这些回调函数是异步执行的，它们会在Promise的状态改变后执行，而不会阻塞后续代码的执行。
异步操作的解析：如果在Promise对象的异步操作完成之前调用了.then()方法，成功回调函数会被加入到微任务队列中，并在当前同步代码执行完毕后执行。这样可以确保回调函数在异步操作完成后执行。
异步操作的延迟：如果在Promise对象的异步操作完成之前调用了.then()方法，异步操作的执行会被延迟到当前同步代码执行完毕后才会开始。

总之，Promise的创建和执行executor函数是同步的过程，而处理.then()和.catch()以及异步操作的解析和延迟是异步的过程。这种异步性质使得Promise能够更好地处理异步操作，并避免了回调地狱的问题。

promise的主体部分代码是同步执行，then和catch是异步执行的

#### promsie的状态

promise有三种状态，pending，rejected（失败），fullfilled（成功）

Promise的状态一旦改变，就不会再变，任何时候都可以得到这个结果，状态不可以逆，只能由 pending变成fulfilled或者由pending变成rejected

#### promise的优点

promise的返回值还是promise，使用then来指定回调，使用catch来捕获错误，catch可以放在最后统一捕获错误

promise相比于传统链式回调的优点在于：传统链式回调要在有结果之前就提前指定好回调，promise可以在获取结果之后再去指定回调

#### promise的缺点

- 无法取消Promise,一旦新建它就会立即执行，无法中途取消

- 如果不设置回调函数，Promise内部抛出的错误，不会反映到外部

- 当处于pending状态时，无法得知目前进展到哪一个阶段，是刚刚开始还是即将完成

#### promise的方法

promise几种常用方法，除了then用来指定成功时的回调和catch用来捕获错误还有：

race和all，race会将最先有结果的promise最为整个promise的结果，all会在所有promise都有结果后再返回结果，如果有一个promise是失败的，那么整个promise的结果都是失败的，all方法返回的promise是一个数组，包含所有promise的结果

finally无论成功还是失败都会调用的回调

常用的方法还有reject和resolve，resolve传入的参数是对的就返回成功的promise，resolve的参数是失败的就返回失败的promise，无论reject的参数是什么都返回失败的promise

#### async和await的使用

我们还可以使用async和await让代码更加简洁易读



### 箭头函数

#### 箭头函数与普通函数的区别：

1. 箭头函数没有自己的this，因此在确定this的值时需要通过查找作用域链。如果箭头函数被非箭头函数包含，this绑定的就是最近一层非箭头函数的this。
2. 箭头函数没有自己的arguments对象，但可以访问外围函数的arguments对象。
3. 箭头函数不能通过new关键字调用，也没有new.target[^new.target]值和原型。

#### 箭头函数的特点：

1. 语法更加简洁、清晰。

2. 箭头函数继承而来的this指向永远不变，它只会从自己的作用域链的上一层继承this。

3. .call()/.apply()/.bind()无法改变箭头函数中this的指向。

4. 箭头函数不能用作构造函数，不能通过new关键字实例化。

5. 箭头函数没有自己的arguments对象，可以使用rest参数来访问箭头函数的参数列表。

6. 箭头函数没有原型prototype。

7. 箭头函数不能用作Generator函数，不能使用yield关键字。

8. 箭头函数不具有super，也不具有new.target[^new.target]

   [^new.target]: 当使用 `new` 关键字调用构造函数创建实例时，`new.target` 会引用正在被构造的对象的构造函数。换句话说，它提供了对正在被构造的类或构造函数的引用

   



### var,let,const

#### var

- 全局声明：使用`var`关键字声明的变量具有全局作用域，可以在代码中的任何位置访问。
- 变量提升：在变量声明之前就可以访问变量，但其值会是`undefined`。这是因为变量声明会被提升到作用域的顶部，但变量赋值的操作会保留在原来的位置。
- 可重复定义：可以在同一作用域内多次使用`var`声明同一个变量，后面的声明会覆盖前面的声明。
- 可修改值：使用`var`声明的变量的值是可变的，可以通过赋值运算符进行修改

var只有全局作用域和函数作用域，所谓全局作用域就是在代码的任何位置都能访问var声明的变量，而函数作用域在变量声明的当前函数内部访问变量。函数外部是无法访问函数内部声明的变量的

```javascript
function example() {
  var y = 20; // 函数作用域
  console.log(y); // 在函数内部可以访问变量y
}
example(); // 输出: 20
console.log(y); // 报错: ReferenceError: y is not defined
```

```javascript
function example() {
  y = 20; // 函数作用域
  console.log(y); // 在函数内部可以访问变量y
}
example(); // 输出: 20
console.log(y); // 输出: 20
```


#### let

- 块级作用域：使用`let`关键字声明的变量具有块级作用域，仅在其声明的块内部可见。
- 不能重复定义：在同一作用域内，不能使用`let`重新声明已存在的变量。这样可以避免变量的重复定义和潜在的错误。
- 可修改值：使用`let`声明的变量的值是可变的，可以通过赋值运算符进行修改。

- 其实是存在变量提升的，但是有暂时性死区[^暂时性死区]

#### const

- 块级作用域：使用`const`关键字声明的变量同样具有块级作用域，仅在其声明的块内部可见。
- 必须初始化：使用`const`声明变量时必须进行初始化，即必须给变量赋初始值。
- 不能修改值：使用`const`声明的变量是常量，其值在初始化后就不能被修改，尝试修改将会导致错误。
- 其实是存在变量提升的，但是有暂时性死区[^暂时性死区]

需要注意的是，虽然使用`const`声明的变量值不能被直接修改，但对于复合类型（如对象和数组），其内部的属性或元素是可以被修改的。`const`只保证变量绑定的引用不变，而不保证引用指向的对象不变。

|                            | var                   | let                                    | const                                  |
| -------------------------- | --------------------- | -------------------------------------- | -------------------------------------- |
| 作用域                     | 函数作用域/全局作用域 | 块级作用域                             | 块级作用域                             |
| 声明提升                   | 提升变量名和初始化    | 仅提升变量名，不包括初始化             | 仅提升变量名，不包括初始化             |
| 暂时性死区                 | 无                    | 存在，访问会抛出 `ReferenceError` 错误 | 存在，访问会抛出 `ReferenceError` 错误 |
| 重复声明                   | 允许                  | 不允许                                 | 不允许                                 |
| 全局声明时作为window的属性 | 是                    | 否                                     | 否                                     |

[^暂时性死区]: 变量声明会在作用域的顶部进行提升，但初始化被留在原地，直到定义位置之后的代码才会执行。在变量声明之前访问该变量会导致暂时性死区（TDZ）的出现，会抛出 `ReferenceError` 错误。只有在声明语句执行之后，变量才会进入到可访问的状态