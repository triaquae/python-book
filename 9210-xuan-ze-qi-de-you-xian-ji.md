# 选择器的优先级

我们现在已经学过了很多的选择器，也就是说我们有很多种方法从HTML中找到某个元素，那么就会有一个问题：如果我通过不用的选择器找到了相同的一个元素，并且设置了不同的样式，那么浏览器究竟应该按照哪一个样式渲染呢？也就是不同的选择器它们的优先级是怎样的呢？

是先来后到呢还是后来居上呢？统统不是，它是按照下面的选择器的权重规则来决定的。

![CSS选择器权重](/assets/chapter9/CSS/CSS_02.png)

注意：

还有一种不讲道理的`!import`方式来强制让样式生效，但是不推荐使用。因为大量使用`!import`的代码是无法维护的。