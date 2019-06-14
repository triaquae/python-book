编码转换是指将一种编码转成另外一种编码，比如 utf-8 to gbk。

为何需要编码转换呢？ 因为不同操作系统编码不同， utf-8在win上没办法直接看，因为windows是GBK编码的，得转成gbk。 反过来如果你的GBK字符相在Linux\Mac上正常显示，就得转成utf-8编码。

## 编码&解码

![](https://book.apeland.cn/media/images/2019/03/20/image_cvOlafM.png)

```py
>>> s.encode("utf-8")   # 编码
b'\xe5\xb0\x8f\xe7\x8c\xbf\xe5\x9c\x88'
>>> s_utf8=s.encode("utf-8")
>>> 
>>> s_utf8.decode("utf-8")  #解码
'小猿圈'
```

在py3里，内存里的字符串是以unicode编码的，unicode的其中一个特性就是跟

所有语言编码都有映射关系。所以你的utf-8格式的文件，在windows电脑上若是不能看，就可以把utf-8先解码成unicode,再由unicode编码成gbk就可以了。

![](https://book.apeland.cn/media/images/2019/03/20/image_sQIWfCp.png)

注意，不管在Windows or Mac or Linux上，你的pycharm IDE都可以支持各种文件编码，所以即使是utf-8的文件，在windows下的pycharm里也可以正常显示

![](https://book.apeland.cn/media/images/2019/03/20/image_PNqKBRf.png)

