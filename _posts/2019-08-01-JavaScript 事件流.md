---
layout: post
title: "JS 事件流"
date: 2019-08-01
tag: 学习
---



## JavaScript 事件流

> “DOM事件流”：三个阶段：事件捕捉，目标阶段，事件冒泡

事件冒泡会从当前触发的事件目标一级一级往上传递，依次触发，直到document为止。
事件捕获会从document开始触发，一级一级往下传递，依次触发，直到真正事件目标为止。

### 事件冒泡

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <style type="text/css">
        #box1 { width: 300px; height: 300px; background: blueviolet; }
        #box2 { width: 200px; height: 200px; background: aquamarine; }
        #box3 { width: 100px; height: 100px; background: tomato; }
        div { overflow: hidden; margin: 50px auto; }
    </style>
    <body>
        <div id="box1">
            <div id="box2">
                <div id="box3"></div>
            </div>
        </div>
        <script>
            function sayBox3() {
                console.log('你点了最里面的box');
            }
            function sayBox2() {
                console.log('你点了最中间的box');
            }
            function sayBox1() {
                console.log('你点了最外面的box');
            }
            // 事件监听，第三个参数是布尔值，默认false，false是事件冒泡，true是事件捕获
            document.getElementById('box3').addEventListener('click', sayBox3, false);
            document.getElementById('box2').addEventListener('click', sayBox2, false);
            document.getElementById('box1').addEventListener('click', sayBox1, false);

        </script>
    </body>
</html>
```

![JS事件冒泡](/images/posts/js事件流/JS事件冒泡.png)

我们发现，我们仅仅是点击了红色的box，但是绿色和紫色的box也被触发了打印事件，触犯顺序是 红色>绿色>紫色，这种现象就是事件冒泡了。



### 事件捕获

我们再试试事件捕获，把上面代码里监听事件的第三个参数改为true，然后点击红色的box：

![JS事件捕获](/images/posts/js事件流/JS事件捕获.png)

我们还是只点击最中间的红色box，和上一次一样，也是三个box都触发了事件，但是顺序反过来了，紫色>绿色>红色，这种现象称为事件捕获。

通过上面的例子，应该很容易就理解了事件冒泡和事件捕获，我们平时都是默认冒泡的，冒泡是一直冒到document根文档为止。



### 事件委托

所谓的事件委托，通过监听一个父元素，来给不同的子元素绑定事件，减少监听次数，从而提升速度。



```
<body>
    <ul id="isUl">
        <li id="li01">1</li>
        <li id="li02">2</li>
        <li id="li03">3</li>
    </ul>
    <script>
        function clickLi01() {
            alert('你点击了第1个li');
        }
        function clickLi02() {
            alert('你点击了第2个li');
        }
        function clickLi03() {
            alert('你点击了第3个li');
        }
        document.getElementById('isUl').addEventListener('click', function(event) {
            var srcID = event.target.id;
            if(srcID == 'li01'){
                clickLi01();
            }else if(srcID == 'li02') {
                clickLi02();
            }else if(srcID == 'li03') {
                clickLi03();
            }
        });
    </script>
</body>
```

这样我们就通过给ul绑定一个点击事件，让所有的li都触发了函数。
那如果想给不同的li绑定不同的函数怎么办？
假设有3个li，我们先写3个不同的函数，再给3个li设置不同的id名，通过判断id名是不是就能给不同的li绑定不同的函数



## 阻止事件冒泡

**停止冒泡行为**

```
event.stopPropagation();
window.event.cancelBubble = true;  // IE 浏览器
```



## 阻止默认事件

**return false**

```
<body>
    
<div id='div'  onclick='alert("div");'>
<ul  onclick='alert("ul");'>
<li id='ul-a' onclick='alert("li");'><a href="http://caibaojian.com/"id="testB">caibaojian.com</a></li>
</ul>
</div>
<script>
var a = document.getElementById("testB");
a.onclick = function(){
return false;
};
</script>
</body>
```



**ev.preventDefault();**