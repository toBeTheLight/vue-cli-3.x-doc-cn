<a name="3.0.0-beta.1"></a>
# [3.0.0-beta.1](https://github.com/vuejs/vue-cli/compare/v3.0.0-alpha.13...v3.0.0-beta.1) (2018-02-16)


### Bug修复

* **babel preset：** 允许设置`useBuiltIns`为`false` ([#843](https://github.com/vuejs/vue-cli/issues/843)) ([a9ac1a9](https://github.com/vuejs/vue-cli/commit/a9ac1a9))
* eslint插件中也包括import规则 ([e8f036b](https://github.com/vuejs/vue-cli/commit/e8f036b))
* eslint + airbnb与TypeScript兼容 ([d391e47](https://github.com/vuejs/vue-cli/commit/d391e47))
* 为全局服务修复core-js导入 ([3a5d125](https://github.com/vuejs/vue-cli/commit/3a5d125))，关闭 [#837](https://github.com/vuejs/vue-cli/issues/837)
* 为TypeScript修复eslint-loader ([9f5d0b9](https://github.com/vuejs/vue-cli/commit/9f5d0b9))



<a name="3.0.0-alpha.13"></a>
# [3.0.0-alpha.13](https://github.com/vuejs/vue-cli/compare/v3.0.0-alpha.12...v3.0.0-alpha.13) (2018-02-13)


### Bug修复

* 补全丢失依赖 (修复 [#831](https://github.com/vuejs/vue-cli/issues/831)) ([6a0bc17](https://github.com/vuejs/vue-cli/commit/6a0bc17))



<a name="3.0.0-alpha.12"></a>
# [3.0.0-alpha.12](https://github.com/vuejs/vue-cli/compare/v3.0.0-alpha.11...v3.0.0-alpha.12) (2018-02-12)


### Bug修复

* 通过切换axios到request解决https代理问题 ([#829](https://github.com/vuejs/vue-cli/issues/829)) ([e8aa688](https://github.com/vuejs/vue-cli/commit/e8aa688))，关闭 [#785](https://github.com/vuejs/vue-cli/issues/785)
* 进行字体文件名不区分大小写的扩展 ([#830](https://github.com/vuejs/vue-cli/issues/830)) ([d7cfa00](https://github.com/vuejs/vue-cli/commit/d7cfa00))
* 仅当tslint.json存在时才启用TSLint ([76d7f77](https://github.com/vuejs/vue-cli/commit/76d7f77))


### 功能特性

* 允许e2e插件确定服务应该启动的模式 ([8f8fe6d](https://github.com/vuejs/vue-cli/commit/8f8fe6d))，关闭 [#814](https://github.com/vuejs/vue-cli/issues/814)
* 暴漏[@vue](https://github.com/vue)/babel-preset-app中的useBuiltIns配置([8e0661e](https://github.com/vuejs/vue-cli/commit/8e0661e))，关闭 [#812](https://github.com/vuejs/vue-cli/issues/812)
* lintOnSave不再直接导致编译失败 ([9040df8](https://github.com/vuejs/vue-cli/commit/9040df8))，关闭 [#817](https://github.com/vuejs/vue-cli/issues/817)
* 启用eslint-plugin-cypress ([9410442](https://github.com/vuejs/vue-cli/commit/9410442))，关闭 [#815](https://github.com/vuejs/vue-cli/issues/815)
* 对css module启用更有描述性的类名 ([fd13106](https://github.com/vuejs/vue-cli/commit/fd13106))，关闭 [#813](https://github.com/vuejs/vue-cli/issues/813)



<a name="3.0.0-alpha.11"></a>
# [3.0.0-alpha.11](https://github.com/vuejs/vue-cli/compare/v3.0.0-alpha.10...v3.0.0-alpha.11) (2018-02-09)


### Bug修复

* eslint配置应为root配置 ([ea74da1](https://github.com/vuejs/vue-cli/commit/ea74da1))
* **eslint：** 默认加载node环境 (修复 [#806](https://github.com/vuejs/vue-cli/issues/806)) ([c2e3228](https://github.com/vuejs/vue-cli/commit/c2e3228))
* 用户设置的输出地址可用 ([b5564af](https://github.com/vuejs/vue-cli/commit/b5564af))，关闭 [#809](https://github.com/vuejs/vue-cli/issues/809)



<a name="3.0.0-alpha.10"></a>
# [3.0.0-alpha.10](https://github.com/vuejs/vue-cli/compare/v3.0.0-alpha.9...v3.0.0-alpha.10) (2018-02-08)


### Bug修复

* 修复pwa详情链接地址 (close [#801](https://github.com/vuejs/vue-cli/issues/801)) ([a0004ea](https://github.com/vuejs/vue-cli/commit/a0004ea))
* vue-class-component和vue-property-decorators 应该为dependencies ([c26559d](https://github.com/vuejs/vue-cli/commit/c26559d))


### 功能特性

* 在prettier配置中添加eslint:recommended ([e261718](https://github.com/vuejs/vue-cli/commit/e261718))
* 支持使用ESLint来规范TypeScript ([dd04add](https://github.com/vuejs/vue-cli/commit/dd04add))



<a name="3.0.0-alpha.9"></a>
# [3.0.0-alpha.9](https://github.com/vuejs/vue-cli/compare/v3.0.0-alpha.8...v3.0.0-alpha.9) (2018-02-06)


### Bug修复

* **unit-mocha：** 修复测试glob避免运行e2e测试 ([172e8eb](https://github.com/vuejs/vue-cli/commit/172e8eb))，关闭 [#790](https://github.com/vuejs/vue-cli/issues/790)
* 为已存在的文件处理vue调用配置合并 ([46166fb](https://github.com/vuejs/vue-cli/commit/46166fb))，关闭 [#788](https://github.com/vuejs/vue-cli/issues/788)
* api.configureWebpack返回的对象应被合并 ([920d8fa](https://github.com/vuejs/vue-cli/commit/920d8fa))
* 只当使用npm时支持taobao源检查和内联注册 ([67df3eb](https://github.com/vuejs/vue-cli/commit/67df3eb))，关闭 [#789](https://github.com/vuejs/vue-cli/issues/789)


### 功能特性

* 在pwa模板中启用Workbox webpack plugin ([#769](https://github.com/vuejs/vue-cli/issues/769)) ([9095483](https://github.com/vuejs/vue-cli/commit/9095483))



<a name="3.0.0-alpha.8"></a>
# [3.0.0-alpha.8](https://github.com/vuejs/vue-cli/compare/v3.0.0-alpha.7...v3.0.0-alpha.8) (2018-02-04)


### Bug修复

* 修复使用airbnb + cypress时的eslint错误 ([313533d](https://github.com/vuejs/vue-cli/commit/313533d))
* 修复jest测试匹配 ([2c61d23](https://github.com/vuejs/vue-cli/commit/2c61d23))，关闭 [#771](https://github.com/vuejs/vue-cli/issues/771)
* 修复复写提示 ([7871c5c](https://github.com/vuejs/vue-cli/commit/7871c5c))
* 在workspace中添加version marker ([d3d040a](https://github.com/vuejs/vue-cli/commit/d3d040a))，关闭 [#772](https://github.com/vuejs/vue-cli/issues/772)
* **inspect:** `resolve`的正确使用方式 ([#773](https://github.com/vuejs/vue-cli/issues/773)) ([0f9a44a](https://github.com/vuejs/vue-cli/commit/0f9a44a))
* 插件数据提取移入GeneratorAPI ([4f2f6f0](https://github.com/vuejs/vue-cli/commit/4f2f6f0))
* 为node modules兼容global ([691cfa2](https://github.com/vuejs/vue-cli/commit/691cfa2))，关闭 [#774](https://github.com/vuejs/vue-cli/issues/774)


### 功能特性

* build --target wc-async ([50fdd9b](https://github.com/vuejs/vue-cli/commit/50fdd9b))
* 调整构建输出 ([dc29e88](https://github.com/vuejs/vue-cli/commit/dc29e88))
* 更新默认组件内容 ([59f5913](https://github.com/vuejs/vue-cli/commit/59f5913))



<a name="3.0.0-alpha.7"></a>
# [3.0.0-alpha.7](https://github.com/vuejs/vue-cli/compare/v3.0.0-alpha.6...v3.0.0-alpha.7) (2018-02-02)


### Bug修复

* 确保使用npm进行安装时，vue初始化正常工作 ([6ce8565](https://github.com/vuejs/vue-cli/commit/6ce8565))


### 功能特性

* 在创建时检查并显示更新的版本 ([3df1289](https://github.com/vuejs/vue-cli/commit/3df1289))
* 在调用插件时支持提示 ([c1142e2](https://github.com/vuejs/vue-cli/commit/c1142e2))



<a name="3.0.0-alpha.6"></a>
# [3.0.0-alpha.6](https://github.com/vuejs/vue-cli/compare/v3.0.0-alpha.5...v3.0.0-alpha.6) (2018-02-02)


### Bug修复

* 全局构建时支持--target ([4fb4e35](https://github.com/vuejs/vue-cli/commit/4fb4e35))
* 允许dev下使用console ([5ad8fae](https://github.com/vuejs/vue-cli/commit/5ad8fae))
* 避免项目配置的深度合并 ([7d590d8](https://github.com/vuejs/vue-cli/commit/7d590d8))
* 兼容safari 10 ([#755](https://github.com/vuejs/vue-cli/issues/755)) ([199c754](https://github.com/vuejs/vue-cli/commit/199c754))
* 不再测试中提取vue.config.js ([7874b0e](https://github.com/vuejs/vue-cli/commit/7874b0e))
* 确保loaders存在 ([fcfb099](https://github.com/vuejs/vue-cli/commit/fcfb099))
* 修复--force标志 ([6661ac2](https://github.com/vuejs/vue-cli/commit/6661ac2))
* 修复路径存在空格时的项目创建问题 (修复 [#742](https://github.com/vuejs/vue-cli/issues/742)) ([5be05f3](https://github.com/vuejs/vue-cli/commit/5be05f3))
* 修复版本检查 ([e5ef34d](https://github.com/vuejs/vue-cli/commit/e5ef34d))
* 将linkBin迁移到 [@vue](https://github.com/vue)/cli，因为需要node 8([120d5c5](https://github.com/vuejs/vue-cli/commit/120d5c5))
* TS 2.7 兼容 ([c7e28fd](https://github.com/vuejs/vue-cli/commit/c7e28fd))
* typescript缓存问题 ([a80cf18](https://github.com/vuejs/vue-cli/commit/a80cf18))
* **typescript：** 明确包含global类型 ([31c1261](https://github.com/vuejs/vue-cli/commit/31c1261))，关闭 [#762](https://github.com/vuejs/vue-cli/issues/762)


### 功能特性

* build --target lib/wc ([faadadf](https://github.com/vuejs/vue-cli/commit/faadadf))
* build --target web-component (WIP) ([6db7735](https://github.com/vuejs/vue-cli/commit/6db7735))
* complete --target wc & multi-wc + tests ([9a07eeb](https://github.com/vuejs/vue-cli/commit/9a07eeb))
* 改进 build lib/web-component ([1c4943b](https://github.com/vuejs/vue-cli/commit/1c4943b))
* 改进检查输出 ([fd87394](https://github.com/vuejs/vue-cli/commit/fd87394))
* web组件模式下在shadow root下插入样式 ([98afd07](https://github.com/vuejs/vue-cli/commit/98afd07))
* 使HTML模板中的env变量可用 ([b626ef1](https://github.com/vuejs/vue-cli/commit/b626ef1))
* parallel mode ([b8f2487](https://github.com/vuejs/vue-cli/commit/b8f2487))
* vue build --target multi-wc [pattern] ([0f59c03](https://github.com/vuejs/vue-cli/commit/0f59c03))
* vue检查代理 vue-cli-service ([4c00cfa](https://github.com/vuejs/vue-cli/commit/4c00cfa))


### 还原

* 功能：加载配置 w/ cosmiconfig ([702b539](https://github.com/vuejs/vue-cli/commit/702b539))



<a name="3.0.0-alpha.5"></a>
# [3.0.0-alpha.5](https://github.com/vuejs/vue-cli/compare/v3.0.0-alpha.4...v3.0.0-alpha.5) (2018-01-29)


### Bug修复

* cache-loader似乎不适用于ts-loader ([63c8f65](https://github.com/vuejs/vue-cli/commit/63c8f65))
* jest应该只运行于给定的文件 ([4a7fd64](https://github.com/vuejs/vue-cli/commit/4a7fd64))，关闭 [#740](https://github.com/vuejs/vue-cli/issues/740)


### 功能特性

* 允许保存多个预设 ([f372f55](https://github.com/vuejs/vue-cli/commit/f372f55))
* 加载配置 w/ cosmiconfig ([5288122](https://github.com/vuejs/vue-cli/commit/5288122))
* 支持专用文件中的配置 ([01edb46](https://github.com/vuejs/vue-cli/commit/01edb46))



<a name="3.0.0-alpha.4"></a>
# [3.0.0-alpha.4](https://github.com/vuejs/vue-cli/compare/v3.0.0-alpha.3...v3.0.0-alpha.4) (2018-01-26)


### Bug修复

* 为node版本兼容将joi固定为12.x ([3bd447a](https://github.com/vuejs/vue-cli/commit/3bd447a))
* 不存在postcss配置时跳过postcss-loader ([1142339](https://github.com/vuejs/vue-cli/commit/1142339))
* 临时固定vue-jest到github分支 ([2d6a0d9](https://github.com/vuejs/vue-cli/commit/2d6a0d9))


### 功能特性

* 将babel-preset和eslint-plugin移动为插件依赖 ([c2583e4](https://github.com/vuejs/vue-cli/commit/c2583e4))



<a name="3.0.0-alpha.3"></a>
# [3.0.0-alpha.3](https://github.com/vuejs/vue-cli/compare/v3.0.0-alpha.2...v3.0.0-alpha.3) (2018-01-26)


### Bug修复

* 在改变前拷贝选项 ([7471f94](https://github.com/vuejs/vue-cli/commit/7471f94))
* **typescript：** 修复tsconfig.json ([235676f](https://github.com/vuejs/vue-cli/commit/235676f))
* **typescript:** 使用[@types](https://github.com/types)/node替换process ([f9c8849](https://github.com/vuejs/vue-cli/commit/f9c8849))
* 确保cache-loader适用于babel和ts ([5f76980](https://github.com/vuejs/vue-cli/commit/5f76980))
* 修复生成器的同步脚本 ([134ac58](https://github.com/vuejs/vue-cli/commit/134ac58))
* 使用ts + babel时强制babel-core版本 ([d7c6af7](https://github.com/vuejs/vue-cli/commit/d7c6af7))
* 缺少loader提供更全面的解决方案和更好的错误提示 ([367b78b](https://github.com/vuejs/vue-cli/commit/367b78b))
* 更全面的服务解决方案 ([76dda73](https://github.com/vuejs/vue-cli/commit/76dda73))
* packageManager标志 ([0c9ecd5](https://github.com/vuejs/vue-cli/commit/0c9ecd5))
* 解析全局服务 ([8f0b52f](https://github.com/vuejs/vue-cli/commit/8f0b52f))


### 功能特性

* 对ts使用cache-loader ([4680544](https://github.com/vuejs/vue-cli/commit/4680544))



<a name="3.0.0-alpha.2"></a>
# [3.0.0-alpha.2](https://github.com/vuejs/vue-cli/compare/v3.0.0-alpha.1...v3.0.0-alpha.2) (2018-01-25)


### Bug修复

* 避免dotfiles没发布到npm ([2e3fe07](https://github.com/vuejs/vue-cli/commit/2e3fe07))
* 如果最新的tag比指定的更旧，不更新依赖 ([b913047](https://github.com/vuejs/vue-cli/commit/b913047))
* 使用babel-loader@8 ([c769110](https://github.com/vuejs/vue-cli/commit/c769110))



<a name="3.0.0-alpha.1"></a>
# [3.0.0-alpha.1](https://github.com/vuejs/vue-cli/compare/a923afb...v3.0.0-alpha.1) (2018-01-25)


### Bug修复

* 在选取功能特性时避免滚动 ([d57208d](https://github.com/vuejs/vue-cli/commit/d57208d))
* bump root deps as well ([f52ff70](https://github.com/vuejs/vue-cli/commit/f52ff70))
* 确保paths + 使html可选 ([2c1ad14](https://github.com/vuejs/vue-cli/commit/2c1ad14))
* 拼写错误 {mdoule => module} ([#721](https://github.com/vuejs/vue-cli/issues/721)) ([4765cc6](https://github.com/vuejs/vue-cli/commit/4765cc6))


### 功能特性

* 为babel添加缓存 ([7605bd6](https://github.com/vuejs/vue-cli/commit/7605bd6))
* 自动DLL ([8dff383](https://github.com/vuejs/vue-cli/commit/8dff383))
* 更好的验证错误提示信息 ([5fef42c](https://github.com/vuejs/vue-cli/commit/5fef42c))
* 完成prettier整合 ([100c5c6](https://github.com/vuejs/vue-cli/commit/100c5c6))
* 核心 ([a923afb](https://github.com/vuejs/vue-cli/commit/a923afb))
* css预处理器 ([d3bb381](https://github.com/vuejs/vue-cli/commit/d3bb381))
* e2e cypress ([8a3ac7e](https://github.com/vuejs/vue-cli/commit/8a3ac7e))
* e2e nightwatch ([655202f](https://github.com/vuejs/vue-cli/commit/655202f))
* 为uglifyjs插件使用缓存 ([abaed00](https://github.com/vuejs/vue-cli/commit/abaed00))
* 实验性支持使用Babel编译TS ([e4dcc2f](https://github.com/vuejs/vue-cli/commit/e4dcc2f))
* 改进生成器hasPlugin检查和调用输出 ([52dad9d](https://github.com/vuejs/vue-cli/commit/52dad9d))
* 改进提示流 ([06af371](https://github.com/vuejs/vue-cli/commit/06af371))
* 使jest插件和TypeScript协同工作 ([ea2648e](https://github.com/vuejs/vue-cli/commit/ea2648e))
* 使tslint为vue文件生效 ([52b587e](https://github.com/vuejs/vue-cli/commit/52b587e))
* mocha-webpack插件 ([21187b4](https://github.com/vuejs/vue-cli/commit/21187b4))
* 优化压缩 ([bd1ffd3](https://github.com/vuejs/vue-cli/commit/bd1ffd3))
* 初步实现TS插件 ([54a902d](https://github.com/vuejs/vue-cli/commit/54a902d))
* pwa ([902f6c0](https://github.com/vuejs/vue-cli/commit/902f6c0))
* router & vuex ([88e9d46](https://github.com/vuejs/vue-cli/commit/88e9d46))
* 支持Prettier eslint配置（待定） ([d84df9a](https://github.com/vuejs/vue-cli/commit/d84df9a))
* 调整调用命令 ([65cc27d](https://github.com/vuejs/vue-cli/commit/65cc27d))
* 为polyfills使用w/ TS ([5b19826](https://github.com/vuejs/vue-cli/commit/5b19826))
* wip 调用命令 ([132b0db](https://github.com/vuejs/vue-cli/commit/132b0db))
* WIP jest插件 ([bb5d968](https://github.com/vuejs/vue-cli/commit/bb5d968))



