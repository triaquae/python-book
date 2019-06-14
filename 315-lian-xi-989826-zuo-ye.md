## 练习题

1. 写函数，计算传入数字参数的和。（动态传参）

2. 写函数，用户传入修改的文件名，与要修改的内容，执行函数，完成整个文件的批量修改操作

3. 写函数，检查用户传入的对象（字符串、列表、元组）的每一个元素是否含有空内容。

4. 写函数，检查传入字典的每一个value的长度,如果大于2，那么仅保留前两个长度的内容（对value的值进行截断），并将新内容返回给调用者，注意传入的数据可以是字符、list、dict

5. 解释闭包的概念

6. 写函数，返回一个扑克牌列表，里面有52项，每一项是一个元组

        例如：\[\(‘红心’，2\),\(‘草花’，2\), …\(‘黑桃A’\)\]

   7.写函数，传入n个数，返回字典{‘max’:最大值,’min’:最小值}

```py
例如:minmax(2,5,7,8,4)
返回:{‘max’:8,’min’:2}
```

    8._写函数，专门计算图形的面积_

* _其中嵌套函数，计算圆的面积，正方形的面积和长方形的面积_

* _调用函数area\(‘圆形’,圆半径\) 返回圆的面积_

* _调用函数area\(‘正方形’,边长\) 返回正方形的面积_

* _调用函数area\(‘长方形’,长，宽\) 返回长方形的面积_

* _ _
  ```py
  #代码模板
  def area():
      def 计算长方形面积():
          pass

      def 计算正方形面积():
          pass

      def 计算圆形面积():
          pass
  ```

    9._写函数，传入一个参数n，返回n的阶乘_

```py
例如:cal(7)
计算7654321
```

10.编写装饰器，为多个函数加上认证的功能（用户的账号密码来源于文件），要求登录成功一次，后续的函数都无需再输入用户名和密码

11.生成器和迭代器的区别？

12 生成器有几种方式获取value？

13._通过生成器写一个日志调用方法， 支持以下功能_

* _根据指令向屏幕输出日志_

* _根据指令向文件输出日志_

* _根据指令同时向文件&屏幕输出日志_



_以上日志格式如下_

```py
2017-10-19 22:07:38 [1] test log db backup 3
2017-10-19 22:07:40 [2]    user alex login success
#注意：其中[1],[2]是指自日志方法第几次调用，每调用一次输出一条日志
```

* _代码结构如下_

```py
 def logger(filename,channel=’file’):
    “””
    日志方法
    :param filename: log filename
    :param channel: 输出的目的地，屏幕(terminal)，文件(file)，屏幕+文件(both)
    :return:
    “””
    …your code…

 #调用
 logobj = logger(filename=”web.log”,channel=’both’)
 log_obj.__next()
 log_obj.send(‘user alex login success’)

```

14.用map来处理字符串列表,把列表中所有人都变成sb,比方alex\_sb

```py
name=[‘alex’,’wupeiqi’,’yuanhao’,’nezha’]
```

  
15.用filter函数处理数字列表，将列表中所有的偶数筛选出来

```py
num = [1,3,5,6,7,8]
```

  
16.如下，每个小字典的name对应股票名字，shares对应多少股，price对应股票的价格

```py
portfolio = [
    {‘name’: ‘IBM’, ‘shares’: 100, ‘price’: 91.1},
    {‘name’: ‘AAPL’, ‘shares’: 50, ‘price’: 543.22},
    {‘name’: ‘FB’, ‘shares’: 200, ‘price’: 21.09},
    {‘name’: ‘HPQ’, ‘shares’: 35, ‘price’: 31.75},
    {‘name’: ‘YHOO’, ‘shares’: 45, ‘price’: 16.35},
    {‘name’: ‘ACME’, ‘shares’: 75, ‘price’: 115.65}
]
```

* 通过哪个内置函数可以计算购买每支股票的总价

* 用filter过滤出，单价大于100的股票有哪些



17.有列表 li = \[‘alex’, ‘egon’, ‘smith’, ‘pizza’, ‘alen’\], 请将以字母“a”开头的元素的首字母改为大写字母；

18.有列表 li = \[‘alex’, ‘egon’, ‘smith’, ‘pizza’, ‘alen’\], 请以列表中每个元素的第二个字母倒序排序；

19.有名为`poetry.txt`的文件，其内容如下，请删除第三行；

```py
   昔人已乘黄鹤去，此地空余黄鹤楼。

   黄鹤一去不复返，白云千载空悠悠。

   晴川历历汉阳树，芳草萋萋鹦鹉洲。

   日暮乡关何处是？烟波江上使人愁。
```

  
20.有名为`username.txt`的文件，其内容格式如下，写一个程序，判断该文件中是否存在”alex”, 如果没有，则将字符串”alex”添加到该文件末尾，否则提示用户该用户已存在；

```py
  pizza
  alex
  egon
```

  
21.有名为user\_info.txt的文件，其内容格式如下，写一个程序，删除id为100003的行；

```py
  pizza,100001
  alex, 100002
  egon, 100003
```



22.有名为user\_info.txt的文件，其内容格式如下，写一个程序，将id为100002的用户名修改为`alex li`；

```py
 pizza,100001
 alex, 100002
 egon, 100003
```

  
23.写一个计算每个程序执行时间的装饰器；

24.lambda是什么？请说说你曾在什么场景下使用lambda？

25.题目：写一个摇骰子游戏，要求用户压大小，赔率一赔一。要求：三个骰子，每个骰子的值从1-6，摇大小，每次打印摇出来3个骰子的值。



## 作业

一些关键练习题的参考答案

#### 递归二分查找

```py
a = [1,3,4,6,7,8,9,11,15,17,19,21,22,25,29,33,38,69,107]
def binary_search(start,end,n,d_list):
    """
    每次把列表规模折半，查找一个数据最多只需要2的n次方 < len(d_list),是2的多少次方，就是最多查多少次。
    假如列表长度为200，那最多只需查询8次(2**8次方）
    :param start: 查找的起始位置 
    :param end: 查找的结束位置 
    :param n: 要查找的值
    :param d_list: 要找的列表
    :return: 
    """
    if start < end: # 查找的范围[start:end]依然大于0个
        mid = (start + end)//2  # 找到中间位置
        if d_list[mid] > n:  # 如果中间的这个值比要找的n大，代表要往d_list[mid]左边找
            print("go left",start,mid,end,"--",d_list[start],d_list[mid],d_list[end-1])
            binary_search(start,mid,n,d_list)
        elif d_list[mid] < n :  # 要往右边找，继续折半
            print("go right..",start,mid,end,"--",d_list[start],d_list[mid],d_list[end-1])
            binary_search(mid+1,end,n,d_list)
        else:  # 找到了
            print("find:",d_list[mid],mid)
    else:  # 假设start=9,end=9, 那d_list[9:9]已经取不到值了，在这种情况下，只能说明，要找的这个值不在这个列表里
        print("cannot find %s in this data list" % n)
binary_search(0, len(a), 22, a)
```



