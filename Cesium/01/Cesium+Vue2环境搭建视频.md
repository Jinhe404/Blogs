# Cesium+vue2环境搭建

## vue 框架下引入Cesium

[TOC]

### 1. 利用vue-cli创建新的vue项目

Vue-cli 官方网址(https://cli.vuejs.org/zh/#起步)

![](E:\软件\typora做的笔记\博客笔记\cesium\项目图片\环境搭建\图片1.png)

安装脚手架

```
npm install -g @vue/cli
```

创建一个Cesium项目：

```
vue create cesiumapp
```

### 2.安装Cesium

作者尝试了多次，Cesium已经更新到1.102.0版本，新版本适配会出现许多问题，建议指定1.95.0版本

```
npm install cesium@1.95.0 -s
```

### 3.安装loader

```
npm install @open-wc/webpack-import-meta-loader
```

### 4.安装webpack

建议安装10.2.4版本

```
npm install copy-webpack-plugin@10.2.4
```

![](E:\软件\typora做的笔记\博客笔记\cesium\项目图片\环境搭建\图片2.png)

### 5.vue-config.js配置

```
const {defineConfig} = require('@vue/cli-service')
const CopyWebpackPlugin = require("copy-webpack-plugin");

const webpack = require("webpack");
const path = require("path");

let cesiumSource = "node_modules/cesium/Source";
let cesiumWorkers = "Workers";
module.exports = defineConfig({
  transpileDependencies: true,
  lintOnSave: false,
  configureWebpack: {
    externals: {
      'cesium': 'Cesium',
    },
    output: {
      sourcePrefix: " ", // 让webpack 正确处理多行字符串配置 amd参数
    },
    amd: {
      toUrlUndefined: true, // webpack在cesium中能友好的使用require
    },
    resolve: {
      extensions: ['.js', '.vue', '.json'],
      alias: {
        "@": path.resolve("src"),
        cesium: path.resolve(__dirname, cesiumSource),
      }
    },
    plugins: [
      new CopyWebpackPlugin({
        patterns: [
          {from: path.join(cesiumSource, cesiumWorkers), to: "Workers"},
          {from: path.join(cesiumSource, "Assets"), to: "Assets"},
          {from: path.join(cesiumSource, "Widgets"), to: "Widgets"},
          {from: path.join(cesiumSource, "ThirdParty/Workers"), to: "ThirdParty/Workers"}
        ]
      }),
      new webpack.DefinePlugin({
        CESIUM_BASE_URL: JSON.stringify("./"),
      }),
    ],
    module: {
      unknownContextCritical: false,
      unknownContextRegExp: /\/cesium\/cesium\/Source\/Core\/buildModuleUrl\.js/,
      rules: [
        {
          test: /\.js$/,
          use: {
            loader: '@open-wc/webpack-import-meta-loader',
          },
        },
      ]
    },
  },
  devServer: {
    hot: true,
    open: true,
    // 代理
    proxy: {
      '/api': {
        target: 'http://localhost:8888/',
        changeOrigin: true,
        ws: true,
        pathRewrite: {
          '^/api': ''
        }
      }
    },
    port: 8080,
  }
})

```

### 6.main.js引入

```
import 'cesium/Widgets/widgets.css';
```

### 7.App.vue中的样式

```
html,body,#cesiumContainer {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
  overflow: hidden;
}
```

### 8.HolloWorld.vue中的代码

```
<template>
  <div id="cesiumContainer">
  </div>
</template>

<script>
import * as Cesium from 'cesium/Cesium'
export default {
  name: 'HelloWorld',

  mounted(){
  this.initCesium()
  },
  methods:{
    initCesium:function (){
      let viewer = new Cesium.Viewer('cesiumContainer')
    }
  }


}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>

```

![](E:\软件\typora做的笔记\博客笔记\cesium\项目图片\环境搭建\图片3.png)