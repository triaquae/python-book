### jQuery的选择器

我们以前在CSS中学习的选择器有：

![img](https://images2018.cnblogs.com/blog/1364810/201805/1364810-20180530164310470-821681311.png)



今天来学习一下jQuery 选择器。

jQuery选择器是jQuery强大的体现，它提供了一组方法，让我们更加方便的获取到页面中的元素。

#### jquery的基本选择器



![img](https://images2018.cnblogs.com/blog/1364810/201805/1364810-20180530164441341-1837779533.png)

![img](https://images2018.cnblogs.com/blog/1364810/201805/1364810-20180530164500967-140993085.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
    <div></div>
    <div id="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div></div>
    <script type="text/javascript" src="jquery-3.3.1.js"></script>
    <script type="text/javascript">
        //入口函数
        $(function(){
            //三种方式获取jquery对象
            var jqBox1 = $("#box");
                   var jqBox2 = $(".box");
            var jqBox3 = $('div');

            //操作标签选择器
            jqBox3.css('width', '100');
            jqBox3.css('height', 100);
            jqBox3.css('background-color', 'red');
            jqBox3.css('margin-top', 10);


            //操作类选择器(隐式迭代，不用一个一个设置)
                    jqBox2.css("background", "green");
                    jqBox2.text('哈哈哈')

                    //操作id选择器
                    jqBox1.css("background", "yellow");

        })
    </script>

</body>
</html>
```

#### 层级选择器

![img](https://images2018.cnblogs.com/blog/1364810/201805/1364810-20180530165910666-772076109.png)

![img](https://images2018.cnblogs.com/blog/1364810/201805/1364810-20180530165935681-993240948.png)

```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <script src="jquery-3.3.1.js"></script>
    <script>
        $(function () {
            //获取ul中的li设置为粉色
            //后代：儿孙重孙曾孙玄孙....
            var jqLi = $("ul li");
            jqLi.css("margin",5);
            jqLi.css("background", "pink");

            //子代：亲儿子
            var jqOtherLi = $("ul>li");
            jqOtherLi.css("background", "red");
        });
    </script>
</head>
<body>
<ul>
    <li>111</li>
    <li>222</li>
    <li>333</li>
    <ol>
        <li>aaa</li>
        <li>bbb</li>
        <li>ccc</li>
    </ol>
</ul>
</body>
</html>
```

#### 基本过滤选择器

![img](https://images2018.cnblogs.com/blog/1364810/201805/1364810-20180530170210737-2052147195.png)

![img](https://images2018.cnblogs.com/blog/1364810/201805/1364810-20180530170245617-2029917748.png)

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>基本过滤选择器</title>
    </head>
    <body>
        <ul>
            <li>哈哈哈哈，基本过滤选择器</li>
            <li>嘿嘿嘿</li>
            <li>天王盖地虎</li>
            <li>小鸡炖蘑菇</li>

        </ul>
    </body>
    <script src="jquery-3.3.1.js"></script>
    <script type="text/javascript">

        $(function(){
            //获取第一个 :first ,获取最后一个 :last

            //奇数
            $('li:odd').css('color','red');
            //偶数
            $('li:even').css('color','green');

            //选中索引值为1的元素 *
            $('li:eq(1)').css('font-size','30px');

            //大于索引值1
            $('li:gt(1)').css('font-size','50px');

            //小于索引值1
            $('li:lt(1)').css('font-size','12px');  

        })

    </script>
</html>
```

#### 属性选择器

![img](https://images2018.cnblogs.com/blog/1364810/201805/1364810-20180531183756059-1051347862.png)

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
         <div id="box">
            <h2 class="title">属性元素器</h2>
            <!--<p class="p1">我是一个段落</p>-->
            <ul>
                <li id="li1">分手应该体面</li>
                <li class="what" id="li2">分手应该体面</li>
                <li class="what">分手应该体面</li>
                <li class="heihei">分手应该体面</li>

            </ul>

            <form action="" method="post">

                <input name="username" type='text' value="1" checked="checked" />
                <input name="username1111" type='text' value="1" />
                <input name="username2222" type='text' value="1" />
                <input name="username3333" type='text' value="1" />
                <button class="btn-default">按钮1</button>
                <button class="btn-info">按钮1</button>
                <button class="btn-success">按钮1</button>
                <button class="btn-danger">按钮1</button>


            </form>
        </div>
    </body>
    <script src="jquery-3.3.1.js"></script>
    <script type="text/javascript">

        $(function(){
            //标签名[属性名] 查找所有含有id属性的该标签名的元素
            $('li[id]').css('color','red');

            //匹配给定的属性是what值得元素
            $('li[class=what]').css('font-size','30px');
            //[attr!=value] 匹配所有不含有指定的属性，或者属性不等于特定值的元素
            $('li[class!=what]').css('font-size','50px');

            //匹配给定的属性是以某些值开始的元素
            $('input[name^=username]').css('background','gray');
            //匹配给定的属性是以某些值结尾的元素
            $('input[name$=222]').css('background','greenyellow');

            //匹配给定的属性是以包含某些值的元素
            $('button[class*=btn]').css('background','red')


        })

    </script>
</html>
```

#### 筛选选择器

![img](https://images2018.cnblogs.com/blog/1364810/201805/1364810-20180530170831837-1810442619.png)

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
         <div id="box">
            <p class="p1">
                <span>我是第一个span标签</span>
                <span>我是第二个span标签</span>
                <span>我是第三个span标签</span>
            </p>
            <button>按钮</button>
        </div>
        <ul>
            <li class="list">2</li>
            <li>3</li>
            <li>4</li>
            <li>5</li>
        </ul>
    </body>
    <script src="jquery-3.3.1.js"></script>
    <script type="text/javascript">

        //获取第n个元素 数值从0开始
        $('span').eq(1).css('color','#FF0000');

        //获取第一个元素 :first :last    点语法  ：get方法 和set方法
        $('span').last().css('color','greenyellow');
        $('span').first().css('color','greenyellow');

        //查找span标签的父元素（亲的）
        $('span').parent('.p1').css({"width":'200px','height':'200px',"background":'red'});

        //选择所有的兄弟元素（不包括自己）
                  $('.list').siblings('li').css('color','red');


                //查找所有的后代元素
                   $('div').find('button').css('background','yellow');


                //不写参数代表获取所有子元素。
                   $('ul').children().css("background", "green");
                   $('ul').children("li").css("margin-top", 10);




    </script>
</html>
```

选择器介绍完毕，内容比较多，大家根据之前学习到的css选择器可以更好的使用jquery选择器的用法。

