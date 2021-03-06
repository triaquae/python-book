## 练习题【答案在页面的末尾\(先自己做再看答案\)】

1、请用代码实现：利用下划线将列表的每一个元素拼接成字符串，li＝\[‘alex’, ‘eric’, ‘rain’\]

2、查找列表中元素，移除每个元素的空格，并查找以a或A开头并且以c结尾的所有元素。

```py
li = ["alec", " aric", "Alex", "Tony", "rain"]
tu = ("alec", " aric", "Alex", "Tony", "rain")
dic = {'k1': "alex", 'k2': ' aric', "k3": "Alex", "k4": "Tony"}
```

3、写代码，有如下列表，按照要求实现每一个功能

li＝\[‘alex’, ‘eric’, ‘rain’\]

* 计算列表长度并输出

* 列表中追加元素“seven”，并输出添加后的列表

* 请在列表的第1个位置插入元素“Tony”，并输出添加后的列表

* 请修改列表第2个位置的元素为“Kelly”，并输出修改后的列表

* 请删除列表中的元素“eric”，并输出修改后的列表

* 请删除列表中的第2个元素，并输出删除的元素的值和删除元素后的列表

* 请删除列表中的第3个元素，并输出删除元素后的列表

* 请删除列表中的第2至4个元素，并输出删除元素后的列表

* 请将列表所有的元素反转，并输出反转后的列表

* 请使用for、len、range输出列表的索引

* 请使用enumrate输出列表元素和序号（序号从100开始）

* 请使用for循环输出列表的所有元素

4、写代码，有如下列表，请按照功能要求实现每一个功能

```py
li = ["hello", 'seven', ["mon", ["h", "kelly"], 'all'], 123, 446]
```

* 请根据索引输出“Kelly”

* 请使用索引找到’all’元素并将其修改为“ALL”，如：li\[0\]\[1\]\[9\]…

5、有如下变量，请实现要求的功能

```py
tu = ("alex", [11, 22, {"k1": 'v1', "k2": ["age", "name"], "k3": (11,22,33)}, 44])
```

* 讲述元组的特性

* 请问tu变量中的第一个元素“alex”是否可被修改？

* 请问tu变量中的”k2”对应的值是什么类型？是否可以被修改？如果可以，请在其中添加一个元素“Seven”

* 请问tu变量中的”k3”对应的值是什么类型？是否可以被修改？如果可以，请在其中添加一个元素“Seven“

6、转换

* 将字符串s = “alex”转换成列表

* 将字符串s = “alex”转换成元祖

* 将列表li = \[“alex”, “seven”\]转换成元组

* 将元组tu = \(‘Alex’, “seven”\)转换成列表

* 将列表li = \[“alex”, “seven”\]转换成字典且字典的key按照10开始向后递增

7、元素分类

有如下值集合\[11,22,33,44,55,66,77,88,99,90\]，将所有大于66的值保存至字典的第一个key中，将小于66的值保存至第二个key的值中。

即：{‘k1’:大于66的所有值, ‘k2’:小于66的所有值}。（编程题）

8、在不改变列表数据结构的情况下找最大值li = \[1,3,2,7,6,23,41,243,33,85,56\]。（编程题）

9、在不改变列表中数据排列结构的前提下，找出以下列表中最接近最大值和最小值的平均值 的数`li = [-100,1,3,2,7,6,120,121,140,23,411,99,243,33,85,56]。`（编程题）

`10、`利用for循环和range输出9 \* 9乘法表 。（编程题）

11、求100以内的素数和。（编程题）

12、请说明python2 与python3中的默认编码是什么？

13、为什么会出现中文乱码？你能列举出现乱码的情况有哪几种？

14、分别写出在windows和mac上用py2输出中文怎么做？ 

## 作业

**股票查询程序开发**

把以下股票数据存入stock\_data.txt  
![](https://book.apeland.cn/media/images/2019/06/02/2AC1BA7A-C196-474E-9F77-97D92897252E.png)数据来源：

[东方财富网](http://http//quote.eastmoney.com/center/gridlist.html#hs_a_board)

开发程序对stock\_data.txt进行以下操作：

1. 程序启动后，给用户提供查询接口，允许用户重复查股票行情信息\(用到循环\)

2. 允许用户通过模糊查询股票名，比如输入“啤酒”, 就把所有股票名称中包含“啤酒”的信息打印出来

3. 允许按股票价格、涨跌幅、换手率这几列来筛选信息，比如输入“价格&gt;50”则把价格大于50的股票都打印，输入“市盈率&lt;50“，则把市盈率小于50的股票都打印，不用判断等于。

思路提示：加载文件内容到内存，转成dict or list结构，然后对dict or list 进行查询等操作。 这样以后就不用每查一次就要打开一次文件了，效率会高。

程序启动后执行效果参考：

```py
股票查询接口>>:换手率>25
['序号', '代码', '名称', '最新价', '涨跌幅', '涨跌额', '成交量(手)', '成交额', '振幅', '最高', '最低', '今开', '昨收', '量比', '换手率', '市盈率', '市净率']
['18', '603697', '有友食品', '22.73', '10.02%', '2.07', '34.93万', '7.68亿', '8.23%', '22.73', '21.03', '21.17', '20.66', '1.4', '43.94%', '38.1', '4.66']
['23', '603956', '威派格', '22.52', '10.01%', '2.05', '18.33万', '4.01亿', '10.60%', '22.52', '20.35', '20.35', '20.47', '2.16', '43.02%', '-', '9.82']
['36', '300748', '金力永磁', '59.7', '10.01%', '5.43', '11.02万', '6.38亿', '6.98%', '59.7', '55.91', '56.88', '54.27', '0.9', '26.49%', '234.09', '23.54']
['37', '300767', '震安科技', '41.13', '10.00%', '3.74', '6.22万', '2.49亿', '10.32%', '41.13', '37.27', '37.48', '37.39', '3.86', '31.11%', '43.32', '3.68']
['38', '603045', '福达合金', '32', '10.00%', '2.91', '17.06万', '5.31亿', '9.87%', '32', '29.13', '29.13', '29.09', '1.39', '25.17%', '52.74', '4.02']
['39', '2952', '亚世光电', '58.98', '10.00%', '5.36', '4.18万', '2.41亿', '7.42%', '58.98', '55', '55.91', '53.62', '3.04', '27.44%', '53.09', '5.51']
找到6条
股票查询接口>>:最新价<5
['序号', '代码', '名称', '最新价', '涨跌幅', '涨跌额', '成交量(手)', '成交额', '振幅', '最高', '最低', '今开', '昨收', '量比', '换手率', '市盈率', '市净率']
['2', '2676', '顺威股份', '3.69', '10.15%', '0.34', '15.23万', '5516万', '9.55%', '3.69', '3.37', '3.37', '3.35', '1.16', '2.11%', '-', '2.58']
['3', '601619', '嘉泽新能', '4.91', '10.09%', '0.45', '16.55万', '8006万', '8.52%', '4.91', '4.53', '4.54', '4.46', '1.82', '3.28%', '52.26', '3.64']
找到2条
股票查询接口>>:食品
['18', '603697', '有友食品', '22.73', '10.02%', '2.07', '34.93万', '7.68亿', '8.23%', '22.73', '21.03', '21.17', '20.66', '1.4', '43.94%', '38.1', '4.66']
找到1条
股票查询接口>>:能源
['9', '2828', '贝肯能源', '14.25', '10.04%', '1.3', '17.83万', '2.52亿', '4.71%', '14.25', '13.64', '13.8', '12.95', '3.45', '18.03%', '-', '3.08']
找到1条
股票查询接口>>:科技
['12', '2866', '传艺科技', '13.81', '10.04%', '1.26', '13.59万', '1.83亿', '9.72%', '13.81', '12.59', '12.61', '12.55', '2.63', '16.86%', '33.37', '3.43']
['19', '300777', '中简科技', '24.92', '10.02%', '2.27', '5952', '1483万', '0.00%', '24.92', '24.92', '24.92', '22.65', '3.45', '1.49%', '102.24', '11.49']
['21', '300245', '天玑科技', '11.53', '10.02%', '1.05', '26.86万', '3.05亿', '9.64%', '11.53', '10.52', '10.52', '10.48', '1.06', '10.35%', '127.47', '2.57']
['26', '300391', '康跃科技', '7.8', '10.01%', '0.71', '3.9万', '3027万', '10.01%', '7.8', '7.09', '7.09', '7.09', '0.75', '1.94%', '27.35', '1.89']
['37', '300767', '震安科技', '41.13', '10.00%', '3.74', '6.22万', '2.49亿', '10.32%', '41.13', '37.27', '37.48', '37.39', '3.86', '31.11%', '43.32', '3.68']
['40', '603327', '福蓉科技', '21.56', '10.00%', '1.96', '3586', '773.1万', '0.00%', '21.56', '21.56', '21.56', '19.6', '2.81', '0.70%', '31.97', '8.05']
找到6条
```

练习题答案如下：

1、请用代码实现：利用下划线将列表的每一个元素拼接成字符串，

```
li = ['alex', 'eric', 'rain']
print("_".join(li))
```

2 查找列表中元素，移除每个元素的空格，并查找以a或A开头并且以c结尾的所有元素。

> li = \["alec", " aric", "Alex", "Tony", "rain"\]

```python
for item in li:
    item = item.strip().replace(" ", "")
    if (item.startswith("A") or item.startswith("a")) and item.endswith("c"):
        print(item)
```

> ```
> tu = ("alec", " aric", "Alex", "Tony", "rain")
> ```

```python
for item in tu:
    item = item.strip().replace(" ", "")
    if (item.startswith("A") or item.startswith("a")) and item.endswith("c"):
        print(item)
```

> ```
> dic = {'k1': "alex", 'k2': ' aric', "k3": "Alex", "k4": "Tony"}
> ```

```python
for item in dic:
    value = dic[item].strip().replace(" ", "")
    if (value.startswith("A") or value.startswith("a")) and value.endswith("c"):
        print(value)
```

3 3、写代码，有如下列表，按照要求实现每一个功能 li＝\[‘alex’, ‘eric’, ‘rain’\]

> * 计算列表长度并输出

```python
print(len(li))
```

> * 列表中追加元素“seven”，并输出添加后的列表

```python
li.append("seven")
print(li)
```

> * 请在列表的第1个位置插入元素“Tony”，并输出添加后的列表

```python
li.insert(1, "Tony")
print(li)
```

> * 请修改列表第2个位置的元素为“Kelly”，并输出修改后的列表

```python
li[1] = "Kelly"
print(li)
```

> * 请删除列表中的元素“eric”，并输出修改后的列表

```python
li.remove("eric")
```

> * 请删除列表中的第2个元素，并输出删除的元素的值和删除元素后的列表

```python
print(li.pop(1))
print(li)
```

> * 请删除列表中的第3个元素，并输出删除元素后的列表

```python
print(li.pop(2))
```

> * 请删除列表中的第2至4个元素，并输出删除元素后的列表

```python
li = ["ale", "eric", "rain", "alex", "luffy", "py"]
del li[2:5]
print(li)
```

> * 请将列表所有的元素反转，并输出反转后的列表

```python
li.reverse()
print(li)
```

> * 请使用for、len、range输出列表的索引

```python
for index in range(len(li)):
    print(index)
```

> * 请使用enumrate输出列表元素和序号（序号从100开始）

```python
for index, ele in enumerate(li):
    print(index, ele)
```

> * 请使用for循环输出列表的所有元素

```python
for i in li:
    print(i)
```

4 写代码，有如下列表，请按照功能要求实现每一个功能

```py
li = ["hello", 'seven', ["mon", ["h", "kelly"], 'all'], 123, 446]
```

> 请根据索引输出“Kelly”

```python
print(li[2][1][1])
```

> 请使用索引找到’all’元素并将其修改为“ALL”，如

```python
li[2][2] = "ALL"
print(li)
```

5 有如下变量，请实现要求的功能

```py
tu = ("alex", [11, 22, {"k1": 'v1', "k2": ["age", "name"], "k3": (11,22,33)}, 44])
```

> 讲述元组的特性

```python
不可变，没有添加和删除的方法
```

> 请问tu变量中的第一个元素“alex”是否可被修改？

```python
不能
```

> 请问tu变量中的”k2”对应的值是什么类型？是否可以被修改？如果可以，请在其中添加一个元素“Seven”

```python
列表，可以被修改
tu[1][2]["k2"].append("seven")
print(tu)
```

> 请问tu变量中的”k3”对应的值是什么类型？是否可以被修改？如果可以，请在其中添加一个元素“Seven“

6、转换

> 将字符串s = “alex”转换成列表

```python
print(list(s))
```

> 将字符串s = “alex”转换成元祖

```python
print(tuple(s))
```

> 将列表li = \[“alex”, “seven”\]转换成元组

```python
print(tuple(li))
```

> 将元组tu = \(‘Alex’, “seven”\)转换成列表

```python
print(list(tu))
```

> 将列表li = \[“alex”, “seven”\]转换成字典且字典的key按照10开始向后递增

```python
li = ["alex", "seven"]
num = 10
dic = {}
for i in range(len(li)):
    dic[num] = li[i]
    num += 1
print(dic)
```

7、元素分类

> 有如下值li = \[11,22,33,44,55,66,77,88,99,90\]，将所有大于66的值保存至字典的第一个key中，将小于66的值保存至第二个key的值中。即：{‘k1’:大于66的所有值, ‘k2’:小于66的所有值}

```python
dic = {"k1":[], "k2":[]}
for i in li:
    if i > 66:
        dic["k1"].append(i)
    elif i < 66:
        dic["k2"].append(i)
print(dic)
```

8、在不改变列表数据结构的情况下找最大值li = \[1,3,2,7,6,23,41,243,33,85,56\]

```python
max_value = li[0]
for i in li:
    if i > max_value:
        max_value = i
print(max_value)
```

9 在不改变列表中数据排列结构的前提下，找出以下列表中最接近最大值和最小值的平均值 的数`li = [-100,1,3,2,7,6,120,121,140,23,411,99,243,33,85,56]`

```python
li = [-100,1,3,2,7,6,142, 120,121,140,23,411,99,243,33,85,56]
max_value = li[0]
min_value = li[0]
for i in li:
    if i > max_value:
        max_value = i
    if i < min_value:
        min_value = i

avg_value = (max_value+min_value)/2
close_n = li[0]
for i in li:
    if abs(i - avg_value) < abs(close_n - avg_value):
        close_n = i
print(close_n)
```

10 利用for循环和range输出9 \* 9乘法表

```python
for i in range(1, 10):
    for j in range(1, i+1):
        print("%s*%s=%s" % (j,i,i*j), end=" ")
    print(end="\n")
```

11 求100以内的素数和

```python
total = 0
for i in range(2, 101):
    for j in range(2, i):
        if i % j == 0:
            break
    else:
        total += i
print(total)
```

12 请说明python2 与python3中的默认编码是什么？

```python
python2默认是ascii
python3默认是utf-8
```

13 为什么会出现中文乱码？你能列举出现乱码的情况有哪几种？

```html
1 文件编码是utf-8，打开文件的时候却指定了gbk的编码
2 windows上的文件(windows上新建的文件默认都是gbk的编码)，传到mac电脑去打开(mac电脑默认的编码是utf-8)
```



