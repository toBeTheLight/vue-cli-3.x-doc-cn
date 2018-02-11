## 配置webpack

- [基本配置](#基本配置)
- [链式](#链式)
- [检查项目的webpack配置](#检查项目的webpack配置)
- [作为文件使用已解析配置](#作为文件使用已解析配置)

### 基本配置

调整webpack配置最简单的方法是在`vue.config.js`文件中为`configureWebpack`选项提供一个对象：

``` js
// vue.config.js
module.exports = {
  configureWebpack: {
    plugins: [
      new MyAwesomeWebpackPlugin()
    ]
  }
}
```

这个对象会被[webpack-merge](https://github.com/survivejs/webpack-merge)合并进最终的webpack配置。

如果你需要基于环境的条件行为，或者想要直接改变配置，可以使用一个函数（在env变量设置之后会被延迟计算）。该函数接受已解析的配置作为参数。在函数内，你可以直接改变配置，或者返回一个会被合并的对象：

``` js
// vue.config.js
module.exports = {
  configureWebpack: config => {
    if (process.env.NODE_ENV === 'production') {
      // mutate config for production...
    } else {
      // mutate for development...
    }
  }
}
```

### 链式

*高级*

内部的webpack配置使用[webpack-chain](https://github.com/mozilla-neutrino/webpack-chain)维护。这个库提供了对原始webpack配置的抽象，这种用法下，能够定义指定的loader规则和指定的插件，并且能够在之后“tap”进入这些规则并修改其选项。

这允许我们对内部配置进行细粒度的控制，这有些例子：

#### 转译一个依赖模块

默认情况下，Babel配置跳过

``` js
// vue.config.js
module.exports = {
  chainWebpack: config => {
    config.module
      .rule('js')
        .include
          .add(/some-module-to-transpile/)
  }
}
```

#### 修改插件选项

``` js
// vue.config.js
module.exports = {
  chainWebpack: config => {
    config
      .plugin('html')
      .tap(args => {
        return [/* 传入html-webpack-plugin's构造函数的新参数 */]
      })
  }
}
```

你需要熟悉[webpack-chain的 API](https://github.com/mozilla-neutrino/webpack-chain#getting-started)并且要[读一些源代码](https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-service/lib/config)以便了解如何去充分利用此选项，不过它为你提供了相比直接了当的修改更直观更安全的方式来修改webpack配置。

### 检查项目的webpack配置

由于`@vue/cli-service`抽象除了webpack配置，可能会使你更难理解配置中有什么，特别在你自己尝试调整的时候。

`vue-cli-service`暴露了`inspect`命令用来检查已解析的webpack配置。全局的`vue` binary也提供了`inspect`命令，它只是代理项目中的`vue-cli-service inspect`。

这个命令会默认输出到stdout，所以你也可以将其重定向到一个文件以便于检查：

``` sh
vue inspect > output.js
```

注意，输出内容不是个可用的webpack配置文件，它只是个用于检查的序列化格式。

你还可以只检查配置的某些路径，用以缩小范围：

``` sh
# 只检查第一条规则
vue inspect module.rules.0
```

### 作为文件使用已解析配置

一些外部工具可能需要以文件形式访问已经解析的配置文件，例如，需要webpack配置的IDE或者命令行工具。这种情况下，你可以使用下方的路径：

```
<projectRoot>/node_modules/@vue/cli-service/webpack.config.js
```

该文件动态解析，并且导出`vue-cli-service`命令行使用的完全相同的配置，包含来自插件的和自定义的配置。
