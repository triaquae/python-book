####  对DOM文档的操作

##### 一.插入操作

###### 知识点1：父子之间

语法：

```
父元素.append(子元素)

```

解释：追加某元素，在父元素中添加新的子元素。子元素可以为：stirng | element（js对象） | jquery元素

代码如下：

```
var oli = document.createElement('li');
oli.innerHTML = '哈哈哈';
$('ul').append('<li>1233</li>');
$('ul').append(oli);
$('ul').append($('#app'));

```

PS:如果追加的是jquery对象那么这些元素将从原位置上消失。简言之，就是一个移动操作。

 

###### 知识点2：父子之间

语法：

```
子元素.appendTo(父元素)

```

解释：追加到某元素 子元素添加到父元素

```javascript
$('<li>天王盖地虎</li>').appendTo($('ul')).addClass('active');
```

PS:要添加的元素同样既可以是stirng 、element(js对象) 、 jquery元素

 

###### 知识点3：父子之间

语法：

```javascript
父元素.prepend(子元素)；
```

解释：前置添加， 添加到父元素的第一个位置

```javascript
$('ul').prepend('<li>我是第一个</li>');
```

 

###### 知识点4：父子之间

语法：

```javascript
子元素.prependTo(父元素)；
```

解释：前置添加， 添加到父元素的第一个位置

```javascript
 $('<a href="#">路飞学诚</a>').prependTo('ul');
```

 

###### 知识点5：兄弟之间

语法：

```javascript
兄弟元素.after(要插入的兄弟元素)；
要插入的兄弟元素.inserAfter(兄弟元素)；
```

解释：在匹配的元素之后插入内容 

```javascript
$('ul').after('<h4>我是一个h3标题</h4>');
$('<h5>我是一个h2标题</h5>').insertAfter('ul');
```

 

###### 知识点6：兄弟之间

语法：

```javascript
兄弟元素.before(要插入的兄弟元素)；
要插入的兄弟元素.inserBefore(兄弟元素)；
```

解释：在匹配的元素之后插入内容 

```javascript
$('ul').before('<h3>我是一个h3标题</h3>');
$('<h2>我是一个h2标题</h2>').insertBefore('ul');
```



##### 二、替换操作

###### 知识点1：

语法：

```js
$(selector).replaceWith(content);

```js

将所有匹配的元素替换成指定的string、js对象、jquery对象。

```js
//将所有的h5标题替换为a标签
$('h5').replaceWith('<a href="#">hello world</a>');
//将所有h5标题标签替换成id为app的dom元素
$('h5').replaceWith($('#app'));

```

###### 知识点2：

语法：

```js
$('<p>哈哈哈</p>').replaceAll('h2');

```

解释：替换所有。将所有的h2标签替换成p标签。

```js
$('<br/><hr/><button>按钮</button>').replaceAll('h4');

```

##### 三、删除操作

###### 知识点1：

语法：

```js
$(selector).remove(); 

```

解释：删除节点后，事件也会删除（简言之，删除了整个标签）

```js
$('ul').remove();

```

 

###### 知识点2：

语法：

```js
$(selector).detach(); 

```

解释：删除节点后，事件会保留

```js
 var $btn = $('button').detach()
 //此时按钮能追加到ul中
 $('ul').append($btn)
```

 

###### 知识点3：

语法：

```js
$(selector).empty(); 

```

解释：清空选中元素中的所有后代节点

```js
//清空掉ul中的子元素，保留ul
$('ul').empty()
```