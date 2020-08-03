### 6.3.1 安装必要的模块
`npm install typescript ts-loader vue-property-decorator vue-class-component -D`

### 6.3.2 在项目根目录新增`tsconfig.json`文件
```js
{
  "compilerOptions": {
        // 与 Vue 的浏览器支持保持一致
        "target": "es5",
        // 这可以对 `this` 上的数据属性进行更严格的推断
        "strict": true,
        // 如果使用 webpack 2+ 或 rollup，可以利用 tree-shake:
        "module": "es2015",
        "moduleResolution": "node",
        "experimentalDecorators": true
    },
    "include": ["src"],
    "exclude": [
        "node_modules",
        "dist"
    ]
}
```

### 6.3.3 `vue.config.js`中新增`webpack`相关配置
```js
module.exports = {
  configureWebpack: {    
      resolve: { extensions: [".ts", ".tsx", ".js", ".json"] },    
      module: {        
          rules: [    
              {    
                  test: /\.tsx?$/,    
                  loader: 'ts-loader',    
                  exclude: /node_modules/,    
                  options: {
                      appendTsSuffixTo: [/\.vue$/],    
                  }    
               }        
           ]    
      }    
  },
}
```

### 6.3.4 在 `src`的根目录下添加`vue-shim.d.ts`文件
```js
declare module "*.vue" {
    import Vue from "vue";
    export default Vue;
}


declare module '*.js';
declare module '*.png';
```

- 新建 `.vue` 文件，结构参考如下
```html
<template>
    <div>
        {{msg}}
    </div>
</template>
<script lang="ts">
    import { Component, Vue } from 'vue-property-decorator';
    @Component
    export default class App extends Vue {
        // 初始化数据
        public msg: string = 'hello typescript';
        // 声明周期钩子
        mounted () {
        }
        // 计算属性
        get computedMsg (): string {
            return 'computed ' + this.msg
        }       
    }
</script>
<style>
</style>
```
### 6.3.5 注意的坑
如果是移动端使用到了`vant`UI组件，并且有些样式加载不了
请参考使用`ts-import-plugin`插件，`webpack`配置如下

```js
const tsImportPluginFactory = require('ts-import-plugin');
{
    test: /\.tsx?$/,
    loader: 'ts-loader',
    exclude: /node_modules/,
    options: {
        transpileOnly: true,
        getCustomTransformers: () => ({
        before: [ tsImportPluginFactory({
        appendTsSuffixTo: [/\.vue$/],
        libraryName: 'vant',
             libraryDirectory: 'es',
                 style: name => `${name}/style/less` // 配置vant主题文件
             }) ]
        }),
        compilerOptions: {
            module: 'es2015'
        }
    }
 }
```

