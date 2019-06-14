## 什么是模块？

在计算机程序的开发过程中，随着程序代码越写越多，在一个文件里代码就会越来越长，越来越不容易维护。

为了编写可维护的代码，我们把很多函数分组，分别放到不同的文件里，这样，每个文件包含的代码就相对较少，很多编程语言都采用这种组织代码的方式。在Python中，一个.py文件就可以称之为一个模块（Module）。

## 使用模块有什么好处？

1. 最大的好处是大大提高了代码的可维护性。其次，编写代码不必从零开始。当一个模块编写完毕，就可以被其他地方引用。我们在编写程序的时候，也经常引用其他模块，包括Python内置的模块和来自第三方的模块。

2. 使用模块还可以避免函数名和变量名冲突。每个模块有独立的命名空间，因此相同名字的函数和变量完全可以分别存在不同的模块中，所以，我们自己在编写模块时，不必考虑名字会与其他模块冲突

## 模块分类

模块分为三种：

* 内置标准模块（又称标准库）执行help\(‘modules’\)查看所有python自带模块列表

* 第三方开源模块，可通过pip install 模块名 联网安装

* 自定义模块

## 模块导入&调用

```py
import module_a  #导入
from module import xx
from module.xx.xx import xx as rename #导入后重命令
from module.xx.xx import *  #导入一个模块下的所有方法，不建议使用
module_a.xxx  #调用
```

> 注意：模块一旦被调用，即相当于执行了另外一个py文件里的代码

## 自定义模块

这个最简单， 创建一个.py文件，就可以称之为模块，就可以在另外一个程序里导入

  


![](https://book.apeland.cn/media/images/2019/04/05/image.png)

  


## 模块查找路径

发现，自己写的模块只能在当前路径下的程序里才能导入，换一个目录再导入自己的模块就报错说找不到了， 这是为什么？

这与导入模块的查找路径有关

```py
import sys
print(sys.path)
```

输出（注意不同的电脑可能输出的不太一样）

```py
['', '/Library/Frameworks/Python.framework/Versions/3.6/lib/python36.zip', 
'/Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6', 
'/Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/lib-dynload', 
'/Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/site-packages']
```

你导入一个模块时，Python解释器会按照上面列表顺序去依次到每个目录下去匹配你要导入的模块名，只要在一个目录下匹配到了该模块名，就立刻导入，不再继续往后找。

> 注意列表第一个元素为空，即代表当前目录，所以你自己定义的模块在当前目录会被优先导入。

我们自己创建的模块若想在任何地方都能调用，那就得确保你的模块文件至少在模块路径的查找列表中。

我们一般把自己写的模块放在一个带有“site-packages”字样的目录里，我们从网上下载安装的各种第三方的模块一般都放在这个目录。

## 练习题：

自己写一个模块，并确保你的python代码在任何一个地方都能导入这个模块。

