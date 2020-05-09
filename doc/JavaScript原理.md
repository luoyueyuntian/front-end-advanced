### new一个对象的过程
+ 1.以构造器的prototype属性为原型，创建新对象；
<pre><code>let child = Object.create(Parent.prototype);</code></pre>
+ 2.将this和调用参数传给构造器执行
<pre><code>let result = Parent.apply(child, rest);</code></pre>
+ 3.如果构造器没有手动返回对象，则返回第一步的对象
<pre><code>return typeof result  === 'object' ? result : child;</code></pre>

用代码模拟new的过程应该为：
<pre><code>let newObject = function (Parent, ...rest) {
    // 1.以构造器的prototype属性为原型，创建新对象；
    let child = Object.create(Parent.prototype);
    // 2.将this和调用参数传给构造器执行
    let result = Parent.apply(child, rest);
    // 3.如果构造器没有手动返回对象，则返回第一步的对象
    return typeof result  === 'object' ? result : child;
};</code></pre>

### js函数执行上下文
JavaScript 中一共有三种执行上下文。
+ 全局执行上下文(Global) -- 它是默认的基本执行上下文。代码要么在全局执行上下文要么在函数执行上下文。它有两个特征：它会创建一个全局对象（在浏览器中就是 window）并且会把 this 设置为全局对象 windows。在一个程序中只会有一个全局执行上下文。
+ 函数执行上下文 -- 当函数执行的时候，一个新的函数执行上下文就会创建。每个函数都有自己的执行上下文，当函数执行的时候上下文会被创建。函数执行上下文可以创建任意多个，每个执行上下文被创建的时候会经历若干步骤，接下来将会讨论。
+ eval 函数执行上下文 -- 在 eval 函数中执行的代码也会有自己的自行上下文

不在任何函数内部的变量，即为全局环境，全局环境的变量可被所有环境访问。

函数内部可以访问函数内部局部变量，也可以沿着调用链往上查找，直至查到到全局环境。
