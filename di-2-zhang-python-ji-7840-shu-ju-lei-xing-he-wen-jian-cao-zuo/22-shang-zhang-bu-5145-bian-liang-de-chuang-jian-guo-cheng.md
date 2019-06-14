## 变量创建过程

首先，当我们定义了一个变量name = ‘oldboy’的时候，在内存中其实是做了这样一件事：

程序开辟了一块内存空间，将‘oldboy’存储进去，再让变量名name指向‘oldboy’所在的内存地址。如下图所示：

![](https://book.apeland.cn/media/images/2019/03/02/oyafan.png)

我们可以通过id\(\)方法查看这个变量在内存中的地址

```py
>>> name = "oldboy"
>>> id(name)
4317182304
```

## 变量的修改

一般我们认为修改一个变量就是用新值把旧值覆盖掉， 可python是这样实现的么？

```py
>>> name = "oldboy"
>>> id(name)
4317182304
>>> 
>>> name = "alex" 
>>> id(name)  # 如果只是在原有地址上修改，那么修改后内存地址不应该变化呀。
4317182360
```

实际的原理什么样的呢？ 程序先申请了一块内存空间来存储‘oldboy’，让name变量名指向这块内存空间

执行到name=‘alex’之后又申请了另一块内存空间来存储‘alex’，并让原本指向‘oldboy’内存的链接断开，让name再指向‘alex’。

![](https://book.apeland.cn/media/images/2019/03/02/2.png)

**变量的指向关系**

提问：下面这段代码为何出现这样的现象？

```py
>>> name1 = 'oldboy'
>>> name2 = name1   # 把name1赋值给name2,这样name2的值也是oldboy了
>>> print(name1,name2)
oldboy oldboy
>>> 
>>> name1 = 'alex'  
>>> print(name1,name2) #改了name1后，name2为何没跟着改？ 
alex oldboy
```

要想知道上面问题的结果是为什么，首先要了解在内存中两个变量的存储情况

![](https://book.apeland.cn/media/images/2019/03/02/4.png)  
  


从上面的示意图中我们可以知道，当执行name2=name1这句话的时候，事实上是让name2指向了‘oldboy’所在的内存地址。

修改name1的值，相当于断开了name1到‘oldboy’的链接，重新建立name1和‘alex’之间的链接。在这个过程中，始终没有影响到name2和‘oldboy‘之间的关系，因此name2还是‘oldboy’，而name1变成了‘alex’。

