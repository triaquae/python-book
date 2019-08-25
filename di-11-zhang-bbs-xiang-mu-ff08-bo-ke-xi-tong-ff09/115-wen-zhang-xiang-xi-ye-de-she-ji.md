## 1 个人站点页

### 1.**1 创建路由**

```
# 个人站点的跳转
re_path('^(?P<username>\w+)/(?P<condition>tag|category|archive)/(?P<param>.*)/$', views.home_site), # home_site(reqeust,username="yuan",condition="tag",param="python")

# 个人站点url
    
re_path('^(?P<username>\w+)/$', views.home_site), # home_site(reqeust,username="yuan")# 个人站点url
```

### **2.5.2 创建视图函数**

```python
def home_site(request, username, **kwargs):
    """
    个人站点视图函数
    :param request:
    :return:
    """

    print("kwargs", kwargs)  # 区分访问是的站点页面还是站点下的跳转页面
    print("username", username)
    user = UserInfo.objects.filter(username=username).first()
    # 判断用户是否存在!
    if not user:
        return render(request, "not_found.html")

    # 查询当前站点对象

    blog = user.blog

    # 1 当前用户或者当前站点对应所有文章
    # 基于对象查询
    # article_list=user.article_set.all()
    # 基于 __


    article_list = models.Article.objects.filter(user=user)

    if kwargs:
        condition = kwargs.get("condition")
        param = kwargs.get("param")  # 2012-12

        if condition == "category":
            article_list = article_list.filter(category__title=param)
        elif condition == "tag":
            article_list = article_list.filter(tags__title=param)
        else:
            year, month = param.split("/")
            article_list = article_list.filter(create_time__year=year, create_time__month=month)

    # 每一个后的表模型.objects.values("pk").annotate(聚合函数(关联表__统计字段)).values("表模型的所有字段以及统计字段")

    # 查询每一个分类名称以及对应的文章数

    # ret=models.Category.objects.values("pk").annotate(c=Count("article__title")).values("title","c")
    # print(ret)


    # 查询当前站点的每一个分类名称以及对应的文章数

    # cate_list=models.Category.objects.filter(blog=blog).values("pk").annotate(c=Count("article__title")).values_list("title","c")
    # print(cate_list)


    # 查询当前站点的每一个标签名称以及对应的文章数

    # tag_list=models.Tag.objects.filter(blog=blog).values("pk").annotate(c=Count("article")).values_list("title","c")
    # print(tag_list)


    # 查询当前站点每一个年月的名称以及对应的文章数

    # ret=models.Article.objects.extra(select={"is_recent":"create_time > '2018-09-05'"}).values("title","is_recent")
    # print(ret)

    # 方式1:
    # date_list=models.Article.objects.filter(user=user).extra(select={"y_m_date":"date_format(create_time,'%%Y/%%m')"}).values("y_m_date").annotate(c=Count("nid")).values_list("y_m_date","c")
    # print(date_list)

    # 方式2:

    # from django.db.models.functions import TruncMonth
ret=models.Article.objects.filter(user=user).annotate(month=TruncMonth("create_time")).values("month").annotate(c=Count("nid")).values_list("month","c")
    # print("ret----->",ret)

    return render(request, "home_site.html", {"username": username, "blog": blog, "article_list": article_list,})
```

### **2.5.3 创建模板**

```html
# base.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <link rel="stylesheet" href="/static/blog/css/home_site.css">
    <link rel="stylesheet" href="/static/theme/{{ blog.theme }}">
    <link rel="stylesheet" href="/static/blog/css/article_detail.css">
    <link rel="stylesheet" href="/static/blog/bs/css/bootstrap.css">
    <script src="/static/js/jquery-3.2.1.min.js"></script>

</head>
<body>

<div class="header">
    <div class="content">
        <p class="title">
            <span>{{ blog.title }}</span>
            <a href="/cn_backend/" class="backend">管理</a>
        </p>
    </div>
</div>


<div class="container">
    <div class="row">
        <div class="col-md-3 menu">
             {% load my_tags %}
             {% get_classification_style username %}
        </div>
        <div class="col-md-9">
            {% block content %}

            {% endblock %}
        </div>
    </div>
</div>


</body>
</html>
```

```html
# home_site.html

{% extends 'base.html' %}
{% block content %}
 <div class="article_list">
                {% for article in article_list %}
                    <div class="article-item clearfix">
                        <h5><a href="/{{ article.user.username }}/articles/{{ article.pk }}">{{ article.title }}</a></h5>
                        <div class="article-desc">
                            {{ article.desc }}
                        </div>
                        <div class="small pub_info pull-right">
                            <span>发布于 &nbsp;&nbsp;{{ article.create_time|date:"Y-m-d H:i" }}</span>&nbsp;&nbsp;
                            <span class="glyphicon glyphicon-comment"></span>评论({{ article.comment_count }})&nbsp;&nbsp;
                            <span class="glyphicon glyphicon-thumbs-up"></span>点赞({{ article.up_count }})&nbsp;&nbsp;
                        </div>
                    </div>
                    <hr>
                {% endfor %}

            </div>
{% endblock %}
```



