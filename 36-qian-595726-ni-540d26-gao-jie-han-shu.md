## 嵌套函数

函数里不仅可以写代码，还可以嵌套函数

```py
name = "小猿圈"
def change():
    name = "小猿圈，自学编程"
    def change2():
        # global name  如果声明了这句，下面的name改的是最外层的全局变层
        name = "小猿圈，自学编程不要钱" #这句注释掉的话，下面name打印的是哪个值？
        print("第3层打印", name) 
    change2()  # 调用内层函数
    print("第2层打印", name)
change()
print("最外层打印", name)
```

输出

```py
第3层打印 小猿圈，自学编程不要钱
第2层打印 小猿圈，自学编程
最外层打印 小猿圈
```

通过上面的例子，我们理解了，每个函数里的变量是互相独立的，变量的查找顺序也是从当前层依次往上层找。

问个哲学问题，这东西有什么用呢？哈，现在没用，不解释，长大后学了装饰器你就知道有啥用了。

## 匿名函数

匿名函数就是不需要显式的指定函数名

```py
#这段代码
def calc(x,y):
    return x**y
print(calc(2,5))
#换成匿名函数
calc = lambda x,y:x**y
print(calc(2,5))
```

你也许会说，用上这个东西没感觉有毛方便呀， 。。。。呵呵，如果是这么用，确实没毛线改进，不过匿名函数主要是和其它函数搭配使用的呢，如下

```py
res = map(lambda x:x**2,[1,5,7,4,8])
for i in res:
    print(i)
```

输出

```py
1
25
49
16
64
```

## 高阶函数

变量可以指向函数，函数的参数能接收变量，那么一个函数就可以接收另一个函数作为参数，这种函数就称之为高阶函数。

```py
def get_abs(n):
    if n < 0 :
        n = int(str(n).strip("-"))
    return n
def add(x,y,f):
    return f(x) + f(y)
res = add(3,-6,get_abs)
print(res)
```

只需满足以下任意一个条件，即是高阶函数

* 接受一个或多个函数作为输入

* return 返回另外一个函数


