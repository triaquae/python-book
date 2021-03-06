## 本节重点

* 掌握什么是类、什么是对象
* 掌握如何定义及使用类与对象
* 了解对类与对象之间的关系

> **本节时长需控制在45分钟内**

### 类与对象的概念

类即类别、种类，是面向对象设计最重要的概念，从一小节我们得知对象是特征与技能的结合体，而类则是一系列对象相似的特征与技能的结合体。

那么问题来了，先有的一个个具体存在的对象（比如一个具体存在的人），还是先有的人类这个概念，这个问题需要分两种情况去看

* 在现实世界中：肯定是先有对象，再有类

```py
世界上肯定是先出现各种各样的实际存在的物体，然后随着人类文明的发展，人类站在不同的角度总结出了不同的种类，比如
人类、动物类、植物类等概念。也就说，对象是具体的存在，而类仅仅只是一个概念，并不真实存在，比如你无法告诉我人类
具体指的是哪一个人。
```

* 在程序中：务必保证先定义类，后产生对象

```py
这与函数的使用是类似的：先定义函数，后调用函数，类也是一样的：在程序中需要先定义类，后调用类。不一样的是：调用
函数会执行函数体代码返回的是函数体执行的结果，而调用类会产生对象，返回的是对象
```

### 定义类

按照上述步骤，我们来定义一个类（我们站在老男孩学校的角度去看，在座的各位都是学生）

* 在现实世界中，先有对象，再有类

```py
对象1：李坦克
    特征:
        学校=oldboy
        姓名=李坦克
        性别=男
        年龄=18
    技能：
        学习
        吃饭
        睡觉

对象2：王大炮
    特征:
        学校=oldboy
        姓名=王大炮
        性别=女
        年龄=38
    技能：
        学习
        吃饭
        睡觉

对象3：牛榴弹
    特征:
        学校=oldboy
        姓名=牛榴弹
        性别=男
        年龄=78
    技能：
        学习
        吃饭
        睡觉


现实中的老男孩学生类
    相似的特征:
        学校=oldboy
    相似的技能：
        学习
        吃饭
        睡觉
```

* 在程序中，务必保证：先定义（类），后使用类（用来产生对象）

```py
#在Python中程序中的类用class关键字定义，而在程序中特征用变量标识，技能用函数标识，因而类中最常见的无非是：变量和函数的定义
class OldboyStudent:
    school='oldboy'
    def learn(self):
        print('is learning')

    def eat(self):
        print('is eating')

    def sleep(self):
        print('is sleeping')
```

注意：

* 类中可以有任意python代码，这些代码在类定义阶段便会执行，因而会产生新的名称空间，用来存放类的变量名与函数名，可以通过OldboyStudent.\_\_dict\_\_查看
* 类中定义的名字，都是类的属性，点是访问属性的语法。
* 对于经典类来说我们可以通过该字典操作类名称空间的名字，但新式类有限制（新式类与经典类的区别我们将在后续章节介绍）

### 类的使用

* 引用类的属性

```py
OldboyStudent.school #查
OldboyStudent.school='Oldboy' #改
OldboyStudent.x=1 #增
del OldboyStudent.x #删
```

* 调用类，或称为实例化，得到程序中的对象

```py
s1=OldboyStudent()
s2=OldboyStudent()
s3=OldboyStudent()

#如此，s1、s2、s3都一样了，而这三者除了相似的属性之外还各种不同的属性，这就用到了__init__
```

* \_\__init_\_\_方法

```py
#注意：该方法是在对象产生之后才会执行，只用来为对象进行初始化操作，可以有任意代码，但一定不能有返回值
class OldboyStudent:
    ......
    def __init__(self,name,age,sex):
        self.name=name
        self.age=age
        self.sex=sex
    ......

s1=OldboyStudent('李坦克','男',18) #先调用类产生空对象s1，然后调用OldboyStudent.__init__(s1,'李坦克','男',18)
s2=OldboyStudent('王大炮','女',38)
s3=OldboyStudent('牛榴弹','男',78)
```

### 对象的使用

```py
#执行__init__,s1.name='牛榴弹'，很明显也会产生对象的名称空间可以用s2.__dict__查看，查看结果为
{'name': '王大炮', 'age': '女', 'sex': 38}

s2.name #查，等同于s2.__dict__['name']
s2.name='王三炮' #改，等同于s2.__dict__['name']='王三炮'
s2.course='python' #增，等同于s2.__dict__['course']='python'
del s2.course #删，等同于s2.__dict__.pop('course')
```

### 补充说明

* 站的角度不同，定义出的类是截然不同的；
* 现实中的类并不完全等于程序中的类，比如现实中的公司类，在程序中有时需要拆分成部门类，业务类等；
* 有时为了编程需求，程序中也可能会定义现实中不存在的类，比如策略类，现实中并不存在，但是在程序中却是一个很常见的类。



