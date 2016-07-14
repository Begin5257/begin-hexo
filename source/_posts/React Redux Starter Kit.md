---
title: React Redux Starter Kit
date: 2016-07-14 11:23:52
categroies: 归纳整理
tags: [redux]
---

### React Redux Starter Kit

这个 start kit 是设计用于使你开始一项令人惊叹的新技术的。所有的文件采用统一配置，使用 webpack 构建。已经配置好了热更新，基于 Sass的 CSS 模块化，单元测试以及代码报告，构建工具，还有更多其他的等你发现的东西。

这个项目的目的不是为了给你一个结构化的模板去完成相似的应用，而是提供了一整套的工具来使你的前端开发更加壮大，简洁，更加重要。

1. Features ( 依赖 )

   - react
   - redux
   - react-router
   - react-redux-router
   - webpack
   - babel
   - koa
   - karma
   - eslint

2. Requirements ( node版本 )

   - node ^4.2.0
   - npm ^3.0.0

3. Getting Started ( 开始 )

   ```
   $ git clone https://github.com/davezuko/react-redux-starter-kit.git
   $ cd react-redux-starter-kit
   $ npm install                   # 安装项目依赖
   $ npm start                     # 编译运行
   ```

   如果一切顺利，你会看到

   ![](https://camo.githubusercontent.com/3868d08713325a075795f42758a1c5ec65a264e5/687474703a2f2f692e696d6775722e636f6d2f7a5237565247362e706e673f32)

   ( ps : 需要本机安装sass，靠谱的 ruby 安装地址 http://ruby-china.org/wiki/install_ruby_guide )

   当你开发时，你大多数只会用到 npm start ;不管怎样，这里还有其他的脚本可供使用。

   | `npm run `     | Description                              |
   | -------------- | ---------------------------------------- |
   | `start`        | 在 `localhost:3000`启动你的app，开发环境中将一直会启动热更新。 |
   | `compile`      | 将应用编译打包到 dist 目录。                        |
   | `dev`          | 效果与 `npm start`相同，并且可以实时同步到生产环境。         |
   | `dev:no-debug` | 效果与`npm run dev` 相同，但是禁用了调试工具。           |
   | `test`         | 用Karma执行单元测试，并且生成一份覆盖报告。                 |
   | `test:dev`     | 执行 Karma 并且监测变化，不生成覆盖报告。                 |
   | `deploy`       | 执行 js 检测，测试。如果成功，将文件打包到 dist 目录。         |
   | `deploy:dev`   | 同上，将 `NODE_ENV` 切换到开发环境。                 |
   | `deploy:prod`  | 同上，将 `NODE_ENV` 切换到生产环境。                 |
   | `lint`         | 使用 eslint 检测所有 `.js` 后缀的文件。              |
   | `lint:fix`     | 使用 eslint 检测并修复所有 `.js` 后缀的文件。 [Read more on this](http://eslint.org/docs/user-guide/command-line-interface.html#fix). |

4. Application Structure ( 文件结构 )

   这个应用的文件结构现在大多是按照功能和模块来进行分区。可以作为参考，但是这个文件结构只是作为一个引导，并不意味着规定。总的来说，这可以作为一个应用构建的指南和模式。

   ```
   .
   ├── bin                      # 启动模块
   ├── blueprints               # Blueprint 文件 for redux-cli
   ├── build                    # 所有与生产环境构建相关的配置
   │   └── webpack              # 关于 webpack 的详细生产环境配置
   ├── config                   # 项目的一些 config 配置
   ├── server                   # Koa 应用 ( 使用 webpack 中间件 )
   │   └── main.js              # 启动项目入口
   ├── src                      # 应用的源文件
   │   ├── main.js              # 应用的引导和渲染
   │   ├── components           # 可重复利用的其他组件
   │   ├── containers           # 可重复利用的核心组件
   │   ├── layouts              # 主页面
   │   ├── static               # 静态资源( 没有在项目的任何地方声明引用 )
   │   ├── styles               # 项目中的通用样式 (初始化设置)
   │   ├── store                # Redux 的 store 部分
   │   │   ├── createStore.js   # 创建redux store
   │   │   └── reducers.js      # Reducer的注册和导出
   │   └── routes               # 主要的路径定义和一些分块的资源
   │       ├── index.js         # 将 store 注入路由
   │       └── Home             # 分组路由
   │           ├── index.js     # 定义和路径和一些分块的资源
   │           ├── assets       # 需要在组件内渲染的静态资源
   │           ├── components   # 分开的 React 组件
   │           ├── container    # 将组件与 action 和 store 连接起来
   │           ├── modules      # 收集 reducer 连接 action
   │           └── routes **    # 分型sub-routes ( 可选择的 )
   └── tests                    # 单元测试
   ```

5. 开发环境

   #### Developer Tools

   我们推荐使用 ***Redux DevTools Chrome Extension***.使用这个扩展程序可以允许你监测正在运行的程序的功能和函数。可以轻易的展现 action 及其他特征表现，并且不需要安装任何的包。

   并且，在你的项目中添加一个扩展程序也是非常简单的。首先，从 npm 安装一个包：

   ```
   npm i --save-dev redux-devtools redux-devtools-log-monitor redux-devtools-dock-monitor
   ```

   之后就按照 [manual integration walkthrough](https://github.com/gaearon/redux-devtools/blob/master/docs/Walkthrough.md) 进行操作.

   ### Routing

   我们使用 `react-router` 来区分我们项目中用到的逻辑和单元。观察项目结构部分可以获取更多的信息。

   ​

