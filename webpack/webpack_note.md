# Webpack 学习笔记

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
