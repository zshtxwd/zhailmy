---
title: 【前端人python学习日记】基础语法【三】
description: 🐍变强，然后赚很多钱给她更好的
mathjax: true
tags:
  - python
categories:
  - python学习日记
abbrlink: 2023902d
swiper_index: 2
date: 2023-09-02 00:20:10
updated: 2023-09-02 12:09:10
cover: https://imgbed.zshlmy.love/picture/python.jpeg
keyword: python,python基础语法,python自学,博客,雨打窗前
---

#### 文件操作

##### 操作文件的步骤

- 打开

- 读写
- 关闭

##### open()打开函数

`open(name，mode，encoding)`

三个**常用参数**，**encodeing**其实是**第四个**参数，所以我们用**关键字传参**，而不是位置传参

`f=open("D:/测试.txt","r",encoding="UTF-8")`

​	**name**要打开的目标文件名的字符串(可以包含目标文件的具体路径)

​	**mode**设置文件的访问模式(**只读**，**写入**，**追加**)

​	**encoding**编码格式，推荐使用**UTF-8**

**mode**常用的三种访问模式

![image-20230901220551881](https://imgbed.zshlmy.love/Typora/image-20230901220551881.png)

##### 读操作的相关方法

- **文件对象.read(num)**

读取文件内容，**num**为读取文件的字节数，不传入**num**则读取所有数据

- **文件对象.readlines()方法**

readlines可以按照**行**的方式，把**整个文件内容**一次性读取，返回一个**列表**，**每一行数据为一个元素**

- **文件对象.readline()方法**

readlines可以按照**行**的方式，**一行一行**的读取文件内容

------

在程序中连续调用两次`read`，第一次读取的结尾会被记录下来

第二次调用`read`的时候，会从**第一次的结尾**继续读

在**读文件**的时候，只要文件打开，不管调用什么方法，文件都会从**上一次读的结束位置继续开始**

------

可以使用for一行一行的遍历文件内容

```python
for line in open("python.txt","r"):
    print(line)
```

##### close()关闭函数

```python
f=open("python.txt","r")
f.close()
```

通过close关闭文件，如果不使用close关闭文件，并且**不结束程序**，那么python会一直**占用该文件**

##### with open语法

```python
with open ("python.txt","r") as f:
    f.read()
```

通过**with open**操作文件，可以在操作完成后**自动调用close**进行关闭

##### 基本写操作

```python
f=open("python.txt","w")
#打开文件
f.write("hello world")
#将内容写入内存中
f.flush()
#将内存中的内容刷到硬盘上
```

**write**并**没有完成文件写入**的操作，只是**将内容暂时存到内存中**，等**flush**执行时将**内存**中的内容**统一写入**硬盘

这样的好处是**不需要频繁操作硬盘导致效率下降**

前端OS：这让我想到vue框架，收集dom操作，最后统一渲染到页面上去，这样就提高了效率和资源损耗，也让我想到了使用canvas画				板，在画完东西之后，需要执行stroke()才能真正画出东西

##### 基本追加操作

不会像w一样覆盖原有内容，而是在原有内容后面接着写

```python
f=open("python.txt","a")
#打开文件
f.write("hello world")
#将内容写入内存中
f.flush()
#将内存中的内容刷到硬盘上
```

**write**并**没有完成文件写入**的操作，只是**将内容暂时存到内存中**，等**flush**执行时将**内存**中的内容**统一写入**硬盘

#### 异常

这还用我解释？

**遇到bug的两种处理方式**

- 不去理会，程序崩溃终止运行
- 对bug进行处理，程序继续运行

##### 捕获异常

- 捕获常规异常

```python
try:
    可能出现异常的代码
except:
    出现异常的操作
```

- 捕获指定类型异常

```python
try:
    可能出现异常的代码
except NameError as e:
    print("出现了变量未定义的异常")
```

- 捕获多个异常

```python
try:
    可能出现异常的代码
except (NameError,ZeroDivisionError):
    print("出现了变量未定义异常 或者 出现了除零异常")
```

- 捕获所有异常

```python
try:
    可能出现异常的代码
except Exception as e:
    print("出现了异常")
    print(e)
    
#或者

try:
    可能出现异常的代码
except:
    出现异常的操作
```

##### 异常的else和finally语法

```python
try:
    可能出现异常的代码
except:
    异常处理
else:
    没出现异常的情况
finally:
    无论是否出现异常都会执行
```

前端OS：这finally好像promise的finally啊

##### 异常的传递性

当函数func01中发生异常，并且没有捕获处理这个异常的时候，异常会传递到函数func02，当func02也没有捕获处理这个异常的时候main函数会捕获这个异常，这就是异常的传递性

前端OS：连续使用promise，可以在最后使用catch统一捕获错误

![image-20230901235313885](https://imgbed.zshlmy.love/Typora/image-20230901235313885.png)

#### 模块Module

前端OS：没必要解释，懂的都懂

##### 模块的导入

**`[from 模块名] import [模块|类|变量|函数|*] [as 别名]`**

`from`和`as`可以不写

##### 自定义模块

```python
#test.py
def plus(a,b):
    return a+b
```

```python
#当前文件
import test
test.plus(1,2)
```

自定义模块的模块名，就是py文件名

引入同名的模块，类，变量，函数，后面引入的会覆盖前面引入的

##### \_\_mian\_\_

只有在自己原本的文件中`__name__=="__mian__"`，这样可以在自定义模块中测试，又不用担心在引入模块时函数就调用

```python
def plus(a,b):
    return a+b
if __name__=="__mian__":
    plus(1,2)
```

##### \_\_all\_\_

```python
#test.py
__all__=['test_A']

def test_A(a,b):
    return a-b
def test_B(a,b):
    return a+b
```

```python
from test import *
#这里使用*
#如果没有写__all__，那么引入所有内容
#如果写了__all__，那么只引入__all__中准备的内容
```

##### 自定义包

只有文件夹里有**\_\_init\_\_.py**文件，才被称之为**包**

\_\_init\_\_.py文件可以**没有内容**，但**必须存在**

\_\_init\_\_.py文件里会写\_\_all\_\_的配置

##### 第三方包安装

`pip install -i https://pypi.tuna.tsinghua.edu.cn/simple 包名称`

在**pip**中使用清华大学提供的镜像下载第三方包
#### JSON

JSON数据格式用于在各种编程语言之间传递数据

前端OS：我可太熟悉了，我说怎么字典第一眼看上去这么眼熟，原来就是JSON

`JSON`和`python`中的**字典**，**列表嵌套字典**可以无缝切换，不能说相似吧，只能说是一模一样

##### JSON数据转化

将JSON数据与python数据之间互相转化

前端OS：是不是`JSON.stringfly`和`JSON.parse`啊？

- 引入JSON库

`import json`

- python数据转化成JSON数据

```python
data=[{"name":"张三","age":18},{"name":"李四","age":19}]

data=json.dumps(data)
#将python数据转为JSON字符串

data=json.loads(data)
#将JSON字符串转为python数据
```

中文转换时会有编码问题，我们可以设置**`ensure_ascii=False`**

```python
import json

data=[{"name":"张三","age":18},{"name":"李四","age":19}]

data=json.dumps(data,ensure_ascii=False)
#将python转为JSON
#设置ensure_ascii=False的意思是不使用ascii来转换他，把内容直接输出出去
#如果不设置，那么中文就会变成unicode字符
```



