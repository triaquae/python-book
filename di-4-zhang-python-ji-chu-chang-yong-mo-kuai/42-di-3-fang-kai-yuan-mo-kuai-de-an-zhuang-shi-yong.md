[https://pypi.python.org/pypi](https://pypi.python.org/pypi)是python的开源模块库，截止2019年4.30日 ，已经收录了**175870**个来自全世界python开发者贡献的模块,几乎涵盖了你想用python做的任何事情。 事实上每个python开发者，只要注册一个账号就可以往这个平台上传你自己的模块，这样全世界的开发者都可以容易的下载并使用你的模块。

![](https://book.apeland.cn/media/images/2019/04/05/pypi.png)![](https://book.apeland.cn/media/images/2019/04/05/image_GL8rU7l.png)

### 那如何从这个平台上下载代码呢？

1.直接在上面这个页面上点download,下载后，解压并进入目录，执行以下命令完成安装

```py
编译源码    python setup.py build
安装源码    python setup.py install
```

1. 直接通过pip安装


   ```py
   pip3 install paramiko #paramiko 是模块名
   ```

   pip命令会自动下载模块包并完成安装。

   软件一般会被自动安装你python安装目录的这个子目录里

   ```py
   /your_python_install_path/3.6/lib/python3.6/site-packages
   ```

   pip命令默认会连接在国外的python官方服务器下载，速度比较慢，你还可以使用国内的豆瓣源，数据会定期同步国外官网，速度快好多

   ```py
   pip install -i http://pypi.douban.com/simple/ alex_sayhi --trusted-host pypi.douban.com   #alex_sayhi是模块名
   ```

   -i 后面跟的是豆瓣源地址

   —trusted-host 得加上，是通过网站https安全验证用的

   ### 使用

   下载后，直接导入使用就可以，跟自带的模块调用方法无差，演示一个连接linux服务器并执行命令的模块

   ```py
   import paramiko
   ssh = paramiko.SSHClient()
   ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
   ssh.connect('192.168.1.108', 22, 'alex', '123')
   stdin, stdout, stderr = ssh.exec_command('df')
   print(stdout.read())
   ssh.close();
   执行命令 - 通过用户名和密码连接服务器
   ```



