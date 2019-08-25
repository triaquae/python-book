## 1 文章详情页

创建路由：

```
 re_path('^(?P<username>\w+)/articles/(?P<article_id>\d+)$', views.article_detail),
 # article_detail(request,username="yuan","article_id":article_id)
```

创建视图：

```
def article_detail(request, username, article_id):
    """
    文章详情页
    :param request:
    :param username:
    :param article_id:
    :return:
    """
    user = UserInfo.objects.filter(username=username).first()
    blog = user.blog
    article_obj = models.Article.objects.filter(pk=article_id).first()

    comment_list = models.Comment.objects.filter(article_id=article_id)

    return render(request, "article_detail.html", locals())
```

### 2.6.1 文章详情页的设计

```html
{% extends "base.html" %}

{% block content %}
    {% csrf_token %}
    <div class="article_info">
        <h3 class="text-center title">{{ article_obj.title }}</h3>
        <div class="cont">
            {{ article_obj.content|safe }}
        </div>
    </div>
{% endblock %}
```

### 2.6.2 详情页的inclution\_tag

因为详情页与个人站点页的模板一致，所以可以直接继承base.html，但是同样会遇到一个问题，即在个人站点视图函数中获取的数据要再写一遍传给模板才能渲染数据出来，这样就会出现代码的复用，所以这里的解决方案用的是django自带的一个inclution\_tag功能，类似于我们之前学习过的django自定义标签

在blog应用下创建templatetags文件夹，创建一个py文件，比如my\_tags.py，在该文件中自定义标签

```python
from django import template
from django.db.models import Count
from blog import models
register=template.Library()

@register.inclusion_tag("classification.html")
def get_classification_style(username):

    user = models.UserInfo.objects.filter(username=username).first()
    blog = user.blog

    cate_list=models.Category.objects.filter(blog=blog).values("pk").annotate(c=Count("article__title")).values_list("title","c")

    tag_list=models.Tag.objects.filter(blog=blog).values("pk").annotate(c=Count("article")).values_list("title","c")

    date_list=models.Article.objects.filter(user=user).extra(select={"y_m_date":"date_format(create_time,'%%Y/%%m')"}).values("y_m_date").annotate(c=Count("nid")).values_list("y_m_date","c")


    return {"blog":blog,"cate_list":cate_list,"date_list":date_list,"tag_list":tag_list}
```

```python
# classification.html文件
 <div>
    <div class="panel panel-warning">
                <div class="panel-heading">我的标签</div>
                <div class="panel-body">
                    {% for tag in tag_list %}
                        <p><a href="/{{ username }}/tag/{{ tag.0 }}">{{ tag.0 }}({{ tag.1 }})</a></p>
                    {% endfor %}

                </div>
            </div>

    <div class="panel panel-danger">
        <div class="panel-heading">随笔分类</div>
        <div class="panel-body">
            {% for cate in cate_list %}
                <p><a href="/{{ username }}/category/{{ cate.0 }}">{{ cate.0 }}({{ cate.1 }})</a></p>
            {% endfor %}
        </div>
    </div>

    <div class="panel panel-success">
        <div class="panel-heading">随笔归档</div>
        <div class="panel-body">
            {% for date in date_list %}
                <p><a href="/{{ username }}/archive/{{ date.0 }}">{{ date.0 }}({{ date.1 }})</a></p>
            {% endfor %}
        </div>
    </div>
 </div>
```

这个自定义的标签get\_classification\_style一旦在模板中被调用，首先会执行get\_classification\_style函数内的逻辑然后将返回的数据传送给模板classification.html去渲染，渲染完的结果就是这次get\_classification\_style标签调用的返回值。

### 2.6.3 django的渲染转义问题

当我们在数据库输入的文章标签字符串在渲染时出于安全的考虑，dajngo会将标签这样敏感的字符进行转义，防止xss攻击，所以这就导致我们发送给客户端的数据是转义后特殊符号，正文没有任何样式，无法阅读，为了解决这个问题，我们需要对渲染的数据进行safe过滤，无非就是告诉django我们信赖该数据，不需要转义，这样显示就不会有任何问题了。

```python
 <div class="cont">
            {{ article_obj.content|safe }}
 </div>
```

有同学会问，那xss攻击怎么办，其实很简单，我们存在数据库的数据本身就要确保它是以安全的，即数据在入库前是一定要进行筛选的。

### 2.6.4 文章点赞

#### **创建路由**

```python
# 点赞
path("digg/",views.digg),
```

#### **点赞样式的构建**

```html
{% extends "base.html" %}


{% block content %}
    {% csrf_token %}
    <div class="article_info">
        <h3 class="text-center title">{{ article_obj.title }}</h3>
        <div class="cont">
            {{ article_obj.content|safe }}
        </div>

        <div class="clearfix">
            <div id="div_digg">
                <div class="diggit action">
                    <span class="diggnum" id="digg_count">{{ article_obj.up_count }}</span>
                </div>
                <div class="buryit action">
                    <span class="burynum" id="bury_count">{{ article_obj.down_count }}</span>
                </div>
                <div class="clear"></div>
                <div class="diggword" id="digg_tips" style="color: red;"></div>
            </div>
        </div>

    </div>
{% endblock %}
```

#### **点赞按钮的事件绑定**

```html
<script>
// 点赞请求
$("#div_digg .action").click(function () {
var is_up = $(this).hasClass("diggit");


$obj = $(this).children("span");

$.ajax({
    url: "/digg/",
    type: "post",
    data: {
        "csrfmiddlewaretoken": $("[name='csrfmiddlewaretoken']").val(),
        "is_up": is_up,
        "article_id": "{{ article_obj.pk }}",
    },
    success: function (data) {
        console.log(data);

        if (data.state) {
            var val = parseInt($obj.text());
            $obj.text(val + 1);
        }
        else {
            var val = data.handled ? "您已经推荐过!" : "您已经反对过!";
            $("#digg_tips").html(val);

            setTimeout(function () {
                $("#digg_tips").html("")
            }, 1000)

        }

    }
})

})

</script>
```

#### **点赞的后端视图函数**

```python
def digg(request):
    """
    点赞功能
    :param request:
    :return:
    """
    print(request.POST)

    article_id = request.POST.get("article_id")
    is_up = json.loads(request.POST.get("is_up"))  # "true"
    # 点赞人即当前登录人
    user_id = request.user.pk
    obj = models.ArticleUpDown.objects.filter(user_id=user_id, article_id=article_id).first()

    response = {"state": True}
    if not obj:
        ard = models.ArticleUpDown.objects.create(user_id=user_id, article_id=article_id, is_up=is_up)

        queryset = models.Article.objects.filter(pk=article_id)
        if is_up:
            queryset.update(up_count=F("up_count") + 1)
        else:
            queryset.update(down_count=F("down_count") + 1)
    else:
        response["state"] = False
        response["handled"] = obj.is_up

    return JsonResponse(response)
```

### 2.6.5 文章评论

#### **创建路由**

```
# 评论
path("comment/",views.comment),
```

#### **创建评论样式**

```html
{% extends "base.html" %}


{% block content %}
    {% csrf_token %}
    <div class="article_info">
        <h3 class="text-center title">{{ article_obj.title }}</h3>
        <div class="cont">
            {{ article_obj.content|safe }}
        </div>

        <div class="clearfix">
            <div id="div_digg">
                <div class="diggit action">
                    <span class="diggnum" id="digg_count">{{ article_obj.up_count }}</span>
                </div>
                <div class="buryit action">
                    <span class="burynum" id="bury_count">{{ article_obj.down_count }}</span>
                </div>
                <div class="clear"></div>
                <div class="diggword" id="digg_tips" style="color: red;"></div>
            </div>
        </div>

        <div class="comments list-group">


          
            <p>发表评论</p>
            <p>昵称：<input type="text" id="tbCommentAuthor" class="author" disabled="disabled" size="50"
                         value="{{ request.user.username }}">
            </p>
            <p>评论内容:</p>
            <textarea name="" id="comment_content" cols="60" rows="10"></textarea>
            <p>
                <button class="btn btn-default comment_btn">提交评论</button>
            </p>
        </div>

    </div>
{% endblock %}
```

#### **绑定评论提交事件**

```html
<script>

    // 评论请求
    var pid = "";

    $(".comment_btn").click(function () {

        var content = $("#comment_content").val();

        if (pid) {
            var index = content.indexOf("\n");
            content = content.slice(index + 1)
        }


        $.ajax({
            url: "/comment/",
            type: "post",
            data: {
                "csrfmiddlewaretoken": $("[name='csrfmiddlewaretoken']").val(),
                "article_id": "{{ article_obj.pk }}",
                "content": content,
                pid: pid
            },
            success: function (data) {

                console.log(data);

                var create_time = data.create_time;
                var username = data.username;
                var content = data.content;

                var s = `
                   <li class="list-group-item">
                      <div>

                          <span>${create_time}</span>&nbsp;&nbsp;
                          <a href=""><span>${username}</span></a>

                      </div>
                      <div class="comment_con">
                          <p>${content}</p>
                      </div>

                    </li>`;

                $("ul.comment_list").append(s);

                // 清空评论框
                pid = "",
                        $("#comment_content").val("");

            }
        })


    });

    // 回复按钮事件

    $(".reply_btn").click(function () {

        $('#comment_content').focus();
        var val = "@" + $(this).attr("username") + "\n";
        $('#comment_content').val(val);


        pid = $(this).attr("comment_pk");


    })
</script>
```

#### **添加评论的视图函数**

```py
def comment(request):
    """
    提交评论视图函数
    功能:
    1 保存评论
    2 创建事务
    3 发送邮件
    :param request:
    :return:
    """
    print(request.POST)

    article_id = request.POST.get("article_id")
    pid = request.POST.get("pid")
    content = request.POST.get("content")
    user_id = request.user.pk

    article_obj = models.Article.objects.filter(pk=article_id).first()

    # 事务操作
    with transaction.atomic():
        comment_obj = models.Comment.objects.create(user_id=user_id, article_id=article_id, content=content,
                                                    parent_comment_id=pid)
        models.Article.objects.filter(pk=article_id).update(comment_count=F("comment_count") + 1)

    response = {}

    response["create_time"] = comment_obj.create_time.strftime("%Y-%m-%d %X")
    response["username"] = request.user.username
    response["content"] = content

    # 发送邮件

    from django.core.mail import send_mail
    from cnblog import settings

    # send_mail(
    #     "您的文章%s新增了一条评论内容"%article_obj.title,
    #     content,
    #     settings.EMAIL_HOST_USER,
    #     ["916852314@qq.com"]
    # )

    import threading

    t = threading.Thread(target=send_mail, args=("您的文章%s新增了一条评论内容" % article_obj.title,
                                                 content,
                                                 settings.EMAIL_HOST_USER,
                                                 ["916852314@qq.com"])
                         )
    t.start()

    return JsonResponse(response)
```

#### **显示评论**

```html
{% extends "base.html" %}


{% block content %}
    {% csrf_token %}
    <div class="article_info">
        <h3 class="text-center title">{{ article_obj.title }}</h3>
        <div class="cont">
            {{ article_obj.content|safe }}
        </div>

        <div class="clearfix">
            <div id="div_digg">
                <div class="diggit action">
                    <span class="diggnum" id="digg_count">{{ article_obj.up_count }}</span>
                </div>
                <div class="buryit action">
                    <span class="burynum" id="bury_count">{{ article_obj.down_count }}</span>
                </div>
                <div class="clear"></div>
                <div class="diggword" id="digg_tips" style="color: red;"></div>
            </div>
        </div>

        <div class="comments list-group">
            <p class="tree_btn">评论树</p>
            <div class="comment_tree">


            </div>

         

            <p>评论列表</p>

            <ul class="list-group comment_list">

                {% for comment in comment_list %}
                    <li class="list-group-item">
                        <div>
                            <a href=""># {{ forloop.counter }}楼</a> &nbsp;&nbsp;
                            <span>{{ comment.create_time|date:"Y-m-d H:i" }}</span>&nbsp;&nbsp;
                            <a href=""><span>{{ comment.user.username }}</span></a>
                            <a class="pull-right reply_btn" username="{{ comment.user.username }}"
                               comment_pk="{{ comment.pk }}">回复</a>
                        </div>

                        {% if comment.parent_comment_id %}
                            <div class="pid_info well">
                                <p>
                                    {{ comment.parent_comment.user.username }}: {{ comment.parent_comment.content }}
                                </p>
                            </div>
                        {% endif %}

                        <div class="comment_con">
                            <p>{{ comment.content }}</p>
                        </div>

                    </li>
                {% endfor %}


            </ul>

            <p>发表评论</p>
            <p>昵称：<input type="text" id="tbCommentAuthor" class="author" disabled="disabled" size="50"
                         value="{{ request.user.username }}">
            </p>
            <p>评论内容:</p>
            <textarea name="" id="comment_content" cols="60" rows="10"></textarea>
            <p>
                <button class="btn btn-default comment_btn">提交评论</button>
            </p>
        </div>

    </div>
{% endblock %}
```

#### **评论树**

```python
def get_comment_tree(request):
    article_id = request.GET.get("article_id")
    response = list(models.Comment.objects.filter(article_id=article_id).order_by("pk").values("pk", "content", "parent_comment_id"))

    return JsonResponse(response, safe=False)
```

```html
...               
<p class="tree_btn">评论树</p>
 <div class="comment_tree">

 </div>  
<script>

     $.ajax({
            url: "/get_comment_tree/",
            type: "get",
            data: {
                article_id: "{{ article_obj.pk }}"
            },
            success: function (comment_list) {
                console.log(comment_list);

                $.each(comment_list, function (index, comment_object) {

                    var pk = comment_object.pk;
                    var content = comment_object.content;
                    var parent_comment_id = comment_object.parent_comment_id;
                    var s = '<div class="comment_item" comment_id=' + pk + '><span>' + content + '</span></div>';

                    if (!parent_comment_id) {

                        $(".comment_tree").append(s);
                    } else {

                        $("[comment_id=" + parent_comment_id + "]").append(s);

                    }

                })


            }
        })

</script>
```



