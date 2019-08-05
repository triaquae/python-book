### jQuery的位置信息

#### 一、宽度和高度

##### 获取宽度

```
.width()
```

描述：为匹配的元素集合中获取第一个元素的当前计算宽度值。这个方法不接受任何参数。`.css(width)` 和 `.width()`之间的区别是后者返回一个没有单位的数值（例如，`400`），前者是返回带有完整单位的字符串（例如，`400px`）。当一个元素的宽度需要数学计算的时候推荐使用`.width()` 方法 。

##### 设置宽度

```
.width( value )
```

描述：给每个匹配的元素设置CSS宽度。

 

##### 高度

##### 获取高度

```
.height()
```

描述：获取匹配元素集合中的第一个元素的当前计算高度值。

- 这个方法不接受任何参数。

##### 设置高度

```
 .height( value )
```

描述：设置每一个匹配元素的高度值。

 

#### 二、innerHeight()和innerWidth()

##### 获取内部宽

```
.innerWidth()
```

描述：为匹配的元素集合中获取第一个元素的当前计算宽度值,包括padding，但是不包括border。

ps:这个方法不适用于`window` 和 `document`对象，对于这些对象可以使用`.width()`代替。

 

##### 设置内部宽

```
.innerWidth(value);
```

描述： 为匹配集合中的每个元素设置CSS内部宽度。如果这个“value”参数提供一个数字，jQuery会自动加上像素单位（px）

##### 获取内部高

```
.innerHeight();
```

描述：为匹配的元素集合中获取第一个元素的当前计算高度值,包括padding，但是不包括border。

ps:这个方法不适用于`window` 和 `document`对象，对于这些对象可以使用`.height()`代替。

 

##### 设置内部宽

```
.innerHeight(value);
```

描述： 为匹配集合中的每个元素设置CSS内部高度。如果这个“value”参数提供一个数字，jQuery会自动加上像素单位（px）

 

#### 三、outerWidth和outerHeight()

 

##### 获取外部宽

```
 .outerWidth( [includeMargin ] )
```

描述：获取匹配元素集合中第一个元素的当前计算外部宽度（包括padding，border和可选的margin）

- includeMargin (默认: `false`)

  类型： `Boolean`

  一个布尔值，表明是否在计算时包含元素的margin值。

- 这个方法不适用于`window` 和 `document`对象，可以使用`.width()`代替

##### 设置外部宽

```
 .outerWidth( value )
```

描述： 为匹配集合中的每个元素设置CSS外部宽度。

 

##### 获取外部宽

```
 .outerHeight( [includeMargin ] )
```

描述：获取匹配元素集合中第一个元素的当前计算外部高度（包括padding，border和可选的margin）

- includeMargin (默认: `false`)

  类型： `Boolean`

  一个布尔值，表明是否在计算时包含元素的margin值。

- 这个方法不适用于`window` 和 `document`对象，可以使用`.width()`代替

##### 设置外部高

```
 .outerHeight( value )
```

描述： 为匹配集合中的每个元素设置CSS外部高度。

 

 

#### 四、偏移

##### 获取

```
.offset()
```

返回值：[Object](http://www.shouce.ren/api/view/a/13081#articleHeader15) 。`.offset()`返回一个包含`top` 和 `left`属性的对象 。

描述：在匹配的元素集合中，获取的第一个元素的当前坐标，坐标相对于文档。

注意：jQuery不支持获取隐藏元素的偏移坐标。同样的，也无法取得隐藏元素的 border, margin, 或 padding 信息。若元素的属性设置的是 `visibility:hidden`，那么我们依然可以取得它的坐标

 

##### 设置

```
 .offset( coordinates )
```

描述： 设置匹配的元素集合中每一个元素的坐标， 坐标相对于文档。

- coordinates

  类型: [Object](http://www.shouce.ren/api/view/a/13081#articleHeader25)

  一个包含`top` 和 `left`属性的对象，用整数指明元素的新顶部和左边坐标。

例子：

```
$("p").offset({ top: 10, left: 30 });
```

 

 

 

#### 五、滚动距离

##### 水平方向获取：

```
.scrollLeft()
```

描述：获取匹配的元素集合中第一个元素的当前水平滚动条的位置（页面卷走的宽度）

 

##### 水平方向设置：

```
.scrollLeft( value )
```

描述：设置每个匹配元素的水平方向滚动条位置。

 

##### 垂直方向获取：

```
.scrollTop()
```

描述：获取匹配的元素集合中第一个元素的当前迟滞滚动条的位置（页面卷走的高度）

 

##### 垂直方向获取：

```
.scrollLeft( value )
```

描述：设置每个匹配元素的垂直方向滚动条位置。