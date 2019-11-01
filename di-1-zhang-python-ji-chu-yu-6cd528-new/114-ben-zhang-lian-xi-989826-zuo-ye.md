## 练习题:【练习题答案再页尾】

1. 简述编译型与解释型语言的区别，且分别列出你知道的哪些语言属于编译型，哪些属于解释型

2. Pyhton 单行注释和多行注释分别用什么?

3. 布尔值分别有什么，及作用是什么?

4. 声明变量注意事项有那些?

5. 如何查看变量在内存中的地址?

6. 请写出 and 、or、not 的作用，并用代码来演示

7. 查看2、2.22、“小猿圈”分别是什么数据类型的语法是什么？

8. 写代码

   1. [ ] 实现用户输入用户名和密码,当用户名为 seven 且 密码为 123 时,显示登陆成功,否则登陆失败!
   2. [ ] 实现用户输入用户名和密码,当用户名为 seven 且 密码为 123 时,显示登陆成功,否则登陆失败,失败时允许重复输入三次
   3. [ ] 实现用户输入用户名和密码,当用户名为 seven 或 alex 且 密码为 123 时,显示登陆成功,否则登陆失败,失败时允许重复输入三次 

9. 写代码

   1. 使用 while 循环实现输出 1,2,3,4,5, 7,8,9, 11,12

   2. 使用while 循环输出100-50，从大到小，如100，99，98…，到50时再从0循环输出到50，然后结束

   3.  使用 while 循环实现输出 1-100 内的所有奇数

   4. 使用 while 循环实现输出 1-100 内的所有偶数

   5. 使用while循环实现输出2-3+4-5+6…+100 的和

10. 现有如下两个变量,请根据执行结果解释原因

    1. ```
       n1 = 123456
       n2 = n1
       n1 = 333
       print(n1,n2)
       ```

11. 制作趣味模板程序（编程题）

    1. 需求：等待用户输入名字、地点、爱好，根据用户的名字和爱好进行任意显示

    2. 如：敬爱可爱的xxx，最喜欢在xxx地方干xxx

12. 输入一年份，判断该年份是否是闰年并输出结果。（编程题）

    1. 注：凡符合下面两个条件之一的年份是闰年。 （1） 能被4整除但不能被100整除。 （2） 能被400整除。

13. 假设一年期定期利率为3.25%，计算一下需要过多少年，一万元的一年定期存款连本带息能翻番？（编程题）

14. 使用while,完成以下图形的输出

    1. ```
       *
       * *
       * * *
       * * * *
       * * * * *
       * * * *
       * * *
       * *
       *
       ```

15. 一球从100米高度自由落下，每次落地后反跳回原高度的一半；再落下，求它在第10次落地时，共经过多少米？第10次反弹多高？



## 作业

**双色球彩票 选购程序**

1. 先让用户依次选择6个红球，再选择2个蓝球，最后统一打印用户选择的球号。

1. 确保用户不能选择重复的，选择的数不能超出范围。 

要达到的结果参考

![](https://book.apeland.cn/media/images/2019/02/22/qq20190222-204445-lottery_pO4lNmv.gif)

![](https://book.apeland.cn/media/images/2019/02/22/image_4UWf34G.png)

练习题答案如下：

1 简述编译型与解释型语言的区别，且分别列出你知道的哪些语言属于编译型，哪些属于解释型。

```html
编译型语言:
	x（源码） --> 编译 --> y（编译后的机器码）
	特点：执行速度快，将整个代码全部编译后再执行，但是跨平台比较差。
解释型语言:
	x（源码） --> 解释器（虚拟机） --> 解释执行
	特点：执行速度比较慢，因为逐行解释再执行，但是跨平台性好。
```

2 Pyhton 单行注释和多行注释分别用什么?

```html
单行使用 
	# 我被注释了 
多行使用 
	"""
	要注释的内容
	要被注释了吗
	"""
```

3 布尔值分别有什么，及作用是什么?

```html
布尔型只有两个值True和False，基本都是用于逻辑判断。
※布尔值实际上也属于整型，True相当于1，False相当于0
```

4 声明变量注意事项有那些?

```html
1、变量名只能是 字母、数字和下划线的任意组合
2、变量名的第一个字符不能使数字
3、[and,print,as,not,or]等关键字不能作为变量名
4、变量名不能为中文、拼音；变量名单词不能过长：变量单词不达意
```

5 如何查看变量在内存中的地址?

```python
id(变量名)
```

6 请写出 and 、or、not 的作用，并用代码来演示

```python
and 、or、not 都是逻辑运算符
and：逻辑的与
>>> 1 and 1
1
>>> 1 and 0
0
or：逻辑的或
>>> 1 or 0
1
>>> 0 or 1
1
not：逻辑的非
>>> a = True
>>> not a
False
```

7 查看2、2.22、“路飞学城”分别是什么数据类型的语法是什么？

```python
>>> type(2)
<class 'int'>
>>> type(2.22)
<class 'float'>
>>> type("路飞学城")
<class 'str'>
```

8 写代码

> 实现用户输入用户名和密码,当用户名为 seven 且 密码为 123 时,显示登陆成功,否则登陆失败!

```python
username = "seven"
password = "123"
name = input(">>>:").strip()
passwd = input(">>>:").strip()

if name == username and passwd == password:
    print("登陆成功")
else:
    print("登陆失败")
```

> ```
> 实现用户输入用户名和密码,当用户名为 seven 且 密码为 123 时,显示登陆成功,否则登陆失败,失败时允许重复输入三次
> ```

```python
username = "seven"
password = "123"

count = 0
while count < 3:
    name = input(">>>:").strip()
    passwd = input(">>>:").strip()

    if name == username and passwd == password:
        print("登陆成功")
        break
    else:
        print("登陆失败")
        count += 1
```

> 实现用户输入用户名和密码,当用户名为 seven 或 alex 且 密码为 123 时,显示登陆成功,否则登陆失败,失败时允许重复输入三次

```python
username1 = "seven"
username2 = "alex"
password = "123"

count = 0
while count < 3:
    name = input(">>>:").strip()
    passwd = input(">>>:").strip()

    if name == username1 or name == username2 and passwd == password:
        print("登陆成功")
        break
    else:
        print("登陆失败")
        count += 1
```

9  写代码

> 使用 while 循环实现输出 1,2,3,4,5, 7,8,9, 11,12

```python
count = 0
while count < 12:
    count += 1
    if count == 6 or count == 10:
        continue
    print(count)
```

> 使用while 循环输出100-50，从大到小，如100，99，98…，到50时再从0循环输出到50，然后结束

```python
count = 100
while count > -2:
    if count >= 50:
        print(count)
    else:
        print(49-count)
    count -= 1
```

> 用 while 循环实现输出 1-100 内的所有奇数

```python
count = 0
while count < 100:
    count+=1
    if count % 2 != 0:
        print(count)
```

> 用 while 循环实现输出 1-100 内的所有偶数

```python
count = 0
while count < 100:
    count+=1
    if count % 2 == 0:
        print(count)
```

> 使用while循环实现输出2-3+4-5+6…+100 的和

```python
count = 2
total = 0
while count <= 100:
    if count % 2 == 0:
        total += count
    else:
        total -= count
    count += 1
print(total)
```

10 现有如下两个变量,请根据执行结果解释原因

```python
n1 = 123456
n2 = n1
n1 = 333
print(n1,n2)
n1等于123456，
将n1的值赋值给n2，此时，n1等于n2都等于123456，
n1=333，
n1等于333，n2还是123456
```

11 制作趣味模板程序（编程题）

> 需求：等待用户输入名字、地点、爱好，根据用户的名字和爱好进行任意显示

```python
username = input("username>>>:").strip()
place = input("place>>>:").strip()
hobby = input(">>>:").strip()
print("敬爱可爱的%s，最喜欢在%s地方干%s" % (username, place, hobby))
```

12 输入一年份，判断该年份是否是闰年并输出结果。（编程题）

```python
凡符合下面两个条件之一的年份是闰年。 
（1） 能被4整除但不能被100整除。 （2） 能被400整除。
while True:
    year = input("year>>>:").strip()
    if year.isdigit():
        year = int(year)
    else:
        print("请输入整数")
        continue
    if year % 4 ==0 and year % 100 != 0:
        print("是闰年")
    elif year % 400 == 0:
        print("是世纪闰年")
    else:
        print("不是闰年")
```

13 假设一年期定期利率为3.25%，计算一下需要过多少年，一万元的一年定期存款连本带息能翻番？（编程题）

```python
year = 0
salary = 10000
rate = 0.0325
while salary < 20000:
    year += 1
    interest = salary*rate
    salary += interest
    print(year, interest, salary)
```

14 使用while,完成以下图形的输出

```
*
* *
* * *
* * * *
* * * * *
* * * *
* * *
* *
*
```

```python
count = 0
while count < 10:
    count += 1
    if count <= 5:
        print(count * " * ")
    else:
        print((10 - count) * " * ")
```

15 一球从100米高度自由落下，每次落地后反跳回原高度的一半；再落下，求它在第10次落地时，共经过多少米？第10次反弹多高？

```python
height = 100
times = 0
total = 0

while times < 10:
    times += 1
    new_height = height/2
    total += 2*new_height
    height = new_height
print(times, new_height, total+100)
```

