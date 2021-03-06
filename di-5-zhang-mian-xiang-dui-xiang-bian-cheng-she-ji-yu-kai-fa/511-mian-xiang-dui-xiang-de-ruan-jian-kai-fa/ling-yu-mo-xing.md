## 本节重点

* 了解什么领域模型

* 掌握如何在开发中使用领域模型进行面向对象程序设计

> **本节时长需控制在15分钟内**

好了，你现在会了面向对象的各种语法了， 那请看下本章最后的作业需求，我相信你可能是蒙蔽的， 很多同学都是学会了面向对象的语法，却依然写不出面向对象的程序，原因是什么呢？原因就是因为你还没掌握一门面向对象设计利器， 你说我读书少别骗我， 什么利器？

答案就是:**领域建模**。 从领域模型开始,我们就开始了面向对象的分析和设计过程,可以说,领域模型是完成从需求分析到面向 对象设计的一座桥梁。

领域模型,顾名思义,就是需求所涉及的领域的一个建模,更通俗的讲法是业务模型。 参考百度百科\([http://baike.baidu.cn/view/757895.htm\),领域模型定义如下](http://baike.baidu.cn/view/757895.htm%29,领域模型定义如下):

从这个定义我们可以看出,领域模型有两个主要的作用:

1. **发掘重要的业务领域概念**
2. **建立业务领域概念之间的关系 **

### **领域建模三字经 **

领域模型如此重要,很多同学可能会认为领域建模很复杂,需要很高的技巧。然而事实上领域建模非常简 单,简单得有点难以让人相信,领域建模的方法概括一下就是“**找名词**”! 许多同学看到这个方法后估计都会笑出来:太假了吧,这么简单,找个初中生都会啊,那我们公司那些分 析师和设计师还有什么用哦?

分析师和设计师当然有用,后面我们会看到,即使是简单的找名词这样的操作,也涉及到分析和提炼,而 不是简单的摘取出来就可,这种情况下分析师和设计师的经验和技能就能够派上用场了。但领域模型分析 也确实相对简单,即使没有丰富的经验和高超的技巧,至少也能完成一个能用的领域模型。

虽然我们说“找名词”很简单,但一个关键的问题还没有说明:**从哪里找**? 如果你还记得领域模型是“需求到面向对象的桥梁”,那么你肯定一下子就能想到:从需求模型中找,具 体来说就是从用例中找。

归纳一下域建模的方法就是“**从用例中找名词**”。 当然,找到名词后,为了能够更加符合面向对象的要求和特点,我们还需要对这些名词进一步完善,这就 是接下来的步骤:**加属性,连关系**!

最后我们总结出领域建模的三字经方法:**找名词、加属性、连关系**。

> 以本章作业为例

#### **找名词**

who : 学员、讲师、管理员

**用例：**

1.**管理员**创建了 北京 和 上海 两个**校区**

1. 管理员 创建了 Linux  Python  Go 3个**课程 **

2. 管理员 创建了 北京校区的Python 16期， Go开发第一期，和上海校区的Linux 36期**班级**

3. 管理员 创建了 北京校区的**学员**小晴 ，并将其 分配 在了 班级  python 16期

4. 管理员 创建了**讲师**Alex , 并将其分配 给了 班级 python 16期 和全栈脱产5期

5. 讲师 Alex 创建 了一条 python 16期的**上课纪录**Day6

6. 讲师 Alex 为Day6这节课 所有的学员 批了**作业**，小晴得了A, 李磊得了C-, 严帅得了B

7. 学员小晴 在 python 16 的 day6里 提交了作业

8. 学员李磊 查看了自己所报的所有课程

9.  学员 李磊  在 查看了 自己在 py16期 的**成绩**列表 ，然后自杀了

10. 学员小晴  跟 讲师 Alex 表白了

**名词列表：**

管理员、校区、课程、班级、上课纪录、作业、成绩、讲师、学员

#### **加属性**

![](/assets/chapter5/领域模型.png)

#### **连关系 **

有了类,也有了属性,接下来自然就是找出它们的关系了。

![](/assets/chapter5/领域模型2.png)

