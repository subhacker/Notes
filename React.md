##JSX语法

JSX 其是一个语法扩展，它既不是单纯的字符串，也不是 HTML，它就是基于JavaScript，在 React当中的一种语法扩展
的实现。
JSX 被用来创建 React 当中的 Elements，React 当中的元素。然后 React 再通过一些方法，把 JSX 创建的元素，
渲染成我们在浏览器当中看到的 DOM元素。

##JSX实现原理
我们想要在浏览器里直接运行采用 JSX 语法的 JavaScript 显然暂时是不可能实现的，在实际的生产过程中，
我们需要利用 Babel 一类的转译器来将我们的 JSX 语法或者 ES6 语法转译成浏览器可以直接运行的 JavaScript，
事实上 JSX 在经过转译之后，会变成 React 创建 Element 的一个方法：
```
ReactDOM.render( <p>Hello world!</p>, document.getElementById('container') )
ReactDOM.render( React.createElement('p',null,`Hello world!`), document.getElementById('container') )
```

###React中的无状态和有状态组件

ES5写法：React.createClass
ES6写法：React.Component
无状态的函数写法，又称为纯组件SFC
React.Component最终会取代React.createClass
```
import React from 'react'
import ReactDOM from 'react-dom'

class SwitchButton extends React.Component {
    constructor(props) {
        super(props)
        this.state = {
            open: this.props.open
        }
        this.handleClick = this.handleClick.bind(this)
    }

    handleClick(event) {
        this.setState({ open: !this.state.open })
    }

    render() {
        let open = this.state.open,
            className = open ? 'switch-button open' : 'btn-switch'

        return (
            <label className={className} onClick={this.handleClick}>
                <input type="checkbox" checked={open}/> 男
            </label>
        )
    }
}

SwitchButton.defaultProps = {
    open: false
}

ReactDOM.render(
    <SwitchButton />,
    document.getElementById('root')
)
```


##无状态的函数写法
无状态的函数创建的组件是无状态组件，它是一种只负责展示的纯组件：
```
function HelloComponent(props) {
    return <div>Hello {props.name}</div>
}
ReactDOM.render(<HelloComponent name="marlon" />, mountNode)
```
对于这种无状态的组件，使用函数式的方式声明，会使得代码的可读性更好，并能大大减少代码量，
箭头函数则是函数式写法的最佳搭档：
```
const Todo = (props) => (
    <li
        onClick={props.onClick}
        style={{textDecoration: props.complete ? "line-through" : "none"}}
    >
        {props.text}
    </li>
)
```
上面定义的 Todo 组件，输入输出数据完全由props决定，而且不会产生任何副作用。对于props为 Object 类型时，
我们还可以使用 ES6 的解构赋值：
```
const Todo = ({ onClick, complete, text, ...props }) => (
    <li
        onClick={onClick}
        style={{textDecoration: complete ? "line-through" : "none"}}
        {...props}
    >
        {props.text}
    </li>
)
```
无状态组件一般会搭配高阶组件（简称：HOC）一起使用，高阶组件用来托管state，Redux 框架就是通过 store 
管理数据源和所有状态，其中所有负责展示的组件都使用无状态函数式的写法。

这种模式被鼓励在大型项目中尽可能以简单的写法 来分割原本庞大的组件，而未来 React 也会面向这种无状态
的组件进行一些专门的优化，比如避免无意义的检查或内存分配。所以建议大家尽可能在项目中使用无状态组件。

无状态组件内部其实是可以使用ref功能的，虽然不能通过this.refs访问到，但是可以通过将ref内容保存到无
状态组件内部的一个本地变量中获取到。

例如下面这段代码可以使用ref来获取组件挂载到DOM中后所指向的DOM元素:
```
function TestComp(props){
    let ref;
    return (
        <div ref={(node) => ref = node}></div>
    )
}
```
无状态函数式写法 优于React.createClass，而React.Component优于React.createClass。
能用React.Component创建的组件的就尽量不用React.createClass形式创建组件


无状态组件：无状态组件(Stateless Component)是最基础的组件形式，由于没有状态的影响所以就是纯静态展示的作用。一般来说，各种UI库里也是最开始会开发的组件类别。如按钮、标签、输入框等。它的基本组成结构就是属性（props）加上一个渲染函数（render）。由于不涉及到状态的更新，所以这种组件的复用性也最强。

有状态组件：在无状态组件的基础上，如果组件内部包含状态（state）且状态随着事件或者外部的消息而发生
改变的时候，这就构成了有状态组件（Stateful Component）。有状态组件通常会带有生命周期(lifecycle)，
用以在不同的时刻触发状态的更新。这种组件也是通常在写业务逻辑中最经常使用到的，根据不同的业务场景组件
的状态数量以及生命周期机制也不尽相同。

而在React中，我们通常通过props和state来处理两种类型的数据。props是只读的，只能由父组件设置。
state在组件内定义，在组件的生命周期中可以更改。基本上，无状态组件（也称为哑组件）使用props来存储数据，
而有状态组件（也称为智能组件）使用state来存储数据。为了能更好的理解，我们通过下面的示例来展示。

无状态组件无State，无生命周期函数



头部从 react 的包当中引入了 React 和 React.js 的组件父类 Component。记住，只要你要写 React.js 组件，
那么就必须要引入这两个东西。著作权归作者所有。

React与React-dom分离的原因

JSX 原理
为了让大家深刻理解 JSX 的含义。有必要简单介绍了一下 JSX 稍微底层的运作原理，
这样大家可以更加深刻理解 JSX 到底是什么东西，为什么要有这种语法，它是经过怎么样的转化变成页面的元素的。

思考一个问题：如何用 JavaScript 对象来表现一个 DOM 元素的结构，举个例子：
```
<div class='box' id='content'>
    <div class='title'>Hello</div>
    <button>Click</button>
</div>
```
每个 DOM 元素的结构都可以用 JavaScript 的对象来表示。你会发现一个 DOM 元素包含的信息其实只有三个：
标签名，属性，子元素。

所以其实上面这个 HTML 所有的信息我们都可以用合法的 JavaScript 对象来表示：
```
{
    tag: 'div',
    attrs: { 
        className: 'box', 
        id: 'content'
    },
    children: [
        {
            tag: 'div',
            arrts: { className: 'title' },
            children: ['Hello']
        },
        {
            tag: 'button',
            attrs: null,
            children: ['Click']
        }
    ]
}
```
你会发现，HTML 的信息和 JavaScript 所包含的结构和信息其实是一样的，我们可以用 JavaScript 对象来描述所有
能用 HTML 表示的 UI 信息。但是用 JavaScript 写起来太长了，结构看起来又不清晰，用 HTML 的方式写起来就方
便很多了。

于是 React.js 就把 JavaScript 的语法扩展了一下，让 JavaScript 语言能够支持这种直接在 JavaScript 
代码里面编写类似 HTML 标签结构的语法，这样写起来就方便很多了。编译的过程会把类似 HTML 的 JSX 结构转换成
 JavaScript 的对象结构。

上面的代码：
```
import React, { Component } from 'react'
import ReactDOM from 'react-dom'
import './index.css'

class Header extends Component {
    render () {
        return (
            <div>
                <h1 className='title'>React 小书</h1>
            </div>
        )
    }
}

ReactDOM.render(
    <Header />,
    document.getElementById('root')
)
```
经过编译以后会变成：
```
import React, { Component } from 'react'
import ReactDOM from 'react-dom'
import './index.css'

class Header extends Component {
    render () {
        return (
            React.createElement(
                "div",
                null,
                React.createElement(
                    "h1",
                    { className: 'title' },
                    "React 小书"
                )
            )
        )
    }
}

ReactDOM.render(
    React.createElement(Header, null), 
    document.getElementById('root')
);
```
React.createElement 会构建一个 JavaScript 对象来描述你 HTML 结构的信息，包括标签名、属性、还有子元素等。
这样的代码就是合法的 JavaScript 代码了。所以使用 React 和 JSX 的时候一定要经过编译的过程。

这里再重复一遍：所谓的 JSX 其实就是 JavaScript 对象。每当在 JavaScript 代码中看到这种 JSX 结构的时候，
脑子里面就可以自动做转化，这样对你理解 React.js 的组件写法很有好处。

有了这个表示 HTML 结构和信息的对象以后，就可以拿去构造真正的 DOM 元素，然后把这个 DOM 元素塞到页面上。
这也是我们最后一段代码中 ReactDOM.render 所干的事情：

ReactDOM.render(
    <Header />,
    document.getElementById('root')
)
ReactDOM.render 功能就是把组件渲染并且构造 DOM 树，然后插入到页面上某个特定的元素上（在这里是 id 为
 root 的 div 元素）。

所以可以总结一下从 JSX 到页面到底经过了什么样的过程：

JSX 描述 React.js 组件

有些同学可能会问，为什么不直接从 JSX 直接渲染构造 DOM 结构，而是要经过中间这么一层呢？

第一个原因是，当我们拿到一个表示 UI 的结构和信息的对象以后，不一定会把元素渲染到浏览器的普通页面上，
我们有可能把这个结构渲染到 canvas 上，或者是手机 App 上。所以这也是为什么会要把 react-dom 单独抽离出
来的原因，可以想象有一个叫 react-canvas 可以帮我们把 UI 渲染到 canvas 上，或者是有一个叫 react-app 
可以帮我们把它转换成原生的 App（实际上这玩意叫 ReactNative）。

第二个原因是，有了这样一个对象。当数据变化，需要更新组件的时候，就可以用比较快的算法操作这个 JavaScript
 对象，而不用直接操作页面上的 DOM，这样可以尽量少的减少浏览器重排，极大地优化性能。这个在以后的章节中我
 们会提到

服务端渲染的WEB开发


服务端渲染图示

就在几年前，前端工程师的大部分工作，可能还停留在利用CSS, HTML切页面，然后利用JS做些简单的动态交互，
更进一步的前端开发者可能需要懂Java, 或者PHP之类的语言，因为需要将写好的页面与模板引擎完成整合。

用服务端语言（例如NodeJS, Java, Python, Ruby, PHP等等）写过Web的朋友应该都很清楚，以前大部分时候我们
写的Web，尤其经典的MVC模型。多年以前，那会还不流行前后端分离式的开发，虽然Ajax技术已经很流行，
但是Web页面的功能和交互并没有那么复杂。大部分的页面点击一个连接，即请求到服务器，服务器控制路由（Router）
决定响应的View，服务器将数据库获取的数据Model与HTML模板结合，然后生成HTML页面响应到浏览器。
那时候Web大部分的业务都是服务器直接处理的，很多所谓的状态管理也都是服务端直接操作操作缓存（Cache）
或者数据库来完成的。所以那时候的前端并没有太多的所谓的状态需要管理，顶多大家有时候会在内存里面用一全局对象，
来处理些简单的数据共享。随着Web前端的发展，越来越多的后端工作转移到了前端，数据的共享，
同步变的异常复杂和麻烦，所以这个时候急需这种完善的状态管理解决方案的出现。

###前后端分离的单页应用(SPA）


单页应用与服务器端交互图示

单页应用（Single Page Application）
利用Ajax做单页应用，经典的案例肯定就是Gmail了。早期可能大家都还用iframe这种古老的子页面加载方案，
随着Ajax技术的愈发成熟和盛行，后来越来越多的Web应用开始利用浏览器Hash做路由转发，Ajax做页面加载 
的方式写无跳转状态的Web应用（即单页应用。后来便有了类似Backbone, Angularjs为代表的MVVM前端框架的诞生。

浏览器越来越快的访问性能，早就了越来越多的PC应用开始WebApp化，很多时候我们不需要安装某个应用，
只需要简单的输入一个URL地址，便可以轻松访问我们需要的服务，相信很多朋友已经在使用Chrome上很多强大
的Web应用了。越来越多的Web开始想靠近类似于Native应用化的体验，所以SPA这种类型的Web开发越来越受欢迎，
典型的就是我们常常开发的后台管理应用了。

组件化与状态管理(Web Component And State Management)


组件直接的数据共享

Web组件化(Component)一个是被聊透了的话题了，它的益处无需多言，更好的编码效率，更好的代码阅读性，维护性，
补充HTML5语义化标签的不足。然而，正因为在开发越来越复杂的SPA时，开始将各个页面开始模块化，
页面公告模块组件化，一个页面拆分成多个子组件，组件的不断复用和重新组合，之前简单的组件端到端
（组件到服务器端）的数据请求变的复杂和多余，单个数据源经常在不同页面但相同组件中共享，各种路由信息（Routing）需要处理。

我们可以想象一下，当一个页面中，相同的组件获取来自同一个接口的数据，这就意味着组件共享的是相同的数据Model。 正常逻辑下，其中一个组件如果进行了Model更新操作，服务器数据库的数据即相应的发生了改变，但是其他相同数据接口的组件，由于组件直接是相互隔离的，数据Model并不是同一个，所以组件与组件直接的数据通信便成为了一个很大的问题。当然，我们有个粗暴的解决方案，就是，在某个组件更新完数据后，我们重新reload整个页面，可这个时候整个原本想达到的SPA效果就没有了，体验大减，而你打开Network检测工具，你会发现整个页面发送了多个重复的接口请求，这无疑造成了很大的性能损失和资源浪费。所以才会出现Redux,Vuex这种专门针对状态管理的技术方案。



