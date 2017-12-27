# HTML事件

### Window 事件属性

针对 window 对象触发的事件（应用到 `<body>`标签）：

#### onafterprint事件 ——Html5新增

文档打印之后运行的脚本。（**提示：**onafterprint 属性常与 onbeforeprint 属性一同使用。）

```
<body onafterprint="printmsg()">
```
**浏览器支持** 

只有 Internet Explorer 和 Firefox 支持 onafterprint 事件属性。

**注释：**在 IE 中，onafterprint 属性在打印对话框出现之前而不是之后发生。


#### onbeforeprint事件 ——Html5新增   

文档打印之前运行的脚本。（**提示：**onbeforeprint 属性常与 onafterprint 属性一同使用。）

```
<body onbeforeprint="printmsg()">
```
**浏览器支持** 

只有 Internet Explorer 和 Firefox 支持 onbeforeprint 事件属性。

#### onbeforeunload事件 ——Html5新增   

文档卸载之前运行的脚本。(关闭浏览器窗口,通过地址栏或收藏夹前往其他页面的时候,点击返回，前进，刷新，主页其中一个的时候,点击 一个前往其他页面的url连接的时候,调用以下任意一个事件的时候：click，document write，document open，document close，window close ，window navigate ，window NavigateAndFind,location replace,location reload,form submit.  )

```
<body onbeforeunload="return fn()">
<script>
function fn(){
    event.returnValue="确定离开当前页面吗？"; //只能使用 event.returnValue 返回，否则无效

}
</script>
```
**浏览器支持** 

chrome , IE , Firefox , safari 都支持,opera 15.0支持

#### onerror事件 ——Html5新增   

onerror 事件会在**文档**或**图像**加载过程中发生错误时被触发。

```
<img src="image.gif" onerror="alert('The image could not be loaded.')" />
```

* 支持该事件的 HTML 标签： `<img>, <object>, <style>`      
* 支持该事件的 JavaScript 对象： `window, image`     


#### onhaschange事件 ——Html5新增   

onhashchange 事件在当前 URL 的锚部分(以 '#' 号为开始) 发生改变时触发 。

```
//在 HTML 中:
<body onhashchange="funcRef()">
//在 JavaScript 中:
window.onhashchange = funcRef;
//为了将一个事件侦听器添加到现有的一个事件处理程序集中，使用函数 "addEventListener"。
window.addEventListener("hashchange", funcRef, false);
```
你可以使用以下方式调用事件:
* 通过设置Location 对象 的 location.hash 或 location.href 属性修改锚部分。
* 使用不同书签导航到当前页面（使用"后退" 或"前进"按钮）
* 点击链接跳转到书签锚

#### onload事件    

onload 事件会在页面或图像加载完成后立即发生。    
onload 常用在 `<body>` 中，一旦完全加载所有内容（包括图像、脚本文件、CSS 文件等），就执行一段脚本。      
 
```
//在 HTML 中:
<body onload="SomeJavaScriptCode">
//在 JavaScript 中:
window.onload=function(){SomeJavaScriptCode};

```
* 支持该事件的 HTML 标签：`<body>, <frame>, <frameset>, <iframe>, <img>,<link>,<script>,<style>, <input type="image"> `

* 支持该事件的 JavaScript 对象：`image, layer, window`

#### onmessage事件  ——Html5新增   

该事件通过或者从对象(WebSocket, Web Worker, Event Source 或者子 frame 或父窗口)接收到消息时触发

```
//首先，需要在客户端页面的 JavaScript 代码中 new 一个 Worker 实例出来，
//参数是需要在另一个线程中运行的 JavaScript 文件名称。然后在这个实例上监听 onmessage 事件。
//最后另一个线程中的 JavaScript 就可以通过调用 postMessage 方法在这两个线程间传递数据了。
 function init(){ 
        var worker = new Worker('compute.js'); 
        //event 参数中有 data 属性，就是子线程中返回的结果数据
        worker.onmessage= function (event) { 
            // 把子线程返回的结果添加到 div 上
            document.getElementById("result").innerHTML += 
               event.data+"<br/>"; 
        }; 
    } 
  init();       
// compute.js 
var i=0; 
function timedCount(){ 
    for(var j=0,sum=0;j<100;j++){ 
        for(var i=0;i<100000000;i++){ 
            sum+=i; 
        } 
    } 
    // 调用 postMessage 向主线程发送消息
    postMessage(sum); 
} 
postMessage("Before computing,"+new Date()); 
timedCount(); 
postMessage("After computing,"+new Date());

```

#### onoffline事件 ——Html5新增    

onoffline 事件在浏览器离线工作时触发

提示： 
  * onoffline 事件的相反事件是 ononline 。
  * 你同样可以使用 navigator.onLine 属性来擦可能浏览器是否是在线或离线模式。

```
<body onoffline="myFunction()">
```
**浏览器支持**：只有火狐支持

#### ononline事件 ——Html5新增   

ononline 事件在浏览器开始在线工作时触发。

提示： 
  * ononline 的相反的事件为 onoffline 事件。
  *	你同样可以使用 navigator.onLine 属性来擦可能浏览器是否是在线或离线模式。

```
<body ononline="myFunction()">
```
**浏览器支持**：只有火狐支持

#### onpagehide事件 ——Html5新增 

onpagehide 事件在用户离开网页时触发。离开网页有多种方式。如点击一个链接，刷新页面，提交表单，关闭浏览器等。     
onpagehide 事件有时可以替代 onunload 事件，但 onunload 事件触发后无法缓存页面。      
为了查看页面是直接从服务器上载入还是从缓存中读取，你可以使用 PageTransitionEvent 对象的 persisted 属性来判断。 如果页面从浏览器的缓存中读取该属性返回 ture，否则返回 false 。
```
<body onpagehide="myFunction()">
```

#### onpageshow事件 ——Html5新增 

onpageshow 事件在用户浏览网页时触发。       
onpageshow 事件类似于 onload 事件，onload 事件在页面第一次加载时触发， onpageshow 事件在每次加载页面时触发，即 onload 事件在页面从浏览器缓存中读取时不触发。       
为了查看页面是直接从服务器上载入还是从缓存中读取，你可以使用 PageTransitionEvent 对象的 persisted 属性来判断。 如果页面从浏览器的缓存中读取该属性返回 ture，否则返回 false 。    

```
<body onpageshow="myFunction()">
```
**浏览器兼容**：IE 11.0+支持，Safari 5.0+支持，其他主流浏览器支持


#### onpopstate事件 ——Html5新增 

当窗口历史记录改变时运行的脚本
每当处于激活状态的历史记录条目发生变化时,popstate事件就会在对应window对象上触发. 如果当前处于激活状态的历史记录条目是由history.pushState()方法创建,或者由history.replaceState()方法修改过的, 则popstate事件对象的state属性包含了这个历史记录条目的state对象的一个拷贝.

调用history.pushState()或者history.replaceState()不会触发popstate事件. popstate事件只会在浏览器某些行为下触发, 比如点击后退、前进按钮(或者在JavaScript中调用history.back()、history.forward()、history.go()方法).

当网页加载时,各浏览器对popstate事件是否触发有不同的表现,Chrome 和 Safari会触发popstate事件, 而Firefox不会.

```
window.onpopstate = funcRef;
```

#### onredo事件 ——Html5新增 

当文档执行撤销（redo）时运行的脚本。

<span style="color:red">未找到</span>


#### onresize事件 ——Html5新增 

onresize 发生于对象被调整大小时。    
onresize 常用于 浏览器窗口被调整尺寸时    


```
<element onresize="script">
```

**浏览器支持**：所有主流浏览器都支持。


#### onstorage事件 ——Html5新增 

在 Web Storage 区域更新后运行的脚本。    

web存储区域（DOM Storage）更新时触发onstorage事件。如果变更了Storage对象的属性值，或者调用了setItem()、removeItem()等方法，就会触发onstorage事件。

StorageEvent对象的属性：
  * key：表示项目的key发生了变化；该属性返回其初始化的值，创建对象后，该值被初始化为null。
  * oldValue:表示变更前的值
  * newValue:变更后的值
  * url:事件触发源的URL
  * source:事件触发源的URL
  * storageArea:受到影响的storage对象

**是否支持冒泡**：否


#### onundo事件 ——Html5新增

在文档执行 undo 时运行的脚本。

<span style="color:red">未找到</span>


#### onunload事件 

onunload 属性会在页面下载时触发（或者浏览器窗口已关闭）。     
onunload 在用户从页面导航离开时发生（通过点击链接、提交表单或者关闭浏览器窗口等等）  
**注释**：如果您重载页面，也会触发 unload 事件（以及 onload 事件）。   


```
<element onunload="script">
```

**浏览器支持**：所有主流浏览器都支持。




### Form 事件属性


#### onblur事件 

元素失去焦点时运行的脚本。

onblur 属性在元素失去焦点时触发。
onblur 常用于表单验证代码（例如用户离开表单字段）。

```
<input type="text"  onblur="upperCase()">
```


**浏览器支持**：所有主流浏览器都支持。


#### onfocus事件

onfocus 事件在对象获得焦点时发生。   
onfocus 通常用于 `<input>`, `<select>`, 和`<a>`.   

```
<element onchange="script">
```


**浏览器支持**：所有主流浏览器都支持。



#### onchange事件

onchange 事件会在域的内容改变时发生。   
onchange 事件也可用于单选框与复选框改变后触发的事件。   
onchange 属性适用于：`<input>`、`<textarea>` 以及 `<select> `元素。     

```
<element onchange="script">
```


**浏览器支持**：所有主流浏览器都支持。



#### oncontextmenu事件 ——Html5新增

oncontextmenu 事件在元素中用户右击鼠标时触发并打开上下文菜单。  

**注意**：所有浏览器都支持 oncontextmenu 事件， contextmenu 元素只有 Firefox 浏览器支持。  

```
<element oncontextmenu="myScript">
```

**浏览器支持**：所有主流浏览器都支持。

**是否支持冒泡**：是


#### onformchange事件 ——Html5新增

在表单改变时运行的脚本。 

<span style="color:red">未找到</span>


#### onforminput事件 ——Html5新增

当表单获得用户输入时运行的脚本。

<span style="color:red">未找到</span>


#### oninput事件 ——Html5新增

oninput 事件在用户输入时触发。
该事件在 `<input> `或 `<textarea>` 元素的值发生改变时触发。

**提示**： 该事件类似于 onchange 事件。不同之处在于 oninput 事件在元素值发生变化是立即触发， onchange 在元素失去焦点时触发。另外一点不同是 onchange 事件也可以作用于` <keygen>` 和 `<select>` 元素。

```
<element oninput="myScript">
```

**浏览器支持**：所有主流浏览器都支持。    

**是否支持冒泡**：是


#### oninvalid事件 ——Html5新增

提交的input元素的值为无效值时，触发oninvalid事件。

```
<element oninvalid="myScript">
```

**浏览器支持**：IE 10.0 ,Chrome 支持,Firefox 4.0, Safai 不支持,Opera 支持 

**是否支持冒泡**：否


#### onreset事件

onreset 事件在表单被重置后触发。

```
<element onreset="myScript">
```

**浏览器支持**：所有主流浏览器都支持。

**是否支持冒泡**：是

####  onselect事件

onselect 属性在元素中的文本被选中时触发。    
onselect 属性可用于以下元素内：`<input type="file">`、`<input type="password">`、`<input type="text">`、`<keygen>` 以及 `<textarea>`.

```
<element onselect="myScript">
```

**浏览器支持**：所有主流浏览器都支持。


####  onsubmit事件

onsubmit 属性在提交表单时触发。    
onsubmit 属性只在 `<form>` 中使用。

```
<form onsubmit="script">
```

**浏览器支持**：所有主流浏览器都支持。



### Keyboard 事件


####  onkeydown事件

onkeydown 属性在用户（在键盘上）按键时触发    
```
<element onkeydown="script">
```

**注释**：onkeydown 属性不适用以下元素：`<base>`、`<bdo>`、`<br>`、`<head>`、`<html>`、`<iframe>`、`<meta>`、`<param>`、`<script>`、`<style>` 或 `<title>`    

**提示**：相对于 onkeydown 事件的事件次序：
`onkeydown onkeypress onkeyup `   

**浏览器支持**：所有主流浏览器都支持。


####  onkeypress事件

onkeypress 属性在用户（在键盘上）按键时触发。   
```
<element onkeypress="script">
```

**注释** onkeypress 属性不适用以下元素：`<base>`、`<bdo>`、`<br>`、`<head>`、`<html>`、`<iframe>`、`<meta>`、`<param>`、`<script>`、`<style>` 或 `<title>`    

**提示**：相对于 onkeypress 事件的事件次序：
`onkeydown onkeypress onkeyup ` 

**注意**： 在所有浏览器中 onkeypress 事件不是适用于所有按键(如： ALT, CTRL, SHIFT, ESC)。监听一个用户是否按下按键请使用 onkeydown 事件,所有浏览器都支持 onkeydown 事件。     

**浏览器支持**：所有主流浏览器都支持。


####  onkeyup事件

onkeyup 事件会在键盘按键被松开时发生。  

```
<element onkeyup="script">
```
**注释** ：onkeyup 属性不适用以下元素：`<base>`、`<bdo>`、`<br>`、`<head>`、`<html>`、`<iframe>`、`<meta>`、`<param>`、`<script>`、`<style>` 或 `<title>` 

**提示**：相对于 onkeyup 事件的事件次序：
`onkeydown onkeypress onkeyup `    


**浏览器支持**：所有主流浏览器都支持。



### Mouse 事件

####  onclick事件

onclick 事件会在元素被点击时发生。  

```
<element onclick="script">
```

**注释**：onclick 属性不适用以下元素：`<base>`、`<bdo>`、`<br>`、`<head>`、`<html>`、`<iframe>`、`<meta>`、`<param>`、`<script>`、`<style>` 或 `<title>` 。

**浏览器支持**：所有主流浏览器都支持。


####  ondblclick事件

ondblclick 属性在鼠标双击元素时触发。

```
<element ondblclick="script">
```

**注释**：ondblclick 属性不适用以下元素：`<base>`、`<bdo>`、`<br>`、`<head>`、`<html>`、`<iframe>`、`<meta>`、`<param>`、`<script>`、`<style>` 或 `<title>` 。

**浏览器支持**：所有主流浏览器都支持。


#### ondrag事件 ——Html5新增

ondrag 事件在元素或者选取的文本被拖动时触发。

```
<element ondrag="myScript">
```

**注意**： 为了让元素可拖动，需要使用 HTML5 draggable 属性。

**提示**： 链接和图片默认是可拖动的，不需要 draggable 属性。

在拖放的过程中会触发以下事件：
  * 在拖动目标上触发事件 (源元素):
      * ondragstart - 用户开始拖动元素时触发
      * ondrag - 元素正在拖动时触发
      * ondragend - 用户完成元素拖动后触发

  * 释放目标时触发的事件:
      * ondragenter - 当被鼠标拖动的对象进入其容器范围内时触发此事件
      * ondragover - 当某被拖动的对象在另一对象容器范围内拖动时触发此事件
      * ondragleave - 当被鼠标拖动的对象离开其容器范围内时触发此事件
      * ondrop - 在一个拖动过程中，释放鼠标键时触发此事件

**注意**： 在拖动元素时，每隔 350 毫秒会触发 ondrag 事件。

**浏览器支持**：IE 9.0 ,Chrome 4.0,Firefox 3.5, Safai 6.0,Opera 12.0

**是否支持冒泡**：是



#### ondragend事件 ——Html5新增

ondragend 事件在用户完成元素或首选文本的拖动时触发。

```
<element ondragend="myScript">
```
**注意**： 为了让元素可拖动，需要使用 HTML5 draggable 属性。
**提示**： 链接和图片默认是可拖动的，不需要 draggable 属性。    
在拖放的过程中会触发以下事件：
  * 在拖动目标上触发事件 (源元素):
      * ondragstart - 用户开始拖动元素时触发
      * ondrag - 元素正在拖动时触发
      * ondragend - 用户完成元素拖动后触发

  * 释放目标时触发的事件:
      * ondragenter - 当被鼠标拖动的对象进入其容器范围内时触发此事件
      * ondragover - 当某被拖动的对象在另一对象容器范围内拖动时触发此事件
      * ondragleave - 当被鼠标拖动的对象离开其容器范围内时触发此事件
      * ondrop - 在一个拖动过程中，释放鼠标键时触发此事件

**浏览器支持**：IE 9.0 ,Chrome 4.0,Firefox 3.5, Safai 6.0,Opera 12.0

**是否支持冒泡**：是


#### ondragenter事件 ——Html5新增

ondragenter 事件在拖动的元素或选择的文本进入到有效的放置目标时触发。   
ondragenter 和 ondragleave 事件可以帮助用户更好的理解可拖动元素进入和离开放置区域的过程。 你可以在可拖动元素进入和离开放置区域时设置不同的背景颜色。    

```
<element ondragenter="myScript">
```
**注意**： 为了让元素可拖动，需要使用 HTML5 draggable 属性。
**提示**： 链接和图片默认是可拖动的，不需要 draggable 属性。    
在拖放的过程中会触发以下事件：
  * 在拖动目标上触发事件 (源元素):
      * ondragstart - 用户开始拖动元素时触发
      * ondrag - 元素正在拖动时触发
      * ondragend - 用户完成元素拖动后触发

  * 释放目标时触发的事件:
      * ondragenter - 当被鼠标拖动的对象进入其容器范围内时触发此事件
      * ondragover - 当某被拖动的对象在另一对象容器范围内拖动时触发此事件
      * ondragleave - 当被鼠标拖动的对象离开其容器范围内时触发此事件
      * ondrop - 在一个拖动过程中，释放鼠标键时触发此事件

**浏览器支持**：IE 9.0 ,Chrome 4.0,Firefox 3.5, Safai 6.0,Opera 12.0

**是否支持冒泡**：是


####  ondragleave事件 ——Html5新增

ondragleave 事件在可拖动的元素或选取的文本移出放置目标时执触发。   
ondragenter 和 ondragleave 事件可以帮助用户更好的理解可拖动元素进入和离开放置区域的过程。 你可以在可拖动元素进入和离开放置区域时设置不同的背景颜色。

```
<element ondragleave="myScript">
```
**注意**： 为了让元素可拖动，需要使用 HTML5 draggable 属性。
**提示**： 链接和图片默认是可拖动的，不需要 draggable 属性。    
在拖放的过程中会触发以下事件：
  * 在拖动目标上触发事件 (源元素):
      * ondragstart - 用户开始拖动元素时触发
      * ondrag - 元素正在拖动时触发
      * ondragend - 用户完成元素拖动后触发

  * 释放目标时触发的事件:
      * ondragenter - 当被鼠标拖动的对象进入其容器范围内时触发此事件
      * ondragover - 当某被拖动的对象在另一对象容器范围内拖动时触发此事件
      * ondragleave - 当被鼠标拖动的对象离开其容器范围内时触发此事件
      * ondrop - 在一个拖动过程中，释放鼠标键时触发此事件

**浏览器支持**：IE 9.0 ,Chrome 4.0,Firefox 3.5, Safai 6.0,Opera 12.0

**是否支持冒泡**：是




#### ondragover事件 ——Html5新增

ondragover 事件在可拖动元素或选取的文本正在拖动到放置目标时触发。    
默认情况下，数据/元素不能放置到其他元素中。 如果要实现改功能，我们需要防止元素的默认处理方法。我们可以通过调用 event.preventDefault() 方法来实现 ondragover 事件。

```
<element ondragover="myScript">
```
**注意**： 为了让元素可拖动，需要使用 HTML5 draggable 属性。
**提示**： 链接和图片默认是可拖动的，不需要 draggable 属性。    
在拖放的过程中会触发以下事件：
  * 在拖动目标上触发事件 (源元素):
      * ondragstart - 用户开始拖动元素时触发
      * ondrag - 元素正在拖动时触发
      * ondragend - 用户完成元素拖动后触发

  * 释放目标时触发的事件:
      * ondragenter - 当被鼠标拖动的对象进入其容器范围内时触发此事件
      * ondragover - 当某被拖动的对象在另一对象容器范围内拖动时触发此事件
      * ondragleave - 当被鼠标拖动的对象离开其容器范围内时触发此事件
      * ondrop - 在一个拖动过程中，释放鼠标键时触发此事件

**浏览器支持**：IE 9.0 ,Chrome 4.0,Firefox 3.5, Safai 6.0,Opera 12.0

**是否支持冒泡**：是



#### ondragstart事件 ——Html5新增

ondragstart 事件在用户开始拖动元素或选择的文本时触发。

```
<element ondragstart="myScript">
```
**注意**： 为了让元素可拖动，需要使用 HTML5 draggable 属性。
**提示**： 链接和图片默认是可拖动的，不需要 draggable 属性。    
在拖放的过程中会触发以下事件：
  * 在拖动目标上触发事件 (源元素):
      * ondragstart - 用户开始拖动元素时触发
      * ondrag - 元素正在拖动时触发
      * ondragend - 用户完成元素拖动后触发

  * 释放目标时触发的事件:
      * ondragenter - 当被鼠标拖动的对象进入其容器范围内时触发此事件
      * ondragover - 当某被拖动的对象在另一对象容器范围内拖动时触发此事件
      * ondragleave - 当被鼠标拖动的对象离开其容器范围内时触发此事件
      * ondrop - 在一个拖动过程中，释放鼠标键时触发此事件

**浏览器支持**：IE 9.0 ,Chrome 4.0,Firefox 3.5, Safai 6.0,Opera 12.0

**是否支持冒泡**：是



#### ondrop事件 ——Html5新增

ondrop 事件在可拖动元素或选取的文本放置在目标区域时触发。    

```
<element ondragstart="myScript">
```
**注意**： 为了让元素可拖动，需要使用 HTML5 draggable 属性。
**提示**： 链接和图片默认是可拖动的，不需要 draggable 属性。    
在拖放的过程中会触发以下事件：
  * 在拖动目标上触发事件 (源元素):
      * ondragstart - 用户开始拖动元素时触发
      * ondrag - 元素正在拖动时触发
      * ondragend - 用户完成元素拖动后触发

  * 释放目标时触发的事件:
      * ondragenter - 当被鼠标拖动的对象进入其容器范围内时触发此事件
      * ondragover - 当某被拖动的对象在另一对象容器范围内拖动时触发此事件
      * ondragleave - 当被鼠标拖动的对象离开其容器范围内时触发此事件
      * ondrop - 在一个拖动过程中，释放鼠标键时触发此事件

**浏览器支持**：IE 9.0 ,Chrome 4.0,Firefox 3.5, Safai 6.0,Opera 12.0

**是否支持冒泡**：是



#### onmousedown事件

onmousedown 事件会在鼠标按键被按下时发生。
```
<element onmousedown="myScript">
``` 

**提示**：      
与 onmousedown 事件相关连得事件发生次序（ 鼠标左侧/中间 按钮）：   
  * onmousedown
  * onmouseup
  * onclick

与 onmousedown 事件相关连得事件发生次序 (鼠标右侧按钮):
  * onmousedown
  * onmouseup
  * oncontextmenu

注释：onmousedown 属性不适用以下元素：   
`<base>`、`<bdo>`、`<br>`、`<head>`、`<html>`、`<iframe>`、`<meta>`、`<param>`、`<script>`、`<style>` 或 `<title>`。

**浏览器支持**：所有主流浏览器都支持。


#### onmousemove事件

onmousemove 事件会在鼠标指针移到指定的对象时发生。

```
<element onmousemove="myScript">
``` 

注释：onmousemove 属性不适用以下元素：   
`<base>`、`<bdo>`、`<br>`、`<head>`、`<html>`、`<iframe>`、`<meta>`、`<param>`、`<script>`、`<style>` 或 `<title>`。

**浏览器支持**：所有主流浏览器都支持。


#### onmouseout事件

onmouseout 事件会在鼠标指针移出指定的对象时发生。

```
<element onmouseout="myScript">
``` 

注释：onmouseout 属性不适用以下元素：   
`<base>`、`<bdo>`、`<br>`、`<head>`、`<html>`、`<iframe>`、`<meta>`、`<param>`、`<script>`、`<style>` 或 `<title>`。

**浏览器支持**：所有主流浏览器都支持。


#### onmouseover事件

onmouseover 事件会在鼠标指针移动到指定的元素上时发生。

```
<element onmouseover="myScript">
``` 

注释：onmouseover 属性不适用以下元素：   
`<base>`、`<bdo>`、`<br>`、`<head>`、`<html>`、`<iframe>`、`<meta>`、`<param>`、`<script>`、`<style>` 或 `<title>`。

**浏览器支持**：所有主流浏览器都支持。



#### onmouseup事件

onmouseup 事件会在鼠标按键被松开时发生。   

```
<element onmouseup="myScript">
``` 
**提示**：      
与 onmouseup 事件相关联的事件触发次序（ 鼠标左侧/中间 按钮）：   
  * onmousedown
  * onmouseup
  * onclick

与 onmouseup 事件相关联的事件触发次序 (鼠标右侧按钮):
  * onmousedown
  * onmouseup
  * oncontextmenu

注释：onmouseup 属性不适用以下元素：   
`<base>`、`<bdo>`、`<br>`、`<head>`、`<html>`、`<iframe>`、`<meta>`、`<param>`、`<script>`、`<style>` 或 `<title>`。

**浏览器支持**：所有主流浏览器都支持。



#### onmousewheel事件 ——Html5新增

nmousewheel 当鼠标滚轮正在被滚动时运行的脚本

<span style="color:red">未找到</span>



#### onscroll事件 ——Html5新增

onscroll 事件在元素滚动条在滚动时触发。   

```
<element onscroll="myScript">
```

**浏览器支持**：所有主流浏览器都支持。

**是否支持冒泡**：是



### Media 事件


#### onabort 事件

onabort 事件在视频/音频（audio/video）终止加载时触发。    
该事件在多媒体数据终止加载时触发，而不是发生错误时触发。    
```
<video onabort="myFunction()">
```
**提示**： 影响多媒体加载的事件有:     
     
  * onemptied
  * onerror
  * onstalled
  * onsuspend

**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。     
**注意**： Windows 7下的 Internet Explorer 11 浏览器不支持 onabort 事件。

**是否支持冒泡**：否


#### oncanplay事件 ——Html5新增

oncanplay 事件在用户可以开始播放视频/音频（audio/video）时触发。 
```
<video oncanplay="myFunction()">
```   
在视频/音频（audio/video）加载过程中，事件的触发顺序如下：     
  * onloadstart
  * ondurationchange
  * onloadedmetadata
  * onloadeddata
  * onprogress
  * oncanplay
  * oncanplaythrough

**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。

**是否支持冒泡**：否


#### oncanplaythrough事件 ——Html5新增

oncanplaythrough 事件在视频/音频（audio/video）可以正常播放且无需停顿和缓冲时触发。      
```
<video oncanplaythrough="myFunction()">
```   
在视频/音频（audio/video）加载过程中，事件的触发顺序如下：     
  * onloadstart
  * ondurationchange
  * onloadedmetadata
  * onloadeddata
  * onprogress
  * oncanplay
  * oncanplaythrough

**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。

**是否支持冒泡**：否


#### ondurationchange事件 ——Html5新增

ondurationchange 事件在视频/音频（audio/video）的时长发生变化时触发。

**注意**： 当视频/音频（audio/video）已经加载后，视频/音频（audio/video）的时长从 "NaN" 修改为正在的时长。          
```
<video ondurationchange="myFunction()">
```   
在视频/音频（audio/video）加载过程中，事件的触发顺序如下：     
  * onloadstart
  * ondurationchange
  * onloadedmetadata
  * onloadeddata
  * onprogress
  * oncanplay
  * oncanplaythrough

**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。

**是否支持冒泡**：否


#### onemptied事件 ——Html5新增

当发生故障并且文件突然不可用时运行的脚本（比如连接意外断开时）。

<span style="color:red">未找到</span>


#### onended事件 ——Html5新增

onended 事件在视频/音频（audio/video）播放结束时触发。    
该事件通常用于送类似"感谢观看"之类的消息。   

```
<audio onended="myFunction()">
```
**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。 

**是否支持冒泡**：否


#### onerror事件 ——Html5新增

onerror 事件在视频/音频（audio/video）数据加载期间发生错误时触发。   

```
<audio onerror="myFunction()">
```
**提示**： 影响媒体数据加载的相关事件有：   
  * onabort
  * onemptied
  * onstalled
  * onsuspend

**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。        
**注意**： Windows 7 下的 Internet Explorer 11 不支持 onerror 事件。   
**是否支持冒泡**：否


#### onloadeddata事件 ——Html5新增

onloadeddata 事件在当前帧的数据加载完成且还没有足够的数据播放视频/音频（audio/video）的下一帧时触发。 
```
<video onloadeddata="myFunction()">
``` 
在加载视频/音频（audio/video），事件的触发顺序如下：     
  * onloadstart
  * ondurationchange
  * onloadedmetadata
  * onloadeddata
  * onprogress
  * oncanplay
  * oncanplaythrough

**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。     
**是否支持冒泡**：否   


#### onloadedmetadata事件 ——Html5新增

onloadedmetadata 事件在指定视频/音频（audio/video）的元数据加载后触发。  
视频/音频（audio/video）的元数据包含: 时长，尺寸大小（视频），文本轨道。

```
<video onloadedmetadata="myFunction()">
``` 
视频/音频（audio/video）在加载过程中，触发的顺序如下：    
  * onloadstart
  * ondurationchange
  * onloadedmetadata
  * onloadeddata
  * onprogress
  * oncanplay
  * oncanplaythrough

**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。     
**是否支持冒泡**：否 


#### onloadstart事件 ——Html5新增

onloadstart 事件在浏览器开始寻找指定视频/音频（audio/video）触发。    
```
<video onloadstart="myFunction()">
```
视频/音频（audio/video）在加载过程中，触发的顺序如下：    
  * onloadstart
  * ondurationchange
  * onloadedmetadata
  * onloadeddata
  * onprogress
  * oncanplay
  * oncanplaythrough

**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。     
**是否支持冒泡**：否 


#### onpause事件 ——Html5新增

onpause 事件在视频/音频（audio/video）暂停时触发。

**提示**： onplay 事件在视频/音频（audio/video）开始播放时触发。

```
<video onpause="myFunction()">
```
**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。     
**是否支持冒泡**：否 


#### onplay事件 ——Html5新增

onplay 事件在视频/音频（audio/video）开始播放时触发。

**提示**：onpause 事件在视频/音频（audio/video）暂停时触发。。

```
<video onplay="myFunction()">
```
**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。     
**是否支持冒泡**：否 


#### onplaying事件 ——Html5新增

onplaying 事件在视频/音频（audio/video）暂停或者在缓冲后准备重新开始播放时触发。    
```
<video onplaying="myFunction()">
```
**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。     
**是否支持冒泡**：否 



#### onprogress事件 ——Html5新增

onprogress 事件在浏览器下载指定的视频/音频（audio/video）时触发。       
```
<video onprogress="myFunction()">
```
在下载视频/音频（audio/video）过程中，事件触发的顺序如下：    
  * onloadstart
  * ondurationchange
  * onloadedmetadata
  * onloadeddata
  * onprogress
  * oncanplay
  * oncanplaythrough

**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。     
**是否支持冒泡**：否 


#### onratechange事件 ——Html5新增

onratechange 事件在视频/音频（audio/video）的播放速度发生改变时触发。 
```
<video onratechange="myFunction()">
```
该事件通过 Audio/Video 对象的 playbackRate属性调用, 该属性用于设置或返回视频/音频（audio/video）的当前播放速度   

**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。     
**是否支持冒泡**：否 


#### onreadystatechange事件 ——Html5新增

每当就绪状态改变时运行的脚本（就绪状态监测媒介数据的状态）。

<span style="color:red">未找到</span>


#### onseeked事件 ——Html5新增

onseeked 事件在用户重新定位视频/音频（audio/video）的播放位置后触发。  

```
<video onseeked="myFunction()">
```

**提示**： 与 onseeked 事件相反的是 onseeking 事件。    
**提示**： 使用 currentTime 可以设置或返回视频/音频（audio/video）播放的当前位置 。   

**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。     
**是否支持冒泡**：否 


#### onseeking事件 ——Html5新增

onseeking 事件在用户开始重新定位视频/音频（audio/video）时触发。
```
<video onseeking="myFunction()">
```
**提示**：与 onseeking 事件相反的是 onseeked 事件。    
**提示**： 使用 currentTime 可以设置或返回视频/音频（audio/video）播放的当前位置 。       
**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。     
**是否支持冒泡**：否 


#### onstalled事件 ——Html5新增

onstalled 事件在浏览器获取媒体数据，但媒体数据不可用时触发。     
```
<video onstalled="myFunction()">
```
**提示**： 影响媒体加载的事件有：     
  * onabort
  * onemptied
  * onerror
  * onsuspend

**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。     
**是否支持冒泡**：否 


#### onsuspend事件 ——Html5新增

onsuspend 事件在浏览器读取媒体数据中止时触发。    
```
<video onsuspend="myFunction()">
```
**提示**： 影响媒体加载的事件有：   
  * onabort
  * onemptied
  * onerror
  * onstalled

**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。     
**是否支持冒泡**：否 


#### ontimeupdate事件 ——Html5新增

ontimeupdate 事件在视频/音频（audio/video）当前的播放位置发送改变时触发。     

该事件通过以下方式调用：    
  * 播放视频/音频（audio/video）
  * 重新定位视频/音频（audio/video）的播放位置。
```
<video ontimeupdate="myFunction()">
```
**提示**： 该事件通常与 Video 对象的 currentTime 属性一起使用， 该属性返回视频/音频（audio/video）的当前播放位置。    

**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。     
**是否支持冒泡**：否 


#### onvolumechange事件 ——Html5新增

onvolumechange 事件在视频/音频（audio/video）的音量发生改变时触发。   
该事件可以通过以下方式调用：    
  * 增大或降低音量
  * 媒体播放器静音或解除静音

```
<video onvolumechange="myFunction()">
```
**提示**： 使用 Audio 或 Video 对象的 volume 属性来设置或返回视频/音频（audio/video）的音量。

**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。     
**是否支持冒泡**：否 


#### onwaiting事件 

onwaiting 事件在视频由于要播放下一帧而需要缓冲时触发。   

该事件可用于 `<audio>` 元素，但通常应用在视频（`<video>` 元素）播放中。  
```
<video onwaiting="myFunction()">
```

**浏览器支持**：除IE外的所有主流浏览器都支持，IE 9.0及以上支持。     
**是否支持冒泡**：否 






