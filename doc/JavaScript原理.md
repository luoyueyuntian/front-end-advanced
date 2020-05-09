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