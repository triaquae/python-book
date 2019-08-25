## 1 系统首页

### 1.1 系统首页的页面设计

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="/static/blog/bs/css/bootstrap.css">
    <script src="/static/js/jquery-3.2.1.min.js"></script>
    <script src="/static/blog/bs/js/bootstrap.min.js"></script>

    <style>
        #user_icon {
            font-size: 18px;
            margin-right: 10px;
            vertical-align: -3px;
        }

        .pub_info{
            margin-top: 10px;
        }

        .pub_info .glyphicon-comment{
            vertical-align: -1px;
        }
    </style>
</head>
<body>

<nav class="tab navbar navbar-default">
    <div class="container-fluid">
        <!-- Brand and toggle get grouped for better mobile display -->
        <div class="navbar-header">
            <button type="button" class="navbar-toggle collapsed" data-toggle="collapse"
                    data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
                <span class="sr-only">Toggle navigation</span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
            </button>
            <a class="navbar-brand" href="#">博客园</a>
        </div>

        <!-- Collect the nav links, forms, and other content for toggling -->
        <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
            <ul class="nav navbar-nav">
                <li class="active"><a href="#">随笔 <span class="sr-only">(current)</span></a></li>
                <li><a href="#">新闻</a></li>
                <li><a href="#">博文</a></li>

            </ul>

            <ul class="nav navbar-nav navbar-right">

                {% if request.user.is_authenticated %}
                    <li><a href="#"><span id="user_icon"
                                          class="glyphicon glyphicon-user"></span>{{ request.user.username }}</a></li>
                    <li class="dropdown">
                        <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true"
                           aria-expanded="false">Dropdown <span class="caret"></span></a>
                        <ul class="dropdown-menu">
                            <li><a href="#">修改密码</a></li>
                            <li><a href="#">修改头像</a></li>
                            <li><a href="/cn_backend/">管理</a></li>
                            <li><a href="/logout/">注销</a></li>
                            <li role="separator" class="divider"></li>
                            <li><a href="#">Separated link</a></li>
                        </ul>
                    </li>

                {% else %}
                    <li><a href="/login/">登录</a></li>
                    <li><a href="/register/">注册</a></li>
                {% endif %}


            </ul>
        </div><!-- /.navbar-collapse -->
    </div><!-- /.container-fluid -->
</nav>


<div class="container-fluid">
    <div class="row">
        <div class="col-md-3">
            <div class="panel panel-warning">
                <div class="panel-heading">Panel heading without title</div>
                <div class="panel-body">
                    Panel content
                </div>
            </div>

            <div class="panel panel-info">
                <div class="panel-heading">Panel heading without title</div>
                <div class="panel-body">
                    Panel content
                </div>
            </div>

            <div class="panel panel-danger">
                <div class="panel-heading">Panel heading without title</div>
                <div class="panel-body">
                    Panel content
                </div>
            </div>

        </div>
        <div class="col-md-6">
            <div class="article_list">
                {% for article in article_list %}
                <div class="article-item small">
                    <h5><a href="/{{ article.user.username }}/articles/{{ article.pk }}">{{ article.title }}</a></h5>
                    <div class="article-desc">
                        <span class="media-left">
                            <a href="/{{ article.user.username }}/"><img width="56" height="56" src="media/{{ article.user.avatar }}" alt=""></a>
                        </span>
                        <span class="media-right">
                            {{ article.desc }}
                        </span>
                    </div>
                    <div class="small pub_info">
                        <span><a href="/{{ article.user.username }}/">{{ article.user.username }}</a></span> &nbsp;&nbsp;&nbsp;
                        <span>发布于 &nbsp;&nbsp;{{ article.create_time|date:"Y-m-d H:i" }}</span>&nbsp;&nbsp;
                        <span class="glyphicon glyphicon-comment"></span>评论({{ article.comment_count }})&nbsp;&nbsp;
                        <span class="glyphicon glyphicon-thumbs-up"></span>点赞({{ article.up_count }})&nbsp;&nbsp;
                    </div>
                </div>
                    <hr>
                {% endfor %}

            </div>
        </div>
        <div class="col-md-3">
            <div class="panel panel-primary">
                <div class="panel-heading">Panel heading without title</div>
                <div class="panel-body">
                    Panel content
                </div>
            </div>
            <div class="panel panel-default">
                <div class="panel-heading">Panel heading without title</div>
                <div class="panel-body">
                    Panel content
                </div>
            </div>
        </div>
    </div>
</div>

</body>
</html>




```

### 1.2 基于admin组件录入数据

在blog/admin.py文件：

```
from django.contrib import admin

# Register your models here.
from blog import models

admin.site.register(models.UserInfo)
admin.site.register(models.Blog)
admin.site.register(models.Category)
admin.site.register(models.Tag)
admin.site.register(models.Article)
admin.site.register(models.ArticleUpDown)
admin.site.register(models.Article2Tag)
admin.site.register(models.Comment)
```



