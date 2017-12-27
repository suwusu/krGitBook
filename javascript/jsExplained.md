#js是怎么被浏览器解析的？

###script标签到底应该放在哪？
一般script标签会被放在头部或尾部。头部就是head里面，尾部一般指body里。

将script放在head里，浏览器解析HTML，发现script标签时，会先下载完所有这些script，再往下解析其他的HTML。讨厌的是浏览器在下载JS时，是不能多个JS并发一起下载的。不管JS是不是来自同一个host，浏览器最多只能同时下载两个JS，且浏览器下载JS时，就block掉解析其他HTML的工作。将script放在头部，会让网页内容呈现滞后，导致用户感觉到卡。所以yahoo建议将script放在尾部，这样能加速网页加载。(同步模式=阻塞模式)

将script放在尾部的缺点，是浏览器只能先解析完整个HTML页面，再下载JS。而对于一些高度依赖于JS的网页，就会显得慢了。所以将script放在尾部也不是最优解，最优解是一边解析页面，一边下载JS。

###async和defer
提出了一种更modern的方式：使用async和defer。80%的现代浏览器都认识async和defer属性，这两个属性能让浏览器做到一边下载JS(还是只能同时下载两个JS)，一边解析HTML。他的优点不是增加JS的并发下载数量，而是做到下载时不block解析HTML。

```
<script type="text/javascript" src="path/to/script1.js" async></script>  
<script type="text/javascript" src="path/to/script2.js" async></script>  
```

带async属性的script会异步执行，只要下载完就执行，这会导致script2.js可能先于script1.js执行（如果script2.js比较大，下载慢）。defer就能保证script有序执行，script1.js先执行，script2.js后执行。

结论：

1.如果可以不考虑支持<IE9的IE，最好的做法是将script标签放在head中，并使用async/defer属性。这样浏览器就能一边下载JS，一边解析其他的HTML。
2. Google自己的代码script放的也有点乱，有的放在body后面，有的放在body里面，还有的放在head里面。总体来说，放在body里其实是最常见的做法。
3. 本文只讨论script的位置，至于link和style，还是放在head里的做法比较常见。link也是要下载CSS的啊，为毛不考虑下载CSS阻塞HTML解析的问题呢？其实，一般情况下，JS和CSS，放在head和放在body区别不大。CSS的link放在body也是可以的，只是可能导致页面暂时没有样式。


<br/>
<br/>
<img src='images/jsexplian.jpeg' width='700px'/>
<br/>
<br/>
蓝色线代表网络读取，红色线代表执行时间，这俩都是针对脚本的；绿色线代表 HTML 解析。
（由图可见，阻塞或者异步指的是js的下载过车）

此图告诉我们以下几个要点：

1.defer 和 async 在网络读取（下载）这块儿是一样的，都是异步的（相较于 HTML 解析）

2.它俩的差别在于脚本下载完之后何时执行，显然 defer是最接近我们对于应用脚本加载和执行的要求的

3.关于 defer，此图未尽之处在于它是按照加载顺序执行脚本的，这一点要善加利用

4.async 则是一个乱序执行的主，反正对它来说脚本的加载和执行是紧紧挨着的，所以不管你声明的顺序如何，只要它加载完了就会立刻执行

5.仔细想想，async 对于应用脚本的用处不大，因为它完全不考虑依赖（哪怕是最低级的顺序执行），不过它对于那些可以不依赖任何脚本或不被任何脚本依赖的脚本来说却是非常合适的，最典型的例子：Google Analytics

async和defer的异同点：

####相同点：    

1.加载文件时不阻塞页面渲染；

2.对于inline的script无效；

3.使用这两个属性的脚本中不能调用document.write方法；

3.允许不定义属性值，仅仅使用属性名；

####不同点：

1.html的版本html4.0中定义了defer；html5.0中定义了async；这将造成由于浏览器版本的不同而对其支持的程度不同；

2.执行时刻：每一个async属性的脚本都在它下载结束之后立刻执行，同时会在window的load事件之前执行。所以就有可能出现脚本执行顺序被打乱 的情况；每一个defer属性的脚本都是在页面解析完毕之后，按照原本的顺序执行，时机为DOM解析完成后,在document的DOMContentLoaded之前执行。（DOMContentLoaded：Dom加载完成，不包括样式表，图片和flash）

###什么情况下使用 defer 和 async？

如果脚本不依赖于任何脚本，并不被任何脚本依赖，那么则使用 defer。

如果脚本是模块化的，不依赖于任何脚本，那么则使用 async。



<br/>
<br/>
<br/>
<br/>
愿我们有能力不向生活缴械投降  ——Lin
<br/>
<br/>
<br/>




