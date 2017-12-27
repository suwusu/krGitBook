## canvas 分享 （平面图)
> canvas 是HTML5 新增的标签，一般可用来进行图片的裁切、选取操作，当然也可以用来画一些类似于地图相关的业务功能，比如平面图。鉴于这次平面图2d的开发，现在总结一下开发经验


#### 1. canvas是什么?(维基百科)

```
Canvas元素是HTML5的一部分，允许脚本语言动态渲染位图像。
它最初由苹果内部使用自己Mac OS X WebKit推出，供应用程序使用像仪表盘的构件和Safari浏览器使用。
后来，有人通过Gecko内核的浏览器（尤其是Mozilla和Firefox），Opera[1]和Chrome，和超文本网络应用技术工作组建议为下一代的网络技术使用该元素。Novell生产的XForms处理器插件作为Internet Explorer插件支持Canvas元素。[2]也有人努力使用VML和JavaScript在Internet Explorer支持Canvas功能而不需要插件。[3]Google也已开始了一个项目，使用同样的技术在Internet Explorer支持Canvas能力。[4]但Internet Explorer自Internet Explorer 9起已经可以支持canvas元素。
Canvas是由HTML代码配合高度和宽度属性而定义出的可绘制区域。JavaScript代码可以访问该区域，类似于其他通用的二维API，通过一套完整的绘图函数来动态生成图形。
一些可能的用途，包括使用Canvas构造图形，动画，游戏和图片。
如果您要在html中加入canvas元素，请将以下代码加入到<body>部分中： <canvas id = "canvas" width = "宽度" height = "高度">您的浏览器不支持canvas元素（此消息在浏览器不支持canvas元素时显示）</canvas>
```

#### 2. 创建Canvas元素
>向 HTML5 页面添加 canvas 元素。
规定元素的 id、宽度和高度：

```
<canvas id="myCanvas" width="200" height="100"></canvas>
```

#### 3. Canvas 的上下文

```
    var canvasElement = document.getElementById('myCanvas);
    var context = canvasElement.getContext('2d');
```

#### 4. canvas 常用的api有哪些?

颜色、样式和阴影

|属性|描述|
|-----|-----:|
|fileStyle|设置或返回用于填充绘画的颜色、渐变或模式|
|strokeStyle|设置或返回用于笔触的颜色、渐变或模式|
|shadownColor|设置或返回用于阴影的颜色|
|shadownBlur|设置或返回用于阴影的模糊级别|
|shadownOffsetX|设置或返回阴影距形状的水平距离|
|shadownOffsetY|设置或返回阴影距形状的垂直距离|



|方法|描述|
|-----|-----:|
|createLinearGradient()|创建线性渐变（用在画布内容上）|
|createPattern()|在指定的方向上重复指定的元素|
|createRadialGradient()|创建放射状/环形的渐变（用在画布内容上)|
|addColorStop()|规定渐变对象中的颜色和停止位置|

线条样式

|方法|描述|
|-----|-----:|
|lineCap|设置或返回线条的结束端点样式|
|lineJoin|设置或返回两条线相交时，所创建的拐角类型|
|lineWidth|设置或返回当前的线条宽度|
|miterLimit|	设置或返回最大斜接长度|


矩形

|方法|描述|
|----|----:|
|rect()|创建矩形|
|fillRect()|绘制“被填充”的矩形|
|strokeRect()|绘制矩形（无填充）|
|clearRect()|在给定的矩形内清除指定的像素|



路径

|方法|描述|
|----|----:|
|fill()|	填充当前绘图（路径）|
|stroke()|	绘制已定义的路径|
|beginPath()|	起始一条路径，或重置当前路径|
|moveTo()	|把路径移动到画布中的指定点，不创建线条|
|closePath()|	创建从当前点回到起始点的路径|
|lineTo()|	添加一个新点，然后在画布中创建从该点到最后指定点的线条|
|clip()	|从原始画布剪切任意形状和尺寸的区域
|quadraticCurveTo()|	创建二次贝塞尔曲线|
|bezierCurveTo()|	创建三次方贝塞尔曲线|
|arc()|	创建弧/曲线（用于创建圆形或部分圆）|
|arcTo()|	创建两切线之间的弧/曲线|
|isPointInPath()|	如果指定的点位于当前路径中，则返回 true，否则返回 false|


转换

|方法	|描述|
|----|----:|
|scale()	|缩放当前绘图至更大或更小|
|rotate()	|旋转当前绘图|
|translate()|	重新映射画布上的 (0,0) 位置|
|transform()	|替换绘图的当前转换矩阵|
|setTransform()|	将当前转换重置为单位矩阵。然后运行 transform()|


文本

|属性|描述|
|----|----:|
|font|设置或返回文本内容的当前字体属性|
|textAlign|	设置或返回文本内容的当前对齐方式|
|textBaseline|	设置或返回在绘制文本时使用的当前文本基线|

|方法|描述|
|----|----:|
|fillText()|	在画布上绘制“被填充的”文本|
|strokeText()|	在画布上绘制文本（无填充）|
|measureText()|	返回包含指定文本宽度的对象|


图像绘制

|方法|描述|
|----|----:|
|drawImage()|向画布上绘制图像、画布或视频|


像素操作

|属性|描述|
|----|----:|

|width|返回 ImageData 对象的宽度|
|height|返回 ImageData 对象的高度|
|data|返回一个对象，其包含指定的 ImageData 对象的图像数据|

|方法|描述|
|----|----:|
|createImageData()|创建新的、空白的 ImageData 对象|
|getImageData()|返回 ImageData 对象，该对象为画布上指定的矩形复制像素数据|
|putImageData()|把图像数据（从指定的 ImageData 对象）放回画布上|

合成

|属性|描述|
|----|----:|
|globalAlpha|	设置或返回绘图的当前 alpha 或透明值|
|globalCompositeOperation|设置或返回新图像如何绘制到已有的图像上|

其他

|方法|描述|
|----|----:|
|save()|保存当前环境的状态|
|restore()	|返回之前保存过的路径状态和属性|
|createEvent()|	 
|getContext()| 
|toDataURL()|	 

#### 5. 用Canvas开发平面图选工位案例 [查看源码](http://gitlab.corp.krspace.cn/f2e/canvas-demo) 

>来，我们开始代码show


#### 4.canvas 开发要注意哪些问题?

```

尽量少使用trasfrom、translate、scale方法，因为执行这些方法，是在原先的基础上再次转换，容易造成实现干扰。一般建议用闭包定义scale、translate 变量，通过数学公式计算，重新渲染canvas画布

每一步渲染的操作，都是重新计算、重新绘制呈现的结果，从而构成交互效果

利用canvas开发复杂的功能，需要预先知道一些常规数学公式,比如两点之间的距离、通过两点计算在x、y方向偏移较大者等，甚至复杂的功能需要知道物理中的力学公式

```
