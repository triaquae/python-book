现在有个需求，现有列表a=`[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]`,要求你把列表里的每个值加1，你怎么实现？你可能会想到2种方式

**二逼青年版**

生成一个新列表b，遍历列表a,把每个值加1后存在b里，最后再把a=b, 这样二逼的原因不言而喻，生成了新列表，浪费了内存空间。

```py
>>> a
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> b = []
>>> for i in a:b.append(i+1)
... 
>>> b
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
>>> a = b
>>> a
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

**普通青年版**

毫无新意

```py
a = [1,3,4,6,7,7,8,9,11]
for index,i in enumerate(a):
    a[index] +=1
print(a)
```

**略屌青年版**

```py
>>> a
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
>>> a = map(lambda x:x+1, a)
>>> a
>>> for i in a:print(i)
... 
3
5
7
9
11
```

**装逼青年版**

```py
>>> a = [i+1 for i in range(10)]
>>> a
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

这样的写法就叫做**列表生成式，**有什么用呢？装逼用，哈哈，写出来显的高级，效果跟上面的都一样哈。

  

