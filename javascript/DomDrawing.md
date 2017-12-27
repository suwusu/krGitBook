# 浏览器渲染、加载过程详解
##一、渲染
####主要渲染的是两大部分：DOM和CSSOM，DOM 和 CSSOM 都是以 Bytes → characters → tokens → nodes → object model.这样的方式生成最终的数据。
![渲染过程](http://delai.me/code/content/images/2016/01/full-process.png?_=5152072)
#####（1）DOM
```
>DOM即Document Object Model，浏览器将HTML解析成树形的数据结构，简称DOM。
```
DOM树的构建过程是一个深度遍历过程：当前节点的所有子节点都构建好后才会去构建当前节点的下一个兄弟节点。
#####（2）CSSOM
```
>CSSOM即CSS Object Model，大体上来说，CSSOM是一个建立在web页面上的 CSS 样式的映射，它和DOM类似，但是只针对CSS而不是HTML。
浏览器将CSS代码解析成树形的数据结构,然后将DOM和CSSOM结合来渲染web页面。
```
#####（3）Render Tree
```
>Render Tree：DOM 和 CSSOM 合并后生成 Render Tree。
```
![渲染过程](http://delai.me/code/content/images/2016/01/render-tree-construction.png?_=5152072)
Render Tree 和DOM一样，以多叉树的形式保存了每个节点的css属性、节点本身属性、以及节点的孩子节点。
注意：Rendering Tree 渲染树并不等同于DOM树，因为一些像Header或display:none的东西就没必要放在渲染树中了，而visibility: hidden 则会，所以，如果某个节点最开始是不显示的，设为display:none是更优的。
####浏览器的渲染过程
1、Create/Update DOM And request css/image/js：浏览器请求到HTML代码后，在生成DOM的最开始阶段（应该是 Bytes → characters 后），并行发起css、图片、js的请求，无论他们是否在HEAD里。

注意：发起js文件的下载request并不需要DOM处理到那个script节点，比如：简单的正则匹配就能做到这一点，虽然实际上并不一定是通过正则）。这是很多人在理解渲染机制的时候存在的误区。

2、Create/Update Render CSSOM：CSS文件下载完成，开始构建CSSOM。

3、Create/Update Render Tree：所有CSS文件下载完成，CSSOM构建结束后， DOM Tree 和 CSS Rule Tree 一起生成 Render Tree。

4、Layout：一个Render Object在绘制之前，会先进行Layout。Layout的目的就是确定一个Render Object的CSS Box Model的margin、border和padding值并计算出每个节点在屏幕中的位置，定位坐标，是否换行，各种position, overflow, z-index属性一旦这些值确定之后，再结合content值，就可以对一个Render Object进行绘制了。（回流会导致Layout）

5、Painting：Layout后，浏览器已经知道了哪些节点要显示（which nodes are visible）、每个节点的CSS属性是什么（their computed styles）、每个节点在屏幕中的位置是哪里（geometry）。就进入了最后一步：Painting，按照Layout计算出来的规则，通过显卡，调用操作系统Native GUI的API绘制，把内容画到屏幕上。(重绘导致Painting)
##***<span style="color:#abcde1">还没写完</span>***
