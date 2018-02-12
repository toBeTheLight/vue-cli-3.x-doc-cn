## CLI服务

- [使用binary](#使用binary)
- [serve](#serve)
  - [配置Proxy](#配置Proxy)
- [build](#build)
  - [缓存和并行模式](#缓存和并行模式)
  - [构建为库或Web组件](#构建为库或Web组件)
  - [DLL模式](#DLL模式)
- [检查](#检查)
- [查看所有可用命令](#查看所有可用命令)

### 使用binary

在Vue CLI项目中，`@vue/cli-service`会安装一个叫做 `vue-cli-service`的binary，你可以在npm脚本命令中直接访问这个binary，或者在终端中使用`./node_modules/.bin/vue-cli-service`。

这就是使用预设默认设置时在项目的`package.json`中看到的内容：

``` json
{
  "scripts": {
    "serve": "vue-cli-service serve --open",
    "build": "vue-cli-service build"
  }
}
```

### serve

```
用法: vue-cli-service serve [options]

选项:

  --open    启动服务器打开浏览器
  --mode    指定env模式（默认：development）
  --host    指定域名（默认：0.0.0.0）
  --port    指定端口（默认: 8080）
  --https   使用https（默认：false）
```

`vue-cli-service serve`启动一个基于[webpack-dev-server](https://github.com/webpack/webpack-dev-server)的开发服务。带有开箱即用的模块热替换（HMR）。

你可以使用`vue.config.js`文件中的`devServer`选项配置开发服务器的行为：

``` js
module.exports = {
  devServer: {
    open: process.platform === 'darwin',
    host: '0.0.0.0',
    port: 8080,
    https: false,
    hotOnly: false,
    proxy: null, // string | Object
    before: app => {
      // app is an express instance
    }
  }
}
```

除了这些默认值，[`webpack-dev-server`的所有配置都支持](https://webpack.js.org/configuration/dev-server/)。

#### 配置Proxy

`devServer.proxy`可以是一个指向开发API服务器的字符串：

``` js
module.exports = {
  devServer: {
    proxy: 'http://localhost:4000'
  }
}
```

这会告知开发服务器代理所有未知的请求（不匹配静态文件的请求）到`http://localhost:4000`。

如果你希望对代理行为有更多的控制权，你也可以使用带有`path: options`键值对的对象。查看所有配置参阅[http-proxy-middleware](https://github.com/chimurai/http-proxy-middleware#proxycontext-config)：

``` js
module.exports = {
  devServer: {
    proxy: {
      '/api': {
        target: '<url>',
        ws: true
      },
      '/foo': {
        target: '<other_url>'
      }
    }
  }
}
```

### build

```
用法: vue-cli-service build [options] [entry|pattern]

Options:

  --mode    指定env模式（默认: production）
  --dest    指定输出文件夹（默认: dist）
  --target  app | lib | wc | wc-async (默认: app)
  --name    lib模式或web组件模式下的名字(默认: package.json中的"name"或入口文件名）
```

`vue-cli-service build`在`dist/`目录下生成一个生产可用的bundle，包含JS/CSS/HTML压缩，优化缓存的vendor代码分割。manifest代码块会被内联到html中。

#### 缓存和并行模式

- 默认启动了Babel/TypeScript转译的`cache-laoder`。
- 当有多个CPU内核时，将启用`thread-loader`进行Babel/TypeScript的转译。

#### 构建为库或Web组件

也可以将项目内的任何组件构建为库或Web组件。查看等多细节参阅[Build Targets](./build-targets.md)。

#### DLL模式

如果你的应用程序具有大量的依赖库，则可以通过选择进入DLL模式来提高构建性能。DLL模式将你的依赖构建到一个单独的vendor bundle中，只要你的依赖关系没有变，此包会在以后的构建中复用。

要启用DLL模式，请将`vue.config.js`文件中的`dll`设置为`true`：

``` js
// vue.config.js
module.exports = {
  dll: true
}
```

默认情况下，会将**`package.json`中`dependencies`字段中列出的所有模块**构建到DLL bundle中。 正确列出你的依赖是非常重要的，否则它可能会包含不必要的代码。

如果你希望更好地控制在DLL bundle中包含的模块，还可以为`dll`选项提供一个模块数组：

``` js
// vue.config.js
module.exports = {
  dll: [
    'dep-a',
    'dep-b/some/nested/file.js'
  ]
}
```

### 检查

```
用法： vue-cli-service inspect [options] [...paths]

选项：

  --mode    指定env模式（默认：development）
```

你可以使用`vue-cli-service inspect`检查Vue CLI项目中的webpack设置。查看更多细节参阅[Inspecting Webpack Config](./webpack.md#inspecting-the-projects-webpack-config)。

### 查看所有可用命令

一些CLI插件会向`vue-cli-service`注入额外的命令。比如，`@vue/cli-plugin-eslint`会插入`vue-cli-service lint`命令。你可以运行下面的指令来查看所有添加的命令：

``` sh
./node_modules/.bin/vue-cli-service help
```

你还可以通过下面的方式了解每个命令的可用选项：

``` sh
./node_modules/.bin/vue-cli-service help [command]
```
