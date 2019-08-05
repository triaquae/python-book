### jQuery的属性操作

上方代码中，关键的地方在于，用了stop函数，再执行动画前，先停掉之前的动画。

jquery的属性操作模块分为四个部分：html属性操作，dom属性操作，类样式操作和值操作

- `html属性操作：是对html文档中的属性进行读取，设置和移除操作。比如attr()、removeAttr()`
- `DOM属性操作：对DOM元素的属性进行读取，设置和移除操作。比如prop()、removeProp()`
- `类样式操作：是指对DOM属性className进行添加，移除操作。比如addClass()、removeClass()、toggleClass()`
- `值操作：是对DOM属性value进行读取和设置操作。比如html()、text()、val()`



#### 对html属性操作

##### attr()

设置属性值或者 返回被选元素的属性值

```javascript
//获取值：attr()设置一个属性值的时候 只是获取值
var id = $('div').attr('id')
console.log(id)
var cla = $('div').attr('class')
console.log(cla)
//设置值
//1.设置一个值 设置div的class为box
$('div').attr('class','box')
//2.设置多个值，参数为对象，键值对存储
$('div').attr({name:'hahaha',class:'happy'})
```

##### removeAttr()

移除属性

```javascript
//删除单个属性
$('#box').removeAttr('name');
$('#box').removeAttr('class');
//删除多个属性
$('#box').removeAttr('name class');
```

##### prop()

prop() 方法设置或返回被选元素的属性和值。

当该方法用于**返回**属性值时，则返回第一个匹配元素的值。

当该方法用于**设置**属性值时，则为匹配元素集合设置一个或多个属性/值对。

语法：

返回属性的值：

```javascript
$(selector).prop(property)
```

设置属性和值：

```javascript
$(selector).prop(property,value)
```

设置多个属性和值：

```javascript
$(selector).prop({property:value, property:value,...})
```

##### 关于attr()和prop()的区别

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
    男<input type="radio" id='test' name="sex"  checked/>
    女<input type="radio" id='test2' name="sex" />
    <button>提交</button>

    <script type="text/javascript" src="jquery-3.3.1.js"></script>
    <script type="text/javascript">
        $(function(){
            //获取第一个input
            var el = $('input').first();
            //undefined  因为attr是获取的这个对象属性节点的值，很显然此时没有这个属性节点，自然输出undefined
            console.log(el.attr('style'));
            // 输出CSSStyleDeclaration对象，对于一个DOM对象，是具有原生的style对象属性的，所以输出了style对象
            console.log(el.prop('style'));
            console.log(document.getElementById('test').style);

            $('button').click(function(){
                alert(el.prop("checked") ? "男":"女");
            })
            


        })
    </script>
    
</body>
</html>
```

##### 什么时候使用attr()，什么时候使用prop()？

1.是有true,false两个属性使用prop();

2.其他则使用attr();

 

#### 对标签class的操作

##### addClass（添加多个类名）

为每个匹配的元素添加指定的类名。

```javascript
$('div').addClass("box");//追加一个类名到原有的类名
```

还可以为匹配的元素添加多个类名

```javascript
$('div').addClass("box box2");//追加多个类名
```

##### removeClass

从所有匹配的元素中删除全部或者指定的类。

 移除指定的类（一个或多个）

```javascript
$('div').removeClass('box')；
```

移除全部的类

```javascript
$('div').removeClass();
```

可以通过添加删除类名，来实现元素的显示隐藏

代码如下：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```javascript
var tag  = false;
    $('span').click(function(){
        if(tag){
            $('span').removeClass('active')
            tag=false;
        }else{
            $('span').addClass('active')
            tag=true;
        }    
})
```

##### 案例：

代码如下：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style type="text/css">
        .active{
            color: red;
        }
    </style>
</head>
<body>
     <ul>
         <li class="item">张三</li>
         <li class="item">李四</li>
         <li class="item">王五</li>
     </ul>
     <script type="text/javascript" src="jquery-3.3.1.js"></script>
     <script type="text/javascript">
         $(function(){

             $('ul li').click(function(){
                 // this指的是当前点击的DOM对象 ,使用$(this)转化jquery对象
                 $(this).addClass('active').siblings('li').removeClass('active');
             })
         })
     </script>
    
</body>
</html>
```

##### toggleClass

如果存在（不存在）就删除（添加）一个类。

语法：toggleClass('box')

```javascript
$('span').click(function(){
    //动态的切换class类名为active
    $(this).toggleClass('active')
})
```



#### 对值的操作

##### html()

获取值：

语法;

html() 是获取选中标签元素中所有的内容

```javascript
$('#box').html();
```

设置值：设置该元素的所有内容 会替换掉 标签中原来的内容

```javascript
$('#box').html('<a href="https://www.baidu.com">百度一下</a>');
```

##### text()

获取值：

text() 获取匹配元素包含的文本内容

语法：

```javascript
$('#box').text();
```

设置值：

设置该所有的文本内容

```javascript
$('#box').text('<a href="https://www.baidu.com">百度一下</a>');
```

注意：值为标签的时候 不会被渲染为标签元素 只会被当做值渲染到浏览器中

##### val()

获取值：

val()用于表单控件中获取值，比如input textarea select等等

设置值：

```javascript
$('input').val('设置了表单控件中的值')；
```

#### 操作input的value值

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title></title>
</head>

<body>
    <form>
        男
        <input type="radio" name="sex" checked=""> 女
        <input type="radio" name="sex">
        <select>
            <option >张三</option>
            <option text='test'>李四</option>
            <option>王五</option>
        </select>
    </form>
    <script type="text/javascript" src="jquery-3.3.1.js"></script>
    <script type="text/javascript">
 

    $(function() {

    	// $('input[type=radio]').get(1).checked = true;
	//设置value=2的项目为当前选中项 
	$("input[type=radio]").eq(1).attr("checked",true);
        $('input[type=radio]').change(function(event) {
            /* Act on the event */
            alert(1);
            // console.log($(this).select());
            console.log($(this).select().prop('checked'));
            var item = $("input[type=radio]:checked").val();
            console.log(item);
            // 获取select被选中项的文本
            var item2 = $("select option[selected]").text();
            console.log(item2);

        });

        $('select').change(function() {
        	   console.log($(this).val());
            //1.获取选中项的值
            console.log($('select');
            // 2.获取选中项的文本
            console.log($("select option:selected").text());
            // 或者
            console.log($("select").find("option:selected").text());

            // 3.获取选中项的索引
            console.log($("select").get(0).selectedIndex);


        });

          // 设置值： 两种方式设置值
          $("select option").get(1).selected = true;
          $("select").get(0).selectedIndex = 2;

    });
    </script>
</body>

</html>
```