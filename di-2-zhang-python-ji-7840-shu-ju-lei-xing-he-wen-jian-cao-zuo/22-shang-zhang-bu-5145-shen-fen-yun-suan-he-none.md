## 身份运算

python 中有很多种数据类型， 查看一个数据的类型的方法是type\(\).

```py
>>> name="小猿圈"
>>> age = 1
>>> 
>>> name
'小猿圈'
>>> 
>>> type(name),type(age)
(, )
```

判断一个数据类型是不是str, or int等，可以用身份运算符is

![](https://book.apeland.cn/media/images/2019/03/02/dudgxa.png)

```py
>>> type(name) is str
True
>>> 
>>> type(name) is not int
True
```

## 空值None

代表什么都没有的意思，一般用在哪呢？ 比如玩游戏，你要初始化一个女朋友， 需要填上姓名、年龄、身高、体重等信息， 这些信息是让玩家填的，在填之前，你要先把变量定义好，那就得存个值 ，这个值用0,1来占位不合适 ，用True,False也不合适 ，用None最合适

```py
>>> name=None
>>> age=None
>>> height=None
>>> weight=None
>>> 
>>> name,age,height,weight
(None, None, None, None)
>>> 
```

此时可用is 运算符来判断变量是不是None

```py
>>> if name is None:
...  print("你的女朋友还没起名字呢.")
... 
你的女朋友还没起名字呢.
```

其实用==判断也行，但是不符合开发规范

```py
>>> name == None
True
```

## 三元运算

显的很NB的代码写法。

```py
name = "Eva"
sex = None
# 普通写法
if name == "Eva":
    sex = "Female"
else:
    sex = "Male"
# 用三元运算来写
sex = "Female" if name == "Eva" else "Male"
```



