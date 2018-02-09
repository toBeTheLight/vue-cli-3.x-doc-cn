## 环境变量和模式

- [概览](#概览)
- [模式](#模式)
- [在客户端代码中使用环境变量](#在客户端代码中使用环境变量)
- [本地变量](#本地变量)

### 概览

你可以通过将下方文件放入项目的根路径来指定env变量：

``` sh
.env                # 在所有情况下加载s
.env.local          # 在所有情况下加载，被git忽略
.env.[mode]         # 只在指定模式下加载
.env.[mode].local   # 只在指定模式下加载，被git忽略
```

env文件只包含环境变量的键值对：

```
FOO=bar
VUE_APP_SECRET=secret
```

加载的变量可用于所有的`vue-cli-service`命令，插件和依赖项。

### 模式

**Mode**时Vue CLI的重要概念。默认情况下，Vue CLI项目中有三种模式：

- `vue-cli-service serve`使用`development`
- `vue-cli-service build`使用`production`
- `vue-cli-service test`使用`test`

注意，模式和`NODE_ENV`是不同的，模式可以包含不同的环境变量。意味着，每种模式下默认情况会将`NODE_ENV`设置为相同的值。例如，`NODE_ENV`在开发模式下会被设置为`"development"`。

你可以通过带有`.env`后缀的文件来设置环境变量只在特定模式下有效。比如，如果你在项目根路径下创建了`.env.development`文件，那么在这个文件中声明的变量将只会在开发模式下加载。

### 在客户端代码中使用环境变量

只有以`VUE_APP_`开头的变量才会静态的嵌入到带有`webpack.DefinePlugin`的客户端代码中。你可以在应用程序中像这样使用它。

``` js
console.log(process.env.VUE_APP_SECRET)
```

在构建过程中，`process.env.VUE_APP_SECRET`会被替换为相应的值。例如，在`VUE_APP_SECRET=secret`的情况下，会被`"secret"`替换。

除了`VUE_APP_*`变量，还有两个特殊的变量，这两个变量在应用代码中总是可用的。

- `NODE_ENV` - 这个值会是`"development"`，`"production"`或`"test"`中的一个，依赖于应用正在运行的[模式](#模式)。
- `BASE_URL` - 对应于`vue.config.js`中的`baseUrl`选项，时项目部署的基本路径（base path）。

### 本地变量

有时，你可能有一些不该提交到代码库中的变量，特别是你的项目托管在公共仓库。这种情况下你应该使用`.env.local`文件。本地env文件在`.gitignore`中默认忽略。

`.local`也可以添加到特定模式的env文件，例如，`.env.development.local`将在开发模式中加载，并且被git忽略。
