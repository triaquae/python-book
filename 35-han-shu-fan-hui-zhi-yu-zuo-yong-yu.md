函数外部的代码要想获取函数的执行结果，就可以在函数里用return语句把结果返回

```py
def stu_register(name, age, course='PY' ,country='CN'):
    print("----注册学生信息------")
    print("姓名:", name)
    print("age:", age)
    print("国籍:", country)
    print("课程:", course)
    if age > 22:
        return False
    else:
        return True
registriation_status = stu_register("王山炮",22,course="PY全栈开发",country='JP')
if registriation_status:
    print("注册成功")
else:
    print("too old to be a student.")
```

**注意**

* 函数在执行过程中只要遇到return语句，就会停止执行并返回结果，so 也可以理解为 return 语句代表着函数的结束

* 如果未在函数中指定return,那这个函数的返回值为None

## 全局与局部变量

```py
name = "Alex Li"
def change_name():
    name = "金角大王,一个有Tesla的高级屌丝"
    print("after change", name)
change_name()
print("在外面看看name改了么?",name)
```

输出

```py
after change 金角大王,一个有Tesla的高级屌丝
在外面看看name改了么? Alex Li
```

为什么在函数内部改了name的值后， 在外面print的时候却没有改呢？ 因为这两个name根本不是一回事

* 在函数中定义的变量称为局部变量，在程序的一开始定义的变量称为全局变量。

* 全局变量作用域\(即有效范围\)是整个程序，局部变量作用域是定义该变量的函数。

* 变量的查找顺序是**局部变量&gt;全局变量**
* 当全局变量与局部变量同名时，在定义局部变量的函数内，局部变量起作用；在其它地方全局变量起作用。

* 在函数里是不能直接修改全局变量的

#### 就是想在函数里修改全局变量怎么办？

```py
name = "Alex Li"
def change_name():
    global name #声明一个全局变量
    name = "Alex 又名金角大王,爱生活、爱自由、爱姑娘"
    print("after change", name)
change_name()
print("在外面看看name改了么?", name)
```

`global name`**的作用就是要在函数里声明全局变量name ，意味着最上面的**`name = “Alex Li”`**即使不写，程序最后面的print也可以打印name**

## 传递列表、字典、集合产生的现象

```py
d = {"name":"Alex","age":26,"hobbie":"大保健"}
l = ["Rebeeca","Katrina","Rachel"]
def change_data(info,girls):
    info["hobbie"] = "学习"
    girls.append("XiaoYun")
change_data(d,l)
print(d,l)
```

执行结果{‘name’: ‘Alex’, ‘age’: 26, ‘hobbie’: ‘学习’} \[‘Rebeeca’, ‘Katrina’, ‘Rachel’, ‘XiaoYun’\]  
  
不是说不能在函数里改全局变量么，怎么改了呀？

![](https://book.apeland.cn/media/images/2019/03/20/image_1J3SWdE.png)

根据上图我们能看出， 程序只是把d这个dict的内存地址传给了change\_data函数，把dict比作鱼缸，里面的k,v比作缸里装的鱼。现在只是把鱼缸丢给了函数，这个鱼缸本身你不能改，但是里面的鱼可以。 相当于只是传了一个对这个d的引用关系给到函数的形参。这样是为了减少内存的浪费，因为如果这个dict比较大，传一次到函数里就要copy一份新的值的话，效率太低了。

