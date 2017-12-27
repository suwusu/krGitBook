#Vue的故事
######vuejs/vue-cli在github 5.7k星
######尤雨溪，Vue.js 创作者，Vue Technology创始人，致力于Vue的研究开发。
<img src='images/builder.jpg' width='700px'/>
######让我们认识一下这个名字很诗意，长相很文雅的帅哥吧,点击下面链接……
######http://www.4u4v.net/vue-js-zuo-zhe-you-yu-xi-yi-jiang-ren-di-tai-du-bu-duan-da-mo-wan-shan-vue.html
# Vue基础
##一、安装
###1、兼容性
######Vue.js 不支持 IE8 及其以下版本，因为 Vue.js 使用了 IE8 不能模拟的ECMAScript 5 特性。 Vue.js 支持所有兼容 ECMAScript 5 的浏览器。因为vue使用Object.defineProperty()。
######Object.defineProperty() 介绍：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty
###2、直接```<script>```引入
######直接下载并用 ```<script>``` 标签引入，Vue 会被注册为一个全局变量
###3、快速搭建大型单页应用
######Vue.js 提供一个官方命令行工具，可用于快速搭建大型单页应用。该工具提供开箱即用的构建工具配置，带来现代化的前端开发流程。只需几分钟即可创建并启动一个带热重载、保存时静态检查以及可用于生产环境的构建配置的项目：
```
# 全局安装 vue-cli
$(sudo)npm install --global vue-cli
# 创建一个基于 webpack 模板的新项目
$ vue init webpack my-project
$ cd my-project
$ npm install
$ npm run dev
```
######详细介绍了安装搭建单页应用的过程https://zhuanlan.zhihu.com/p/22329282

##二、指令   
####1、v-bind  
```
<div id="app-2">
  <span v-bind:title="message">
    鼠标悬停几秒钟查看此处动态绑定的提示信息！
  </span>
</div>   

```
```
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: '页面加载于 ' + new Date()
  }
})

```
######将这个元素节点的 title 属性和 Vue 实例的 message 属性保持一致。
####2、v-if  
```
<div id="app-3">
  <p v-if="seen">现在你看到我了</p>
</div>
```
```
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})  

```
######不仅可以绑定 DOM 文本到数据，也可以绑定 DOM 结构到数据。Vue 也提供一个强大的过渡效果系统，可以在 Vue 插入/更新/删除元素时自动应用过渡效果。
####3、v-for  
```
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>  

```
```
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: '学习 JavaScript' },
      { text: '学习 Vue' },
      { text: '整个牛项目' }
    ]
  }
})
```
####4、v-on
######v-on 指令绑定一个事件监听器 
```
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">逆转消息</button>
</div>
```
``` 
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```
####5、v-model
######实现表单输入和应用状态之间的双向绑定
```
<div id="app-6">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
```
``` 
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Hello Vue!'
  }
})
```
###缩写
####v-bind缩写
```
<!-- 完整语法 -->
<a v-bind:href="url"></a>
<!-- 缩写 -->
<a :href="url"></a>
```
####v-on缩写
```
<!-- 完整语法 -->
<a v-on:click="doSomething"></a>
<!-- 缩写 -->
<a @click="doSomething"></a>

```
##三，过滤器
######过滤器函数总接受表达式的值作为第一个参数。
```
new Vue({
  // ...
  filters: {
    capitalize: function (value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  }
})
```
######过滤器可以串联：
```
{{ message | filterA | filterB }}

```
######过滤器是 JavaScript 函数，因此可以接受参数：
```
{{ message | filterA('arg1', arg2) }}
```
##四、计算属性
######https://cn.vuejs.org/v2/guide/computed.html

##五、组件化应用构建
```
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: '蔬菜' },
      { id: 1, text: '奶酪' },
      { id: 2, text: '随便其他什么人吃的东西' }
    ]
  }
})
```
```
<todo-item
  v-for="item in groceryList"
  v-bind:todo="item"
  v-bind:key="item.id">
</todo-item>
```
##六、实例

######在实例化 Vue 时，需要传入一个选项对象，它可以包含数据、模板、挂载元素、方法、生命周期钩子等选项。
###属性和方法
######每个 Vue 实例都会代理其 data 对象里所有的属性：
```
var data = { a: 1 }
var vm = new Vue({
  data: data
})
vm.a === data.a // -> true
// 设置属性也会影响到原始数据
vm.a = 2
data.a // -> 2
// ... 反之亦然
data.a = 3
vm.a // -> 3
```

######注意只有这些被代理的属性是响应的。如果在实例创建之后添加新的属性到实例上，它不会触发视图更新。我们将在后面详细讨论响应系统。
######除了 data 属性， Vue 实例暴露了一些有用的实例属性与方法。这些属性与方法都有前缀 $，以便与代理的 data 属性区分。例如：
```
var data = { a: 1 }
var vm = new Vue({
  el: '#example',
  data: data
})
vm.$data === data // -> true
vm.$el === document.getElementById('example') // -> true
// $watch 是一个实例方法
vm.$watch('a', function (newVal, oldVal) {
  // 这个回调将在 `vm.a`  改变后调用
})
```
######注意，不要在实例属性或者回调函数中（如 vm.$watch('a', newVal => this.myMethod())）使用箭头函数。因为箭头函数绑定父级上下文，所以 this 不会像预想的一样是 Vue 实例，而是 this.myMethod 未被定义。




##七、生命周期
####vue2.0的生命周期分为4主要个过程

######create。 创建---实例化Vue(new Vue) 时，会先进行create。

######mount。挂载---根据el, template, 
######render方法等属性，会生成DOM，并添加到对应位置。

######update。更新---当数据发生变化后，更新DOM。

######destory。销毁---销毁时执行。

<img src='images/lifecycle.png' width='700px'/>

##vue对比其他框架

#####1、vue vs angular

######1）vue在设计之初参考了很多angular的思想

######2）vue相比于angular来说更加的简单

######3)vue相当于angular要变得小巧很多，运行速度比angular快

######4）vue和angular绑定都可以用双大括号

######5）vue指令用v-xxx，angular用ng-xxx

######6）vue中数据放在data对象里面，angular数据绑定在$scope上面

######7）vue有组件化概念，angular中没有

#####2、vue vs react

######1）react和vue都是用虚拟DOM Virtual DOM

######2)React和Vue都提供了响应式（Reactive）和组件化（Componsable）的视图组件

######3）React和vue都将注意力集中保持在核心库，伴随于此，有配套的路由和负责处理全局状态管理的库

######4）React使用JSX渲染页面，Vue使用简单的模板

######5）Vue比react运行更快

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
#####分享者寄语：
######愿我们都有能力，不向生活缴械投降       ——Lin
<br/>
<br/>






