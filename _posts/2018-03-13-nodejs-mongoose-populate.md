---
title: "NodeJS: Mongoose Populate 基本使用"
categories:
  - NodeJS
tags:
  - Mongoose
---

## 环境
* 操作系统: Ubuntu 16.04
* Node: v7.0.0
* Express: 4.x

## 模块及样式
markdown解析工具 和 样式及语法高亮的插件有很多，比如解析工具还有[markdown-js](https://github.com/evilstreak/markdown-js)，语法高亮还有[Google Code Prettify](https://github.com/google/code-prettify)，等等。

这里我们只介绍使用其中的三个，作为一个组合。

* Markdown解析: [marked v0.3.6](https://github.com/chjj/marked)
* Markdown-css: [github-markdown-css](https://github.com/sindresorhus/github-markdown-css)
* 语法高亮: [prismjs](http://prismjs.com/)

### Marked
> A full-featured markdown parser and compiler, written in JavaScript. Built for speed.

这是它的[github](https://github.com/chjj/marked)上的介绍，安装和基本使用在[github](https://github.com/chjj/marked)上都有，我使用它的最新版本 v0.3.6。
用它来解析 *markdown* 语法。

### Github-markdown-css
> The minimal amount of CSS to replicate the GitHub Markdown style

用来给解析好的 *html* 加样式，这里有个使用它的示例: [Demo](https://sindresorhus.com/github-markdown-css/)

### Prismjs
> Prism is a lightweight, extensible syntax highlighter, built with modern web standards in mind. It’s used in thousands of websites, including some of those you visit daily.

它是一款轻量、可扩展的代码语法高亮库，使用现代化的 Web 标准构建的，同时支持大部分流行的编程语言，并且支持多种主题样式。使用起来也很简单，只需要在 *html* 中引入 *css* 和 *js* 文件即可。

我们可以根据需要自己在 [Prismjs Download](http://prismjs.com/download.html) 中选择主题、语言和各种插件。

## 目录介绍
就是 *express-generator* 默认生成的目录，在根目录加了个 markdown 文件夹，里面放 <code>.md</code> 文件。在 public 目录里的 javascript 和 stylesheets 目录分别放下载好的 *js* 和 *css* 文件。
```
app/
	bin/
    	www
    markdown/
    	README.md  # marked github上的readme
    node_modules/
    	...
    public/
    	javascripts/
        	prism.js  # 1
        stylesheets/
        	style.css
        	prism.css  # 2
            github-markdown.css  # 3
    routes/
    	index.js
    views/
    	layout.jade
    	index.jade
    app.js
    package.json
```
## 基本使用
将 routes/index.js 改为
```javascript
var express = require('express');
var router = express.Router();
var marked = require('marked');
var fs = require('fs');

/* GET home page. */
router.get('/', function(req, res, next) {
  fs.readFile('markdown/README.md', function(err, data) {
    var html = marked(data.toString());
    res.send(html);
  });
});

module.exports = router;
```

显示效果
![显示效果1](http://img.blog.csdn.net/20161202225606039)

这么写的话，整个页面只能单独的显示一个 markdown 文件，要引入 css 或者 js 的话会很麻烦。

## 使用 jade + Github-markdown-css + prism
express 默认的模板引擎为 *jade*，所以这里以 *jade* 为例。
将 routes/index.js 改为
```javascript
var express = require('express');
var router = express.Router();
var marked = require('marked');
var fs = require('fs');

/* GET home page. */
router.get('/', function(req, res, next) {
  fs.readFile('markdown/README.md', function(err, data) {
    var html = marked(data.toString());
    res.render('index', {mdContent: html});
  });
});

module.exports = router;
```
在 views/layout.jade 中引入 prism.js、prism.css 和 github-markdown.css。
```
doctype html
html
  head
    title= title
    link(rel='stylesheet', href='/stylesheets/style.css')
    link(rel='stylesheet', href='/stylesheets/github-markdown.css')
    link(rel='stylesheet', href='/stylesheets/prism.css')
  body
    block content
    script(src='/javascripts/prism.js')
```

根据 [github-markdown-css](https://github.com/sindresorhus/github-markdown-css) 上的使用说明
> Import the github-markdown.css file and add a markdown-body class to the container of your rendered Markdown and set a width for it.

解析后的 markdown 要放在一个以 <code>markdown-body</code> 为类名的容器中。

views/index.jade 改为
```jade
extends layout

block content
  .markdown-body
    != mdContent

```

这里的 <code>mdContent</code> 一会儿渲染为 *marked* 解析后的内容。

我们还可以在 stylesheets/style.css 中加上
```css
.markdown-body {
    box-sizing: border-box;
    min-width: 200px;
    max-width: 980px;
    margin: 0 auto;
    padding: 45px;
}
```
整体页面显得更规整一点。

显示效果
![显示效果2](http://img.blog.csdn.net/20161202230211526)

这里代码中的 <code>=</code> 与背景不太和谐，我们只要改一下 prism.css 就好了
```css
.token.operator,
.token.entity,
.token.url,
.language-css .token.string,
.style .token.string {
	color: #a67f59;
	/*background: hsla(0, 0%, 100%, .5);*/
	background: transparent;
}
```

全部完成，看起来舒服多啦。

完整代码下载: [Github express+markdown](https://github.com/Els-y/csdn-demos/tree/master/express%2Bmarkdown)

以上所有，如有错误，麻烦指出，我会及时更改的。