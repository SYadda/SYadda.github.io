# 董杭杭的React学习笔记 2023.12.02

本笔记基于Next.JS的官方教程：[From JavaScript to React](https://nextjs.org/learn-pages-router/foundations/from-javascript-to-react)

##### 教程第1-3节

HTML，JS，DOM，React，JSX，babel，Next.JS 彼此之间的关系

### 静态网页(无JS)和动态网页(有JS)

HTML：网页的文本部分
JS：网页的代码部分
CSS：网页的显示格式（文本美化、字体、排版等）

DOM：网页文本的层次结构（例如，一个目录包含很多条目，一个大版块包含多个文本框和图片），以树形结构表示。

JS代码可以监视用户行为（如点击按钮，输入文字等）并做出反馈，通过增删改DOM树中的元素，**动态**修改网页的显示内容，让用户与网页**产生交互**。

有JS，网页才能动，否则网页就是类似markdown的文档。

> 在Edge F12开发者工具中：
“源代码”显示未运行时，静态的HTML，JS等代码文件；
“元素”显示运行JS更新DOM树之后，此时实际显示的页面，对应的的HTML代码。

运行JS代码，以得到实际显示的HTML代码(即“渲染网页UI”)，需要一定的计算资源。而用户的终端（手机、电脑、车机）可能性能不足。

由此，一种**服务器端渲染**的技术应运而生：基于React编写网页，而将运行JS代码的工作，部分转移到服务器上，以减小通过网络传输给用户的JS文件大小，及对用户的计算资源需求，从而加快网页访问速度。这就是**Next.JS**，一个基于 React 的开源前端框架，用于帮助构建网站。

### 命令式编程(直接写JS)和声明式编程(调JS库，即React)

JS是一种**命令式编程**, 即一步接一步的告诉电脑该做什么。

因此，理论上，纯JS可以写出一切前端页面，但很麻烦，相当于自己手搓所有轮子，例如网页中的按钮、窗口、动画等。

如果现有一些造好的轮子，前端程序员只是告诉电脑，我要拿按钮轮子来用，电脑自动调库，执行这个轮子内部的JS代码，而具体细节，不需要前端程序员关心。这就是一种**声明式编程**。

> React官方教程的举例：
**命令式编程**：“编织面团，擀面团，加入番茄酱，加入奶酪，加入火腿，加入菠萝，在石炉中以200摄氏度烘烤......”
**声明式编程**：“请来个夏威夷披萨。”

React是一个**声明式 UI 库**，包含大量前端UI轮子，这些轮子底层用JS编写。

写React代码，即是调用这些轮子，以**声明式编程**编写网页。

### JSX

基于React，当想要在DOM中新增一个元素时，可以直接**声明式**的告诉程序，这个元素长什么样子，即其HTML代码，React可以帮你把它做出来，放在DOM树里。

但是，由于React轮子们的底层由JS实现，这一HTML代码实际上被转化为一个JS对象实例，然后再按照JS语法，在DOM树中增删改。

因此，为JS引入了一个**语法糖**，叫做`JSX`，实现“**将声明式的HTML代码嵌入JS代码**”这一功能。

> 语法糖，又名语法扩展，其作用是：**让代码更加简洁易读**，例如用 ? : 替代if else，用for循环替代while循环。
使用语法糖不会提高代码运行效率，语言的编译器不认语法糖，需要将语法糖还原为原本的语法，再编译运行。

JSX的语法与HTML，JS几乎完全一样，但需要遵循三个规则：

1. 函数只能返回一个DOM元素，如果想要返回多个，必须用一个父元素包裹它们。
2. 所有DOM元素必须显式闭合，即使它们在HTML中是自闭合的，例如 `<img xx="yy">`应当改成 `<img xx="yy"/>`, `<li>oranges`应当改成`<li>oranges</li>`
3. 尽量使用小驼峰命名变量。

所有浏览器都支持JS，但如果要在浏览器中运行JSX，则必须“解语法糖”，将其还原为JS，这一过程需要使用`babel`

此外，还必须显式声明这是一段JSX代码 `<script type="text/jsx"> ...your JSX code...  </script>`

例如，使用React，在DOM树中新增一个h1标题元素，需要调用三个库：

- `react`(核心代码库)
- `react-dom` (使React支持DOM的库)
- `babel` (将JSX转为浏览器能看懂的JS)

``` html
<html>
  <body>
    <div id="app"></div>
    <script src="https://unpkg.com/react@17/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
    <!-- Babel Script -->
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script type="text/jsx">
      const app = document.getElementById('app');
      ReactDOM.render(<h1>Develop. Preview. Ship. 🚀</h1>, app);
    </script>
  </body>
</html>
```

其中，`ReactDOM.render`是用来向DOM中新增元素的函数，其里面的`<h1>Develop. Preview. Ship. 🚀</h1>` 就是JSX中的“嵌入HTML代码”。

##### 教程第4节

学习 React 所需的基本 JS，包括：

- 函数和箭头函数
- 对象
- 数组和数组方法
- 解构
- 模板文本
- 三元运算符
- ES 模块和导入/导出语法

##### 教程第5节

React的三个核心概念，包括组件(Components)、道具(Props)、状态(State)

##### 教程第6节

### 组件 Components

组件是整个网页UI的组成单元，每个组件是一个DOM树的元素，可视为一个封装好的轮子，亦可将几个小组件打包为一个大组件。

将许多组件像“搭积木”一样拼起来，就构成了整个网页UI。

组件彼此间互不依赖，修改网页UI时，可以只修改部分组件，其他保持原样。

> React 理念：**UI = render(data)** <br>
UI：最终呈现给用户的网页
data：数据
render： JSX函数，它是“纯函数”，即return输出完全取决于输入，且除返回一个值外，无其他“副作用”。

JSX函数的首字母必须大写，返回值为一个组件。因此，要使用JSX函数返回的组件，就要像HTML元素那样，套上尖括号`</>`

在上述代码中加入JSX函数：

``` html
<script type="text/jsx">
    const app = document.getElementById('app');
    ReactDOM.render(<h1>Develop. Preview. Ship. 🚀</h1>, app);
</script>
```

``` html
<script type="text/jsx">
    const app = document.getElementById("app")
    function Header() {
        return (<h1>Develop. Preview. Ship. 🚀</h1>)
    }
    ReactDOM.render(<Header />, app);
</script>
```

### 把HTML和JS分开

这一部分和教程关系不大，是我自己折腾的。

众所周知，良好的网页，应当将HTML，CSS，JS拆分为三个不同的文件，分别维护开发。

当只有一个HTML文件时，可在Windows系统文件资源管理器中，直接使用浏览器打开它，此时，浏览器将通过file文件协议，读取这个文件，并解析HTML，此时一切正常。例如：

``` bash
file:///C:/Users/abc/Desktop/a.html
file://wsl.localhost/Ubuntu-18.04/home/abc/react/a.html
```

但是，如果这个HTML引用了一个JS文件，那么，浏览器出于安全考虑，默认将**禁止**这么做，即同源策略(**CORS**，Cross-Origin Resource Sharing)

> Edge F12可查看到如下报错信息：
Access to XMLHttpRequest at 'file://...' from origin 'null' has been blocked by CORS policy: Cross origin requests are only supported for protocol schemes: http, data, isolated-app, chrome-extension, chrome-untrusted, https, edge.

（想象一下，如果一个文件，只要知道其他文件的地址，就可以任意读取本地文件系统下的任何一个文件，这将有多大的安全隐患！）

因此，较为安全的做法是：在项目文件夹内，**架设一个本地服务器**，管理该文件夹内的所有HTML，CSS，JS等文件。然后，通过 `http://localhost:8080/` 访问。

此时，该文件夹内的文件地址，将映射为网络文件地址，例如：
`file://wsl.localhost/Ubuntu-18.04/home/abc/react/a.html` 可映射为 `http://localhost:8080/a.html`，CSS，JS文件同理。

然后，在浏览器中输入`http://localhost:8080/a.html`，以HTTP协议访问本地服务器，使浏览器拿到对应的HTML文件。当引用JS时，再走一次HTTP协议，使浏览器拿到JS文件。

这样一来，`a.html`所能引用的文件，就只能是本地服务器管理下的文件，即该项目文件夹内的文件，这显然是更安全的。

##### 如何用npm架设本地服务器

JS原本是用于在浏览器端运行的代码。如果把所有的HTML，JS都放到用户的浏览器上运行，则不需要node.js和npm

Node.js是一个开源的、跨平台的JavaScript运行环境，它可以让开发者在服务器端运行JS代码。

npm是Node.js的包管理器(如同pip是python的包管理器)

使用npm安装一个名为`http-server`的包：

``` bash
sudo npm install -g http-server # -g 表示全局安装
```

`http-server`通过在Node.js环境中，运行一些JS代码，即可以本地电脑作为服务器端，架设localhost服务器。

最简单的运行方式是，在在项目文件夹内，打开bash，运行`http-server`，即可从默认端口`http://localhost:8080/`访问

`http-server`亦有很多可供设置的参数，详见 [官方文档](https://www.npmjs.com/package/http-server)，在此不做赘述。

##### 附注：关于npm的安装

如果直接使用apt安装Node.js和npm，即：

``` bash
sudo apt install nodejs npm
```

那么，Node.js和npm默认会被安装在`/usr/local`目录下。

如果你害怕npm里的东西太多太乱，也可以直接从Node.js官网下载了一个预编译的版本，并将其解压到`/opt`目录(通常用于存放第三方或额外的软件和应用)

`/opt`目录不在环境变量中，其中的程序，不输入完整路径，就无法直接在bash中运行。

再将其**软连接**到`/usr/local/bin`目录下。软连接由`ln -s`创建，如同Windows中的快捷方式。由于`/usr/local/bin`目录在PATH环境变量中，此后就可以在任何位置的bash中运行npm了。

``` bash
sudo ln -s /opt/node-v16.20.2-linux-x64/bin/npm /usr/local/bin/npm
sudo ln -s /opt/node-v16.20.2-linux-x64/bin/http-server /usr/local/bin/http-server
```
