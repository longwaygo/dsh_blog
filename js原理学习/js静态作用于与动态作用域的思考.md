# 静态作用于与动态作用域的思考

标签： javascript

---

**静态作用域的作用域当定义的时候就被确定了，不会因为调用的环境而改变。**

代码如下
---

    var value = 1;
    
    function foo() {
        console.log(value);
    }
    
    function bar() {
        var value = 2;
        foo();
    }
    
    bar();
    
    // 结果是 1
函数的作用域在定义的时候已经被确定。我一开始脑子里突然冒出了，this的指向问题怎么说。
然后翻看了一些资料，我发现自己搞错了一些问题。

this只是一个属性,它与js的函数或者变量本身的作用域是两个东西，换句话说。
**this只是一个辅助的工具，目的是让js能够拥有动态作用域的功能**
    var value = 1;
    
    function foo() {
        console.log(this.value);
    }
    
    function bar() {
        var value = 2;
        foo();
    }
    
    bar();
    
    // 结果是 2




