#### 什么叫序列化？

序列化是指把内存里的数据类型转变成字符串，以使其能存储到硬盘或通过网络传输到远程，因为硬盘或网络传输时只能接受bytes

#### 为什么要序列化？

你打游戏过程中，打累了，停下来，关掉游戏、想过2天再玩，2天之后，游戏又从你上次停止的地方继续运行，你上次游戏的进度肯定保存在硬盘上了，是以何种形式呢？游戏过程中产生的很多临时数据是不规律的，可能在你关掉游戏时正好有10个列表，3个嵌套字典的数据集合在内存里，需要存下来？你如何存？把列表变成文件里的多行多列形式？那嵌套字典呢？根本没法存。所以，若是有种办法可以直接把内存数据存到硬盘上，下次程序再启动，再从硬盘上读回来，还是原来的格式的话，那是极好的。

用于序列化的两个模块

* json，用于字符串 和 python数据类型间进行转换

* pickle，用于python特有的类型 和 python的数据类型间进行转换

pickle模块提供了四个功能：dumps、dump、loads、load

```py
import pickle
data = {'k1':123,'k2':'Hello'}
# pickle.dumps 将数据通过特殊的形式转换位只有python语言认识的字符串
p_str = pickle.dumps(data)  # 注意dumps会把数据变成bytes格式
print(p_str)
# pickle.dump 将数据通过特殊的形式转换位只有python语言认识的字符串，并写入文件
with open('result.pk',"wb") as fp:
    pickle.dump(data,fp)
# pickle.load  从文件里加载
f = open("result.pk","rb")
d = pickle.load(f)
print(d)
```

Json模块也提供了四个功能：dumps、dump、loads、load，用法跟pickle一致

```py
import json
# json.dumps 将数据通过特殊的形式转换位所有程序语言都认识的字符串
j_str = json.dumps(data) # 注意json dumps生成的是字符串，不是bytes
print(j_str)
#dump入文件 
with open('result.json','w') as fp:
    json.dump(data,fp)
#从文件里load
with open("result.json") as f:
    d = json.load(f)
    print(d)
```



#### json vs pickle:

**JSON:**

优点：跨语言\(不同语言间的数据传递可用json交接\)、体积小

缺点：只能支持int\str\list\tuple\dict

**Pickle:**

优点：专为python设计，支持python所有的数据类型

缺点：只能在python中使用，存储数据占空间大

