## 业务实现

## 2.1 创建项目

通过命令来创建一个django项目

```
dajngo-admin startproject cnblog
```

当然，也可以借助pycharmIDE来快速创建一个项目。

数据库因为选择mysql，所以需要重新配置一下settings文件：

```python
创建django默认使用的是sqlite3
# DATABASES = {
#     'default': {
#         'ENGINE': 'django.db.backends.sqlite3',
#         'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
#     }
# }

# 配置mysql数据库连接参数
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME':'cnblog', # 要连接的数据库，连接前需要创建好
        'USER':'root',# 连接数据库的用户名
        'PASSWORD':'',# 连接数据库的密码
        'HOST':'127.0.0.1', # 连接主机，默认本级
        'PORT':3306 #  端口 默认3306
    }
}
```

接下里将我们设计好的模型表写入到项目的models文件中，然后数据库迁移

```python
python3 manage.py makemigrations
python3 manage.py migrate
```

这时项目可能会报一个错误：![](/assets/QQ截图20190813100148.png)这是因为我们的模型表中UserInfo表继承了原生用户表，即后面以Userinfo表作为默认的用户表，但必须在配置文件中告诉django，所有需要添加配置：

```
AUTH_USER_MODEL = "blog.UserInfo"
```

其中，blog是userinfo所在app的名称。

然后再重新数据库迁移即可。

