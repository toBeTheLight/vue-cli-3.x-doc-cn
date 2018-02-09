## Static Asset Handling

- [Relative Path Imports](#relative-path-imports)
  - [URL Transform Rules](#url-transform-rules)
- [The `public` Folder](#the-public-folder)
  - [When to use the `public` folder](#when-to-use-the-public-folder)

### Relative Path Imports

当你用相对路径在JavaScript，CSS或`*.vue`文件中引用静态资源时，资源会被包含在webpack的依赖统计中。在这个编译过程中，所有的资源URL如`<img src="...">`，`background: url(...)`和CSS中的`@import`都会被**解析为模块依赖**。

例如：`url(./image.png)`将会被编译为`require('./image.png')`。    
例如：

``` html
<img src="../image.png">
```

将会被编译为：

``` js
createElement('img', { attrs: { src: require('../image.png') }})
```

内部使用`file-loader`通过版本哈希值和正确的公共基本路径（public base paths）来确定最终文件的位置，使用`url-loader`来有条件的内敛小于10kb的资源，来减少HTTP请求。

#### URL转换规则

- 如果URL是一个绝对路径（如，`/images/foo.png`）将会保持原状。

- 如果URL以`.`开始，它将会被理解为相对模块请求，并根据文件系统上的文件夹结构被解析。

- 如果URL以`~`开头，则后面的任何内容都会被理解为模块请求，这意味着你甚至可以引用在node modules的资源：

  ``` html
  <img src="~/some-npm-package/foo.png">
  ```

- 如果URL以`@`开始，也会被理解为一个模块请求。因为Vue CLI默认将`@`作为`<projectRoot>/src`的别名（webpack alias）。

### `public`文件夹

所有放在`public`文件夹中的静态资源都会被简单的复制到打包文件路径中，而不会经过webpack解析，你需要使用绝对路径来引用它们。

注意，我们建议将资源作为模块依赖的一部分导入，以便于能通过webpack解析来获得以下好处:

- Scripts和stylesheets会压缩合并以减少额外的网络请求。
- 缺少文件不会出现404错误，而在编译时就会报错。
- 输出文件名包含内容哈希值，你不用担心浏览器会缓存旧版本。

`public`文件是作为**逃生出口**用的，当你通过绝对路径引用它时，你需要考虑下应用程序会被部署到哪。如果你的应用被部署到域名的根目录下，你需要为你的地址加上基本路径（base path）:

- 在`public/index.html`文件中，你需要在地址链接前加上`<%= webpackConfig.output.publicPath %>`：

  ``` html
  <link rel="shortcut icon" href="<%= webpackConfig.output.publicPath %>favicon.ico">
  ```

- 在templates中你需要项将基本路径传给你的组件：

  ``` js
  data () {
    return {
      baseUrl: process.env.BASE_URL
    }
  }
  ```

  然后：

  ``` html
  <img :src="`${baseUrl}my-image.png`">
  ```

#### 什么时候使用`public`文件夹

- 你需要在构建输出中具有特殊名称的文件。
- 你有很多很多很多的图片，需要动态的引用他们。
- 有些库与webpack不兼容，除了使用`<script>`标签引用没有别的办法。
