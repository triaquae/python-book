你是一家视频网站的后端开发工程师，你们网站有以下几个版块。

```py
def home():
    print("---首页----")
def america():
    print("----欧美专区----")
def japan():
    print("----日韩专区----")
def henan():
    print("----河南专区----")
```

视频刚上线初期，为了吸引用户，你们采取了免费政策，所有视频免费观看，迅速吸引了一大批用户，免费一段时间后，每天巨大的带宽费用公司承受不了了，所以准备对比较受欢迎的几个版块收费，其中包括“欧美” 和 “河南”专区，你拿到这个需求后，想了想，想收费得先让其进行用户认证，认证通过后，再判定这个用户是否是VIP付费会员就可以了，是VIP就让看，不是VIP就不让看就行了呗。 你觉得这个需求很是简单，因为要对多个版块进行认证，那应该把认证功能提取出来单独写个模块，然后每个版块里调用 就可以了，与是你轻轻的就实现了下面的功能 。

```py
account = {
    "is_authenticated":False,# 用户登录了就把这个改成True
    "username":"alex", # 假装这是DB里存的用户信息
    "password":"abc123" # 假装这是DB里存的用户信息
}
def login():
    if account["is_authenticated"] is False:
        username = input("user:")
        password = input("pasword:")
        if username == account["username"] and password == account["password"]:
            print("welcome login....")
            account["is_authenticated"] = True
        else:
            print("wrong username or password!")
    else:
        print("用户已登录，验证通过...")
def home():
    print("---首页----")
def america():
    login()  # 执行前加上验证
    print("----欧美专区----")
def japan():
    print("----日韩专区----")
def henan():
    login()  # 执行前加上验证
    print("----河南专区----")
home()
america()
henan()
```

此时你信心满满的把这个代码提交给你的TEAM LEADER审核，没成想，没过5分钟，代码就被打回来了， TEAM LEADER给你反馈是，我现在有很多模块需要加认证模块，你的代码虽然实现了功能，但是需要更改要加认证的各个模块的源代码，这直接违反了软件开发中的一个原则“开放-封闭”原则，简单来说，它规定已经实现的功能代码不应该被修改，但可以被扩展，即：

* 封闭：已实现的功能代码块不应该被修改

* 开放：对现有功能的扩展开放

这个原则你还是第一次听说，我擦，再次感受了自己这个野生程序员与正规军的差距，BUT ANYWAY,老大要求的这个怎么实现呢？如何在不改原有功能代码的情况下加上认证功能呢？你一时想不出思路，只好带着这个问题回家继续憋，媳妇不在家，去隔壁老王家串门了，你正好落的清静，一不小心就想到了解决方案，不改源代码可以呀。 你师从沙河金角大王时，记得他教过你，高阶函数，就是把一个函数当做一个参数传给另外一个函数，当时大王说，有一天，你会用到它的，没想到这时这个知识点突然从脑子 里蹦出来了，我只需要写个认证方法，每次调用 需要验证的功能 时，直接 把这个功能 的函数名当做一个参数 传给 我的验证模块不就行了么，哈哈，机智如我，如是你啪啪啪改写了之前的代码。

```py
account = {
    "is_authenticated":False,# 用户登录了就把这个改成True
    "username":"alex", # 假装这是DB里存的用户信息
    "password":"abc123" # 假装这是DB里存的用户信息
}
def login(func):
    if account["is_authenticated"] is False:
        username = input("user:")
        password = input("pasword:")
        if username == account["username"] and password == account["password"]:
            print("welcome login....")
            account["is_authenticated"] = True
        else:
            print("wrong username or password!")
    if account["is_authenticated"] is True:  # 主要改了这
        func() # 认证成功了就执行传入进来的函数
def home():
    print("---首页----")
def america():
    print("----欧美专区----")
def japan():
    print("----日韩专区----")
def henan():
    print("----河南专区----")
home()
login(america) # 需要验证就调用 login，把需要验证的功能 当做一个参数传给login
login(henan)
```

你很开心，终于实现了老板的要求，不改变原功能代码的前提下，给功能加上了验证，此时，媳妇回来了，后面还跟着老王，你两家关系 非常 好，老王经常来串门，老王也是码农，你跟他分享了你写的代码，兴奋的等他看完 夸奖你NB,没成想，老王看后，并没有夸你，抱起你的儿子，笑笑说，你这个代码还是改改吧， 要不然会被开除的，WHAT? 会开除，明明实现了功能 呀， 老王讲，没错，你功能 是实现了，但是你又犯了一个大忌，什么大忌？ 你改变了调用方式呀， 想一想，现在没每个需要认证的模块，都必须调用你的login\(\)方法，并把自己的函数名传给你，人家之前可不是这么调用 的， 试想，如果 有100个模块需要认证，那这100个模块都得更改调用方式，这么多模块肯定不止是一个人写的，让每个人再去修改调用方式 才能加上认证，你会被骂死的。。。。 你觉得老王说的对，但问题是，如何即不改变原功能代码，又不改变原有调用方式，还能加上认证呢？ 你苦思了一会，还是想不出，老王在逗你的儿子玩，你说，老王呀，快给我点思路 ，实在想不出来，老王背对着你问，

老王：学过匿名函数没有？

你：学过学过，就是lambda嘛

老王：那lambda与正常函数的区别是什么？

你：最直接的区别是，正常函数定义时需要写名字，但lambda不需要

老王：没错，那lambda定好后，为了多次调用 ，可否也给它命个名？

你：可以呀，可以写成plus = lambda x:x+1类似这样，以后再调用plus就可以了，但这样不就失去了lambda的意义了，明明人家叫匿名函数呀，你起了名字有什么用呢？

老王：我不是要跟你讨论它的意义 ，我想通过这个让你明白一个事实

老王边说着，边拿起你儿子的画板，在上面写了以下代码：

```py
def plus(n):
    return n+1
plus2 = lambda x:x+1
```

老王： 上面这两种写法是不是代表 同样的意思？

你：是的

老王：我给lambda x:x+1 起了个名字叫plus2，是不是相当于def plus2\(x\) ?

你：我擦，你别说，还真是，但老王呀，你想说明什么呢？

老王： 没啥，只想告诉你，给函数赋值变量名就像def func\_name　是一样的效果，如下面的plus\(n\)函数，你调用时可以用plus名，还可以再起个其它名字，如

```py
calc = plus
calc(n)
```

你明白我想传达什么意思了么？ 你：。。。。。。。。。。。这。。。。。。嗯 。。。。。不太。。。。明白 。。

老王：。。。。这。。。。。呵呵。。。。。。好吧。。。。，那我在给你点一下，你之前写的下面这段调用 认证的代码

```py
home()
login(america) #需要验证就调用 login，把需要验证的功能 当做一个参数传给login
# home()
# america()
login(henan)
```

老王：你之所以改变了调用方式，是因为用户每次调用时需要执行login\(henan\)，类似的。其实稍一改就可以了呀

```py
home()
america = login(america)
henan = login(henan)
```

老王：这样以后其它人调用henan时，其实相当于调用了login\(henan\), 通过login里的验证后，就会自动调用henan功能。

你：我擦，还真是唉。。。，老王，还是你nb。。。不过，等等， 我这样写了好，那用户调用时，应该是下面这个样子

```py
home()
america = login(america) #你在这里相当于把america这个函数替换了
henan = login(henan)
#那用户调用时依然写
america()
```

但问题在于，还不等用户调用 ，你的america = login\(america\)就会先自己把america执行了呀。。。。，你应该等我用户调用 的时候 再执行才对呀，不信我试给你看。。。

老王：哈哈，你说的没错，这样搞会出现这个问题，但你想想有没有解决办法 呢？

你：我擦，你指的思路呀，大哥。。。我哪知道下一步怎么走。。。

老王：算了，估计你也想不出来。。。 学过嵌套函数没有？

你：yes,然后呢？

老王：想实现一开始你写的america = login\(america\)不触发你真正的america函数的执行，只需要在这个login里面再定义一层函数，第一次调用america = login\(america\)只调用到外层login，这个login虽然会执行，但不会触发认证了，因为认证的所有代码被封装在login里层的新定义 的函数里了，login只返回 里层函数的函数名，这样下次再执行america\(\)时， 就会调用里层函数啦。。。

你：。。。。。。什么？ 什么个意思，我蒙逼了。。。

老王：还是给你看代码吧。。

```py
account = {
    "is_authenticated":False,# 用户登录了就把这个改成True
    "username":"alex", # 假装这是DB里存的用户信息
    "password":"abc123" # 假装这是DB里存的用户信息
}
def login(func):
    def inner(): # 再定义一层函数
        if account["is_authenticated"] is False:
            username = input("user:")
            password = input("pasword:")
            if username == account["username"] and password == account["password"]:
                print("welcome login....")
                account["is_authenticated"] = True
            else:
                print("wrong username or password!")
        if account["is_authenticated"] is True:
            func()
    return inner  # 注意这里只返回inner的内存地址，不执行
def home():
    print("---首页----")
def america():
    print("----欧美专区----")
def japan():
    print("----日韩专区----")
def henan():
    print("----河南专区----")
home()
america = login(america) # 这次执行login返回的是inner的内存地址 .inner at 0x101762840>
henan = login(henan)  # .inner at 0x102562840>
america()  # 相当于执行inner()
henan()

```

此时你仔细着了老王写的代码　，感觉老王真不是一般人呀，连这种奇淫巧技都能想出来。。。，心中默默感谢上天赐你一个大牛邻居。

你: 老王呀，你这个姿势很nb呀，你独创的？ 此时你媳妇噗嗤的笑出声来，你也不知道 她笑个球。。。

老王：呵呵， 这不是我独创的呀当然 ，这是开发中一个常用的玩法，叫语法糖，官方名称“装饰器”，其实上面的写法，还可以更简单 可以把下面代码去掉

```py
america = login(america) # 这次执行login返回的是inner的内存地址
henan = login(henan)  # .inner at 0x102562840>
```

只在你要装饰的函数上面加上下面代码

```py
@login
def america():
    print("----欧美专区----")
def japan():
    print("----日韩专区----")
@login
def henan():
    print("----河南专区----")
```

效果是一样的。

你开心的玩着老王教你的新姿势 ，玩着玩着就手贱给你的“河南专区”版块 加了个参数，然后，结果 出错了。。

![](https://book.apeland.cn/media/images/2019/03/21/image_el9ASyG.png)

你：老王，老王，怎么传个参数就不行了呢？

老王：那必然呀，你调用henan时，其实是相当于调用的login，你的henan第一次调用时henan = login\(henan\)， login就返回了inner的内存地址，第2次用户自己调用henan\(5\),实际上相当于调用的是inner,但你的inner定义时并没有设置参数，但你给他传了个参数，所以自然就报错了呀

你：但是我的 版块需要传参数呀，你不让我传不行呀。。。

老王：没说不让你传，稍做改动便可。。

![](https://book.apeland.cn/media/images/2019/03/21/image_LkpLnXE.png)

老王：你再试试就好了 。

你： 果然好使，大神就是大神呀。 。。 不过，如果有多个参数呢？

老王：。。。。老弟，你不要什么都让我教你吧，非固定参数你没学过么？_args,\*_kwargs…

你：噢 。。。还能这么搞?,nb,我再试试。 你身陷这种新玩法中无法自拔，竟没注意到老王已经离开，你媳妇告诉你说为了不打扰你加班，今晚带孩子去跟她姐妹住 ，你觉得媳妇真体贴，最终，你终于搞定了所有需求，完全遵循开放-封闭原则，最终代码如下。

```py
account = {
    "is_authenticated":False,# 用户登录了就把这个改成True
    "username":"alex", # 假装这是DB里存的用户信息
    "password":"abc123" # 假装这是DB里存的用户信息
}
def login(func):
    def inner(*args,**kwargs): # 再定义一层函数
        if account["is_authenticated"] is False:
            username = input("user:")
            password = input("pasword:")
            if username == account["username"] and password == account["password"]:
                print("welcome login....")
                account["is_authenticated"] = True
            else:
                print("wrong username or password!")
        if account["is_authenticated"] is True:
            func(*args,**kwargs)
    return inner  # 注意这里只返回inner的内存地址，不执行
def home():
    print("---首页----")
@login
def america():
    print("----欧美专区----")
def japan():
    print("----日韩专区----")
@login
def henan(vip_level):
    if vip_level < 3:
        print("----河南专区普通会员----")
    else:
        print("欢迎来到尊贵河南口音RMB玩家私密社区".center(50,"-"))
        print("再充值500就可以获取演员微信号，幸福大门即将开启".center(50," "))
# home()
# america = login(america) # 这次执行login返回的是inner的内存地址 .inner at 0x101762840>
# henan = login(henan)  # .inner at 0x102562840>
america()  # 相当于执行inner()
henan(5)
```

此时，你已累的不行了，洗洗就抓紧睡了，半夜，上厕所，隐隐听到隔壁老王家有微弱的女人的声音传来，你会心一笑，老王这家伙，不声不响找了女朋友也不带给我看看，改天一定要见下真人。。。。。你本想着给媳妇打个电话问问她到了闺蜜家没有，想着想着竟然睡着了。。。

翌日，你精神抖擞到了公司，把代码扔给leader, leader看完后，会心一笑，小伙子不错，这才是专业的写法嘛。

