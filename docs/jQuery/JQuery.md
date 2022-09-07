# jQuery

## 1. 初识jQuery

http://jquery.com

### 1.1 什么是jQuery？

一个优秀的JS函数库

在Vue和React之前是中大型WEB项目开发首选

### 1.2 为什么要用jQuery？

- HTML元素选取（选择器）
- HTML元素操作
- CSS操作
- HTML事件处理
- JS动画效果
- 链式调用
- 读写合一
- 浏览器兼容
- 易扩展插件
- ajax封装

### 1.3 如何使用jQuery？

jQuery 库位于一个 JavaScript 文件中，其中包含了所有的 jQuery 函数。

可以通过下面的标记把 jQuery 添加到网页中：

```html
<head>
<script type="text/javascript" src="jquery.js"></script>
</head>
```

**注意：**`<script>` 标签应该位于页面的 `<head>` 部分。

每个版本的jQuery包含两个包，一个是压缩版本（Production version），一个是开发者版本（Development version）。

为减小服务器压力，也可以使用网络上的jQuery库。

**使用 Google 的 CDN**

```html
<head>
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs
/jquery/1.4.0/jquery.min.js"></script>
</head>
```

**使用 Microsoft 的 CDN**

```html
<head>
<script type="text/javascript" src="http://ajax.microsoft.com/ajax/jquery
/jquery-1.4.min.js"></script>
</head>
```

### 1.4 jQuery语法

Query 语法是为 HTML 元素的选取编制的，可以对元素执行某些操作。

基础语法是：`$(selector).action()`

- 美元符号`$`定义 jQuery
- 选择符`（selector）`“查询”和“查找” HTML 元素
- jQuery 的 `action()` 执行对元素的操作

**示例**

> `$(this).hide()` - 隐藏当前元素
>
> `$("p").hide()` - 隐藏所有段落
>
> `$(".test").hide()` - 隐藏所有 class="test" 的所有元素
>
> `$("#test").hide()` - 隐藏所有 id="test" 的元素

**文档就绪函数**

```javascript
$(document).ready(function(){

  // jQuery functions go here

});
```

这是为了防止文档在完全加载（就绪）之前运行 jQuery 代码。

如果在文档没有完全加载之前就运行函数，操作可能失败。下面是两个具体的例子：

- 试图隐藏一个不存在的元素
- 获得未完全加载的图像的大小

### 1.5 jQuery选择器

jQuery 元素选择器和属性选择器允许通过标签名、属性名或内容对 HTML 元素进行选择。

选择器允许对 HTML 元素组或单个元素进行操作。

在 HTML DOM 术语中：

选择器允许对 DOM 元素组或单个 DOM 节点进行操作。

#### 1.5.1 jQuery 元素选择器

jQuery 使用 CSS 选择器来选取 HTML 元素。

`$("p")` 选取 `<p>` 元素。

`$("p.intro")` 选取所有 `class="intro"` 的 `<p>` 元素。

`$("p#demo")` 选取所有 `id="demo"` 的 `<p>` 元素。

#### 1.5.2 jQuery 属性选择器

jQuery 使用 XPath 表达式来选择带有给定属性的元素。

`$("[href]")` 选取所有带有 href 属性的元素。

`$("[href='#']")` 选取所有带有 href 值等于 "#" 的元素。

`$("[href!='#']")` 选取所有带有 href 值不等于 "#" 的元素。

`$("[href$='.jpg']")` 选取所有 href 值以 ".jpg" 结尾的元素。

#### 1.5.3 jQuery CSS 选择器

jQuery CSS 选择器可用于改变 HTML 元素的 CSS 属性。

下面的例子把所有 p 元素的背景颜色更改为红色：

```javascript
$("p").css("background-color","red");
```

### 1.6 jQuery事件

#### 1.6.1 jQuery 事件函数

jQuery 事件处理方法是 jQuery 中的核心函数。

事件处理程序指的是当 HTML 中发生某些事件时所调用的方法。术语由事件“触发”（或“激发”）经常会被使用。

通常会把 jQuery 代码放到 `<head>`部分的事件处理方法中：

```html
<html>
<head>
<script type="text/javascript" src="jquery.js"></script>
<script type="text/javascript">
$(document).ready(function(){
  $("button").click(function(){
    $("p").hide();
  });
});
</script>
</head>

<body>
<h2>This is a heading</h2>
<p>This is a paragraph.</p>
<p>This is another paragraph.</p>
<button>Click me</button>
</body>

</html>
```

#### 1.6.2 单独文件中的函数

如果网站包含许多页面，并且希望 jQuery 函数易于维护，那么把 jQuery 函数放到独立的 .js 文件中。

```html
<head>
<script type="text/javascript" src="jquery.js"></script>
<script type="text/javascript" src="my_jquery_functions.js"></script>
</head>
```

#### 1.6.3 jQuery 名称冲突

jQuery 使用 $ 符号作为 jQuery 的简介方式。

某些其他 JavaScript 库中的函数（比如 Prototype）同样使用 $ 符号。

jQuery 使用名为 `noConflict()` 的方法来解决该问题。

*`var jq=jQuery.noConflict()`*，帮助使用自己的名称（比如 jq）来代替 $ 符号。

> 由于 jQuery 是为处理 HTML 事件而特别设计的，那么当您遵循以下原则时，您的代码会更恰当且更易维护：
>
> - 把所有 jQuery 代码置于事件处理函数中
> - 把所有事件处理函数置于文档就绪事件处理器中
> - 把 jQuery 代码置于单独的 .js 文件中
> - 如果存在名称冲突，则重命名 jQuery 库

## 2. jQuery效果

### 2.1 隐藏和显示

通过 jQuery，可以使用 `hide()` 和 `show()` 方法来隐藏和显示 HTML 元素：

```javascript
$("#hide").click(function(){
  $("p").hide();
});

$("#show").click(function(){
  $("p").show();
});
```

**语法：**

```javascript
$(selector).hide(speed,callback);

$(selector).show(speed,callback);
```

可选的 *speed* 参数规定隐藏/显示的速度，可以取以下值："slow"、"fast" 或毫秒。

可选的 *callback* 参数是隐藏或显示完成后所执行的函数名称。

下面的例子演示了带有 *speed* 参数的 `hide()` 方法：

```javascript
$("button").click(function(){
  $("p").hide(1000);
});
```

`jQuery toggle()`

通过 jQuery，可以使用 `toggle()` 方法来切换 `hide()` 和 `show()` 方法。

显示被隐藏的元素，并隐藏已显示的元素：

```javascript
$("button").click(function(){
  $("p").toggle();
});
```

### 2.2 淡入淡出

jQuery Fading 方法

通过 jQuery，可以实现元素的淡入淡出效果。

jQuery 拥有下面四种 fade 方法：

- `fadeIn()`
- `fadeOut()`
- `fadeToggle()`
- `fadeTo()`

#### 2.2.1 jQuery fadeIn() 方法

`jQuery fadeIn()` 用于淡入已隐藏的元素。

语法：

```javascript
$(selector).fadeIn(speed,callback);
```

```javascript
$("button").click(function(){
  $("#div1").fadeIn();
  $("#div2").fadeIn("slow");
  $("#div3").fadeIn(3000);
});
```

#### 2.2.2 jQuery fadeOut() 方法

`jQuery fadeOut()` 方法用于淡出可见元素。

语法：

```javascript
$(selector).fadeOut(speed,callback);
```

```javascript
$("button").click(function(){
  $("#div1").fadeOut();
  $("#div2").fadeOut("slow");
  $("#div3").fadeOut(3000);
});
```

#### 2.2.3 jQuery fadeToggle() 方法

`jQuery fadeToggle()` 方法可以在 `fadeIn()` 与 `fadeOut()` 方法之间进行切换。

如果元素已淡出，则 `fadeToggle()` 会向元素添加淡入效果。

如果元素已淡入，则 `fadeToggle()` 会向元素添加淡出效果。

#### 2.2.4 jQuery fadeTo() 方法

`jQuery fadeTo()` 方法允许渐变为给定的不透明度（值介于 0 与 1 之间）。

```javascript
$(selector).fadeTo(speed,opacity,callback);
```

必需的 speed 参数规定效果的时长。它可以取以下值："slow"、"fast" 或毫秒。

`fadeTo()` 方法中必需的 opacity 参数将淡入淡出效果设置为给定的不透明度（值介于 0 与 1 之间）。

可选的 callback 参数是该函数完成后所执行的函数名称。

### 2.3 滑动

jQuery 拥有以下滑动方法：

- `slideDown()`
- `slideUp()`
- `slideToggle()`

#### 2.3.1 jQuery slideDown() 方法

用于向下滑动元素。

语法：

```javascript
$(selector).slideDown(speed,callback);
```

可选的 speed 参数规定效果的时长。可以取以下值："slow"、"fast" 或毫秒。

可选的 callback 参数是滑动完成后所执行的函数名称。

#### 2.3.2 jQuery slideUp() 方法

用于向上滑动元素。

语法：

```javascript
$(selector).slideUp(speed,callback);
```

可选的 *speed* 参数规定效果的时长。可以取以下值："slow"、"fast" 或毫秒。

可选的 *callback* 参数是滑动完成后所执行的函数名称。

#### 2.3.3 jQuery slideToggle() 方法

可以在 `slideDown()` 与 `slideUp()` 方法之间进行切换。

如果元素向下滑动，则 `slideToggle()` 可向上滑动它们。

如果元素向上滑动，则 `slideToggle()` 可向下滑动它们。

```javascript
$(selector).slideToggle(speed,callback);
```

可选的 *speed* 参数规定效果的时长。它可以取以下值："slow"、"fast" 或毫秒。

可选的 *callback* 参数是滑动完成后所执行的函数名称。

### 2.4 动画

`jQuery animate()` 方法用于创建自定义动画。

```javascript
$(selector).animate({params},speed,callback);
```

**必需**的 *params* 参数定义形成动画的 CSS 属性。

可选的 *speed* 参数规定效果的时长。可以取以下值："slow"、"fast" 或毫秒。

可选的 *callback* 参数是动画完成后所执行的函数名称。

> **提示：**默认地，所有 HTML 元素都有一个静态位置，且无法移动。
>
> 如需对位置进行操作，要记得首先把元素的 CSS position 属性设置为 relative、fixed 或 absolute！

#### 2.4.1 操作多个属性

生成动画的过程中可同时使用多个属性：

```javascript
$("button").click(function(){
  $("div").animate({
    left:'250px',
    opacity:'0.5',
    height:'150px',
    width:'150px'
  });
}); 
```

> **提示：**可以用 animate() 方法来操作所有 CSS 属性吗？
>
> 是的，几乎可以！不过，需要记住一件重要的事情：当使用 animate() 时，必须使用 Camel 标记法书写所有的属性名，比如，必须使用 paddingLeft 而不是 padding-left，使用 marginRight 而不是 margin-right，等等。
>
> 同时，色彩动画并不包含在核心 jQuery 库中。
>
> 如果需要生成颜色动画，需要从 jQuery.com 下载 Color Animations 插件。

#### 2.4.2 使用相对值

可以定义相对值（该值相对于元素的当前值）。需要在值的前面加上 += 或 -=：

```javascript
$("button").click(function(){
  $("div").animate({
    left:'250px',
    height:'+=150px',
    width:'+=150px'
  });
});
```

#### 2.4.3 使用预定义的值

可以把属性的动画值设置为 "show"、"hide" 或 "toggle"：

```javascript
$("button").click(function(){
  $("div").animate({
    height:'toggle'
  });
});
```

#### 2.4.4 使用队列功能

在彼此之后编写多个 animate() 调用，jQuery 会创建包含这些方法调用的“内部”队列。然后逐一运行这些 animate 调用。

```javascript
$("button").click(function(){
  var div=$("div");
  div.animate({height:'300px',opacity:'0.4'},"slow");
  div.animate({width:'300px',opacity:'0.8'},"slow");
  div.animate({height:'100px',opacity:'0.4'},"slow");
  div.animate({width:'100px',opacity:'0.8'},"slow");
});
```

### 2.5 停止动画

`jQuery stop()` 方法用于在动画或效果完成前对它们进行停止。

stop() 方法适用于所有 jQuery 效果函数，包括滑动、淡入淡出和自定义动画。

```javascript
$(selector).stop(stopAll,goToEnd);
```

可选的 *stopAll* 参数规定是否应该清除动画队列。默认是 false，即仅停止活动的动画，允许任何排入队列的动画向后执行。

可选的 *goToEnd* 参数规定是否立即完成当前动画。默认是 false。

因此，默认地，stop() 会清除在被选元素上指定的当前动画。

### 2.6 Callback 函数

在当前动画 100% 完成之后执行。

由于 JavaScript 语句（指令）是逐一执行的 - 按照次序，动画之后的语句可能会产生错误或页面冲突，因为动画还没有完成。

为了避免这个情况，可以以参数的形式添加 Callback 函数。

```javascript
$(selector).hide(speed,callback)
```

### 2.7 Chaining

通过 jQuery，可以把动作/方法链接起来。

Chaining 允许在一条语句中允许多个 jQuery 方法（在相同的元素上）。

这样的话，浏览器就不必多次查找相同的元素。

```javascript
$("#p1").css("color","red").slideUp(2000).slideDown(2000);
```

## 3. jQuery HTML

### 3.1 获得内容和属性

#### 3.1.1 获得内容 - text()、html() 以及 val()

- `text()` - 设置或返回所选元素的文本内容
- `html()` - 设置或返回所选元素的内容（包括 HTML 标记）
- `val()` - 设置或返回表单字段的值

#### 3.1.2 获取属性 - attr()

用于获取属性值。

```javascript
$("button").click(function(){
  alert($("#w3s").attr("href"));
});
```

### 3.2 设置内容和属性

#### 3.2.1 设置内容 - text()、html() 以及 val()

- text() - 设置或返回所选元素的文本内容
- html() - 设置或返回所选元素的内容（包括 HTML 标记）
- val() - 设置或返回表单字段的值

```javascript
$("#btn1").click(function(){
  $("#test1").text("Hello world!");
});
$("#btn2").click(function(){
  $("#test2").html("<b>Hello world!</b>");
});
$("#btn3").click(function(){
  $("#test3").val("Dolly Duck");
});
```

#### 3.2.2 text()、html() 以及 val() 的回调函数

回调函数由两个参数：被选元素列表中当前元素的下标，以及原始（旧的）值。然后以函数新值返回您希望使用的字符串。

```javascript
$("#btn1").click(function(){
  $("#test1").text(function(i,origText){
    return "Old text: " + origText + " New text: Hello world!
    (index: " + i + ")";
  });
});

$("#btn2").click(function(){
  $("#test2").html(function(i,origText){
    return "Old html: " + origText + " New html: Hello <b>world!</b>
    (index: " + i + ")";
  });
});
```

#### 3.2.3 设置属性 - attr()

`jQuery attr()` 方法也用于设置/改变属性值。

```javascript
$("button").click(function(){
  $("#w3s").attr("href","http://www.w3school.com.cn/jquery");
});
```

