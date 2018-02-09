## CSS

- [PostCSS](#postcss)
- [CSS Modules](#css-modules)
- [预处理器](#预处理器)
- [将配置选项传给预编译loaders](#将配置选项传给预编译loaders)

### PostCSS

Vue CLI在内部使用PostCSS，默认启用[autoprefixer](https://github.com/postcss/autoprefixer)。你可以通过`.postcssrc`或[postcss-load-config](https://github.com/michael-ciniawsky/postcss-load-config)支持的任意配置源进行PostCSS的配置。

### CSS Modules

你可以使用`<style module>`[在`*.vue`文件中使用CSS Modules](https://vue-loader.vuejs.org/en/features/css-modules.html)。

对于独立的样式文件，任何以`.module.(css|sass|scss|less|styl|stylus)`结尾的文件会被当作CSS modules处理。

如果你希望能够使在没有`.module`后缀的情况下使用CSS modules，你可以在`vue.config.js`文件总设置`css: { modules: true }`。此选项不会影响到`*.vue`文件。

### 预处理器

你可以在创建项目时选择预处理器（Sass/Less/Stylus）。如果你没有这么做，你也可以手动安装对应的webpack loader。Loaders的配置已经被预先配置好了，会被自动加载。例如，在已有项目中安装Sass，只需简单的运行：

``` sh
npm install -D sass-loader node-sass
```

然后你就可以导入`.scss`文件了，或者像下面一样在`*.vue`文件中使用：

``` vue
<style lang="scss">
$color = red;
</style>
```

### 将配置选项传给预编译loaders

有时你可能想将选项配置传给预编译器webpack liader。你可以在`vue.config.js`中使用`css.loaderOptions`选项。例如，要将一些共享的全局变量传递给所有的Sass样式：

``` js
// vue.config.js
const fs = require('fs')

module.exports = {
  css: {
    loaderOptions: {
      sass: {
        data: fs.readFileSync('src/variables.scss', 'utf-8')
      }
    }
  }
}
```
