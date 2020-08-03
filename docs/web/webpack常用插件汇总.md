### 6.1.1 Externals
- Externals 用来告诉在 Webpack 要构建的代码中使用了哪些不用被打包的模块，也就是说这些模块是`外部环境`提供的，Webpack 在打包时可以`忽略`他们。
- 通过 externals 可以告诉 webpack 在javascript 运行环境中已经`内置了`哪些全局变量，不用将这些全局变量打包到代码中而是直接使用他们。配置如下

```js
// import $ from 'jquery';
module.export = {
    externals: {
        // 将导入语句中的 jquery 替换成运行环境里的全局变量 jQuery
        jquery: 'jQuery'
    }
}
```

### 6.1.2 clean-webpack-plugin
- 在打包前清除当前根目录`已存在`的 dist 目录（打包后的输出目录）

- 配置：
```js
// webpack.config.js
const { CleanWebpackPlugin } = require('clean-webpack-plugin');
module.exports = {
    entry: './src/main.js',
    pligins:[
        new CleanWebpackPlugin()
    ]
}
```

### 6.1.3 html-webpack-plugin
- 用于生成 html 的插件
- 配置
```js
// webpack.config.js
const { CleanWebpackPlugin } = require('clean-webpack-plugin');
const { HtmlWebpackPlugin } = require('html-webpack-plugin');
module.exports = {
    entry: './src/main.js',
    pligins:[
        new CleanWebpackPlugin(),
        
        new HtmlWebpackPlugin({
            title: 'webpack plugin sample', // 配置 title
            meta: {
                viewport: 'width=device-width', // 配置 meta 标签
            }
        })
    ]
}
```

- 配置模板 HTML
    - 模板 HTML 
    ```html
    <!-- ./src/index.html -->
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <!-- 从 webpack 配置中读取 title -->
        <title><%= htmlWebpackPlugin.options.title %></title>
    </head>
    <body>
        <div class="container">
            <h1>页面上的基础结构</h1>
            <div id="root"></div>
        </div>
    </body>
    </html>
    ```
    - webpack 配置
    
    ```js
    // webpack.config.js
    const { CleanWebpackPlugin } = require('clean-webpack-plugin');
    const { HtmlWebpackPlugin } = require('html-webpack-plugin');
    
    module.exports = {
        entry: './src/main.js',
        pligins:[
            new CleanWebpackPlugin(),
            
            new HtmlWebpackPlugin({
                title: 'webpack plugin sample', // 配置 title
                template: './src/index.html' // 配置相关模板路径
            })
        ]
    }
    ```
