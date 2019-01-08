# js执行栈与执行上下文理解

标签（空格分隔）： javascript

---
本文来自于
[冴羽博客](https://github.com/mqyqingfeng/Blog/issues/4)

[掘金子非](https://juejin.im/post/5ba32171f265da0ab719a6d7)

## 一、执行上下文栈

** JavaScript 引擎并非一行一行地分析和执行程序，而是一段一段地分析执行**

对于段的划分包括以下几个方面

1. 全局代码

2. 函数代码

3. eval代码（这玩意我也不知道是什么）

语言描述一下
执行一段代码
首先》将全局代码引入封装为执行上下文并放入执行栈底部》当遇到函数被调用时》开始将函数代码封装为执行上下文放入执行栈》调用结束以后根据后进先出的规则一次释放。
举个例子

    let a = 'Hello World!';
    
    function first() {
      console.log('Inside first function');
      second();
      console.log('Again inside first function');
    }
    
    function second() {
      console.log('Inside second function');
    }
    
    first();
    console.log('Inside Global Execution Context');

![代码的执行情况为](https://user-gold-cdn.xitu.io/2018/9/20/165f539572076fe3?imageslim)


## 二、执行上下文

创建执行上下文的步骤有：

1、	绑定this。

2、	创建词法作用域（静态作用域）

3、	创建变量作用域

### this的绑定
与介绍可参考[原型与原型链](https://github.com/longwaygo/dsh_blog/blob/master/js%E5%8E%9F%E7%90%86%E5%AD%A6%E4%B9%A0/js%E5%8E%9F%E5%9E%8B%E4%B8%8E%E5%8E%9F%E5%9E%8B%E9%93%BE%E7%9A%84%E6%80%9D%E8%80%83.md#2-this%E6%8C%87%E5%90%91%E9%97%AE%E9%A2%98)中的this介绍

### 词法环境
1、	词法环境的作用

（1）**将标识符（变量和函数的名字）与变量（函数对象、原始数据类型对象）进行关联（引用）。**

2、	词法环境由两个组件构成

（1）环境记录器：记录变量的与函数申明的具体位置

（2）外部环境引用：他可以访问父级的作用域

3、	词法环境的类型

（1）	全局环境：没有外部环境引用，环境记录器记录包括（原型函数，全局关联变量，例如window对象等）用户自己定义的全局变量

（2）	函数环境：环境记录器记录包括（函数内部用户定义的变量），外部环境引用（全局变量、包好此内部函数的外部函数）

（3）	环境记录器也因此分为两类

 . 声明式环境记录器（函数）：存储函数、变量、参数
 
 . 对象环境记录器（全局）：定义全局上下文中变量和函数的关系
 
### 变量环境（词法环境）

1.	记录变量声明语句在执行上下文中创建的绑定关系

2.	let、const与var的区别baokuo 

