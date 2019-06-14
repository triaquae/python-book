## 引子

我们学了列表 ， 现在有个需求， 把你们公司每个员工的姓名、年龄、职务、工资存到列表里，你怎么存？

```py
staff_list = [
    ["Alex",23,"CEO",66000],
    ["黑姑娘",24,"行政",4000],
    ["佩奇",26,"讲师",40000],
    # [xxx,xx,xx,xxx]
    # [xxx,xx,xx,xxx]
    # [xxx,xx,xx,xxx]  
]
```

这样存没问题，不过你要查一个人的工资的话， 是不是得把列表遍历一遍

```py
for i in staff_list:
    if i[0] == '黑姑娘':
        print(i)
        break
```

但假如你公司有2万人，如果你要找的黑姑娘正好在列表末尾，那意味着你要遍历2万次，才能找到这个信息。列表越大，查找速度越慢。

好了，现在福音来了， 接下来学要的字典可以 查询数据又快、操作又方便，是日后开发中必备神器。

字典是Python语言中唯一的映射类型。

## 定义：

**｛key1:value1,key2:value2｝**

```py
1、键与值用冒号“：”分开；
2、项与项用逗号“，”分开；
```

示例：

```py
info = {
    "name":"小猿圈",
    "mission": "帮一千万极客高效学编程",
    "website": "http://apeland.com"
}
```

**特性：**

1. key-value结构

2. key必须为不可变数据类型、必须唯一

3. 可存放任意多个value、可修改、可以不唯一

4. 无序

5. 查询速度快，且不受dict的大小影响，至于为何快？我们学完hash再解释。

## 创建操作

```py
>>>person = {"name": "alex", 'age': 20} 
#或
>>>person = dict(name='seven', age=20)
#或
>>>person = dict({"name": "egon", 'age': 20})
#或
>>> {}.fromkeys([1,2,3,4,5,6,7,8],100)
{1: 100, 2: 100, 3: 100, 4: 100, 5: 100, 6: 100, 7: 100, 8: 100} 
```

## 增加操作

```py
names = {
    "alex": [23, "CEO", 66000],
    "黑姑娘": [24, "行政", 4000],
}
# 新增k
names["佩奇"] = [26, "讲师", 40000]
names.setdefault("oldboy",[50,"boss",100000])  # D.setdefault(k[,d]) -> D.get(k,d), also set D[k]=d if k not in D
```

## 删除操作

```py
names.pop("alex") # 删除指定key
names.popitem()   # 随便删除1个key
del names["oldboy"] # 删除指定key,同pop方法
names.clear()     # 清空dict
```

## 修改操作

```py
dic['key'] = 'new_value',如果key在字典中存在，'new_value'将会替代原来的value值；
dic.update(dic2) 将字典dic2的键值对添加到字典dic中
```

## 查操作

```py
dic['key'] #返回字典中key对应的值，若key不存在字典中，则报错；
dic.get(key, default = None)#返回字典中key对应的值，若key不存在字典中，则返回default的值（default默认为None）
'key' in dic #若存在则返回True，没有则返回False
dic.keys() 返回一个包含字典所有KEY的列表；
dic.values() 返回一个包含字典所有value的列表；
dic.items() 返回一个包含所有（键，值）元组的列表；
```

## 循环

```py
1、for k in dic.keys()
2、for k,v in dic.items() 
3、for k in dic   # 推荐用这种，效率速度最快
info = {
    "name":"小猿圈",
    "mission": "帮一千万极客高效学编程",
    "website": "http://apeland.com"
}
for k in info:
    print(k,info[k])
输出
name 小猿圈
mission 帮一千万极客高效学编程
website http://apeland.com
```

## 求长度

```py
len(dic)
```



## 练习题

1. 用你能想到的最少的代码生成一个包含100个key的字典，每个value的值不能一样

2. {‘k0’: 0, ‘k1’: 1, ‘k2’: 2, ‘k3’: 3, ‘k4’: 4, ‘k5’: 5, ‘k6’: 6, ‘k7’: 7, ‘k8’: 8, ‘k9’: 9} 请把这个dict中key大于5的值value打印出来。

3. 把题2中value是偶数的统一改成-1

4. 请设计一个dict, 存储你们公司每个人的信息， 信息包含至少姓名、年龄、电话、职位、工资，并提供一个简单的查找接口，用户按你的要求输入要查找的人，你的程序把查到的信息打印出来

  


