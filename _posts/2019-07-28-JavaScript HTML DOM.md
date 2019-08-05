---
layout: post
title: "JS DOM"
date: 2019-07-28
tag: 学习
---



## JavaScript HTML DOM

> 通过 HTML DOM，JavaScript 能够访问和改变 HTML 文档的所有元素。



### HTML DOM Document 对象

HTML DOM 文档对象是您的网页中所有其他对象的拥有者。

#### 查找 HTML 元素

| 方法                                    | 描述                   |
| :-------------------------------------- | :--------------------- |
| document.getElementById(*id*)           | 通过元素 id 来查找元素 |
| document.getElementsByTagName(*name*)   | 通过标签名来查找元素   |
| document.getElementsByClassName(*name*) | 通过类名来查找元素     |

#### 改变 HTML 元素

| 方法                                       | 描述                   |
| :----------------------------------------- | :--------------------- |
| element.innerHTML = *new html content*     | 改变元素的 inner HTML  |
| element.attribute = *new value*            | 改变 HTML 元素的属性值 |
| element.setAttribute(*attribute*, *value*) | 改变 HTML 元素的属性值 |
| element.style.property = *new style*       | 改变 HTML 元素的样式   |

#### 添加和删除元素

| 方法                              | 描述             |
| :-------------------------------- | :--------------- |
| document.createElement(*element*) | 创建 HTML 元素   |
| document.removeChild(*element*)   | 删除 HTML 元素   |
| document.appendChild(*element*)   | 添加 HTML 元素   |
| document.replaceChild(*element*)  | 替换 HTML 元素   |
| document.write(*text*)            | 写入 HTML 输出流 |

#### 添加事件处理程序

| 方法                                                     | 描述                            |
| :------------------------------------------------------- | :------------------------------ |
| document.getElementById(id).onclick = function(){*code*} | 向 onclick 事件添加事件处理程序 |

#### 查找 HTML 对象

| 属性                         | 描述                                        | DOM  |
| :--------------------------- | :------------------------------------------ | :--- |
| document.anchors             | 返回拥有 name 属性的所有 <a> 元素。         | 1    |
| document.applets             | 返回所有 <applet> 元素（HTML5 不建议使用）  | 1    |
| document.baseURI             | 返回文档的绝对基准 URI                      | 3    |
| document.body                | 返回 <body> 元素                            | 1    |
| document.cookie              | 返回文档的 cookie                           | 1    |
| document.doctype             | 返回文档的 doctype                          | 3    |
| document.documentElement     | 返回 <html> 元素                            | 3    |
| document.documentMode        | 返回浏览器使用的模式                        | 3    |
| document.documentURI         | 返回文档的 URI                              | 3    |
| document.domain              | 返回文档服务器的域名                        | 1    |
| document.domConfig           | 废弃。返回 DOM 配置                         | 3    |
| document.embeds              | 返回所有 <embed> 元素                       | 3    |
| document.forms               | 返回所有 <form> 元素                        | 1    |
| document.head                | 返回 <head> 元素                            | 3    |
| document.images              | 返回所有 <img> 元素                         | 1    |
| document.implementation      | 返回 DOM 实现                               | 3    |
| document.inputEncoding       | 返回文档的编码（字符集）                    | 3    |
| document.lastModified        | 返回文档更新的日期和时间                    | 3    |
| document.links               | 返回拥有 href 属性的所有 <area> 和 <a> 元素 | 1    |
| document.readyState          | 返回文档的（加载）状态                      | 3    |
| document.referrer            | 返回引用的 URI（链接文档）                  | 1    |
| document.scripts             | 返回所有 <script> 元素                      | 3    |
| document.strictErrorChecking | 返回是否强制执行错误检查                    | 3    |
| document.title               | 返回 <title> 元素                           | 1    |
| document.URL                 | 返回文档的完整 URL                          | 1    |





### HTML DOM 方法

方法是可以在节点（HTML 元素）上执行的动作。

| 方法                     | 描述                                                         |
| :----------------------- | :----------------------------------------------------------- |
| getElementById()         | 返回带有指定 ID 的元素。                                     |
| getElementsByTagName()   | 返回包含带有指定标签名称的所有元素的节点列表（集合/节点数组）。 |
| getElementsByClassName() | 返回包含带有指定类名的所有元素的节点列表。                   |
| appendChild()            | 把新的子节点添加到指定节点。                                 |
| removeChild()            | 删除子节点。                                                 |
| replaceChild()           | 替换子节点。                                                 |
| insertBefore()           | 在指定的子节点前面插入新的子节点。                           |
| createAttribute()        | 创建属性节点。                                               |
| createElement()          | 创建元素节点。                                               |
| createTextNode()         | 创建文本节点。                                               |
| getAttribute()           | 返回指定的属性值。                                           |
| setAttribute()           | 把指定属性设置或修改为指定的值。                             |



### HTML DOM 属性

属性是节点（HTML 元素）的值，能够获取或设置。

#### innerHTML 属性

获取元素内容的最简单方法是使用 innerHTML 属性。

innerHTML 属性对于获取或替换 HTML 元素的内容很有用。

```javascript
## 下面的代码获取 id="intro" 的 <p> 元素的 innerHTML：
<html>
<body>

<p id="intro">Hello World!</p>

<script>
var txt=document.getElementById("intro").innerHTML;
document.write(txt);
</script>

</body>
</html>
```

在上面的例子中，getElementById 是一个方法，而 innerHTML 是属性。

innerHTML 属性可用于获取或改变任意 HTML 元素，包括` <html> `和 `<body>`。



#### nodeName 属性

nodeName 属性规定节点的名称。

- nodeName 是只读的
- 元素节点的 nodeName 与标签名相同
- 属性节点的 nodeName 与属性名相同
- 文本节点的 nodeName 始终是 #text
- 文档节点的 nodeName 始终是 #document

**注释：**nodeName 始终包含 HTML 元素的大写字母标签名。



#### nodeValue 属性

nodeValue 属性规定节点的值。

- 元素节点的 nodeValue 是 undefined 或 null
- 文本节点的 nodeValue 是文本本身
- 属性节点的 nodeValue 是属性值

下面的例子会取回 `<p id="intro">` 标签的文本节点值：

```
<html>
<body>

<p id="intro">Hello World!</p>

<script type="text/javascript">
x=document.getElementById("intro");
document.write(x.firstChild.nodeValue);
</script>

</body>
</html>
```



#### nodeType 属性

nodeType 属性返回节点的类型。nodeType 是只读的。

比较重要的节点类型有：

| 元素类型 | NodeType |
| :------- | :------- |
| 元素     | 1        |
| 属性     | 2        |
| 文本     | 3        |
| 注释     | 8        |
| 文档     | 9        |



### HTML DOM 访问

**访问 HTML 元素（节点）**

访问 HTML 元素等同于访问节点

- 通过使用 getElementById() 方法
- 通过使用 getElementsByTagName() 方法
- 通过使用 getElementsByClassName() 方法



#### 查找 HTML 元素

通常，通过 JavaScript，您需要操作 HTML 元素。

为了达成此目的，您需要首先找到这些元素。有好几种完成此任务的方法：

- 通过 id 查找 HTML 元素
- 通过标签名查找 HTML 元素
- 通过类名查找 HTML 元素
- 通过 CSS 选择器查找 HTML 元素
- 通过 HTML 对象集合查找 HTML 元素



#### 通过 id 查找 HTML 元素

DOM 中查找 HTML 元素最简单的方法是，使用元素的 id。

本例查找 id="intro" 的元素：

```
var myElement = document.getElementById("intro");
```

如果元素被找到，此方法会以对象返回该元素（在 myElement 中）。

如果未找到元素，myElement 将包含 null。



#### 通过标签名查找 HTML 元素

本例查找所有 <p> 元素：

```
var x = document.getElementsByTagName("p");
```



#### 通过类名查找 HTML 元素

如果您需要找到拥有相同类名的所有 HTML 元素，请使用 getElementsByClassName()。

本例返回包含 class="intro" 的所有元素的列表：

```
var x = document.getElementsByClassName("intro");
```



#### 通过 CSS 选择器查找 HTML 元素

如果您需要查找匹配指定 CSS 选择器（id、类名、类型、属性、属性值等等）的所有 HTML 元素，请使用 querySelectorAll() 方法。

本例返回 class="intro" 的所有 <p> 元素列表：

```
var x = document.querySelectorAll("p.intro");
```



#### 通过 HTML 对象选择器查找 HTML 对象

本例查找 id="frm1" 的 form 元素，在 forms 集合中，然后显示所有元素值：

```
var x = document.forms["frm1"];
var text = "";
 var i;
for (i = 0; i < x.length; i++) {
    text += x.elements[i].value + "<br>";
}
document.getElementById("demo").innerHTML = text;
```



### HTML DOM 修改

- 改变 HTML 内容
- 改变 CSS 样式
- 改变 HTML 属性
- 创建新的 HTML 元素
- 删除已有的 HTML 元素
- 改变事件（处理程序）



#### 改变 HTML 内容

改变元素内容的最简答的方法是使用 innerHTML 属性。

下面的例子改变一个 <p> 元素的 HTML 内容：

```
<html>
<body>

<p id="p1">Hello World!</p>

<script>
document.getElementById("p1").innerHTML="New text!";
</script>

</body>
</html>
```

- 上面的 HTML 文档包含 id="p1" 的 <p> 元素
- 我们使用 HTML DOM 来获取 id="p1" 的这个元素
- JavaScript 把该元素的内容（innerHTML）更改为 "New text!"



#### 改变 HTML 输出流

JavaScript 能够创建动态 HTML 内容：

```
Mon Jul 29 2019 06:20:49 GMT+0800 (中国标准时间)
```

在 JavaScript 中，document.write() 可用于直接写入 HTML 输出流：

```
<!DOCTYPE html>
<html>
<body>

<script>
document.write(Date());
</script>

</body>
</html>
```



#### 改变 HTML 样式

通过 HTML DOM，您能够访问 HTML 元素的样式对象。

```
document.getElementById(id).style.property = new style
```

下面的例子改变一个段落的 HTML 样式：

```
<html>

<body>
<p id="p2">Hello world!</p>

<script>
document.getElementById("p2").style.color="blue";
</script>

</body>
</html>
```



#### 创建新的 HTML 元素

如需向 HTML DOM 添加新元素，您首先必须创建该元素（元素节点），然后把它追加到已有的元素上。

```
<div id="d1">
<p id="p1">This is a paragraph.</p>
<p id="p2">This is another paragraph.</p>
</div>

<script>
var para=document.createElement("p");
var node=document.createTextNode("This is new.");
para.appendChild(node);

var element=document.getElementById("d1");
element.appendChild(para);
</script>
```



#### 改变属性的值

如需修改 HTML 属性的值，请使用如下语法：

```
document.getElementById(id).attribute = new value
```

```
<!DOCTYPE html>
<html>
<body>

<img id="myImage" src="smiley.gif">

<script>
document.getElementById("myImage").src = "landscape.jpg";
</script>

</body>
</html> 
```

- 上面的 HTML 文档含有一个 id="myImage" 的 <img> 元素
- 我们使用 HTML DOM 来获取 id="myImage" 的元素
- JavaScript 把此元素的 src 属性从 "smiley.gif" 更改为 "landscape.jpg"



#### 使用事件

HTML DOM 允许您在事件发生时执行代码。

当 HTML 元素”有事情发生“时，浏览器就会生成事件：

- 在元素上点击
- 加载页面
- 改变输入字段

下面两个例子在按钮被点击时改变 <body> 元素的背景色：

```
<html>
<body>

<input type="button" onclick="document.body.style.backgroundColor='lavender';"
value="Change background color" />

</body>
</html>
```



### HTML DOM 元素

#### 创建新的 HTML 元素 - appendChild()

如需向 HTML DOM 添加新元素，您首先必须创建该元素，然后把它追加到已有的元素上。

```
<div id="div1">
<p id="p1">This is a paragraph.</p>
<p id="p2">This is another paragraph.</p>
</div>

<script>
var para=document.createElement("p");
var node=document.createTextNode("This is new.");
para.appendChild(node);

var element=document.getElementById("div1");
element.appendChild(para);
</script>
```

这段代码创建了一个新的 <p> 元素：

```
var para=document.createElement("p");
```

如需向 <p> 元素添加文本，您首先必须创建文本节点。这段代码创建文本节点：

```
var node=document.createTextNode("This is a new paragraph.");
```

然后您必须向 <p> 元素追加文本节点：

```
para.appendChild(node);
```

最后，您必须向已有元素追加这个新元素。

这段代码查找到一个已有的元素：

```
var element=document.getElementById("div1");
```

这段代码向这个已存在的元素追加新元素：

```
element.appendChild(para);
```



#### 创建新的 HTML 元素 - insertBefore()

上一个例子中的 appendChild() 方法，将新元素作为父元素的最后一个子元素进行添加。

如果不希望如此，您可以使用 insertBefore() 方法：

```
<div id="div1">
<p id="p1">This is a paragraph.</p>
<p id="p2">This is another paragraph.</p>
</div>

<script>
var para=document.createElement("p");
var node=document.createTextNode("This is new.");
para.appendChild(node);

var element=document.getElementById("div1");
var child=document.getElementById("p1");
element.insertBefore(para,child);
</script>
```



#### 删除已有的 HTML 元素

如需删除 HTML 元素，您必须清楚该元素的父元素：

```
<div id="div1">
<p id="p1">This is a paragraph.</p>
<p id="p2">This is another paragraph.</p>
</div>
<script>
var parent=document.getElementById("div1");
var child=document.getElementById("p1");
parent.removeChild(child);
</script>
```

这个 HTML 文档包含一个带有两个子节点（两个 <p> 元素）的 <div> 元素：

```
<div id="div1">
<p id="p1">This is a paragraph.</p>
<p id="p2">This is another paragraph.</p>
</div>
```

查找 id="div1" 的元素：

```
var parent=document.getElementById("div1");
```

查找 id="p1" 的 <p> 元素：

```
var child=document.getElementById("p1");
```

从父元素中删除子元素：

```
parent.removeChild(child);
```



#### 替换 HTML 元素

如需替换 HTML DOM 中的元素，请使用 replaceChild() 方法：

```
<div id="div1">
<p id="p1">This is a paragraph.</p>
<p id="p2">This is another paragraph.</p>
</div>

<script>
var para=document.createElement("p");
var node=document.createTextNode("This is new.");
para.appendChild(node);

var parent=document.getElementById("div1");
var child=document.getElementById("p1");
parent.replaceChild(para,child);
</script>
```



### HTML DOM 事件

#### 对事件作出反应

当事件发生时，可以执行 JavaScript，比如当用户点击一个 HTML 元素时。

如需在用户点击某个元素时执行代码，请把 JavaScript 代码添加到 HTML 事件属性中：

```
onclick=JavaScript
```

HTML 事件的例子：

- 当用户点击鼠标时
- 当网页已加载时
- 当图片已加载时
- 当鼠标移动到元素上时
- 当输入字段被改变时
- 当 HTML 表单被提交时
- 当用户触发按键时



#### HTML 事件属性

如需向 HTML 元素分配事件，您可以使用事件属性。

向 button 元素分配一个 onclick 事件：

```
<button onclick="displayDate()">试一试</button>
```



#### 使用 HTML DOM 来分配事件

HTML DOM 允许您使用 JavaScript 向 HTML 元素分配事件：

为 button 元素分配 onclick 事件：

```
<script>
document.getElementById("myBtn").onclick=function(){displayDate()};
</script>
```

在上面的例子中，名为 displayDate 的函数被分配给了 id=myButn" 的 HTML 元素。

当按钮被点击时，将执行函数。



#### onload 和 onunload 事件

当用户进入或离开页面时，会触发 onload 和 onunload 事件。

onload 事件可用于检查访客的浏览器类型和版本，以便基于这些信息来加载不同版本的网页。

onload 和 onunload 事件可用于处理 cookies。

```
<body onload="checkCookies()">
```



#### onchange 事件

onchange 事件常用于输入字段的验证。

下面的例子展示了如何使用 onchange。当用户改变输入字段的内容时，将调用 upperCase() 函数。

```
<input type="text" id="fname" onchange="upperCase()">
```



#### onmouseover 和 onmouseout 事件

onmouseover 和 onmouseout 事件可用于在鼠标指针移动到或离开元素时触发函数。



#### onmousedown、onmouseup 以及 onclick 事件

onmousedown、onmouseup 以及 onclick 事件是鼠标点击的全部过程。首先当某个鼠标按钮被点击时，触发 onmousedown 事件，然后，当鼠标按钮被松开时，会触发 onmouseup 事件，最后，当鼠标点击完成时，触发 onclick 事件。



### HTML DOM 事件监听

添加当用户点击按钮时触发的事件监听器：

```
document.getElementById("myBtn").addEventListener("click", displayDate);
```

addEventListener() 方法为指定元素指定事件处理程序。

addEventListener() 方法为元素附加事件处理程序而不会覆盖已有的事件处理程序。

您能够向一个元素添加多个事件处理程序。

您能够向一个元素添加多个相同类型的事件处理程序，例如两个 "click" 事件。

您能够向任何 DOM 对象添加事件处理程序而非仅仅 HTML 元素，例如 window 对象。

addEventListener() 方法使我们更容易控制事件如何对冒泡作出反应。

当使用 addEventListener() 方法时，JavaScript 与 HTML 标记是分隔的，已达到更佳的可读性；即使在不控制 HTML 标记时也允许您添加事件监听器。

您能够通过使用 removeEventListener() 方法轻松地删除事件监听器。

**语法:**

```
element.addEventListener(event, function, useCapture);
```

第一个参数是事件的类型（比如 "click" 或 "mousedown"）。

第二个参数是当事件发生时我们需要调用的函数。

第三个参数是布尔值，指定使用事件冒泡还是事件捕获。此参数是可选的。

**注意：**请勿对事件使用 "on" 前缀；请使用 "click" 代替 "onclick"。



#### 向元素添加事件处理程序

当用户点击某个元素时提示 "Hello World!"：

```
element.addEventListener("click", function(){ alert("Hello World!"); });
```



#### 向相同元素添加多个事件处理程序

addEventListener() 方法允许您向相同元素添加多个事件，同时不覆盖已有事件：

```
element.addEventListener("click", myFunction);
element.addEventListener("click", mySecondFunction);
```

向相同元素添加不同类型的事件：

```
element.addEventListener("mouseover", myFunction);
element.addEventListener("click", mySecondFunction);
element.addEventListener("mouseout", myThirdFunction);
```



#### 向 Window 对象添加事件处理程序

addEventListener() 允许您将事件监听器添加到任何 HTML DOM 对象上，比如 HTML 元素、HTML 对象、window 对象或其他支持事件的对象，比如 xmlHttpRequest 对象。

添加当用户调整窗口大小时触发的事件监听器：

```
window.addEventListener("resize", function(){
    document.getElementById("demo").innerHTML = sometext;
});
```



#### 传递参数

当传递参数值时，请以参数形式使用调用指定函数的“匿名函数”：

```
element.addEventListener("click", function(){ myFunction(p1, p2); });
```



#### 事件冒泡、捕获

在 addEventListener() 方法中，你能够通过使用“useCapture”参数来规定传播类型：

```
addEventListener(event, function, useCapture);
```

默认值是 false，将使用冒泡传播，如果该值设置为 true，则事件使用捕获传播。



#### removeEventListener() 方法

removeEventListener() 方法会删除已通过 addEventListener() 方法附加的事件处理程序：

```
element.removeEventListener("mousemove", myFunction);
```



#### 浏览器支持

```
element.attachEvent(event, function);
element.detachEvent(event, function);
```

跨浏览器解决方案：

```
var x = document.getElementById("myBtn");
if (x.addEventListener) {                    // 针对主流浏览器，除了 IE 8 及更正版本
    x.addEventListener("click", myFunction);
} else if (x.attachEvent) {                  // 针对 IE 8 及更早版本
    x.attachEvent("onclick", myFunction);
} 
```



### HTML DOM 元素(节点)

#### 创建新 HTML 元素（节点）

如需向 HTML DOM 添加新元素，您必须首先创建这个元素（元素节点），然后将其追加到已有元素。

```
<div id="div1">
<p id="p1">这是一个段落。</p>
<p id="p2">这是另一个段落。</p>
</div>

<script>
var para = document.createElement("p");
var node = document.createTextNode("这是新文本。");
para.appendChild(node);

var element = document.getElementById("div1");
element.appendChild(para);
</script>
```

这段代码创建了一个新的 <p> 元素：

```
var para = document.createElement("p");
```

如需向 <p> 元素添加文本，则必须首先创建文本节点。这段代码创建了一个文本节点：

```
var node = document.createTextNode("这是一个新段落。");
```

然后您需要向 <p> 元素追加这个文本节点：

```
para.appendChild(node);
```

最后您需要向已有元素追加这个新元素。

这段代码查找一个已有的元素：

```
var element = document.getElementById("div1");
```

这段代码向这个已有的元素追加新元素：

```
element.appendChild(para);
```



#### 创建新 HTML 元素 - insertBefore()

前面例子中的 appendChild() 方法，追加新元素作为父的最后一个子。

除此之外您还可以使用 insertBefore() 方法：

```
<div id="div1">
<p id="p1">这是一个段落。</p>
<p id="p2">这是另一个段落。</p>
</div>

<script>
var para = document.createElement("p");
var node = document.createTextNode("这是新文本。");
para.appendChild(node);

var element = document.getElementById("div1");
var child = document.getElementById("p1");
element.insertBefore(para, child);
</script>
```



#### 删除已有 HTML 元素

如需删除某个 HTML 元素，需要知晓该元素的父：



```
<div id="div1">
<p id="p1">这是一个段落。</p>
<p id="p2">这是另一个段落。</p>
</div>

<script>
var parent = document.getElementById("div1");
var child = document.getElementById("p1");
parent.removeChild(child);
</script>
```

这个 HTML 文档包含了一个带有两个子节点（两个 <p> 元素）的 <div> 元素：

```
<div id="div1">
<p id="p1">这是一个段落。</p>
<p id="p2">这是另一个段落。</p>
</div>
```

查找 id="div1" 的元素：

```
var parent = document.getElementById("div1");
```

查找 id="p1" 的 <p> 元素：

```
var child = document.getElementById("p1");
```

从父删除子：

```
parent.removeChild(child);
```

能够在不引用父的情况下删除某个元素是极好的。

但是很遗憾。DOM 需要同时了解您需要删除的元素及其父。

这是一种常见的解决方法：找到你想要删除的子，并利用其 parentNode 属性找到父：

```
var child = document.getElementById("p1");
child.parentNode.removeChild(child);
```



#### 替换 HTML 元素

如需替换元素的，请使用 replaceChild() 方法：



```
<div id="div1">
<p id="p1">这是一个段落。</p>
<p id="p2">这是另一个段落。</p>
</div>

<script>
var para = document.createElement("p");
var node = document.createTextNode("这是新文本。");
para.appendChild(node);

var parent = document.getElementById("div1");
var child = document.getElementById("p1");
parent.replaceChild(para, child);
</script>
```



### HTML DOM 集合

**HTMLCollection 并非数组！**

HTMLCollection 也许看起来像数组，但并非数组。

能够遍历列表并通过数字引用元素（就像数组那样）。



#### HTMLCollection 对象

getElementsByTagName() 方法返回 *HTMLCollection* 对象。

HTMLCollection 对象是类数组的 HTML 元素列表（集合）。

下面的代码选取文档中的所有 <p> 元素：

```
var x = document.getElementsByTagName("p");
```

该集合中的元素可通过索引号进行访问。

如需访问第二个 <p> 元素，您可以这样写：

```
y = x[1];
```



#### HTML HTMLCollection 长度

length 属性定义了 HTMLCollection 中元素的数量：

```
var myCollection = document.getElementsByTagName("p");
document.getElementById("demo").innerHTML = myCollection.length; 
```



改变所有 <p> 元素的背景色：

```
var myCollection = document.getElementsByTagName("p");
var i;
for (i = 0; i < myCollection.length; i++) {
    myCollection[i].style.backgroundColor = "red";
}
```