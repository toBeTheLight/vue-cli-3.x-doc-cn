## 构建目标

### 应用
*App*

应用模式是默认的模式，这种模式下：

- 资源和资源提示会被插入到`index.html`文件
- vendor库们被打包进一个独立的块（chunk）来更好的缓存
- 10kb大小以下的静态资源被内联进JavaScript
- `public`文件中的静态资源被复制到构建输出目录

### 库
*Library*

你可以使用一个独立的入口文件来构建库

```
vue-cli-service build --target lib --name myLib [entry]
```

```
File                     Size                     Gzipped

dist/myLib.umd.min.js    13.28 kb                 8.42 kb
dist/myLib.umd.js        20.95 kb                 10.22 kb
dist/myLib.common.js     20.57 kb                 10.09 kb
dist/myLib.css           0.33 kb                  0.23 kb
```

入口文件可以是`.js`或`.vue`文件。如果没有指定入口文件，将会使用`src/App.vue`。

lib构建输出：

- `dist/myLib.common.js`： 通过打包器使用的CommonJS包（不幸的是，webpack还不支持包的ES模块化标准输出）

- `dist/myLib.umd.js`: 一个UMD格式的包，可直接在浏览器使用或通过AMD加载器加载

- `dist/myLib.umd.min.js`: UMD格式构建的压缩版本

- `dist/myLib.css`: 提取出来的CSS样式文件（可通过在`vue.config.js`中设置`css: { extract: false }`强制内联）

**在库模式下，Vue是被外部化设置的**这意味即使你导入了Vue，包也不会打包Vue。如果通过打包器使用此库，它将试图通过依赖关系加载Vue；否则会降级使用全局变量`Vue`。

### Web组件

*HTML Web Component*

> [兼容性](https://github.com/vuejs/vue-web-component-wrapper#compatibility)

你可以使用一个独立的入口文件来构建库

```
vue-cli-service build --target wc --name my-element [entry]
```

这将生成一个JavaScript文件（和他的压缩版本），其中包含所有内容。当script文件在页面中使用时，会使用`@vue/web-component-wrapper`注册包含目标Vue组件的`<my-element>`自定义元素。wrapper会自动代理prop属性，attr属性，事件和slots插槽。查看更多详情参阅[`@vue/web-component-wrapper`的文档](https://github.com/vuejs/vue-web-component-wrapper)。

**注意，此包依赖与Vue页面全局可用**

该模式允许组件的使用者将Vue作为普通的DOM元素使用：

``` html
<script src="https://unpkg.com/vue"></script>
<script src="path/to/my-element.js"></script>

<!-- 在纯html或任何其他framework中使用 -->
<my-element></my-element>
```

#### 捆绑打包多个web组件

当构建web组件包时，你还可以使用匹配模式指定多个组件作为打包入口：

```
vue-cli-service build --target wc --name foo 'src/components/*.vue'
```

在构建多个web组件时，`--name`会被作为前缀使用，并且自定义元素名会从组件文件名中被推断出来。比如，使用`--name foo`且组件名为`HelloWorld.vue`的话，生成的自定义元素将会被注册为`<foo-hello-world>`。

### 异步Web组件

> [兼容性](https://github.com/vuejs/vue-web-component-wrapper#compatibility)

当指定捆绑打包多个web组件时，这个包会变得相当大，而且用户可能只用包里的部分组件。异步web组件模式下会生成一个代码拆分包，其中包含一个用于在所有组件间提供共享运行时的小的入口文件并且会提前注册所有的自定义元素。然后只有在页面上使用相应的自定义元素的实例时，才会按需获取组件的代码：

```
vue-cli-service build --target wc-async --name foo 'src/components/*.vue'
```

```
File                Size                        Gzipped

dist/foo.0.min.js    12.80 kb                    8.09 kb
dist/foo.min.js      7.45 kb                     3.17 kb
dist/foo.1.min.js    2.91 kb                     1.02 kb
dist/foo.js          22.51 kb                    6.67 kb
dist/foo.0.js        17.27 kb                    8.83 kb
dist/foo.1.js        5.24 kb                     1.64 kb
```

然后用户只需要在页面中加载Vue和入口文件：

``` html
<script src="https://unpkg.com/vue"></script>
<script src="path/to/foo.min.js"></script>

<!-- foo-one的代码块会在它被使用时自动加载 -->
<foo-one></foo-one>
```
