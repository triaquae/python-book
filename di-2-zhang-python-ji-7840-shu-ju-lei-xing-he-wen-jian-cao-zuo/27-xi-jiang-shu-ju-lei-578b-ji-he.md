## 定义

集合跟我们学的列表有点像，也是可以存一堆数据，不过它有几个独特的特点，令其在整个Python语言中占有一席之地，

1. 里面的元素不可变，代表你不能存一个list、dict 在集合里，字符串、数字、元组等不可变类型可以存

2. 天生去重，在集合里没办法存重复的元素

3. 无序，不像列表一样通过索引来标记在列表中的位置 ，元素是无序的，集合中的元素没有先后之分，如集合{3,4,5}和{3,5,4}算作同一个集合



基于上面的特性，我们可以用集合来干2件事，**去重和关系运算**

## 语法

**创建集合**

```py
>>> a = {1,2,3,4,2,'alex',3,'rain','alex'}
>>> a
{1, 2, 3, 4, 'alex', 'rain'}
```

由于它是天生去重的，重复的值你根本存不进去

**帮列表去重**

帮列表去重最快速的办法是什么？ 就是把它转成集合，去重完，再转回列表

```py
>>> b
[1, 2, 3, 4, 2, 'alex', 3, 'rain', 'alex']
>>> set(b)
{1, 2, 3, 4, 'alex', 'rain'}
>>> 
>>> b = list(set(b)) #一句代码搞定
>>> b
[1, 2, 3, 4, 'alex', 'rain']
```



## 增删改查

```py
>>> a
{1, 2, 3, 4, 'alex', 'rain'}
#新增
>>> a.add('黑姑娘')  
#删除discard
>>> a
{2, 3, '黑姑娘', 'alex', 'rain'}
>>> a.discard('rain')   #删除一个存在的值
>>> a.discard('rain2')   #如果这个值不存在，do nothing.
>>> a
{2, 3, '黑姑娘', 'alex'}
>>> 
#随机删除,少用，或特定场景用
>>> a.pop() #删除并返回
1
#删除remove
>>> a.remove(4)
#查
>>> a
{2, 3, '黑姑娘', 'alex', 'rain'}
>>> 'alex' in a
True
#改
呵呵，不能改。。。 
```



## 关系运算

```py
s_1024 = {"佩奇","老男孩","海峰","马JJ","老村长","黑姑娘","Alex"}
s_pornhub = {"Alex","Egon","Rain","马JJ","Nick","Jack"}
print(s_1024 & s_pornhub)  # 交集, elements in both set
print(s_1024 | s_pornhub)  # 并集 or 合集
print(s_1024 - s_pornhub)  # 差集 , only in 1024
print(s_pornhub - s_1024)  # 差集,  only in pornhub
print(s_1024 ^ s_pornhub)  # 对称差集, 把脚踩2只船的人T出去
```

两个集合之间一般有三种关系，相交、包含、不相交。在Python中分别用下面的方法判断：

```py
print(s_1024.isdisjoint(s_pornhub))     # 判断2个集合是不是不相交，返回True or False
print(s_1024.issubset(s_pornhub))       # 判断s_1024是不是s_pornhub的子集，返回True or False
print(s_1024.issuperset(s_pornhub))     # 判断s_1024是不是s_pornhub的父集，返回True or False
```



