# Webpack 学习笔记

## Main

默认配置文件: `webpack.config.js`

webpack配置组成部分

```js
// webpack.config.js example

module.exports = {
  entry: './src/index.js',    // 1.打包的输入文件
  output: './dist/main.js',   // 2.打包的输出文件
  mode: 'production',         // 3.打包环境
  module: {
    rules: [                  // 4.loader配置
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  },
  plugins: [                  // 5.插件配置
    new HtmlwebpackPlugin({
      template: './src/index.html'
    })
  ]
}
```

可以通过 `./node_modules/.bin/webpack` 手动来执行`webpack`,

使用`npm script`来运行webpack

```json
// 通过 npm run build 来运行
// 原理是：模块局部安装会在 node_modules/.bin 目录下创建软链接
"script": {
  "build": "webpack",
}
```

## 核心概念

### Entry

* `entry` 指示 webpack 应该使用哪个模块，用来作为内部`依赖图`的开始。
* 默认值是`./src/index,js`

![依赖图长啥样子](https://tva1.sinaimg.cn/large/006tNbRwly1gb9uw6cgg5j316i0kwwmt.jpg)

#### entry 基本用法

* 单入口: entry 是一个字符串 (项目是单页应用)

  ```js
  module.exports = {
    entry: './your_path/index.js',
  }
  ```

* 多入口：entry 是一个对象 (项目是多页应用)

```js
module.exports = {
  entry: {
    app: './src/app.js',
    user: './src/user.js',
  }
}
```

### Output

* output 用来指定打包的输出，包括在哪里输出它所创建的bundle，以及如何命名这些文件

#### output的基本用法

* 单入口配置

```js
  module.exports = {
    entry: './your_path/index.js',
    // 针对单入口只需要指定 filename 和  path 就可以了
    output: {
      filename: 'bundle.js',
      path: __dirname + '/dist',
    }
  }
```

* 多入口配置

```js
module.exports = {
  // 多入口
  entry: {
    app: './src/app.js',
    search: './src/search.js',
  },
  // 出口通过占位符来确保文件名称的唯一
  // 其中的 [name] 代表的是 entry 中的键
  output: {
    filename: '[name].js',
    path: __dirname + '/dist',
  }
}
```

### Loaders

* webpack 原生只支持 `js` 和 `json` 两种类型的文件，但是如果想要将其他类型的文件转化为有效的模块，并且加入到依赖树中，就需要 `Loaders`.
* 一般来说一个loader只做一件事情，比如说我们使用`less-loader`将less转化为css文件，再通过`css-loader`来处理css文件

比较常见的 Loaders：

* css-loader
* 需要补充

#### Loaders的使用方法

```js
...
module: {
  rules: [
    // test 指定匹配规则
    // use 指定使用的 loader 名称
    { test: /\.txt$/, use: 'raw-loader' },
  ]
}
...
```

### Plugins

* 使用于 bundle 文件的优化，资源管理和环境变量的注入
* 作用域整个构建过程
* 可以理解为 loader 干不了的事情，用 plugins 干
