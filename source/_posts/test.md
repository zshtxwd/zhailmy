---
title: 【前端八股文】ES6新特性,面向对象编程,事件循环,null和undefined,前端缓存的理解,防抖和节流,数组去重,深浅拷贝,import和require,export导出
description: 📚行了，已经准备卷铺盖回家了
mathjax: true
tags:
  - 面试
  - 前端八股文
categories:
  - 前端八股文
abbrlink: 2023715d
sticky: 2
swiper_index: 2
date: 2023-07-15 18:19:03
updated: 2023-07-15 22:00:00
cover: https://imgbed.zshlmy.love/picture/js汽水.jpg
keyword: 前端八股文,面向对象编程,事件循环,null和undefined,前端缓存的理解,防抖和节流,数组去重,深浅拷贝,import和require,export导出,博客,雨打窗前
---

### ES6新特性

#### 块级作用域

引入`let`和`const`关键字，允许在块级作用域中声明变量和常量，解决了以前使用`var`关键字带来的作用域问题

#### 箭头函数

提供了一种更简洁的函数定义语法，使用`=>`箭头符号，可以减少函数声明的代码量

#### 默认参数

在函数定义时设置参数的默认值，在不传入参数时使用默认值

#### 扩展运算符

在函数调用，数组，对象中展开数组或对象

#### 解构赋值

允许通过模式匹配的方法从数组或对象中解析出值，并赋给变量，可以快速获取使用值

#### 模板字符串

使用反引号\`包裹字符串，使用`${}`插入变量和表达式，支持多行字符串的书写

#### 类

引入类`class`的概念，并通过`constructor`方法定义构造函数，简化了面向对象编程

#### 模块化

ES6引入了原生的模块系统，使用`import`和`export`关键字可以方便地导入和导出模块，提供了更好的代码组织和复用

#### Promise和异步await

引入了Promise对象和异步/await语法，提供了更好的异步编程方式，避免了回调地狱

#### Map和Set

引入了Map和Set两种新的数据结构，提供了更方便高效的数据存储和操作方式

#### 数组方法

1. `find()`：返回数组中满足条件的第一个元素。
2. `findIndex()`：返回数组中满足条件的第一个元素的索引。
3. `filter()`：返回数组中满足条件的所有元素组成的新数组。
4. `forEach()`：遍历数组中的每个元素，并执行指定的回调函数。
5. `map()`：将数组中的每个元素进行处理，返回一个新数组。
6. `some()`：判断数组中是否有至少一个元素满足指定条件。
7. `every()`：判断数组中的所有元素是否都满足指定条件。
8. `reduce()`：对数组中的元素进行累加或累积计算。
9. `includes()`：判断数组是否包含指定的元素。
10. `Array.from()`：将类似数组的对象或可迭代对象转换为真正的数组。

#### 字符串方法

1. `startsWith()`：判断字符串是否以指定的字符开头。
2. `endsWith()`：判断字符串是否以指定的字符结尾。
3. `includes()`：判断字符串是否包含指定的字符。
4. `repeat()`：重复字符串指定次数。
5. `padStart()`：在字符串的开头添加指定字符，直到字符串达到指定长度。
6. `padEnd()`：在字符串的结尾添加指定字符，直到字符串达到指定长度。
7. `trim()`：去除字符串两端的空格。

### 面向对象编程

#### 面向对象的特征

1、“抽象”，把现实世界中的某一类东西，提取出来，用程序代码表示；

2、“封装”，把过程和数据包围起来，对数据的访问只能通过已定义的界面；

3、“继承”，一种联结类的层次模型；

4、“多态”，允许不同类的对象对同一消息做出响应。

### 事件循环

事件循环过程确保了 JavaScript 在单线程环境下的异步执行

通过将异步任务转换为微任务，在适当的时机执行，保证了任务的顺序性和及时性

1. 同步任务执行，这个过程可能会产生微任务，将微任务加入到微任务队列中

2. 微任务执行，微任务执行的时候可能会产生新的微任务，系统会将所有微任务执行完成，直到微任务队列为空

3. 执行宏任务，执行过程可能会产生微任务，将微任务加入到微任务队列中

4. 微任务执行，微任务执行的时候可能会产生新的微任务，系统会将所有微任务执行完成，直到微任务队列为空

5. 执行下一个宏任务，执行过程可能还会产生微任务，将微任务加入到微任务队列中

再次执行2，如此往复，事件就循环起来了

### null和undefined

undefined代表未定义的，通常是

- 定义一个变量没有初始化，JavaScript就会给他一个undefined
- 没有给一个形参传实参，那么这个形参的变量值为undefined
- 一个没有指定返回值的函数调用后返回undefined

null代表一个空值，JavaScript不会主动给一个变量设置null，JavaScript只会给一个未初始化的变量设置为undefined，它是用来让程序员表明某个用var声明的变量时没有值

### 前端缓存的理解 \|| 前端数据持久化的理解

http缓存是做http请求传输时带上的缓存，一般是后端配置，主要在服务器代码上配置，浏览器缓存一般是前端在js中配置的

一个优秀的缓存策略可以缩短网页请求资源的距离，减少延迟，并且由于**缓存文件可以重复利用**，还可以减少带宽，降低网络负荷

缓存是最简单高效的数据请求优化方法，数据请求可分为，发送请求，后端处理，浏览器响应三个阶段，缓存可以在一和三中进行优化，比如直接使用缓存不请求数据，或者前端发送请求，但后端和前端数据一样，后端就不用回传数据，减少浏览器响应数据

### 防抖和节流

#### 防抖

防抖是触发后在单位时间里，再次触发，会重新计算触发时间

可以理解成游戏里的回城，点击回城后，在回城过程里再次点击回城，回城会重新开始读条

非立即执行版的意思是触发事件后函数不会立即执行，而是在 n 秒后执行，如果在 n 秒内又触发了事件，则会重新计算函数执行时间。

立即执行版的意思是触发事件后函数会立即执行，然后 n 秒内不触发事件才能继续执行函数的效果。

#### 节流

节流是单位时间里，多次触发，事件只执行一次，会稀释函数执行频率

可以理解成游戏里的技能cd，cd没转好，点技能也没用

对于节流，一般有两种方式可以实现，分别是时间戳版和定时器版

### 数组去重

- 利用ES6 Set去重（ES6中最常用）
- 利用for嵌套for，然后使用splice去重（ES5中最常用）
- 利用indexOf去重
- 利用sort
- 利用includes
- 利用hasOwnProperty
- 利用filter
- 利用递归去重
- 利用Map数据结构去重

### 深浅拷贝

深拷贝只针对Array和Object这种引用类型的数据

我们在定义一个引用类型的数据的变量后，JavaScript会为这个数据开辟一个内存空间，然后把这个内存空间的地址赋给这个变量

浅拷贝就是给新的变量拷贝这个引用数据的引用，新变量将引用原始数据的同一存储位置，因此对其中一个变量所做的更改会反映在另一个变量中，因为这两个变量的引用指向同一片内存空间

深拷贝会创建一个新的数据结构，并将原始数据的值复制到新的存储位置中，两个变量将引用不同的内存位置，因此对一个变量的更改不会影响到另一个变量

![avatar](https://img-blog.csdnimg.cn/img_convert/6e13a5cbeab9aaf0a19bcbf88d9b2cde.png)

#### 深拷贝的方法

- JSON序列化与反序列化

```javascript
let clonedObject = JSON.parse(JSON.stringify(originalObject));
```

- 递归复制
- 使用第三方库，例如lodash的cloneDeep



### import和require

- 在ES6模块系统中，import语句在代码编译阶段执行，而require在CommonJS模块系统中是在运行时执行的。
- import语句必须放在文件的顶部，不能在条件语句或函数中动态导入模块，而require可以根据需要动态加载模块。
- 无论是import还是require，当导入的模块是可变对象时，修改导入的对象会影响原始对象，需要进行深拷贝操作以避免修改原始对象。
- import语句有助于静态分析和优化，实现Tree-shaking（消除未使用的代码）的可能性，而require在CommonJS模块系统中不支持静态分析和优化。
- import语句是ES6模块系统的一部分，需要在浏览器中使用时进行转换为ES5语法，通过构建工具（如Webpack、Babel）可以实现在现代浏览器中使用import语句。
- require是Node.js中的模块系统，不直接适用于浏览器环境，但现代浏览器对ES6模块进行了广泛支持。
- require使用module.exports导出模块，而import使用export关键字导出模块，支持具名导出和默认导出。
- require通过相对路径或绝对路径解析模块，而import支持相对路径、绝对路径和模块名称解析，使用更先进的模块解析算法。
- require适用于Node.js环境，import适用于现代浏览器和一些支持ES6模块的开发环境。

需要注意的是，尽管现代浏览器和构建工具对import语法进行了广泛支持，但在特殊情况下可能需要进行转码或使用其他解决方案以实现更广泛的浏览器兼容性。



### export导出

#### 默认导出

默认导出允许在一个模块中只导出一个默认的值，该值可以是任何类型，例如对象、函数或类。在导入时，不需要使用花括号，而是直接指定导入的名称。

```JavaScript
javascriptCopy code// module.js
export default function add(a, b) {
  return a + b;
}

// 使用默认导出
// main.js
import add from './module.js';
console.log(add(2, 3)); // 输出: 5
```

#### 具名导出

具名导出允许在一个模块中导出多个变量、函数或类，并使用花括号指定要导入的名称。

```javascript
javascriptCopy code// module.js
export const name = 'John';
export function sayHello() {
  console.log(`Hello, ${name}!`);
}

// 使用具名导出
// main.js
import { name, sayHello } from './module.js';
console.log(name);      // 输出: John
sayHello();             // 输出: Hello, John!
```

#### 分别导出

分别导出允许在一个模块中同时使用默认导出和具名导出。

```JavaScript
javascriptCopy code// module.js
const name = 'John';
function sayHello() {
  console.log(`Hello, ${name}!`);
}

export { name, sayHello };

export default function add(a, b) {
  return a + b;
}

// 使用分别导出
// main.js
import add, { name, sayHello } from './module.js';
console.log(add(2, 3)); // 输出: 5
console.log(name);      // 输出: John
sayHello();             // 输出: Hello, John!
```

#### 导出重命名

```java
// module.js
const name = 'John';
export { name as firstName };

// 使用重命名的导出变量
// main.js
import { firstName } from './module.js';
console.log(firstName); // 输出: John
```
