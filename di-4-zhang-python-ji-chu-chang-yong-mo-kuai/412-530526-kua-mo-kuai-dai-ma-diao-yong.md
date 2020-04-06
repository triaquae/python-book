## 包\(Package\)

当你的模块文件越来越多，就需要对模块文件进行划分，比如把负责跟数据库交互的都放一个文件夹，把与页面交互相关的放一个文件夹，

```py
my_proj/
├── apeland_web  #代码目录
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   └── views.py
├── manage.py
└── my_proj    #配置文件目录
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

像上面这样，**一个文件夹管理多个模块文件，这个文件夹就被称为包**

一个包就是一个文件夹，但该文件夹下必须存在**init**.py 文件, 该文件的内容可以为空，**int**.py用于标识当前文件夹是一个包。

这个**init**.py的文件主要是用来对包进行一些初始化的，当当前这个package被别的程序调用时，**init**.py文件会先执行，一般为空， 一些你希望只要package被调用就立刻执行的代码可以放在**init**.py里，一会后面会演示。

## 跨模块导入

目录结构如下

```py
my_proj
├── apeland_web
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   └── views.py
├── manage.py
└── my_proj
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

根据上面的结构，如何实现在apeland_web`/views.py`里导入my_`proj/settings.py`模块？

直接导入的话，会报错，说找到不模块

![](https://book.apeland.cn/media/images/2019/04/11/image.png)

是因为路径找不到，my\_proj/settings.py 相当于是apeland\_web/views.py的父亲\(apeland\_web\)的兄弟\(my\_proj\)的儿子\(settings.py\)，settings.py算是views.py的表弟啦，在views.py里只能导入同级别兄弟模块代码，或者子级别包里的模块，根本不知道表弟表哥的存在。这可怎么办呢？

答案是**添加环境变量，把父亲级的路径添加到sys.path中，就可以了，这样导入 就相当于从父亲级开始找模块了。**

_apeland\_web/views.py中添加环境变量_

```py
import sys ,os
BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__))) #__file__的是打印当前被执行的模块.py文件相对路径，注意是相对路径
print(BASE_DIR) # 输出是/Users/alex/PycharmProjects/apeland_py_learn/day4_常用模块/my_proj 
sys.path.append(BASE_DIR)
from  my_proj import settings
print(settings.DATABASES)
```

### 官方推荐的跨目录导入方法

虽然通过添加环境变量的方式可以实现跨模块导入，但是官方不推荐这么干，因为这样就需要在每个目录下的每个程序里都写一遍添加环境变量的代码。

官方推荐的玩法是，在项目里创建个入口程序，整个程序调用的开始应该是从入口程序发起，这个入口程序一般放在项目的顶级目录

这样做的好处是，项目中的二级目录 apeland\_web/views.py中再调用他表亲my\_proj/settings.py时就不用再添加环境变量了。

原因是由于manage.py在顶层，manage.py启动时项目的环境变量路径就会自动变成….xxx/my\_proj/这一级别

![](http://m.qpic.cn/psc?/V11zJNSn1iYfOW/X7Nyc96QcijfM21*qh5ymbjeiuvFCSwGecv82oAuAjaaMQapNvtZlrVZZPqOdN1Bf5OY8UClvDVdKvbzT88nzQ!!/b&bo=YgVaAgAAAAADBx0!&rf=viewer_4)

