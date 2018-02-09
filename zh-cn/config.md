## `vue.config.js`

这是所有可用的带有默认值的选项（所有可选）：

``` js
module.exports = {
  // 项目部署基础
  // 默认情况下，我们假设你的应用将被部署在域的根目录下,
  // 例如：https://www.my-app.com/
  // 如果您的应用程序部署在子路径中，则需要在这指定子路径
  // 例如：https://www.foobar.com/my-app/
  // 需要将它改为'/my-app/'
  baseUrl: '/',

  // 输出构建的文件的地方
  outputDir: 'dist',

  // 是否为保存的lint使用eslint-loader
  lintOnSave: false,

  // 是否使用带有浏览器编译的完整版本？
  // https://vuejs.org/v2/guide/installation.html#Runtime-Compiler-vs-Runtime-only
  compiler: false,

  // 调整内部webpack配置
  // 查看 https://github.com/vuejs/vue-cli/blob/dev/docs/webpack.md
  chainWebpack: () => {},
  configureWebpack: () => {},

  // vue-loader配置
  // https://vue-loader.vuejs.org/en/options.html
  vueLoader: {},

  // 为生产构建生成sourceMap？
  productionSourceMap: true,

  // CSS相关设置
  css: {
    // 将组件中的CSS提取到一个CSS文件中（只在生产环境下）
    extract: true,

    // 启用CSS sourceMap？
    sourceMap: false,

    // 将自定义选项传递给预处理器加载器，例如：将选项传给
    // sass-loader, use { sass: { ... } }
    loaderOptions: {},

    // 为所有css/预编译文件启用CSS modules？
    // 不会影响到.vue文件
    modules: false
  },

  // 在生产版本中使用babel＆TS的thread-loader
  // 如果机器拥有多个核心，则默认启用
  parallel: require('os').cpus().length > 1,

  // 使用autoDLLPlugin拆分vendors？
  // 也可以时包含在DLL块中的数组
  // 参阅 https://github.com/vuejs/vue-cli/blob/dev/docs/cli-service.md#dll-mode
  dll: false,

  // PWA plugin插件配置
  // 参阅 https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-pwa
  pwa: {},

  // 配置webpack-dev-server行为
  devServer: {
    open: process.platform === 'darwin',
    host: '0.0.0.0',
    port: 8080,
    https: false,
    hotOnly: false,
    // 参阅 https://github.com/vuejs/vue-cli/blob/dev/docs/cli-service.md#configuring-proxy
    proxy: null, // string | Object
    before: app => {}
  },

  // 第三方插件的选项
  pluginOptions: {
    // ...
  }
}
```
