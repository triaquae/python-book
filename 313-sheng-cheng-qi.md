## 生成器generator

通过列表生成式，我们可以直接创建一个列表。但是，受到内存限制，列表容量肯定是有限的。而且，创建一个包含100万个元素的列表，不仅占用很大的存储空间，如果我们仅仅需要访问前面几个元素，那后面绝大多数元素占用的空间都白白浪费了。比如我要循环100万次，按py的语法，for i in range\(1000000\)会先生成100万个值的列表。但是循环到第50次时，我就不想继续了，就退出了。但是90多万的列表元素就白为你提前生成了。

```py
for i in range(1000000):
    if i == 50: 
        break
    print(i)
```

所以，如果列表元素可以按照某种算法推算出来，那我们是否可以在循环的过程中不断推算出后续的元素呢？

像上面这个循环，每次循环只是+1而已，我们完全可以写一个算法，让他执行一次就自动+1，这样就不必创建完整的list，从而节省大量的空间。**在Python中，这种一边循环一边计算后面元素的机制，称为生成器：generator。**

要创建一个generator，有很多种方法。第一种方法很简单，只要把一个列表生成式的`[]`改成`()，`就创建了一个generator：

```py
>>> [x * x for x in range(10)]
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
>>> 
>>> (x * x for x in range(10))
 at 0x101ebc3b8>
```

\(x\*x for x in range\(10\)）生成的就是一个生成器。

我们可以直接打印出list的每一个元素，但我们怎么打印出generator的每一个元素呢？

如果要一个一个打印出来，可以通过`next()`函数获得generator的下一个返回值：

```py
>>> g = (x * x for x in range(10))
>>> next(g)
0
>>> next(g)
1
>>> next(g)
4
>>> next(g)
9
>>> next(g)
16
>>> next(g)
25
>>> next(g)
36
>>> next(g)
49
>>> next(g)
64
>>> next(g)
81
>>> next(g)
Traceback (most recent call last):
  File "", line 1, in 
StopIteration
```

我们讲过，generator保存的是算法，每次调用`next(g)`就计算出`g`的下一个元素的值，直到计算到最后一个元素，没有更多的元素时，抛出`StopIteration`的错误。

当然，上面这种不断调用`next(g)`实在是太变态了，正确的方法是使用`for`循环，因为generator也是可迭代\(遍历\)对象：

```py
>>> g = (x * x for x in range(10))
>>> for n in g:
...     print(n)
...
0
1
4
9
16
25
36
49
64
81
```

通过for循环来迭代它，就不需要关心StopIteration的错误了。

### 函数生成器

generator非常强大。如果推算的算法比较复杂，用类似列表生成式的for循环无法实现的时候，还可以用函数来实现。

比如，著名的斐波拉契数列（Fibonacci），除第一个和第二个数外，任意一个数都可由前两个数相加得到：

1, 1, 2, 3, 5, 8, 13, 21, 34, …

实现100以内的斐波那契数代码：

```py
a,b = 0,1
n = 0  # 斐波那契数
while n < 100:
    n = a + b
    a = b # 把b的旧值给到a
    b = n # 新的b = a + b(旧b的值)
    print(n)
```

改成函数也可以的

```py
def fib(max):
    a,b = 0,1
    n = 0  # 斐波那契数
    while n < max:
        n = a + b
        a = b # 把b的旧值给到a
        b = n # 新的b = a + b(旧b的值)
        print(n)
fib(100)
```

输出 ：

1  
  
2  
  
3  
  
5  
  
8  
  
13  
  
21  
  
34  
  
55  
  
89  
  
144

仔细观察，可以看出，`fib`函数实际上是定义了斐波拉契数列的推算规则，可以从第一个元素开始，推算出后续任意的元素，这种逻辑其实非常类似generator。

**也就是说，上面的函数和generator仅一步之遥。要把`fib`函数变成generator，只需要把`print(b)`改为`yield b`就可以了：**

```py
def fib(max):
    a,b = 0,1
    n = 0  # 斐波那契数
    while n < max:
        n = a + b
        a = b # 把b的旧值给到a
        b = n # 新的b = a + b(旧b的值)
        #print(n)
        yield n # 程序走到这，就会暂停下来，返回n到函数外面，直到被next方法调用时唤醒
f = fib(100) # 注意这句调用时，函数并不会执行，只有下一次调用next时，函数才会真正执行
print(f)
print(f.__next__())
print(f.__next__())
print(f.__next__())
print(f.__next__())
```

输出

```py
1
2
3
5
```

这就是定义generator的另一种方法。如果一个函数定义中包含`yield`关键字，那么这个函数就不再是一个普通函数，而是一个generator：

这里，最难理解的就是generator和函数的执行流程不一样。函数是顺序执行，遇到return语句或者最后一行函数语句就返回。**而变成generator的函数，在每次调用next\(\)的时候执行，遇到yield语句暂停并返回数据到函数外，再次被next\(\)调用时从上次返回的yield语句处继续执行**。

![](https://book.apeland.cn/media/images/2019/03/22/image.png)

`在上面fib`的例子，我们在循环过程中不断调用`yield`，函数就会不断的中断\(暂停\)。当然要给循环设置一个条件来退出循环，不然就会产生一个无限数列出来。同样的，把函数改成generator后，我们基本上从来不会用`next()`来获取下一个返回值，而是直接使用`for`循环来迭代：

```py
f = fib(100) # 注意这句调用时，函数并不会执行，只有下一次调用next时，函数才会真正执行
for i in f:
    print(i)
#输出：
1
2
3
...
...
55
89
144
```



### 并发编程

虽然我们还没学并发编程，但我们肯定听过cpu 多少核多少核之类的，cpu的多核就是为了可以实现并行运算，让你同时边听歌、边聊qq、边刷知乎。单核的cpu同一时间只能干一个事，所以你用单核电脑同时做好几件事的话，就会变的很慢，因为cpu要在不同程序任务间来回切换。

通过yield, 我们可以实现单核下并发做多件事的效果。

```py
import time
def consumer(name):
    print("%s 准备吃包子啦!" %name)
    while True:
       baozi = yield  # yield可以接收到外部send传过来的数据并赋值给baozi
       print("包子[%s]来了,被[%s]吃了!" %(baozi,name))
c = consumer('A')
c2 = consumer('B')
c.__next__() # 执行一下next可以使上面的函数走到yield那句。 这样后面的send语法才能生效
c2.__next__()
print("----老子开始准备做包子啦!----")
for i in range(10):
    time.sleep(1)
    print("做了2个包子!")
    c.send(i)  # send的作用=next, 同时还把数据传给了上面函数里的yield
    c2.send(i)
```

**注意：调用send\(x\)给生成器传值时，必须确保生成器已经执行过一次next**\(\)调用, 这样会让程序走到yield位置等待外部第2次调用。

