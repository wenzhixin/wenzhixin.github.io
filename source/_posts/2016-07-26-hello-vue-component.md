---
layout: post
title: 开发 vue-bootstrap-table 组件之单文件组件
date: 2016-07-26 09:58:44
comments: true
categories: [Vue, JavaScript]
---

根据文档[单文件组件](http://vuejs.org.cn/guide/application.html#单文件组件)一节，我们可以将组件集成为一个文件，将 html，css，JavaScript 代码都放到同个文件中，最终编译成我们想要的文件。vue 文件的基本模板为：

```
<template>
    <div>
        <h1>{{message}}</h1>
    </div>
</template>
<script>
module.export = {
    props: {
        message: {
            type: String,
            default: 'Hello Vue.js'
        }
    }
};
</script>
<style>
h1 {font-size: 24px;}
</style>
```

其中 template 为 html 代码，script 为 JavaScript 代码，style 为 css 代码。

这里使用最简单的例子理解如何创建 vue 单文件组件，我们将该文件保存为 `Hello.vue`，并创建 `main.js` 文件：

```
Hello = require('./Hello.vue');
module.exports = Hello;
```

然后使用官方工具[vue-cli](https://github.com/vuejs/vue-cli)，对我们的组件进行编译，提供了几个模板：

- [webpack](https://github.com/vuejs-templates/webpack) - A full-featured Webpack + vue-loader setup with hot reload, linting, testing & css extraction.

- [webpack-simple](https://github.com/vuejs-templates/webpack-simple) - A simple Webpack + vue-loader setup for quick prototyping.

- [browserify](https://github.com/vuejs-templates/browserify) - A full-featured Browserify + vueify setup with hot-reload, linting & unit testing.

- [browserify-simple](https://github.com/vuejs-templates/browserify-simple) - A simple Browserify + vueify setup for quick prototyping.

- [simple](https://github.com/vuejs-templates/simple) - The simplest possible Vue setup in a single HTML file

在这里我使用的是 browserify-simple 的方式。根据文档进行安装即可：

```
vue init bro"wserify-simple hello
```

然后将上面创建两个文件放到 hello/src 下，然后修改 package.json 中的
```
"build": "cross-env NODE_ENV=production browserify src/main.js > dist/vue-hello.js"
```

运行 `npm run build`，就可以在 dist 下得到我们想要的文件了。