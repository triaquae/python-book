Python的len为什么你可以直接用？肯定是解释器启动时就定义好了

![](https://book.apeland.cn/media/images/2019/03/21/chapter3-built-in.png)

> 内置参数详解[https://docs.python.org/3/library/functions.html?highlight=built\#ascii](https://docs.python.org/3/library/functions.html?highlight=built#ascii)

## 每个函数的作用我都帮你标好了

abs \# 求绝对值  
  
all \#Return True if bool\(x\) is True for all values x in the iterable.If the iterable is empty, return True.  
  
any \#Return True if bool\(x\) is True for any x in the iterable.If the iterable is empty, return False.  
  
ascii \#Return an ASCII-only representation of an object,ascii\(“中国”\) 返回”‘\u4e2d\u56fd’”  
  
bin \#返回整数的2进制格式  
  
bool \# 判断一个数据结构是True or False, bool\({}\) 返回就是False, 因为是空dict  
  
bytearray \# 把byte变成 bytearray, 可修改的数组  
  
bytes \# bytes\(“中国”,”gbk”\)  
  
callable \# 判断一个对象是否可调用  
  
chr \# 返回一个数字对应的ascii字符 ， 比如chr\(90\)返回ascii里的’Z’

classmethod \#面向对象时用，现在忽略  
  
compile \#py解释器自己用的东西，忽略  
  
complex \#求复数，一般人用不到  
  
copyright \#没用  
  
credits \#没用  
  
delattr \#面向对象时用，现在忽略  
  
dict \#生成一个空dict  
  
dir \#返回对象的可调用属性  
  
divmod \#返回除法的商和余数 ，比如divmod\(4,2\)，结果\(2, 0\)  
  
enumerate \#返回列表的索引和元素，比如 d = \[“alex”,”jack”\]，enumerate\(d\)后，得到\(0, ‘alex’\) \(1, ‘jack’\)  
  
eval \#可以把字符串形式的list,dict,set,tuple,再转换成其原有的数据类型。  
  
exec \#把字符串格式的代码，进行解义并执行，比如exec\(“print\(‘hellworld’\)”\)，会解义里面的字符串并执行  
  
exit \#退出程序  
  
filter \#对list、dict、set、tuple等可迭代对象进行过滤， filter\(lambda x:x&gt;10,\[0,1,23,3,4,4,5,6,67,7\]\)过滤出所有大于10的值  
  
float \#转成浮点  
  
format \#没用  
  
frozenset \#把一个集合变成不可修改的  
  
getattr \#面向对象时用，现在忽略  
  
globals \#打印全局作用域里的值  
  
hasattr \#面向对象时用，现在忽略  
  
hash \#hash函数  
  
help  
  
hex \#返回一个10进制的16进制表示形式,hex\(10\) 返回’0xa’  
  
id \#查看对象内存地址  
  
input  
  
int  
  
isinstance \#判断一个数据结构的类型，比如判断a是不是fronzenset, isinstance\(a,frozenset\) 返回 True or False  
  
issubclass \#面向对象时用，现在忽略  
  
iter \#把一个数据结构变成迭代器，讲了迭代器就明白了  
  
len  
  
list  
  
locals  
  
map \# map\(lambda x:x\*\*2,\[1,2,3,43,45,5,6,\]\) 输出 \[1, 4, 9, 1849, 2025, 25, 36\]  
  
max \# 求最大值  
  
memoryview \# 一般人不用，忽略  
  
min \# 求最小值  
  
next \# 生成器会用到，现在忽略  
  
object \#面向对象时用，现在忽略  
  
oct \# 返回10进制数的8进制表示  
  
open  
  
ord \# 返回ascii的字符对应的10进制数 ord\(‘a’\) 返回97，  
  
print  
  
property \#面向对象时用，现在忽略  
  
quit  
  
range  
  
repr \#没什么用  
  
reversed \# 可以把一个列表反转  
  
round \#可以把小数4舍5入成整数 ，round\(10.15,1\) 得10.2  
  
set  
  
setattr \#面向对象时用，现在忽略  
  
slice \# 没用  
  
sorted  
  
staticmethod \#面向对象时用，现在忽略  
  
str  
  
sum \#求和,a=\[1, 4, 9, 1849, 2025, 25, 36\],sum\(a\) 得3949  
  
super \#面向对象时用，现在忽略  
  
tuple  
  
type  
  
vars \#返回一个对象的属性，面向对象时就明白了  
  
zip \#可以把2个或多个列表拼成一个， a=\[1, 4, 9, 1849, 2025, 25, 36\]，b = \[“a”,”b”,”c”,”d”\]，

```py
list(zip(a,b)) #得结果 
[(1, 'a'), (4, 'b'), (9, 'c'), (1849, 'd')]
```



#### 几个刁钻古怪的内置方法用法提醒

```py
#compile
f = open("函数递归.py")
data =compile(f.read(),'','exec')
exec(data)
#print
msg = "又回到最初的起点"
f = open("tofile","w")
print(msg,"记忆中你青涩的脸",sep="|",end="",file=f)
# #slice
# a = range(20)
# pattern = slice(3,8,2)
# for i in a[pattern]: #等于a[3:8:2]
#     print(i)
#
#
#memoryview
#usage:
#>>> memoryview(b'abcd')
#
#在进行切片并赋值数据时，不需要重新copy原列表数据，可以直接映射原数据内存，
import time
for n in (100000, 200000, 300000, 400000):
    data = b'x'*n
    start = time.time()
    b = data
    while b:
        b = b[1:]
    print('bytes', n, time.time()-start)
for n in (100000, 200000, 300000, 400000):
    data = b'x'*n
    start = time.time()
    b = memoryview(data)
    while b:
        b = b[1:]
    print('memoryview', n, time.time()-start)

```

#### 

#### 练习题

#### 员工信息修改程序

#### 在一个文件里存多个人的个人信息，如以下

```py
username,password,age,position,department,phone
alex,abc123,30,Engineer,IT,13651830433
rain,df2@432,25,Teacher,Teching,18912334223
黑姑娘,df2@432,26,行政,人事,13811177306
```

#### 需求：

#### 1.输入用户名密码，正确后登录系统 ，打印

```py
1. 修改个人信息
2. 打印个人信息
3. 修改密码
```

#### 2.每个选项写一个方法

#### 3. 当用户选择1时，提示用户选择要修改的字段，根据用户输入对相应字段进行修改

#### 4.登录时输错3次退出程序

#### 执行时应该达到的效果参考：

#### python /Users/alex/PycharmProjects/apeland_py\_learn/day3_函数编程/个人信息修改练习.py

```py
Username:alex
Password:abc123
-------------------welcome alex --------------------
1. 打印个人信息
2. 修改个人信息
3. 修改密码
>>>1
    ------------------
    Name:   abc123
    Age :   30
    Job :   Engineer
    Dept:   Sales
    Phone:  13651830433
    ------------------
1. 打印个人信息
2. 修改个人信息
3. 修改密码
>>>2
person data: ['alex', 'abc123', '30', 'Engineer', 'Sales', '13651830433']
0.  Username: alex
1.  Password: abc123
2.  Age: 30
3.  Job: Engineer
4.  Dept: Sales
5.  Phone: 13651830433
[select column id to change]:4
current value>: Sales
new value>:Marketing
['alex', 'abc123', '30', 'Engineer', 'Marketing', '13651830433']
1. 打印个人信息
2. 修改个人信息
3. 修改密码
>>>q
bye.
```

#### 代码提示

#### ![](https://book.apeland.cn/media/images/2019/03/21/image.png)



