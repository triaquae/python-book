## 1 后台管理

### 1.1 页面设计

创建路由映射

```
# 后台管理url
re_path("cn_backend/$",views.cn_backend),
re_path("cn_backend/add_article/$",views.add_article),
```

创建后台管理首页的视图函数

```python
@login_required
def cn_backend(request):
    """
    后台管理的首页
    :param request:
    :return:
    """
    article_list = models.Article.objects.filter(user=request.user)

    return render(request, "backend/backend.html", locals())
```

创建后台管理页面

```html
# base.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>博客后台管理 - 博客园</title>

    <link rel="stylesheet" href="/static/blog/bs/css/bootstrap.css">
    <script src="/static/js/jquery-3.2.1.min.js"></script>
    <script src="/static/blog/bs/js/bootstrap.min.js"></script>
    <link rel="stylesheet" href="/static/blog/css/backend.css">
</head>
<body>

<div class="header">
    <p class="title">
        后台管理

        <a class="info" href="/logout/">注销</a>
        <span class="info"><span class="glyphicon glyphicon-user"></span>&nbsp;&nbsp;{{ request.user.username }}</span>
    </p>
</div>


<div class="container">
    <div class="col-md-3">
        <div class="panel-group" id="accordion" role="tablist" aria-multiselectable="true">
            <div class="panel panel-default">
                <div class="panel-heading" role="tab" id="headingOne">
                    <h4 class="panel-title">
                        <a role="button" data-toggle="collapse" data-parent="#accordion" href="#collapseOne"
                           aria-expanded="true" aria-controls="collapseOne">
                            操作
                        </a>
                    </h4>
                </div>
                <div id="collapseOne" class="panel-collapse collapse in" role="tabpanel" aria-labelledby="headingOne">
                    <div class="panel-body">
                        <p><a href="/cn_backend/add_article/">添加文章</a></p>
                    </div>
                </div>
            </div>

        </div>
    </div>
    <div class="col-md-9">

        <div>

            <!-- Nav tabs -->
            <ul class="nav nav-tabs" role="tablist">
                <li role="presentation" class="active"><a href="#home" aria-controls="home" role="tab"
                                                          data-toggle="tab">文章</a></li>
                <li role="presentation"><a href="#profile" aria-controls="profile" role="tab"
                                           data-toggle="tab">日记</a></li>
                <li role="presentation"><a href="#messages" aria-controls="messages" role="tab" data-toggle="tab">眼镜</a>
                </li>
                <li role="presentation"><a href="#settings" aria-controls="settings" role="tab" data-toggle="tab">相册</a>
                </li>
            </ul>

            <!-- Tab panes -->
            <div class="tab-content">
                <div role="tabpanel" class="tab-pane active" id="home">

                    {% block content %}

                    {% endblock %}


                </div>
                <div role="tabpanel" class="tab-pane" id="profile">

                    <img src="/static/blog/img/meinv2.jpg" alt="">
                    <img src="/static/blog/img/meinv3.jpg" alt="">
                    <img class="pull-right" src="/static/blog/img/meinv.jpg" alt="">
                </div>
                <div role="tabpanel" class="tab-pane" id="messages">

                    <img width="180" height="180" src="/static/blog/img/hashiqi2.jpg" alt="">

                    <img width="180" height="180" src="/static/blog/img/dogg4.jpg" alt="">
                    <img width="180" height="180" src="/static/blog/img/linhaifeng.jpg" alt=""><br>
                    <img width="180" height="180" src="/static/blog/img/dogg3.jpeg" alt="">
                    <img width="180" height="180" src="/static/blog/img/dogge2.jpg" alt="">

                    <img width="180" height="180" src="/static/blog/img/dogg5.jpg" alt="">

                </div>
                <div role="tabpanel" class="tab-pane" id="settings">

                </div>
            </div>

        </div>

    </div>
</div>

</body>
</html>
```

```html
{% extends 'backend/base.html' %}


{% block content %}
 <div class="article_list small">

     <table class="table table-hover table-striped">
         <thead>
             <th>标题</th>
             <th>评论数</th>
             <th>点赞数</th>
             <th>操作</th>
             <th>操作</th>
         </thead>
         <tbody>
             {% for article in article_list %}
             <tr>
                 <td>{{ article.title }}</td>
                 <td>{{ article.comment_count }}</td>
                 <td>{{ article.up_count }}</td>
                 <td><a href="">编辑</a></td>
                 <td><a href="">删除</a></td>
             </tr>
             {% endfor %}

         </tbody>
     </table>
</div>
{% endblock %}
```

创建添加文章页面

```html
{% extends 'backend/base.html' %}

{% block content %}
<form action="" method="post">
    {% csrf_token %}
   <div class="add_article">
     <div class="alert-success text-center">添加文章</div>

     <div class="add_article_region">
          <div class="title form-group">
             <label for="">标题</label>
             <div>
                 <input type="text" name="title">
             </div>
         </div>

         <div class="content form-group">
             <label for="">内容(Kindeditor编辑器，不支持拖放/粘贴上传图片) </label>
             <div>
                 <textarea name="content" id="article_content" cols="30" rows="10"></textarea>
             </div>
         </div>

         <input type="submit" class="btn btn-default">

     </div>
</div>
</form>   

{% endblock %}
```

### 1.2 富文本编辑器

KindEditor 是一套开源的在线HTML编辑器，主要用于让用户在网站上获得所见即所得编辑效果，开发人员可以用 KindEditor 把传统的多行文本输入框\(textarea\)替换为可视化的富文本输入框。 KindEditor 使用 JavaScript 编写，可以无缝地与 Java、.NET、PHP、ASP 等程序集成，比较适合在 CMS、商城、论坛、博客、Wiki、电子邮件等互联网应用上使用。

为了能够更好地在后台编辑文章，我们在项目中引入富文本编辑器中的其中一款kindeditor

```html
<script src="/static/js/jquery-3.2.1.min.js"></script>
<script charset="utf-8" src="/static/blog/kindeditor/kindeditor-all.js"></script>

<script>
    KindEditor.ready(function(K) {
            window.editor = K.create('#article_content',{
                width:"800",
                height:"600",
                resizeType:0,
                uploadJson:"/upload/",
                extraFileUploadParams:{
                    csrfmiddlewaretoken:$("[name='csrfmiddlewaretoken']").val()
                },
                filePostName:"upload_img"


            });
    });
</script>
```

后端对应设置：

路由：

```python
# 文本编辑器上传图片url
path('upload/', views.upload),
```

视图：

```python
def upload(request):
    """
    编辑器上传文件接受视图函数
    :param request:
    :return:
    """

    print(request.FILES)
    img_obj=request.FILES.get("upload_img")
    print(img_obj.name)

    path=os.path.join(settings.MEDIA_ROOT,"add_article_img",img_obj.name)

    with open(path,"wb") as f:

        for line in img_obj:
            f.write(line)


    return HttpResponse("ok")
```

### 1.3 添加文章的逻辑实现

```python
from bs4 import BeautifulSoup


@login_required
def add_article(request):
    """
    后台管理的添加书籍视图函数
    :param request:
    :return:
    """
    if request.method == "POST":
        title = request.POST.get("title")
        content = request.POST.get("content")

        # 防止xss攻击,过滤script标签
        soup=BeautifulSoup(content,"html.parser")
        for tag in soup.find_all():

            print(tag.name)
            if tag.name=="script":
                tag.decompose()

        # 构建摘要数据,获取标签字符串的文本前150个符号

        desc=soup.text[0:150]+"..."

        models.Article.objects.create(title=title,desc=desc,content=str(soup), user=request.user)
        return redirect("/cn_backend/")

    return render(request, "backend/add_article.html")
```



