# 回流(重排)(reflows)&重绘(repaints)
##一、HTML 布局
HTML使用流式布局模型（flow based layout）， 这意味着多数情况下一次扫描就可以计算所有的图形显示。 处于流后面的元素一般不会影响前面元素的图形， 所以布局过程可以从左到右、从上到下来进行。

所有的HTML回流都是从根frame开始（HTML标签）的，递归地处理部分或全部子frame。 回流过程中也可能创建新的frame，比如文本发生了换行。 一个frame的回流会导致它的所有父节点以及所有后续元素的回流。

有些HTML回流是立即执行的（immediate to user or script）并且会影响整个frame树， 比如窗口大小变化、更改文档的默认字体；有些HTML回流则是异步的、渐进的（incremental）， 比如更多的文档流从网络中到达，这些渐进的回流可以入队列进行批量处理。

##二、回流的原因
浏览器在实现回流时，会递归地处理frame。 每个frame的回流都有一个原因， 这个原因会随着frame逐级向下传递（传递过程中可能会改变）。 回流的原因决定了当前frame的回流行为，有这样5种原因：

1、初始化（Initial）。DOM载入后的第一次回流，将会遍历所有frame。

2、渐进（Incremental）。当一个frame发生渐进回流时，意味着它前面的元素都没有变， 而是它里面的元素变了。这会引起自底向上的作用。

3、改变大小（Resize）。元素的容器边界发生变化时，此时元素内部状态没变。 在计算自顶向下的布局约束的同时，可以复用内部状态。

4、样式改变（StyleChange）。整个frame树都应得到遍历。

5、Dirty。当一个容器已经缓存了多个子元素的Incremental回流时，该容器出于Dirty的状态。

前面四种原因的回流都是在Presentation Shell中立即调用的， 而最后一种回流只有Incremental回流已经到达目标frame时才进行。 （因为这时自底向上的影响才被计算出来，才能决定容器的图形显示）

如果你是Web开发者，可能更关注的是哪些具体原因会引起浏览器的回流，下面罗列一下：

1、调整窗口大小

2、字体大小

3、样式表变动

4、元素内容变化，尤其是输入控件

5、CSS伪类激活（:hover），在用户交互过程中发生

6、DOM操作，DOM元素增删、修改

7、width, clientWidth, scrollTop等布局宽高的计算（见视口的宽高与滚动高度一文）。

计算这些元素和布局大小时，浏览器会立即Flush渐进回流队列。

这些会引起回流的操作中，6、7 是和JavaScript代码相关的。 


所以为了避免回流提高页面性能，前端开发需要注意的主要是这两点：避免大量的DOM操作和布局计算。
Reflow要比Repaint更花费时间，也就更影响性能。所以在写代码的时候，要尽量避免过多的Reflow。

当然，我们的浏览器是聪明的，它不会像上面那样，你每改一次样式，它就reflow或repaint一次。一般来说，浏览器会把这样的操作积攒一批，然后做一次reflow，这又叫异步reflow或增量异步reflow。但是有些情况浏览器是不会这么做的，比如：resize窗口，改变了页面默认的字体，等。对于这些操作，浏览器会马上进行reflow。

```
1. 用户输入网址（假设是个html页面，并且是第一次访问），浏览器向服务器发出请求，服务器返回html文件； 　
2. 浏览器开始载入html代码，发现<head>标签内有一个<link>标签引用外部CSS文件； 　　
3. 浏览器又发出CSS文件的请求，服务器返回这个CSS文件； 　　
4. 浏览器继续载入html中<body>部分的代码，并且CSS文件已经拿到手了，可以开始渲染页面了； 　　
5. 浏览器在代码中发现一个<img>标签引用了一张图片，向服务器发出请求。此时浏览器不会等到图片下载完，而是继续渲染后面的代码； 　　
6. 服务器返回图片文件，由于图片占用了一定面积，影响了后面段落的排布，因此浏览器需要回过头来重新渲染这部分代码； 　　
7. 浏览器发现了一个包含一行Javascript代码的<script>标签，赶快运行它； 　　
8. Javascript脚本执行了这条语句，它命令浏览器隐藏掉代码中的某个<div> （style.display=”none”）。杯具啊，突然就少了这么一个元素，浏览器不得不重新渲染这部分代码； 　　
9. 终于等到了</html>的到来，浏览器泪流满面…… 　　
10. 等等，还没完，用户点了一下界面中的“换肤”按钮，Javascript让浏览器换了一下<link>标签的CSS路径； 　　
11. 浏览器召集了在座的各位<div><span><ul><li>们，“大伙儿收拾收拾行李，咱得重新来过……”，浏览器向服务器请求了新的CSS文件，重新渲染页面。
```

减少reflow的一些tips：
1）不要一条一条地修改DOM的样式。与其这样，还不如预先定义好css的class，然后修改DOM的className。

1
2
3
4
5
6
7
8
9
10
11
// bad
var left = 10,
top = 10;
el.style.left = left + "px";
el.style.top  = top  + "px";
  
// Good
el.className += " theclassname";
  
// Good
el.style.cssText += "; left: " + left + "px; top: " + top + "px;";
2）把DOM离线后修改。如：

使用documentFragment 对象在内存里操作DOM
先把DOM给display:none(有一次reflow)，然后你想怎么改就怎么改。比如修改100次，然后再把他显示出来。
clone一个DOM结点到内存里，然后想怎么改就怎么改，改完后，和在线的那个的交换一下。
3）不要把DOM结点的属性值放在一个循环里当成循环里的变量。不然这会导致大量地读写这个结点的属性。

4）尽可能的修改层级比较低的DOM。当然，改变层级比较底的DOM有可能会造成大面积的reflow，但是也可能影响范围很小。

5）为动画的HTML元件使用fixed或absoult的position，那么修改他们的CSS是不会reflow的。

6）千万不要使用table布局。因为可能很小的一个小改动会造成整个table的重新布局。

##***<span style="color:#abcde1">还没写完</span>***