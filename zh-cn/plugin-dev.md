# 插件开发指南

## 核心概念

- [Creator](#creator)
- [Service](#service)
- [CLI Plugin](#cli-plugin)
- [Service Plugin](#service-plugin)
- [Generator](#generator)
- [Prompts](#prompts)

该系统主要有两部分：

- `@vue/cli`：全局安装，暴露`vue create <app>`命令；
- `@vue/cli-service`：本地安装，暴漏`vue-cli-service`命令。

两者都使用基于插件的体系。

### Creator

[Creator][creator-class]是调用`vue create <app>`时创建的类。负责提示偏好，调用生成器和安装依赖。

### Service

[Service][service-class]是调用`vue-cli-service <command> [...args]`时创建的类。负责管理内部的webpack配置，公开服务命令，构建项目。

### CLI插件

CLI插件是一个可以将功能特性添加到`@vue/cli`项目的npm包。他应该总是包含一个[Service插件](#service-plugin)作为主要导出内容，并可以包含一个[Generator](#generator)一个[Prompt文件](#prompts-for-3rd-party-plugins)。

典型的CLI插件的文件夹结构如下所示：

```
.
├── README.md
├── generator.js  # generator （可选）
├── prompts.js    # prompts file （可选）
├── index.js      # service plugin
└── package.json
```

### Service插件

Service插件在每次创建服务实例时自动加载 - 即，每次在项目中调用`vue-cli-service`命令时。

注意，我们这里谈论的“service插件”的概念比作为npm包发布的“CLI插件”的概念更窄。“service插件”只是指在初始化时由`@vue/cli-service`加载的模块，通常是“CLI插件”的一部分。

另外，`@vue/cli-service`'的[内建命令][commands]和[配置模块][config]也都作为service插件来实现。

Service插件应该导出一个接受两个参数的函数：

- [插件API][plugin-api]实例

- 包含`vue.config.js`中指定的项目本地选项或`package.json`文件中的`"vue"`字段的对象。
例如：

``` js
module.exports = (api, projectOptions) => {
  api.chainWebpack(webpackConfig => {
    // webpack-chain修改webpack配置
  })

  api.configureWebpack(webpackConfig => {
    // 修改webpack配置
    // 会返回一个会被webpack-merge合并的对象
  })

  api.registerCommand('test', args => {
    // 注册`vue-cli-service test`
  })
}
```

#### Service插件中的环境变量

关于环境变量的一个重要的事情是得知他们什么时候被解析了。通常，像`vue-cli-service serve`或`vue-cli-service build`这样的命令总是头等调用`api.setMode()`。然而，这也意味着当一个service插件被调用时，这些环境变量可能还不能用：

``` js
module.exports = api => {
  process.env.NODE_ENV // 可能还没被解析

  api.registerCommand('build', () => {
    api.setMode('production')
  })
}
```

相反，在`configureWebpack`或`chainWebpack`函数中依赖环境变量是比较安全的，只有当最后调用`api.resolveWebpackConfig()`时，才会被懒加载：

``` js
module.exports = api => {
  api.configureWebpack(config => {
    if (process.env.NODE_ENV === 'production') {
      // ...
    }
  })
}
```

#### 在插件中解析webpack配置

插件可通过调用`api.resolveWebpackConfig()`来取得已解析的webpack配置。每次调用生成一个新的webpack配置，可根据需要进一步突变：

``` js
api.registerCommand('my-build', args => {
  // 确保设置了模式并且记载环境变量
  api.setMode('production')

  const configA = api.resolveWebpackConfig()
  const configB = api.resolveWebpackConfig()

  // 为不同目的改变configA和configB
})
```

或者，插件也可以通过调用`api.resolveChainableWebpackConfig()`获得一个新的[链式性配置](https://github.com/mozilla-neutrino/webpack-chain)：

``` js
api.registerCommand('my-build', args => {
  api.setMode('production')

  const configA = api.resolveChainableWebpackConfig()
  const configB = api.resolveChainableWebpackConfig()

  // 链式修改configA和configB

  const finalConfigA = configA.toConfig()
  const finalConfigB = configB.toConfig()
})
```

#### 第三方插件的自定义选项

`vue.config.js`的导出将会[根据schema验证](https://github.com/vuejs/vue-cli/blob/dev/packages/%40vue/cli-service/lib/options.js#L3)以避免错误拼写和错误的配置。但是，第三方插件依然可以允许用户通过`pluginOptions`字段配置其行为。例如，使用如下`vue.config.js`：

``` js
module.exports = {
  pluginOptions: {
    foo: { /* ... */ }
  }
}
```

第三方插件可以读取`projectOptions.pluginOptions.foo`来确定条件配置。

### 生成器

*Generator*

作为包发布的CLI插件包括一个`generator.js`或`generator/index.js` 文件。插件中的生成器会在两种情况下被调用：

- 项目创建期间，如果CLI插件作为项目预设的一部分进行安装时

- 项目创建之后，安装并通过`vue invoke`单独调用时

[生成器API][generator-api]允许生成器将其他依赖项或字段添加到`package.json`文件，并向项目中添加文件。

生成器应该导出一个接受三个参数的函数：

1. `生成器API`实例;

2. 这个插件的生成器配置。这些配置在项目创建的提示阶段被解析，或者从`~/.vuerc`保存的预设至中。例如，如果保存的`~/.vuerc`看起来像这样：

    ``` json
    {
      "presets" : {
        "foo": {
          "plugins": {
            "@vue/cli-plugin-foo": { "option": "bar" }
          }
        }
      }
    }
    ```

    如果用户使用`foo`预设创建一个项目，那么`@vue/cli-plugin-foo`的生成器将接受`{ option: 'bar' }`作为它的第二个参数。

    对于第三方插件，配置会在用户执行`vue invoke`命令时从提示或者命令行解析(查看[第三方插件提示](#第三方插件提示))。

3. 整个预设（`presets.foo`）会作为第三个参数。

**示例：**

``` js
module.exports = (api, options, rootOptions) => {
  // 修改package.json字段
  api.extendPackage({
    scripts: {
      test: 'vue-cli-service test'
    }
  })

  // 使用ejs复制和渲染./template中的所有文件
  api.render('./template')

  if (options.foo) {
    // 有条件的生成文件
  }
}
```

### 提示

*Prompts*

#### 内建插件的提示

只有内建插件能够在创建新项目时自定义初始提示，提示模块位于[`@vue/cli`包内][prompt-modules]。

提示模块应该导出一个函数接受[提示模块API][prompt-api]实例。提示使用[询问者（inquirer）](https://github.com/SBoudrias/Inquirer.js)进行显示：

``` js
module.exports = api => {
  // injectFeature应该是有效的查询者选择对象
  cli.injectFeature({
    name: 'Some great feature',
    value: 'my-feature'
  })

  // injectPrompt需要一个有效的查询者提示对象
  cli.injectPrompt({
    name: 'someFlag',
    // 确保你的提示只在用户选了你的特性功能时显示
    when: answers => answers.features.include('my-feature'),
    message: 'Do you want to turn on flag foo?',
    type: 'confirm'
  })

  // 当完成所有提示之后，将你的插件注入到将会被传到生成器的选项中
  cli.onPromptComplete((answers, options) => {
    if (answers.features.includes('my-feature')) {
      options.plugins['vue-cli-plugin-my-feature'] = {
        someFlag: answers.someFlag
      }
    }
  })
}
```

#### 第三方插件提示

第三方插件通常在创建项目后手动安装，用户将通过调用“vue invoke”来初始化插件。如果插件的根目录中包含一个`prompts.js`，在调用过程中它将被使用。这个文件需要导出一个由`Inquirer.js`处理的[问题](https://github.com/SBoudrias/Inquirer.js#question)数组。解析的答案对象将会作为选项配置被传给插件的生成器。

或者用户可以跳过提示，并通过命令行传递选项直接初始化插件，像这样：

``` sh
vue invoke my-plugin --mode awesome
```

## 关于核心插件开发的注意事项

> 本节只适用于你在这个库内研究内建插件时。

注入在这个库(例如，`chai`被`@vue/cli-plugin-unit-mocha/generator/index.js`注入)之外的额外依赖的带有生成起的插件需要在自己的的`devDependencies`字段列出那些依赖。这确保了：

1. 包总是在这个库的根`node_modules`存在，可确保我们不需要在每次测试时都重新安装它。

2. `yarn.lock`保持一致，以便于CI（持续集成）可以更好的用它来推断缓存行为。

[creator-class]: https://github.com/vuejs/vue-cli/tree/dev/packages/@vue/cli/lib/Creator.js
[service-class]: https://github.com/vuejs/vue-cli/tree/dev/packages/@vue/cli-service/lib/Service.js
[generator-api]: https://github.com/vuejs/vue-cli/tree/dev/packages/@vue/cli/lib/GeneratorAPI.js
[commands]: https://github.com/vuejs/vue-cli/tree/dev/packages/@vue/cli-service/lib/commands
[config]: https://github.com/vuejs/vue-cli/tree/dev/packages/@vue/cli-service/lib/config
[plugin-api]: https://github.com/vuejs/vue-cli/tree/dev/packages/@vue/cli-service/lib/PluginAPI.js
[prompt-modules]: https://github.com/vuejs/vue-cli/tree/dev/packages/@vue/cli/lib/promptModules
[prompt-api]: https://github.com/vuejs/vue-cli/tree/dev/packages/@vue/cli/lib/PromptModuleAPI.js
