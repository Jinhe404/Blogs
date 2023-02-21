# Cesium+vue环境搭建

以下是搭建Cesium+Vue环境的详细步骤和示例代码：

步骤：

1. 创建一个新的Vue项目

   在终端中运行以下命令来创建一个新的Vue项目：

```
vue create my-cesium-app
```

1. 根据提示选择需要的配置，等待项目创建完成。

2. 安装Cesium

   在终端中进入Vue项目目录，运行以下命令来安装Cesium：

```
npm install cesium
```

配置Webpack

在Vue项目中，需要配置Webpack来支持加载Cesium的相关资源。

首先在Vue项目的根目录下创建一个名为`vue.config.js`的文件，然后添加以下配置：

```
const CopyWebpackPlugin = require('copy-webpack-plugin');

module.exports = {
  configureWebpack: {
    plugins: [
      new CopyWebpackPlugin({
        patterns: [
          { from: 'node_modules/cesium/Build/Cesium/Workers', to: 'Workers' },
          { from: 'node_modules/cesium/Build/Cesium/ThirdParty', to: 'ThirdParty' },
          { from: 'node_modules/cesium/Build/Cesium/Assets', to: 'Assets' },
          { from: 'node_modules/cesium/Build/Cesium/Widgets', to: 'Widgets' }
        ]
      })
    ],
    output: {
      amd: {
        toUrlUndefined: true
      }
    },
    resolve: {
      alias: {
        cesium: 'cesium/Cesium'
      }
    }
  },
  chainWebpack: config => {
    config.module
      .rule('cesium')
      .test(/\.js$/)
      .include.add(/cesium/)
      .end()
      .use('babel')
      .loader('babel-loader')
      .end();
  },
  devServer: {
    public: 'localhost:8080',
    hot: false
  },
  productionSourceMap: false
};

```

在Vue组件中使用Cesium

在Vue组件中，可以使用Cesium的相关组件和API来开发虚拟地球应用。例如，以下是一个简单的Vue组件，展示一个包含Cesium的地球：

```
<template>
  <div id="cesiumContainer"></div>
</template>

<script>
import * as Cesium from 'cesium';

export default {
  name: 'CesiumViewer',
  mounted() {
    const viewer = new Cesium.Viewer('cesiumContainer');
  }
};
</script>

<style>
#cesiumContainer {
  height: 100%;
}
</style>

```

在这个组件中，使用`import * as Cesium from 'cesium'`来导入Cesium的API，然后在`mounted`钩子中创建一个Cesium的Viewer对象，并将其绑定到名为`cesiumContainer`的DOM元素上。

当该组件渲染到页面中时，就会显示一个包含Cesium的地球。