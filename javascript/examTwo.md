# 前端 javascript

#### CSS

### 1、容器包含若干浮动元素时如何清理浮动

* ##### 父级div定义height   

 **原理**：父级div手动定义height，就解决了父级div无法自动获取到高度问题

 **优点**：简单，代码少，容易掌握

 **缺点**：只适合高度固定的布局，要给出精确的高度，如果高度和父级div不一样时，会产生问题

 **建议**：不推荐使用，只建议高度固定的布局时使用

* ##### 结尾处加空div标签clear：both

 **原理**：添加一个空div，利用css提高的clear：both清除浮动，让父级div能自动获取到高度

 **优点**：简单，代码少，浏览器支持好，不容易出现怪问题

 **缺点**：不少初学者不理解原理；如果页面浮动布局多，就要增加很多空div，让人感觉很不爽

 **建议**：不推荐使用，但此方法是以前主要使用的一种清除浮动的方法


* ##### 父级div定义伪类：after和zoom
```
 .clearFix:after{display:block;clear:both;content:"";visibility:hidden;height:0}
 .clearFix{zoom:1}
```

 **原理**：IE8以上和非IE浏览器才支持：after，原理和方法2有点类似，zoom（IE专有属性）可解决IE6，IE7浮动问题

 **优点**：浏览器支持好，不容易出现怪问题（目前：大型网站都有使用，如腾讯，网易，新浪等等）

 **缺点**：代码多，不少初学者不理解原理，要两句代码结合使用，才能让主流浏览器都支持

 **建议**：推荐使用，建议定义公共类，一减少css代码

 >先说原理：这种方法清除浮动是现在网上最拉风的一种清除浮动，他就是利用:after和:before来在元素内部插入两个元素块，从面达到清除浮动的效果。其实现原理类似于clear:both方法，只是区别在于:clear在html插入一个div.clear标签，而outer利用其伪类clear:after在元素内部增加一个类似于div.clear的效果。
 其中clear:both;指清除所有浮动；content: '.'; display:block;对于FF/chrome/opera/IE8不能缺少，其中content（）可以取值也可以为空。visibility:hidden;的作用是允许浏览器渲染它，但是不显示出来，这样才能实现清楚浮动。
 最后：但不是不重要，也不是不知道！下一标签直接清浮动兄弟标签浮动时，在下一标签的属性中直接写入 清除clear:both;这样就可以清除以上标签的浮动而不用加入空标签来清除浮动。

* ##### 父级div定义overflow：hidden

 **原理**：必须定义width或zoom：1，同时不能定义height，使用overflow：hidden时，浏览器会自动检查浮动区域的高度

 **优点**：简单，代码少，流浪器支持好

 **缺点**：不能喝position配合使用，因为超出的尺寸会被隐藏

 **建议**：只推荐没有使用position或对overflow：hidden理解比较深的朋友使用


* ##### 父级div定义overflow：auto

 **原理**：必须定义width或zoom：1，同时不能定义height，使用overflow：auto时，浏览器会自动检查浮动区域的高度

 **优点**：简单，代码少，浏览器支持好

 **缺点**：内部宽高超过父级div时，会出现滚动条

 **建议**：不推荐使用，如果你需要出现滚动条或者确保你的代码不会出现滚动条就使用吧


* ##### 父级div也一起浮动

 **原理**：所有代码一起浮动，就变成了一个整体

 **优点**：没有优点

 **缺点**：会产生新的浮动问题

 **建议**：不推荐使用，只作了解


* ##### 父级div定义display：table

 **原理**：将div属性变成表格

 **优点**：没有优点

 **缺点**：会产生新的未知问题

 **建议**：不推荐使用，只作了解


* ##### 父级div定义zoom：1，结尾处加br标签clear：both

 **原理**：父级div定义zoom：1来解决IE浮动问题，结尾处加br标签clear：both

 **建议**：不推荐使用，只作了解


### 2、display,float,position的关系
>1、绝对定位完全脱离普通流，因此绝对定位元素无法跟普通流搭建交互关系（普通流能影响绝对定位，绝对定位不影响普通流），这样来说，在一些自适应布局场 景中，绝对定位就存在一些缺陷（需要更多的限制因素，非常不灵活）。如果希望用绝对定位实现你说的 float 或 inline-block 同样的效果，这个时候一般是不推荐用 绝对定位。


>2、对于浮动，这个属性一般不是用来做布局的（偏向于排版），但是CSS2.1好像也就这个属性 能够满足一些特定需求，所有才有了浮动布局。浮动相对绝对定位好处是，它默认可以影响行内布局，通过 clear 清除浮动也可以影响 块布局，可以与普通流建立良好的交互。 而且浮动本身是脱离普通流的，在元素的水平定位上相比于 inline-block 更加灵活多变， 而 inline-block 的水平定位则更加有序。


>3、inline-block，这个属性也不是用来布局的（偏向于排版），但是在 CSS3 普及之前，它的用处也很大。该元素的盒子在行框中进行格式化，其顺序与源HTML中的顺序一一对应。 同时该元素不脱离普通流，这比浮动来说有更大的优势，它可以跟普通流自然交互，而不必要借助去其他属性。而且相比浮动，相邻元素间的垂直对齐方 式，inline-block 比 float 更加灵活， float 格式化时有一条规则，就是越高越好（因此常常表现为顶端对齐），而 inline-block 在行内格式化，拥有更灵活的垂直对齐方式。应用：
如果使用了浮动，清除浮动就会成为你的副作用，而且如果你没有良好的HTML/CSS 结构的话，清除浮动是一个很复杂的事情。
inline-block 虽然避免了清除浮动的事情，但是会有另一个副作用，即空白符问题。这个问题的解决方案也令人十分蛋疼，因为毕竟 inline-block 不是布局属性，它仅仅是 行内级块容器盒子。 同时，作为IFC环境中的格式化问题，垂直居中、行高等问题也有可能是一个副作用。

**display,float,position的优先级**

1.如果'display'设置为'none'，用户端必须忽略掉'position'和'float'。在这种情况下，元素不产生框。 

2.否则，'position'设置为'absolute'或'fixed'，'display'设置为'block'且'float'设置为'none'。框的位置将由'top'，'right'，'bottom'和'left'属性和该框的包含块确定。

3.否则，如果'float'的值不是'none'，'display'设置为'block'并且该框浮动。 

4.否则，应用指定的其它'display'属性。 
即如果'position'设置为'absolute'或'fixed'且‘float’的值不为‘none’，display的值就会被设置为‘block’，所以设置display: inline; float: left;等同于float:left，display:inline 的属性并未生效。因为用户端会忽略掉对’display‘的设置。float:left和display:inline-block当然是不等同的。 

### 3、这两个兄弟元素之间的外边距是多少？
```
<p style="margin-bottom: 30px;">这个段落的下边距30px。</p>
<p style="margin-top: 20px;">这个段落的上边距20px。</p>
```



### 4、如何水平垂直居中一个元素

### 5、link与@import的区别

```
link引入形式：

<link href="styles.css" type="text/css" />

@import引用形式：

<style type="text/css">@import url("styles.css");</style>

```

 **差别1:归属差别**

  ```
  link和@import的最根本区别就是，link是一个html的一个标签，而@import是css的一个标签。
  link标签除了可以加载CSS外，还可以做很多其它的事情，比如声明页面链接属性，声明目录等，
  @import就只能加载CSS了。

  ```
**差别2:加载顺序的差别**

  ```
  当一个页面被加载的时候（就是被浏览者浏览的时候），link引用的CSS会同时被加载，
  而@import引用的CSS会等到页面全部被下载完再被加载。所以有时候浏览@import加载CSS的
  页面时开始会没有样式（就是闪烁），网速慢的时候比较明显。

  ```
**差别3:兼容性的差别**
 ```
  由于@import是CSS2.1提出的所以老的浏览器不支持，@import只有在IE5以上的才能识别，
  而link标签无此问题。

 ```

**差别4:使用DOM控制样式时的差别**

  ```
  当使用JavaScript控制DOM去改变样式的时候，只能使用link标签，因为@import不是DOM可以控制的。

  ```
**差别5：@import可以在css中再次引入其他样式表**

```
  比如可以创建一个主样式表，在主样式表中再引入其他的样式表，如：

  main.css
  ———————-
  @import “sub1.css”;
  @import “sub2.css”;

  sub1.css
  ———————-
  p {color:red};

  sub2.css
  ———————-
  .myclass {color:blue}

 ```

### 6、PNG,GIF,JPG的区别及如何选

### 7、了解哪些CSS布局方式


### 8、响应式，自适应

* 自适应：目的是在不同分辨率的不同设备上面显示相同的页面。
* 响应式：覆盖了自适应，但是包括的东西更多了。响应式布局可以根据屏幕的大小自动的调整页面的展现方式，以及布局。
* 流式：采用了一些设置，当宽度大于多少时怎么展示，小于多少时怎么展示，而且展示的方式向水流一样，一部分一部分的加载。
* 静态：采用固定宽度。

简单说：设备变化：响应式；窗口变化：自适应

响应式设计的步骤：
1. 设置 Meta 标签
```
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
```
user-scalable = no 属性能够解决 iPad 切换横屏之后触摸才能回到具体尺寸的问题。
2.通过媒介查询来设置样式 Media Queries
它根据条件告诉浏览器如何为指定视图宽度渲染页面。假如一个终端的分辨率小于 980px，那么可以这样写：
```
@media screen and (max-width: 980px) {
  #head { … }
  #content { … }
  #footer { … }
}
```
这里的样式就会覆盖上面已经定义好的样式。

3.设置多种视图宽度
```
/** iPad **/
@media only screen and (min-width: 768px) and (max-width: 1024px) {}
/** iPhone **/
@media only screen and (min-width: 320px) and (max-width: 767px) {}
```
响应式布局的一些技术点纪录：
* 允许网页的宽度自动的调整
* 尽量少使用绝对的宽度，多点百分比
* 相对大小的字体:字体不要使用px写死，最好使用相对大小的em，或者高清方案rem，这个不限制与字体，别的属性也可以这么设置
* 流式布局，float的好处是，如果宽度太小，放不下两个元素，后面的元素会自动滚动到前面元素的下方，不会在水平方向overflow（溢出），避免了水平滚动条的出现。
* 选择加载css，<link rel="stylesheet" type="text/css" media="screen and (max-device-width: 400px)" href="tinyScreen.css" />，这个意思是如果屏幕宽度小于400像素（max-device-width: 400px），就加载tinyScreen.css文件。


#### JS 部分

1、null  ，undefined 的区别

2、简述同步和异步的区别

3、介绍js有哪些内置对象？

4、如何消除一个数组里面重复的元素？

5、简述 Javascript 作用域链，作用域分为几种。
  全局作用域，函数作用域。


6、JavaScript原型，原型链 ? 有什么特点？

7、Javascript如何实现继承？



8、javascript创建对象的几种方式？
  new
  var a = {};

9、什么是闭包（closure），为什么要用它？

10、js延迟加载的方式有哪些

11、如何解决跨域问题
  域名，端口号，协议
  document.domain+iframe的设置

12、你有用过哪些前端性能优化的方法


13、一个页面从输入 URL 到页面加载显示完成，这个过程中都发生了什么

14、谈谈This对象的理解


15、一次完整的HTTP事务是怎样的一个过程

16、谈一谈你对前端自动化工具的了解？

17、用过哪些前端框架
