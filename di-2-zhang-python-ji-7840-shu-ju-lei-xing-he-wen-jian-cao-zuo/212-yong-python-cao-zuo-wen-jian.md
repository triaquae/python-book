用word操作一个文件的流程如下：

1. 找到文件，双击打开

2. 读或修改

3. 保存&关闭



用python操作文件也差不多：

```py
f=open(filename)  # 打开文件
f.write("我是野生程序员") # 写操作
f.read()  #读操作
f.close() #保存并关闭
```

不过有一点跟人肉操作word文档不同，就是word文档只要打开了，就即可以读、又可以修改。 但Python比较变态，只能以读、创建、追加 3种模式中的任意一种打开文件，不能即写又读。

## 操作模式

* r 只读模式

* w 创建模式，若文件已存在，则覆盖旧文件

* a 追加模式，新数据会写到文件末尾



## 创建文件

```py
f = open(file='D:/工作日常/staff.txt',mode='w')
f.write("Alex  CEO  600\n")
f.write("黑姑娘  行政  5000\n")
f.close()
```

## 只读模式

```py
f = open(file='兼职白领学生空姐模特护士联系方式.txt',mode='r')
print(f.readline())  # 读一行
print('------分隔符-------')
data = f.read()  # 读所有，剩下的所有
print(data)
f.close()
```

执行输出

```py
马纤羽     深圳    173    50    13744234523
------分隔符-------
乔亦菲     广州    172    52    15823423525
罗梦竹     北京    175    49    18623423421
刘诺涵     北京    170    48    18623423765
岳妮妮     深圳    177    54    18835324553
贺婉萱     深圳    174    52    18933434452
叶梓萱     上海    171    49    18042432324
```

## 追加模式

```py
f = open(file='兼职白领学生空姐模特护士联系方式.txt',mode='a')
f.write("黑姑娘 北京  168  48\n")  # 会追加到文件尾部
f.close()
```

## 循环文件

```py
f = open(file='兼职白领学生空姐模特护士联系方式.txt',mode='a')
f.write("黑姑娘 北京  168  48\n")  # 会追加到文件尾部
f.close()
```

```py
f = open(file='兼职白领学生空姐模特护士联系方式.txt',mode='r')
for line in f:
    line = line.split()
    name,addr,height,weight,phone = line
    height = int(height)
    weight = int(weight)
    if height > 170 and weight <= 50:
        print(line)
f.close()
```

输出

```py
['马纤羽', '深圳', '173', '50', '13744234523']
['罗梦竹', '北京', '175', '49', '18623423421']
['叶梓萱', '上海', '171', '49', '18042432324']
```



## 其它功能

```py
 def mode(self) -> str:
        返回文件打开的模式
    def name(self) -> str:
        返回文件名
    def fileno(self, *args, **kwargs): # real signature unknown
        返回文件句柄在内核中的索引值，以后做IO多路复用时可以用到
    def flush(self, *args, **kwargs): # real signature unknown
        把文件从内存buffer里强制刷新到硬盘
    def readable(self, *args, **kwargs): # real signature unknown
        判断是否可读
    def readline(self, *args, **kwargs): # real signature unknown
        只读一行，遇到\r or \n为止
    def seek(self, *args, **kwargs): # real signature unknown
        把操作文件的光标移到指定位置
        *注意seek的长度是按字节算的， 字符编码存每个字符所占的字节长度不一样。
        如“路飞学城” 用gbk存是2个字节一个字，用utf-8就是3个字节，因此以gbk打开时，seek(4) 就把光标切换到了“飞”和“学”两个字中间。
        但如果是utf8,seek(4)会导致，拿到了飞这个字的一部分字节，打印的话会报错，因为处理剩下的文本时发现用utf8处理不了了，因为编码对不上了。少了一个字节
    def seekable(self, *args, **kwargs): # real signature unknown
        判断文件是否可进行seek操作
    def tell(self, *args, **kwargs): # real signature unknown
        返回当前文件操作光标位置 
    def truncate(self, *args, **kwargs): # real signature unknown
        按指定长度截断文件
        *指定长度的话，就从文件开头开始截断指定长度，不指定长度的话，就从当前位置到文件尾部的内容全去掉。
    def writable(self, *args, **kwargs): # real signature unknown
        判断文件是否可写
```



## 混合模式

其实我一直像你隐瞒，因为怕你觉得复杂。 打开文件其实还有3种混合模式

w+ 写读 , 这个功能基本没什么意义，它会创建一个新文件 ，写一段内容，可以再把写的内容读出来，没什么卵用。

r+ 读写，能读能写,但都是写在文件最后，跟追加一样

a+ 追加读,文件 一打开时光标会在文件尾部,写的数据全会是追加的形式



### **r+模式**

![](https://book.apeland.cn/media/images/2019/03/07/image_9X06BqU.png)

因为默认就是往文件 尾部写



## 修改文件

尝试直接以r+模式打开文件，默认会把新增的内容追加到文件最后面。但我想要的是修改中间的内容 ，怎么办？ 为什么会把内容添加到尾部呢？\(最新测试r+会从头覆盖，测试代码如下\)

![](https://book.apeland.cn/media/images/2019/03/07/image_V9CyraT.png)

**问：为什么原有数据会被覆盖呢？**

这是硬盘的存储原理导致的，当你把文件存到硬盘上，就在硬盘上划了一块空间，存数据，等你下次打开这个文件 ，seek到一个位置，每改一个字，就是把原来的覆盖掉，如果要插入，是不可能的，因为后面的数据在硬盘上不会整体向后移。所以就出现 当前这个情况 ，你想插入，却变成了会把旧内容覆盖掉。

**问：但是人家word, vim 都可以修改文件 呀，你这不能修改算个什么玩意？**

我并没说就不能修改了，你想修改当然可以，就是不要在硬盘上修改，把内容全部读到内存里，数据在内存里可以随便增删改查，修改之后，把内容再全部写回硬盘，把原来的数据全部覆盖掉。vim word等各种文本编辑器都是这么干的。

**问：说的好像有道理，但你又没看过word软件的源码，你凭什么这么笃定？**

哈哈，我不需要看源码，硬盘 的存储原理决定了word必须这么干 ，不信的话，还有个简单的办法来确认我说的，就是用word or vim读一个编辑一个大文件 ，至少几百MB的，你 会发现，加载过程会花个数十秒，这段时间干嘛了？ cpu 去玩了？去上厕所啦？ 当然不是，是在努力把数据 从硬盘上读到内存里。

**问：但是文件如果特别大，比如5个GB,读到内存，就一下子吃掉了5GB内存，好费资源呀，有没有更好的办法呢？**

如果不想占内存，只能用另外一种办法啦，就是边读边改， 什么意思？ 不是不能改么？是不能改原文件 ，但你可以打开旧文件 的同时，生成一个新文件呀，边从旧的里面一行行的读，边往新的一行行写，遇到需要修改就改了再写到新文件 ，这样，在内存里一直只存一行内容。就不占内存了。 但这样也有一个缺点，就是虽然不占内存 ，但是占硬盘，每次修改，都要生成一份新文件，虽然改完后，可以把旧的覆盖掉，但在改的过程中，还是有2份数据 的。

**问：还有更好的方式 么？**

有完没完？ 没了。

**占硬盘方式的文件修改代码示例**

```py
f_name = "兼职白领学生空姐模特护士联系方式.txt"
f_new_name = "%s.new" % f_name
old_str = "刘诺涵"
new_str = "[黑姑娘]"
f = open(f_name,'r')
f_new = open(f_new_name,'w')
for line in f:
    if old_str in line:
        new_line = line.replace(old_str,new_str)
    else:
        new_line = line
    f_new.write(new_line)
f.close()
f_new.close()
```

上面的代码，会生成一个修改后的新文件 ，原文件不动，若想覆盖原文件

```py
import os
f_name = "兼职白领学生空姐模特护士联系方式.txt"
f_new_name = "%s.new" % f_name
old_str = "刘诺涵"
new_str = "[黑姑娘]"
f = open(f_name,'r')
f_new = open(f_new_name,'w')
for line in f:
    if old_str in line:
        new_line = line.replace(old_str,new_str)
    else:
        new_line = line
    f_new.write(new_line)
f.close()
f_new.close()
os.rename(f_new_name,f_name) #把新文件名字改成原文件 的名字，就把之前的覆盖掉了,windows使用os.replace # 帮助文档说明replace会覆盖原文件
```

## 

## 练习题

**练习题1 —— 全局替换程序：**

* 写一个脚本，允许用户按以下方式执行时，即可以对指定文件内容进行全局替换

```
python your_script.py old_str new_str filename
```

* 替换完毕后打印替换了多少处内容  

**练习题2 —— 模拟登陆：**

* 用户输入帐号密码进行登陆

* 用户信息保存在文件内

* 用户密码输入错误三次后锁定用户，下次再登录，检测到是这个用户也登录不了



