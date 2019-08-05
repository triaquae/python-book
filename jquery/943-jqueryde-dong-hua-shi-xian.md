### jQuery动画

jQuery提供的一组网页中常见的动画效果，这些动画是标准的、有规律的效果；同时还提供给我们了自定义动画的功能。

#### 显示动画

方式一：

```
  $("div").show();
```

解释：无参数，表示让指定的元素直接显示出来。其实这个方法的底层就是通过`display: block;`实现的。

方式二：

```
$('div').show(3000);
```

解释：通过控制元素的宽高、透明度、display属性，逐渐显示，2秒后显示完毕。

方式三：

```
 $("div").show("slow");
```

参数可以是：

- slow 慢：600ms
- normal 正常：400ms
- fast 快：200ms

解释：和方式二类似，也是通过控制元素的宽高、透明度、display属性，逐渐显示。

方式四：

```
 //show(毫秒值，回调函数;
    $("div").show(5000,function () {
        alert("动画执行完毕！");
    });
```

解释：动画执行完后，立即执行回调函数。

**总结：**

上面的四种方式几乎一致：参数可以有两个，第一个是动画的执行时长，第二个是动画结束后执行的回调函数。

#### 隐藏动画

方式参照上面的show()方法的方式。如下：


```
    $(selector).hide();

    $(selector).hide(1000); 

    $(selector).hide("slow");

    $(selector).hide(1000, function(){});
```



###### **实现点击按钮显示盒子，再点击按钮隐藏盒子**

**代码如下：**



```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
        <style type="text/css">
            #box{
                width: 200px;
                height: 200px;
                background-color: green;
                border: 1px solid red;
                display: none;
            }
        </style>
    </head>
    <body>
        <div id="box">        
        </div>
        <button id="btn">隐藏</button>    
    </body>
    <script src="jquery-3.3.1.js"></script>
    
    <script type="text/javascript">
        
        //jquery 提供了一些方法 show() hide() 控制元素显示隐藏
        var isShow = true;
        $('#btn').click(function(){
            if(isShow){
                $('#box').show('slow',function(){
                    $(this).text('盒子出来了');            
                    $('#btn').text('显示');
                    isShow = false;
                })
            }else{
                $('#box').hide(2000,function(){
                    $(this).text('');    
                    $('#btn').text('隐藏');
                    isShow = true;
                    
                })
            }
        })
    
        
    </script>
</html>
```


 

#### **开关式显示隐藏动画**

```
$('#box').toggle(3000,function(){});
```

显示和隐藏的来回切换采用的是toggle()方法：就是先执行show()，再执行hide()。

代码如下：



```javascript
    $('#btn').click(function(){
            $('#box').toggle(3000,function(){
                $(this).text('盒子出来了');    
                if ($('#btn').text()=='隐藏') {
                    $('#btn').text('显示');    
                }else{
                    $('#btn').text('隐藏');    
                }
            });
     })
```


#### 滑入和滑出

**1、滑入动画效果**：（类似于生活中的卷帘门）

```
$(selector).slideDown(speed, 回调函数);
```

解释：下拉动画，显示元素。

注意：省略参数或者传入不合法的字符串，那么则使用默认值：400毫秒（同样适用于fadeIn/slideDown/slideUp）

**2、滑出动画效果：** 

```
 $(selector).slideUp(speed, 回调函数);
```

解释：上拉动画，隐藏元素。

**3、滑入滑出切换动画效果：**

```
 $(selector).slideToggle(speed, 回调函数);
```

代码如下：



```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        div {
            width: 300px;
            height: 300px;
            display: none;
            background-color: green;
        }
    </style>

    <script src="jquery-3.3.1.js"></script>
    <script>
        $(function () {
            //点击按钮后产生动画
            $("button:eq(0)").click(function () {

                //滑入动画： slideDown(毫秒值，回调函数[显示完毕执行什么]);
                $("div").slideDown(2000, function () {
                    alert("动画执行完毕！");
                });
            })

            //滑出动画
            $("button:eq(1)").click(function () {

                //滑出动画：slideUp(毫秒值，回调函数[显示完毕后执行什么]);
                $("div").slideUp(2000, function () {
                    alert("动画执行完毕！");
                });
            })

            $("button:eq(2)").click(function () {
                //滑入滑出切换（同样有四种用法）
                $("div").slideToggle(1000);
            })

        })
    </script>
</head>
<body>
<button>滑入</button>
<button>滑出</button>
<button>切换</button>
<div></div>

</body>
</html>
```

#### 淡入淡出动画

1、淡入动画效果：

```
 $(selector).fadeIn(speed, callback);

```

作用：让元素以淡淡的进入视线的方式展示出来。

 

2、淡出动画效果：

```
$(selector).fadeOut(1000);

```

作用：让元素以渐渐消失的方式隐藏起来

 

3、淡入淡出切换动画效果：

```
 $(selector).fadeToggle('fast', callback);

```

作用：通过改变透明度，切换匹配元素的显示或隐藏状态。

参数的含义同show()方法。



```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        div {
            width: 300px;
            height: 300px;
            display: none;
            /*透明度*/
            opacity: 0.5;
            background-color: red;
        }
    </style>

    <script src="jquery-3.3.1.js"></script>
    <script>
        $(function () {
            //点击按钮后产生动画
            $("button:eq(0)").click(function () {
//                //淡入动画用法1:   fadeIn();   不加参数
                $("div").fadeIn();

//                //淡入动画用法2:   fadeIn(2000);   毫秒值
//                $("div").fadeIn(2000);
//                //通过控制  透明度和display

                //淡入动画用法3:   fadeIn(字符串);   slow慢：600ms   normal正常:400ms   fast快：200ms
//                $("div").fadeIn("slow");
//                $("div").fadeIn("fast");
//                $("div").fadeIn("normal");

                //淡入动画用法4:   fadeIn(毫秒值，回调函数[显示完毕执行什么]);
//                $("div").fadeIn(5000,function () {
//                    alert("动画执行完毕！");
//                });
            })

            //滑出动画
            $("button:eq(1)").click(function () {
//                //滑出动画用法1:   fadeOut();   不加参数
               $("div").fadeOut();

//                //滑出动画用法2:   fadeOut(2000);   毫秒值
//                $("div").fadeOut(2000);  //通过这个方法实现的：display: none;
//                //通过控制  透明度和display

                //滑出动画用法3:   fadeOut(字符串);   slow慢：600ms   normal正常:400ms   fast快：200ms
//                $("div").fadeOut("slow");
//                $("div").fadeOut("fast");
//                $("div").fadeOut("normal");

                //滑出动画用法1:   fadeOut(毫秒值，回调函数[显示完毕执行什么]);
//                $("div").fadeOut(2000,function () {
//                    alert("动画执行完毕！");
//                });
            })

            $("button:eq(2)").click(function () {
                //滑入滑出切换
                //同样有四种用法
                $("div").fadeToggle(1000);
            })

            $("button:eq(3)").click(function () {
                //改透明度
                //同样有四种用法
                $("div").fadeTo(1000, 0.5, function () {
                    alert(1);
                });
            })
        })
    </script>
</head>
<body>
<button>淡入</button>
<button>淡出</button>
<button>切换</button>
<button>改透明度为0.5</button>
<div></div>

</body>
</html>
```



#### 自定义动画

语法：

```
 $(selector).animate({params}, speed, callback);

```

作用：执行一组CSS属性的自定义动画。

- 第一个参数表示：要执行动画的CSS属性（必选）
- 第二个参数表示：执行动画时长（可选）
- 第三个参数表示：动画执行完后，立即执行的回调函数（可选）

代码如下：



```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        div {
            position: absolute;
            left: 20px;
            top: 30px;
            width: 100px;
            height: 100px;
            background-color: green;
        }
    </style>
    <script src="jquery-3.3.1.js"></script>
    <script>
        jQuery(function () {
            $("button").click(function () {
                var json = {"width": 500, "height": 500, "left": 300, "top": 300, "border-radius": 100};
                var json2 = {
                    "width": 100,
                    "height": 100,
                    "left": 100,
                    "top": 100,
                    "border-radius": 100,
                    "background-color": "red"
                };

                //自定义动画
                $("div").animate(json, 1000, function () {
                    $("div").animate(json2, 1000, function () {
                        alert("动画执行完毕！");
                    });
                });

            })
        })
    </script>
</head>
<body>
<button>自定义动画</button>
<div></div>
</body>
</html>
```



#### 停止动画

```
$(selector).stop(true, false);

```

**里面的两个参数，有不同的含义。**

第一个参数：

- true：后续动画不执行。
- false：后续动画会执行。

第二个参数：

- true：立即执行完成当前动画。
- false：立即停止当前动画。

PS：参数如果都不写，默认两个都是false。实际工作中，直接写stop()用的多。

 

**案例：鼠标悬停时，弹出下拉菜单（下拉时带动画）**



```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style type="text/css">
        * {
            margin: 0;
            padding: 0;
        }

        ul {
            list-style: none;
        }

        .wrap {
            width: 330px;
            height: 30px;
            margin: 100px auto 0;
            padding-left: 10px;
            background-color: pink;
        }

        .wrap li {
            background-color: green;
        }

        .wrap > ul > li {
            float: left;
            margin-right: 10px;
            position: relative;
        }

        .wrap a {
            display: block;
            height: 30px;
            width: 100px;
            text-decoration: none;
            color: #000;
            line-height: 30px;
            text-align: center;
        }

        .wrap li ul {
            position: absolute;
            top: 30px;
            display: none;
        }
    </style>
    <script src="jquery-3.3.1.js"></script>
    <script>
        //入口函数
        $(document).ready(function () {
            //需求：鼠标放入一级li中，让他里面的ul显示。移开隐藏。
            var jqli = $(".wrap>ul>li");

            //绑定事件
            jqli.mouseenter(function () {
                $(this).children("ul").stop().slideDown(1000);
            });

            //绑定事件(移开隐藏)
            jqli.mouseleave(function () {
                $(this).children("ul").stop().slideUp(1000);
            });
        });
    </script>

</head>
<body>
<div class="wrap">
    <ul>
        <li>
            <a href="javascript:void(0);">一级菜单1</a>
            <ul>
                <li><a href="javascript:void(0);">二级菜单2</a></li>
                <li><a href="javascript:void(0);">二级菜单3</a></li>
                <li><a href="javascript:void(0);">二级菜单4</a></li>
            </ul>
        </li>
        <li>
            <a href="javascript:void(0);">二级菜单1</a>
            <ul>
                <li><a href="javascript:void(0);">二级菜单2</a></li>
                <li><a href="javascript:void(0);">二级菜单3</a></li>
                <li><a href="javascript:void(0);">二级菜单4</a></li>
            </ul>
        </li>
        <li>
            <a href="javascript:void(0);">三级菜单1</a>
            <ul>
                <li><a href="javascript:void(0);">三级菜单2</a></li>
                <li><a href="javascript:void(0);">三级菜单3</a></li>
                <li><a href="javascript:void(0);">三级菜单4</a></li>
            </ul>
        </li>
    </ul>
</div>
</body>
</html>
```



ps:

```
javascript:void(0); //跟javascript:;效果一样 阻止默认事件 比如a标签和form表单
```