# vue-cli-practice

Vue CLI 是一个基于 Vue.js 进行快速开发的完整系统，包含 @vue/cli, @vue/cli-service
@vue/cli 是一个全局安装的 npm package, 提供了终端里的 vue 命令，可以执行 vue create 来创建一个新项目，或者通过 vue serve 构建新想法的原型。也可以通过 vue ui 来使用一套图形化界面管理你的项目
@vue/cli-service 是一个开发环境依赖，它是一个 npm package, 局部安装在每个 通过 @vue/cli 创建的项目里。 CLI service 是构建于 webpack 和 webpack-dev-server 之上的，它包含了
  * 加载其它 CLI 插件的核心服务
  * 一个针对大部分项目优化过的内部的 webpack 配置
  * 项目内部的 vue-cli-service 命令，提供 serve, build, inspect 命令
CLI 插件是向你的 Vue 项目提供可选功能的 npm package, 例如 babel/type script 转译， eslint, 单元测试等。 vue cli 插件的名字以 @vue/cli-plugin- 或 vue-cli-plugin 开头
当你在项目内部运行 vue-cli-service 命令时，它会自动解析并加载 package.json 中列出的所有 CLI 插件

## 快速原型开发
你可以使用 vue serve 和 vue build 命令对单个 .vue 文件进行快速原型开发，不过这需要全局安装额外的 @vue/cli-service-global package
vue serve 在开发环境下零配置为 .js 或者 .vue 文件启动一个服务器。 注意 vue serve 使用和 vue create 相同的默认配置(webpack, babel, eslint...)
vue build 在生产环境下零配置构建一个 .js 或 .vue 文件

## 创建一个项目
vue create app-name

## 插件和 Preset
Vue CLI 使用了一套基于插件的架构，通过Vue CLI 创建的项目，查看它的 package.json 会发现，它的所有依赖都是以 @vue/cli-plugin- 开头的。插件可以修改 webpack 内部配置，也可以向 vue-cli-service 注入命令。
在项目的创建过程中，绝大部分列出的特性，都是通过插件来实现的。

每个 CLI 插件都会包含一个用来创建文件的生成器，和一个用来调整 webpack 核心配置以及注入命令的 运行时插件。当你使用 vue create 来创建一个新项目时，有些插件会根据你选择的特性被预安装好。如果你想在一个创建好的项目里添加插件，可以使用 vue add.
注意 vue add 只是用来处理 vue cli 插件， 对于普通的 npm package， 还是需要 npm 来管理

Preset 用来存放创建新项目所需预定义选项和插件的 JSON 对象，存放在~/.vuerc 里。

## CLI Service
@vue/cli-service 在项目中安装了一个名为 vue-cli-service 的命令，你可以在 npm scripts 中以 vue-cli-service,或者从终端 './node_modules/.bin/vue-cli-service' 访问这个命令

### vue-cli-service serve
用法：vue-cli-service serve [options] [entry]
选项：

  --open    在服务器启动时打开浏览器
  --copy    在服务器启动时将 URL 复制到剪切版
  --mode    指定环境模式 (默认值：development)
  --host    指定 host (默认值：0.0.0.0)
  --port    指定 port (默认值：8080)
  --https   使用 https (默认值：false)

vue-cli-service serve 会启动一个基于 webpack-dev-server 的开发服务器，并附带开箱即用的模块热加载。出了命令行参数，也可以使用 vue.config.js 里的 devServer 字段配置开发服务器， entry 用来指定入口文件

### vue-cli-service build
用法：vue-cli-service build [options] [entry|pattern]

选项：

  --mode        指定环境模式 (默认值：production)
  --dest        指定输出目录 (默认值：dist)
  --modern      面向现代浏览器带自动回退地构建应用
  --target      app | lib | wc | wc-async (默认值：app)
  --name        库或 Web Components 模式下的名字 (默认值：package.json 中的 "name" 字段或入口文件名)
  --no-clean    在构建项目之前不清除目标目录
  --report      生成 report.html 以帮助分析包内容
  --report-json 生成 report.json 以帮助分析包内容
  --watch       监听文件变化

vue-cli-service build 会在 dist/目录下产生一个可用于生产环境的包，带有 JS/CSS/HTML 的压缩

### vue-cli-service inspect
用法：vue-cli-service inspect [options] [...paths]

选项：

  --mode    指定环境模式 (默认值：development)

使用 vue-cli-service inspect 来审查一个 Vue CLI 项目的 webpack config

### 查看所有的可用命令
有的 CLI 插件会向 vue-cli-service 注入额外的命令， 可以使用 npx vue-cli-service help 来查看
