# Next.js 分享

>Next.js提供了基于React的简单通用JavaScript框架
来自 Zeit 的团队在React的基础和组件模型上构建了Next.js，同时还提供了一个关键扩展：通过使用名为 getInitialProps() 的组件生命周期钩子方法，框架能够在服务器上进行初始渲染，如果需要的话，还可以在客户端继续进行渲染。不过这个高级特性是一个很小却功能强大的框架所额外提供的。
按照Next.js的最小功能集，它提供了一种便利的方式来创建新的Web应用，这个过程中，并不需要很多的工具集配置。类似于create-react-app，安装这个框架会搭建一个基于React、Webpack和Babel的构建过程。以往编写React组件的开发人员将会基于React语法来创建页面，每个页面提供了一个render函数：

```
import React from 'react'
export default () =>{}
```

#### 安装相关工具

```
npm install next 
```

#### 构建项目

```
npm init next-demo
```



#### 添加首页内容

```
mkdir pages 
touch pages/index.js
```
index.js内容如下

```
import React from 'react';
import Link from 'next/link';

const Index = () =>  <div> welcome next.js </div> ;
export default Index;

```

#### 修改package.json 文件

```
{
	"name": "kr-next",
	"version": "1.0.0",
	"description": "",
	"main": "index.js",
	"dependencies": {
		"next": "^3.0.0-beta13",
		"react": "^15.5.4",
		"react-dom": "^15.5.4",
	},
	"devDependencies": {
		"next-redux-wrapper": "^1.1.2"
	},
	"scripts": {
		"dev": "next",
		"build": "next build",
		"start": "next start"
	},
	"author": "",
	"license": "ISC"
}
```

#### 项目结构

```

├── next.config.js
├── package.json
├── pages
│   └── index.js

```


#### 启动项目

```
npm run dev
```
#### 浏览器查看(浏览器网页内容自动更新)

## 语法

####  每个pages文件对应一个路由
比如新建一个about页面,操作如下

```
touch pages/about.js
```

about.js 内容如下

```
import React from 'react';
import Link from 'next/link';

const About = () =>  <div> about page </div> ;
export default About;
```

修改pages/index.js 增加跳转到about页面的链接

```
import React from 'react';
import Link from 'next/link';

const Index = () =>  <div> welcome next.js Click <Link href="/about"><a>here</a></Link> to read more</div> ;
export default Index;

```


#### css 添加方式


CSS-in-JS

```
export default () => (
  <p style={{ color: 'red' }}>hi there</p>
)
```

```
import React from 'react'
import css from 'next/css'

export default () => <p className={style}>Hi there!</p>

const style = css({
  color: 'red',
  ':hover': {
    color: 'blue'
  },
  '@media (max-width: 500px)': {
    color: 'rebeccapurple'
  }
})

```

styled-jsx 

```
export default () => (
  <div>
    Hello world
    <p>scoped!</p>
    <style jsx>{`
      p {
        color: blue;
      }
      div {
        background: red;
      }
      @media (max-width: 600px) {
        div {
          background: blue;
        }
      }
    `}</style>
    <style global jsx>{`
      body {
        background: black;
      }
    `}</style>
  </div>
)
```

#### 服务器基础数据渲染(getInitialProps)

```
import React from 'react'
import 'isomorphic-fetch'
export default class extends React.Component {
  static async getInitialProps () {
    const res = await fetch('https://api.company.com/user/123')
    const data = await res.json()
    return { username: data.profile.username }
  }
}
```


#### Link 组件

```
import React from 'react';
import Link from 'next/link';

const Index = () =>  <div> welcome next.js Click <Link href="/about"><a>here</a></Link> to read more</div> ;
export default Index;

```

<Link>组件的工作流程和浏览器很相似：

1. 获取新的组件
2. 如果新组件定义了getInitialProps，则获取数据，如果发生错误，则渲染_error.js
步骤1，2完成之后，执行pushState并渲染新组件
每个顶层组件中还会传入一个url对象，提供了几个路由相关的方法：

pathname：String-当前URL不包括查询字符串的path部分
query：Object-当前URL中查询字符串解析成的对象
back-后退
push(url, as=url)-使用传入的url（字符串）执行pushState操作
replace(url, as=url)-使用传入的url（字符串）执行replaceState操作 注意：push和replace方法中的第二个参数as为可选项，只有在服务端配置了自定义路由才有作用。


#### Router对象

除了使用<Link>组件之外，Next还提供了一个Router对象满足命令式写法的需要：

```
import Router from 'next/router'

export default () => (
  <div>Click <span onClick={() => Router.push('/about')}>here</span> to read more</div>
)

```

路由事件

Router对象还提供了三个路由事件方法：

1. routeChangeStart(url) - 路由变化开始时触发
2. routeChangeComplete(url) - 路由变化完成时触发
3. routeChangeError(err, url) - 路由变化发生错误时触发 如果使用Router.push(url, as)或相似的方法并传入了as参数，则路由事件方法中的url参数值为as的值，否则，url参数的值是路由舔砖目标的URL
注意：与Router对象中其他的属性和方法不同的是，这三个路由事件方法可以在服务端渲染的页面使用。

监听路由变化：

```
Router.onRouteChangeStart = (url) => {
  console.log('App is changing to: ', url)
}
```

取消监听

```
Router.onRouteChangeStart = null;
```

如果路由加载取消了（连续快速点击两个链接），就会触发routeChangeError的回调，传入的err参数中将包含一个cancelled属性，值为true。

```
Router.onRouteChangeError = (err, url) => {
  if (err.cancelled) {
    console.log(`Route to ${url} was cancelled!`)
  }
}
```

#### 预获取页面

Next提供了一个基于ServiceWorker实现的，具有预获取页面功能的模块：next/prefetch。 使用预获取功能，可以使APP预加载那些可能到达的页面，提升网站的使用体验和性能。当然，前提是你的浏览器必须支持ServiceWorker。并且预获取功能只支持应用内的页面，不支持外部链接。

#### <Link>组件

next/prefetch模块也提供了一个具有预获取功能的<Link>组件，代替路由系统中的<Link>组件，使用方法一致：


```

import Link from 'next/prefetch'

export default () => (
  <nav>
    <ul>
      <li><Link href='/'><a>Home</a></Link></li>
      <li><Link href='/about'><a>About</a></Link></li>
      <li><Link href='/contact'><a>Contact</a></Link></li>
    </ul>
  </nav>
)

```

此外预获取功能可以精确控制到每个<Link>标签，使用prefetch属性来控制开关：

```
<Link href='/contact' prefetch={false}><a>Home</a></Link>
```

#### prefetch方法

和路由器一样，预获取模块也提供了一个prefetch方法，用来方便命令式的写法：

```
import { prefetch } from 'next/prefetch'
export default ({ url }) => (
  <div>
    <a onClick={ () => setTimeout(() => url.pushTo('/dynamic'), 100) }>
      100ms后执行路由跳转
    </a>
    {
      预获取页面
      prefetch('/dynamic')
    }
  </div>
)
```

#### 自定义配置

如果默认的配置无法满足需要的话，Next还提供了诸多的自定义配置接口，可以根据自己的需求灵活配置。

#### 自定义服务器和路由

默认的服务器和路由系统可能无法满足需要，比如，我需要把/a的路由解析到pages/b.js，把/b的路由解析到pages/a.js，此时，就需要通过自定义，手动控制页面渲染来实现，在项目根目录下创建server.js文件：

```

// server.js

const { createServer } = require('http')
const { parse } = require('url')
const next = require('next')

const dev = process.env.NODE_ENV !== 'production'
const app = next({ dev })
const handle = app.getRequestHandler()

app.prepare().then(() => {
  createServer((req, res) => {
    const parsedUrl = parse(req.url, true)
    const { pathname, query } = parsedUrl

    if (pathname === '/a') {
      app.render(req, res, '/b', query)
    } else if (pathname === '/b') {
      app.render(req, res, '/a', query)
    } else {
      handle(req, res, parsedUrl)
    }
  })
  .listen(3000, (err) => {
    if (err) throw err
    console.log('> Ready on http://localhost:3000')
  })
})

```

#### 自定义<head>

Next提供了<HEAD>组件，可以自定义页面<head>标签中的内容。每个组件都可以在内部自定义<head>的内容：

```
import Head from 'next/head'
export default () => (
  <div>
    <Head>
      <title>My page title</title>
      <meta name="viewport" content="initial-scale=1.0, width=device-width" />
    </Head>
    <p>Hello world!</p>
  </div>
)
```
每个页面组件只需要定义本页面需要的<head>内容，并且对于相同的标签，例如<title>。会按照组件渲染的顺序，后定义的覆盖先定义的内容。

#### 自定义<Document>

在前面的例子中，服务端渲染时，所有的页面我们只需要写内容组件，这是因为使用了默认的<Document>模板。当然，可以自定义自己的服务端渲染模板。首先，创建pages/_document.js文件，写上内容：

```

// pages/_document.js
import Document, { Head, Main, NextScript } from 'next/document'

export default class MyDocument extends Document {
  static async getInitialProps (ctx) {
    const props = await Document.getInitialProps(ctx)
    return { ...props, customValue: 'hi there!' }
  }

  render () {
    return (
     <html>
       <Head>
         <style>{`body { margin: 0 } /* custom! */`}</style>
       </Head>
       <body className="custom_class">
         {this.props.customValue}
         <Main />
         <NextScript />
       </body>
     </html>
    )
  }
}

```
其中的ctx对象与其他组件中的getInitialProps方法中收到的参数一样，只不过多了一个额外的方法：renderPage()。

#### 自定义错误处理

Next中，有一个默认组件error.js，负责处理404或者500这种错误。当然，你也可以自定义一个_error.js组件覆盖默认的错误处理组件：

```
// _error.js

import React from 'react'
export default class Error extends React.Component {
  static getInitialProps ({ res, xhr }) {
    const statusCode = res ? res.statusCode : (xhr ? xhr.status : null)
    return { statusCode }
  }

  render () {
    return (
      <p>{
        this.props.statusCode
        ? `An error ${this.props.statusCode} occurred on server`
        : 'An error occurred on client'
      }</p>
    )
  }
}

```

#### 自定义配置

相对Next进行自定义配置的话，可以在项目根目录下创建一个next.config.js

```
// next.config.js

module.exports = {
  /* 自定义配置 */
}
```

#### 自定义Webpack配置

在创建好的next.config.js文件中，可以扩展Webpack配置：

```
module.exports = {
  webpack: (config, { dev }) => {
   
    // 修改config对象
   
    return config
  }
}
```

该函数接收默认的Webpack config对象作为参数，返回修改后的config对象。需要注意的是，next.config.js文件会被直接执行，因为只能使用本机安装的Node.js所支持的JS语法。

警告：不建议在自定义Webpack配置中添加loader以支持新的文件类型！因为只有客户端渲染的代码会经过打包，而服务端执行的是源代码，并没有经过Webpack处理，因此新的loader对服务端渲染不起作用。所以最好是使用Babel插件来处理新的文件类型，因为无论是客户端还是服务端渲染的代码，都会经过Babel处理。




#### 自定义Babel配置

自定义Babel配置，只需要在项目根目录下创建.babelrc文件，因为自定义配置会覆盖默认配置，而不是扩展默认配置。因此需要把next preset写到.babelrc中。例如：


```
{
  "presets": [
    "next/babel",  // Next默认配置
    "stage-0"
  ],
}
```

#### 部署

生产模式下，需要先使用生产模式构建代码，再启动服务器。因此，需要两条命令：

```
next build
next start
```

Next官方推荐使用now作为部署工具，只要在package.json文件中写入：

```
{
  "name": "my-app",
  "dependencies": {
    "next": "latest"
  },
  "scripts": {
    "dev": "next",
    "build": "next build",
    "start": "next start"
  }
}

```

接着运行now命令，就可以实现一键部署。


#### 参考文献

1. [zeit/next.js](https://github.com/zeit/next.js)
2. [最简单的服务端渲染框架-Next.js快速入门](https://zhuanlan.zhihu.com/p/25191863)