## 1 登陆功能

基于用户认证组件与Ajax实现登录功能,首先创建路由映射表：

```
 path('login/', views.login),
```

然后创建视图:

```
def login(request):

    return render(request,"blog/login.html")
```

再实现具体逻辑前先将静态文件配置好,再static文件夹下创建一个blog的文件夹，将与blog功能相关的静态文件放在这个包下，实现一定的解耦，另外需要配置信息：

```
STATIC_URL = '/static/'

STATICFILES_DIRS=[
    os.path.join(BASE_DIR,"static"),
]
```

接下来就是完成templates文件夹下的login.html页面的设计了

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="/static/blog/bs/css/bootstrap.css">

</head>
<body>
<h3>登录页面</h3>
<div class="container">
    <div class="row">
        <div class="col-md-6 col-lg-offset-3">

            <form>
                {% csrf_token %}
                <div class="form-group">
                    <label for="user">用户名</label>
                    <input type="text" id="user" class="form-control">
                </div>
                <div class="form-group">
                    <label for="pwd">密码</label>
                    <input type="password" id="pwd" class="form-control">
                </div>


                <div class="form-group">
                    <label for="pwd">验证码</label>
                    <div class="row">
                        <div class="col-md-6">
                            <input type="text" class="form-control" id="valid_code">
                        </div>
                        <div class="col-md-6">
                            <img width="270" height="36" id="valid_code_img" src="/get_validCode_img/" alt="">
                        </div>
                    </div>
                </div>


                <input type="button" class="btn btn-default login_btn" value="submit"><span class="error"></span>
                <a href="/register/" class="btn btn-success pull-right">注册</a>
            </form>

        </div>
    </div>
</div>

    <script src="/static/js/jquery-3.2.1.min.js"></script>
<script>

    // 刷新验证码
    $("#valid_code_img").click(function () {

        $(this)[0].src += "?"

    });

    // 登录验证
    $(".login_btn").click(function () {

        $.ajax({
            url: "",
            type: "post",
            data: {
                user: $("#user").val(),
                pwd: $("#pwd").val(),
                valid_code: $("#valid_code").val(),
                csrfmiddlewaretoken: $("[name='csrfmiddlewaretoken']").val(),
            },
            success: function (data) {
                console.log(data);

                if (data.user) {
                    if (location.search){
                        location.href = location.search.slice(6)
                    }
                    else {
                         location.href = "/index/"
                    }

                }
                else {
                    $(".error").text(data.msg).css({"color": "red", "margin-left": "10px"});
                    setTimeout(function(){
                         $(".error").text("");
                    },1000)

                }
            }
        })

    })

</script>

</body>
</html>
```

涉及到动态验证码的获取，视图函数如下：

```python
from blog.utils import validCode
def get_valid_code_img(request):
    """
    基于PIL模块动态生成响应状态码图片
    :param request:
    :return:
    """
    img_data = validCode.get_valid_code_img(request)

    return HttpResponse(img_data)

# blog.utils


import random

def get_random_color():
        return (random.randint(0, 255), random.randint(0, 255), random.randint(0, 255))


def get_valid_code_img(request):

    # 方式1:
    # with open("lufei.jpg","rb") as f:
    #     data=f.read()

    # 方式2: # pip install pillow

    # from PIL import Image
    # img=Image.new("RGB",(270,40),color=get_random_color())
    #
    # with open("validCode.png","wb") as f:
    #     img.save(f,"png")
    #
    # with open("validCode.png","rb") as f:
    #     data=f.read()


    # 方式3:

    # from PIL import Image
    # from io import BytesIO
    #
    # img=Image.new("RGB",(270,40),color=get_random_color())
    # f=BytesIO()
    # img.save(f,"png")
    # data=f.getvalue()

    # 方式4:

    from PIL import Image, ImageDraw, ImageFont
    from io import BytesIO
    import random

    img = Image.new("RGB", (270, 40), color=get_random_color())

    draw = ImageDraw.Draw(img)
    kumo_font = ImageFont.truetype("static/font/kumo.ttf", size=32)

    valid_code_str = ""
    for i in range(5):
        random_num = str(random.randint(0, 9))
        random_low_alpha = chr(random.randint(95, 122))
        random_upper_alpha = chr(random.randint(65, 90))
        random_char = random.choice([random_num, random_low_alpha, random_upper_alpha])
        draw.text((i * 50 + 20, 5), random_char, get_random_color(), font=kumo_font)

        # 保存验证码字符串
        valid_code_str += random_char

    # width=270
    # height=40
    # for i in range(10):
    #     x1=random.randint(0,width)
    #     x2=random.randint(0,width)
    #     y1=random.randint(0,height)
    #     y2=random.randint(0,height)
    #     draw.line((x1,y1,x2,y2),fill=get_random_color())
    #
    # for i in range(100):
    #     draw.point([random.randint(0, width), random.randint(0, height)], fill=get_random_color())
    #     x = random.randint(0, width)
    #     y = random.randint(0, height)
    #     draw.arc((x, y, x + 4, y + 4), 0, 90, fill=get_random_color())

    print("valid_code_str", valid_code_str)

    request.session["valid_code_str"] = valid_code_str

    '''
    1 sdajsdq33asdasd
    2 COOKIE {"sessionid":sdajsdq33asdasd}
    3 django-session
      session-key       session-data
      sdajsdq33asdasd   {"valid_code_str":"12345"}


    '''

    f = BytesIO()
    img.save(f, "png")
    data = f.getvalue()


    return data
```

当浏览器加载 &lt;img src="/get\_validCode\_img/" alt=""&gt;标签时即向服务器相应视图函数获取动态验证码。

最后完成视图函数的逻辑：

```python
def login(request):
    """
    登录视图函数:
       get请求响应页面
       post(Ajax)请求响应字典
    :param request:
    :return:
    """

    if request.method == "POST":

        response = {"user": None, "msg": None}
        user = request.POST.get("user")
        pwd = request.POST.get("pwd")
        valid_code = request.POST.get("valid_code")

        valid_code_str = request.session.get("valid_code_str")
        if valid_code.upper() == valid_code_str.upper():
            user = auth.authenticate(username=user, password=pwd)
            if user:
                auth.login(request, user)  # request.user== 当前登录对象
                response["user"] = user.username
            else:
                response["msg"] = "用户名或者密码错误!"

        else:
            response["msg"] = "验证码错误!"

        return JsonResponse(response)

    return render(request, "login.html")
```

## 2 注册功能

**基于forms组件和Ajax实现注册功能**

### 2.1 基于forms组件设计注册页面

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="/static/blog/bs/css/bootstrap.css">
    <script src="/static/js/jquery-3.2.1.min.js"></script>
    <style>
        #avatar_img {
            margin-left: 20px;
        }

        #avatar {
            display: none;
        }

        .error {
            color: red;
        }
    </style>

</head>
<body>
<h3>注册页面</h3>
<div class="container">
    <div class="row">
        <div class="col-md-6 col-lg-offset-3">

            <form id="form">
                {% csrf_token %}

                {% for field in form %}
                    <div class="form-group">
                        <label for="{{ field.auto_id }}">{{ field.label }}</label>
                        {{ field }} <span class="error pull-right"></span>
                    </div>
                {% endfor %}

                <div class="form-group">
                    <label for="avatar">
                        头像
                        <img id="avatar_img" width="60" height="60" src="/static/blog/img/default.png" alt="">
                    </label>
                    <input type="file" id="avatar" name="avatar">
                </div>

                <input type="button" class="btn btn-default reg_btn" value="submit"><span class="error"></span>

            </form>

        </div>
    </div>
</div>


</body>
</html>
```

### 2.2 头像的预览

```html
<script>
    // 头像预览
    $("#avatar").change(function () {

        // 获取用户选中的文件对象
        var file_obj = $(this)[0].files[0];
        // 获取文件对象的路径
        var reader = new FileReader();
        reader.readAsDataURL(file_obj);
        // 修改img的src属性 ，src=文件对象的路径
        reader.onload = function () {
            $("#avatar_img").attr("src", reader.result)
        };

    });
</script>
```

### 2.3 ajax提交注册信息

```html
<script>
    // 基于Ajax提交数据

    $(".reg_btn").click(function () {
        //console.log($("#form").serializeArray());
        var formdata = new FormData();
        var request_data = $("#form").serializeArray();
        $.each(request_data, function (index, data) {
            formdata.append(data.name, data.value)
        });

        formdata.append("avatar", $("#avatar")[0].files[0]);

        $.ajax({
            url: "",
            type: "post",
            contentType: false,
            processData: false,
            data: formdata,
            success: function (data) {
                //console.log(data);
                if (data.user) {
                    // 注册成功
                    location.href="/login/"
                }
                else { // 注册失败
                    //console.log(data.msg)
                    // 清空错误信息
                    $("span.error").html("");
                    $(".form-group").removeClass("has-error");

                    // 展此次提交的错误信息!
                    $.each(data.msg, function (field, error_list) {
                        console.log(field, error_list);
                        if (field=="__all__"){
                            $("#id_re_pwd").next().html(error_list[0]).parent().addClass("has-error");
                        }
                        $("#id_" + field).next().html(error_list[0]);
                        $("#id_" + field).parent().addClass("has-error");
                    })
                }
            }
        })
    })

</script>
```

### 2.4 FileField，ImageFiled与Media配置

**FileField与ImageFiled**

```python
# 表模型
class UserInfo(AbstractUser):

      avatar = models.FileField(upload_to='avatars/', default="/avatars/default.png")

# 添加数据        
avatar_obj=request.FILES.get("avatar")
user_obj=UserInfo.objects.create_user(username=user,password=pwd,email=email,avatar=avatar_obj)

# 注解：
  Dajngo实现：
    会将文件对象下载到项目的根目录中avatars文件夹中（如果没有avatar文件夹，Django会自动建）,user_obj的avatar存的是文件的相对路径。
```

**meida配置**

```python
Media 配置之MEDIA_ROOT：

Dajngo有两种静态文件：

     ／static／    ：  js，css，img
     ／media/      :   用户上传文件

一旦配置了
        MEDIA_ROOT=os.path.join(BASE_DIR,"media")

    Dajngo实现：

      会将文件对象下载到MEDIA_ROOT中avatars文件夹中（如果没有avatar文件夹，Django会自动创建）,user_obj的avatar存的是文件的相对路径。
Media 配置之MEDIA_URl：

浏览器如何能直接访问到media中的数据


   settings.py:
      MEDIA_URL="/media/"

   urls.pt:
      # media配置:
      re_path(r"media/(?P<path>.*)$",serve,{"document_root":settings.MEDIA_ROOT})
```

### 2.5 注册功能的视图逻辑

创建路由：

```
path('register/', views.register)
```

创建视图函数：

```python
from django import forms

from django.forms import widgets

from blog.models import UserInfo
from django.core.exceptions import NON_FIELD_ERRORS, ValidationError

# 用户相关的form表单
class UserForm(forms.Form):

    user=forms.CharField(max_length=32,
                         error_messages={"required":"该字段不能为空"},
                         label="用户名",
                         widget=widgets.TextInput(attrs={"class":"form-control"},)
                         )
    pwd=forms.CharField(max_length=32,
                         label="密码",
                         widget=widgets.PasswordInput(attrs={"class":"form-control"},)
                        )
    re_pwd=forms.CharField(max_length=32,
                            label="确认密码",
                            widget=widgets.PasswordInput(attrs={"class":"form-control"},)
                           )
    email=forms.EmailField(max_length=32,
                            label="邮箱",
                            widget=widgets.EmailInput(attrs={"class":"form-control"},)
                            )


    def clean_user(self):
        val=self.cleaned_data.get("user")

        user=UserInfo.objects.filter(username=val).first()
        if not user:
            return val
        else:
            raise ValidationError("该用户已注册!")


    def clean(self):
        pwd=self.cleaned_data.get("pwd")
        re_pwd=self.cleaned_data.get("re_pwd")

        if pwd and re_pwd:
            if pwd==re_pwd:
                return self.cleaned_data
            else:
                raise ValidationError("两次密码不一致!")
        else:
            return self.cleaned_data


# 注册功能的视图函数        
def register(request):
    """
    注册视图函数:
       get请求响应注册页面
       post(Ajax)请求,校验字段,响应字典
    :param request:
    :return:
    """

    if request.is_ajax():
        print(request.POST)
        form = UserForm(request.POST)

        response = {"user": None, "msg": None}
        if form.is_valid():
            response["user"] = form.cleaned_data.get("user")

            # 生成一条用户纪录
            user = form.cleaned_data.get("user")
            print("user", user)
            pwd = form.cleaned_data.get("pwd")
            email = form.cleaned_data.get("email")
            avatar_obj = request.FILES.get("avatar")

            extra = {}
            if avatar_obj:
                extra["avatar"] = avatar_obj

            UserInfo.objects.create_user(username=user, password=pwd, email=email, **extra)

        else:
            print(form.cleaned_data)
            print(form.errors)
            response["msg"] = form.errors

        return JsonResponse(response)

    form = UserForm()
    return render(request, "register.html", {"form": form})
```



