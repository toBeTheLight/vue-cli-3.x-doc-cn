## Table of Contents

- [简介](#简介)
- [CLI](#cli)
- [CLI服务](#cli服务)
- [约定](#约定)
  - [首页文件](#首页文件)
  - [静态资源处理](#静态资源处理)
  - [环境变量和模式](#环境变量和模式)
- [配置](#配置)
  - [webpack](#webpack)
  - [browserslist](#browserslist)
  - [开发服务器代理](#开发服务器代理)
  - [Babel](#babel)
  - [CSS](#css)
  - [ESLint](#eslint)
  - [TypeScript](#typescript)
  - [单元测试](#单元测试)
  - [E2E测试](#e2e测试)

## 简介

Vue CLI是一个针对Vue.js快速开发的一个完整系统，提供：

- 交互性项目脚手架，通过`@vue/cli`。
- 零配置快速原型，通过`@vue/cli`和`@vue/cli-service-global`。
- 一个运行时依赖（`@vue/cli-service`）：
  - 可升级；
  - 以webpack为基础，有默认的合理配置；
  - 通过项目内配置文件可配置；
  - 通过插件可扩展
- 集成了前端生态系统中的最好工具的丰富官方插件。

Vue CLI旨在成为Vue生态系统的标准工具基准。它可以确保各种构建工具在合理的默认设置下可以顺利工作，已助于你可专注于编写你的应用，而不用花费大量时间在配置中挣扎。同时，也保证了调整各个工具配置的灵活性。

## CLI

CLI被全局安装，并且在你的终端中提供`vue`命令：

``` sh
npm install -g @vue/cli
vue create my-project
```

查看全部可用命令参阅[CLI文档](./cli.md)。

## CLI服务

`@vue/cli-service`是在每个由`@vue/cli`创建的每格项目中本地安装的依赖项。它包含了加载其他插件的核心服务，为你的项目提供`vue-cli-service` binary文件。如果你熟悉[create-react-app](https://github.com/facebookincubator/create-react-app)的话，`@vue/cli-service`本质上相当于`react-scripts`，但是更灵活。

查看全部可用命令参阅[CLI服务文档](./cli-service.md)。

## 约定

### 首页文件

*The Index Page*

`public/index.html`文件是一个会被[html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin)处理的模板。构建期间，资源文件链接会被自动插入此模板。此外，Vue ClI还会自动插入资源提示（`preload/prefetch`）,manifest/icon链接（使用PWA插件时），为了保证最佳性能还会内联webpack runtime/chunk manifest。

### 静态资源处理

*Static Assets Handling*

静态资源文件可以使用两种不同的方式处理:

- 在JS中导入，或者通过相对路径在template/CSS部分引用。这样的引用会被webpack处理。

- 放在`public目录中，并通过绝对路径引用。这样使用的文件只会被复制过去，不会经过webpack处理。

查看更多细节参阅[静态资源处理](./assets.md)。

### 环境变量和模式

根据目标环境自定义应用行为是中普遍的需求。比如，你可能希望应用在开发/演示/生产环境下使用不同的API或凭证。

Vue CLI全面支持了指定不同的环境变量使用模式和`.env`。

查看更多细节参阅[环境变量和模式](./env.md)。

## 配置

使用`vue create`创建的项目开箱即用。插件被设计为可以彼此协作，因此大多数情况下，你只需要在交互命令下选取你需要的功能即可。

不过我们也明白迎合每一种可能的需求是不可能的，而且项目的需求也可能随时发生变化。由Vue CLI创建的项目也允许你配置工具的几乎所有方面，而不需要eject。

### vue.config.js

Vue CLI项目的许多方面都允许你通过在你项目的根目录下放置一个`vue.config.js`文件来配置。这个文件可能已有，这取决于你创建项目时的选择。

`vue.config.js`应该导出一个对象，比如：

``` js
// vue.config.js
module.exports = {
  lintOnSave: true
}
```

查看完整的可能的选项列表，参阅[这里](./config.md)。

### webpack

可能最常见的配置需要是调整webpack内部的配置。Vue CLI提供了灵活的方式来实现。

查看全部详情参阅[这里](./webpack.md)。

### browserslist

你会注意到`package.json`中的`browserslist`字段，它指定了该项目目标的一系列浏览器。这个值会被`babel-preset-env`和`autoprefixer`用来确定所需的JavaScript polyfills和CSS浏览器前缀。

如何指定浏览器范围参阅[这里](https://github.com/ai/browserslist)。

### 开发服务器代理

*Dev Server Proxy*

如果你的前端应用和后端API服务不在同一主机上运行，你需要在开发阶段将API请求代理给API服务器。可以通过`vue.config.js`中的`devServer.proxy`选项配置。
查看更多细节参阅[设置Proxy](./cli-service.md#configuring-proxy)。

### Babel

Babel可以通过`.babelrc`或`package.json`中的`babel`字段配置。

所有的Vue CLI应用都使用`@vue/babel-preset-app`，它包括`babel-preset-env`，JSX支持和针对更小的包体积的优化配置。更多细节和预设置参阅[它的文文档](https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/babel-preset-app)。 

### CSS

Vue CLI项目支持[PostCSS](http://postcss.org/)，[CSS Modules](https://github.com/css-modules/css-modules)和包括[Sass](https://sass-lang.com/)，[Less](http://lesscss.org/)，[Stylus](http://stylus-lang.com/)在内的预处理器。

查看更多有关CSS的配置参阅[这里](./css.md)。

### ESLint

ESLint可以通过`.eslintrc`文件或`package.json`文件中的`eslintConfig`字段配置。

查看更多细节参阅[@vue/cli-plugin-eslint](https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint)。

### TypeScript

TypeScript可以通过`tsconfig.json`配置。

查看更多细节参阅[@vue/cli-plugin-typescript](https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-typescript)。

### 单元测试

*Unit Testing*

- #### Jest

  查看更多细节参阅[@vue/cli-plugin-unit-jest](https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-unit-jest)。

- #### Mocha (通过`mocha-webpack`)

  查看更多细节参阅[@vue/cli-plugin-unit-mocha](https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-unit-mocha)。

### E2E测试

- #### Cypress

  查看更多细节参阅[@vue/cli-plugin-e2e-cypress](https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-e2e-cypress)。

- #### Nightwatch

  查看更多细节参阅[@vue/cli-plugin-e2e-nightwatch](https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-e2e-nightwatch)。

<!-- ## Development

- [Contributing Guide](https://github.com/vuejs/vue-cli/blob/dev/.github/CONTRIBUTING.md)
- [Plugin Development Guide](https://github.com/vuejs/vue-cli/blob/dev/docs/plugin-dev.md) -->

