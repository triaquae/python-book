## 浅copy

现有数据

```py
data = {
    "name":"alex",
    "age":18,
    "scores":{
        "语文":130,
        "数学":60,
        "英语":98,
    }
}
d2 = data
data["age"] = 20 
print(d2) 
```

你说d2打印的值里，age是18，还是20？

```py
{'name': 'alex', 'age': 20, 'scores': {'语文': 130, '数学': 60, '英语': 98}}
```

为何是20呢？ 因为d2=data相当于只是拿到了data的内存地址，但data里的每个k,v都是有单独的内存的地址的。d2,data会一直共享这个dict里的数据，不会出现像之前字符串a=1,b=a, a=2, b依然等于1的情况。

![](https://book.apeland.cn/media/images/2019/03/22/image_cz3kwST.png)

如果我确实想复制一份完成的dict数据怎么办呢？

可以用浅copy语法

```py
data = {
    "name":"alex",
    "age":18,
    "scores":{
        "语文":130,
        "数学":60,
        "英语":98,
    }
}
d2 = data.copy()
data["age"] = 20
print(d2)
print(data)
```

输出

```py
{'name': 'alex', 'age': 18, 'scores': {'语文': 130, '数学': 60, '英语': 98}}
{'name': 'alex', 'age': 20, 'scores': {'语文': 130, '数学': 60, '英语': 98}}
```

这样就相当于是2份独立数据了， 但是为什么这个语法叫做浅copy呢？ 你改一下score里的值 就知道了。

```py
data = {
    "name":"alex",
    "age":18,
    "scores":{
        "语文":130,
        "数学":60,
        "英语":98,
    }
}
d2 = data.copy()
data["age"] = 20
data["scores"]["数学"] = 77  
print(d2)
print(data)
```

看输出 ， 很神奇，两个Dict里age的值是独立的，但score字典里的分数值貌似是共享的

```py
{'name': 'alex', 'age': 18, 'scores': {'语文': 130, '数学': 77, '英语': 98}}
{'name': 'alex', 'age': 20, 'scores': {'语文': 130, '数学': 77, '英语': 98}}
```

因为浅copy会仅复制dict的第一层数据，更深层的scores下面的值依然是共享一份。

![](https://book.apeland.cn/media/images/2019/03/25/image.png)

注意图中的2个dict中的name都是alex,内存地址也一样，在没改前，两个name都确实指向同一个内存地址，但只要改任何一个的值，内存地址都会变更， 如age这个key一样。



深copy

若你想彻底使上面的2个dict完全独立，无论有多少层数据。那就要用python工具包里的一个工具了，![](https://book.apeland.cn/media/images/2019/03/25/image_EZSClpQ.png)

最后，这东西有什么用呢？ 坦白讲，以后开发中多数情况下你用不到，但是你有要知道有这个知识点，说不定哪天有个需求就要求你必须确保你的2个复制出来的dict,list必须是独立的了。

