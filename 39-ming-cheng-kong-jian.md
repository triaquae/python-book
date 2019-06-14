又名name space, 顾名思义就是存放名字的地方，存什么名字呢？举例说明，若变量x=1，1存放于内存中，那名字x存放在哪里呢？**名称空间正是存放名字x与1绑定关系的地方**

python里面有很多名字空间，每个地方都有自己的名字空间，互不干扰，不同空间中的两个相同名字的变量之间没有任何联系。

名称空间有4种:`LEGB`

* `locals`:函数内部的名字空间，一般包括函数的局部变量以及形式参数

* `enclosing function`:在嵌套函数中外部函数的名字空间, 若fun2嵌套在fun1里，对`fun2`来说，`fun1`的名字空间就enclosing.

* `globals`:当前的模块空间，模块就是一些`py`文件。也就是说，globals\(\)类似全局变量。

* **`builtins`**: 内置模块空间，也就是内置变量或者内置函数的名字空间，print\(dir\(**builtins**\)\)可查看包含的值。

**不同变量的作用域不同就是由这个变量所在的名称空间决定的。**

作用域即范围

* 全局范围：全局存活，全局有效

* 局部范围：临时存活，局部有效



查看作用域方法 globals\(\),locals\(\)

## 作用域查找顺序

当程序引用某个变量的名字时，就会从当前名字空间开始搜索。搜索顺序规则便是:`LEGB`。**即locals -&gt; enclosing function -&gt; globals -&gt;builtins**。一层一层的查找，找到了之后，便停止搜索，如果最后没有找到,则抛出在`NameError`的异常。

```py
level = 'L0'
n = 22
def func():
    level = 'L1'
    n = 33
    print(locals())
    def outer():
        n = 44
        level = 'L2'
        print("outer:",locals(),n)
        def inner():
            level = 'L3'
            print("inner:",locals(),n) #此外打印的n是多少？
        inner()
    outer()
func()
```

输出

```py
{'n': 33, 'level': 'L1'}
outer: {'level': 'L2', 'n': 44} 44
inner: {'level': 'L3', 'n': 44} 44
```



