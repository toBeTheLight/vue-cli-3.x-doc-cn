## CLI

- [安装](#安装)
- [用法](#用法)
- [创建一个新项目](#创建一个新项目)
- [零配置原型](#零配置原型)
- [在现有项目中安装插件](#在现有项目中安装插件)
- [检查项目的Webpack配置](#检查项目的Webpack配置)
- [拉取`vue-cli@2.x`模板（旧API）](#拉取`vue-cli@2.x`模板（旧API）)

### 安装

``` sh
npm install -g @vue/cli
vue create my-project
```

### 用法

```
用法: vue <command> [options]

命令:

  create [options] <app-name>      创建一个由vue-cli-service支持的新项目
  invoke <plugin> [pluginOptions]  调用已经创建的项目中插件的生成器
  inspect [options] [paths...]     使用vue-cli-service检查项目中的webpack配置
  serve [options] [entry]          在开发者模式下以零配置运行一个js或vue文件
  build [options] [entry]          在生产模式下以零配置构建一个js或vue文件
  init <template> <app-name>       从远程模板生成项目（旧api 需要@vue/cli-init）
```

对于每个命令，还可以使用`vue <command> --help`来查看更详细的用法。

### 创建一个新项目

```
用法： create [options] <app-name>

创建一个由vue-cli-service支持的新项目


选项：

  -p, --preset <presetName>       跳过提示并使用保存的预设
  -d, --default                   跳过提示并使用默认预设
  -i, --inlinePreset <json>       跳过提示并使用内联的JSON字符串作为预设
  -m, --packageManager <command>  安装依赖关系时使用指定的npm客户端
  -r, --registry <url>            安装依赖时使用指定的npm源（只在npm下生效）
  -f, --force                     覆盖目标目录，如果存在
  -h, --help                      输出用法信息
```

``` sh
vue create my-project
```

<p align="center">
  <img width="682px" src="https://raw.githubusercontent.com/vuejs/vue-cli/dev/docs/screenshot.png">
</p>

#### 预设值

在你选择完功能特性之后，可以选择将其保存为一份预设值以便将来可以复用。如果要删除保存的预设值，可以通过编辑`~/.vuerc`实现。

### 零配置原型

你可以通过`vue serve`和`vue build`命令在只有一个`*.vue`文件的情况下开始一个原型，但是需要先安装一个额外的全局插件：

``` sh
npm install -g @vue/cli-service-global
```

`vue serve`的缺点是它依赖于全局安装的依赖，在不同的机器上可能不同。所以，只建议在快速开始原型时使用。

#### vue serve

```
用法： serve [options] [entry]

零配置在开发模式下启动一个.js或.vue文件

配置：

  -o, --open  打开浏览器
  -h, --help  输出用法信息
```

你只需要一个`*.vue`文件：

``` sh
echo '<template><h1>Hello!</h1></template>' > App.vue
vue serve
```

`vue serve`使用和`vue create`创建的项目相同的默认设置（webpack, babel, postcss 和 eslint）。它自动推断当前目录下的入口文件 - 入口文件可以是`main.js`, `index.js`, `App.vue`或`app.vue`中的一个。你也可以指定入口文件：

``` sh
vue serve MyComponent.vue
```

如果需要的话，你还可以提供一个`index.html`, `package.json`，安装使用本地依赖, 甚至使用对应的文件配置babel，postcss和eslint。

#### vue build

```
用法： build [options] [entry]

零配置在生产模式下构建一个.js或.vue文件


选项：

  -t, --target <target>  构建目标（app | lib | wc | wc-async, 默认: app）
  -n, --name <name>      库或web组件的名字（默认：入口文件名）
  -d, --dest <dir>       指定输出文件夹（默认: dist）
  -h, --help             输出用法信息
```

你也可以使用`vue build`将目标文件构建到生产bundle中进行部署：

``` sh
vue build MyComponent.vue
```

`vue build`还提供了将组件构建为库或Web组件的功能。查看更多详情参阅[Build Targets](./build-targets.md)。

### 在现有项目中安装插件

每个CLI插件附带一个生成器（创建文件）和一个运行时插件（调整webpack核心配置并注入新命令）。当你使用`vue create`创建一个新项目时，根据你的特性选择，将会为你预先安装一些插件。 如果您想要将插件安装到已经创建的项目中，只需要先简单的安装它：

``` sh
npm install -D @vue/cli-plugin-eslint
```

然后你可以调用插件的生成器，以使其在你的项目中生成文件：

``` sh
# @vue/cli-plugin- 前缀可以省略
vue invoke eslint
```

另外，您可以将选项传递给插件：

``` sh
vue invoke eslint --config airbnb --lintOn save
```

建议在运行`vue invoke`前提交项目的当前状态，便于你查看文件更改，或在必要时恢复。

### 检查项目的Webpack配置

你可以在Vue CLI项目中使用`vue inspect`查看webpack配置。查看更多详情参阅[Inspecting Webpack Config](./webpack.md#inspecting-the-projects-webpack-config)。

### 拉取`vue-cli@2.x`模板（旧API）

`@vue/cli`使用相同的`vue` binary，所以它被改写为`vue-cli@2.x`。如果你仍需要旧的`vue init`功能，你可以安装一个全局包：

``` sh
npm install -g @vue/cli-init
# vue init现在和vue-cli@2.x一样
vue init webpack my-project
```
