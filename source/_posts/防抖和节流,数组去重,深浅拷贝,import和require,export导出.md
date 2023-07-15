---
title: 【前端八股文】防抖和节流,数组去重,深浅拷贝,import和require,export导出
description: 📚太难了，摆了摆了
mathjax: true
tags:
  - 面试
  - 前端八股文
categories:
  - 前端八股文
abbrlink: 2023716d
sticky: 2
swiper_index: 2
date: 2023-07-16 15:03:03
updated: 2023-07-16 20:00:00
cover: https://imgbed.zshlmy.love/picture/js汽水.jpg
keyword: 前端八股文,防抖和节流,数组去重,深浅拷贝,import和require,export导出,博客,雨打窗前
---

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

