## 练习题

1. 导入模块的方式有哪几种，官方不推荐哪种？

2. 如何让你写的模块可以被系统上任何一个py文件导入

3. 写一个用户登录验证程序，文件名account.json，内容如下

```py
{“expire_date”: “2021-01-01”, “id”: 1234, “status”: 0, “pay_day”: 22, “password”: “abc”}
```

* 根据用户输入的用户名&密码，找到对应的json文件，把数据加载出来进行验证

* 用户名为json文件名，密码为 password。

* 判断是否过期，与expire\_date进行对比。

* 登陆成功后，打印“登陆成功”，三次登陆失败，status值改为1，并且锁定账号。

  4.把第3题用户密码进行hashlib加密处理。即：json文件里的密码保存为md5的值，然后用md5的值进行验证账号信息是否正确。

  5.最近alex买了个Tesla Model S，通过转账的形式，并且支付了5%的手续费，tesla价格为95万。账户文件为json，请用程序实现该转账行为。

需求如下：

* 目录结构为

```py
.
├── account
│   ├── alex.json
│   └── tesla_company.json
└── bin
      └── start.py
```

当执行start.py时，出现交互窗口

```py
   ———- ICBC Bank ————-
  1.  账户信息
  2.  转账
```

* 选择1 账户信息 显示alex的当前账户余额。

* 选择2 转账 直接扣掉95万和利息费用并且tesla\_company账户增加95万

 6. 对上题增加一个需求：提现。

    目录结构如下

* ```py
  ├── account
  │   └── alex.json
  │   └── tesla_company.json
  ├── bin
  │   └── start.py
  └── core
   └── withdraw.py
  ```

当执行start.py时，出现交互窗口

```py
   ———- ICBC Bank ————-
1.  账户信息
2.  提现
```

* 选择1 账户信息 显示alex的当前账户余额和信用额度。

* 选择2 提现 提现金额应小于等于信用额度，利息为5%，提现金额为用户自定义。

* 体现代码的实现要写在withdraw.py里

  7. 尝试把上一章的验证用户登陆的装饰器添加到提现和转账的功能上。

  8. 对第6题的用户转账、登录、提现操作均记录日志,日志文件位置如下

```py
 .
 ├── account
 │   └── alex.json
 ├── bin
 │   └── start.py
 └── core
 |   └── withdraw.py
 └── logs
     └── bank.log
```

日志格式如下

```py
20190502 18:34:23  alex   transfer      transfered to  [tesla_company]  with amount RMB950000, intrest is RMB47500.
20190812 14:21:15  alex   withdraw      withdraw cash RMB800, intrest is RMB40.
20190815 22:27:19  alex   consume      consumed cash RMB600 in shop [神仙岛洗浴中心], intrest is RMB0.
```

## 作业

题目：网站访问日志分析

需求：

1. 统计本日志文件的总pv、uv

2. 列出全天每小时的pv、uv数

3. 列出top 10 uv的IP地址，以及每个ip的pv点击数

4. 列出top 10 访问量最多的页面及每个页面的访问量

5. 列出访问来源的设备列表及每个设备的访问量

日志格式解释

![](https://book.apeland.cn/media/images/2019/04/16/image_VPk53q8.png)

名词解释：

pv:page visit , 页面访问量，一次请求就是一次pv

uv: user visit, 独立用户，一个ip就算一个独立用户

数据源：[下载链接](http://hcdn1.luffycity.com/data/course_related/72/courseware/课件.zip)

![](https://book.apeland.cn/media/images/2019/04/16/image_xKtqPfX.png)

