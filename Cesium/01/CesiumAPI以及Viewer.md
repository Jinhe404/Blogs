## 1.cesium 的 API 结构

以下是Cesium的所有API汇总：

1. Core：核心模块，包含Cesium的基础构件、数据结构、算法等。
2. Scene：场景模块，包含Cesium的渲染引擎、摄像机、灯光、图像合成等。
3. Widgets：小部件模块，包含Cesium的用户界面、控制面板、信息窗口等。
4. DataSources：数据源模块，包含Cesium的数据解析、可视化、编辑等。
5. ThirdParty：第三方模块，包含Cesium的依赖库、插件、工具等。
6. Workers：工作线程模块，包含Cesium的并行计算、异步加载等。
7. Plugins：插件模块，包含Cesium的地理编码、路线规划、地形分析等。

每个模块都包含了许多API，以下是一些常用的API：

1. Cesium：Cesium命名空间，包含Cesium的全局变量、常量、函数等。
2. Viewer：Cesium.Viewer类，用于创建和管理Cesium场景和小部件。
3. Camera：Cesium.Camera类，用于管理摄像机的位置、朝向、视野等。
4. Entity：Cesium.Entity类，用于描述Cesium场景中的实体，包含位置、属性、图形等。
5. DataSource：Cesium.DataSource类，用于加载和解析各种格式的地理数据源。
6. ImageryLayer：Cesium.ImageryLayer类，用于管理Cesium场景中的图像图层。
7. TerrainProvider：Cesium.TerrainProvider类，用于加载和管理Cesium场景中的地形数据源。
8. Ellipsoid：Cesium.Ellipsoid类，用于描述Cesium场景中的椭球体。
9. Color：Cesium.Color类，用于描述颜色，包含RGBA、HSVA等。
10. Cartesian3：Cesium.Cartesian3类，用于描述三维空间中的点，包含x、y、z坐标。

以上是Cesium的部分API，更多API详细信息可以参考Cesium官方文档。

## 2.Viewer的详细介绍

在Cesium中，Viewer是一个核心对象，用于管理场景的显示和交互。

### 创建Viewer对象

可以通过以下方式创建Viewer对象：

```
var viewer = new Cesium.Viewer(container, options);
```

其中，`container`参数是一个DOM元素，用于容纳Viewer对象，可以是一个`div`元素或者其他任意类型的容器元素。`options`参数是一个可选的配置对象，包含一系列属性和方法，用于控制Viewer的行为和功能。

### 设置地球的初始状态

创建Viewer对象后，可以通过`viewer`对象的`camera`属性和`scene`属性来控制地球的初始状态。例如：

```
var viewer = new Cesium.Viewer('cesiumContainer');
var camera = viewer.camera;
var scene = viewer.scene;

camera.setView({
  destination: Cesium.Cartesian3.fromDegrees(-74.01881302800248, 40.69114333714821, 1000),
  orientation: {
    heading: Cesium.Math.toRadians(0),
    pitch: Cesium.Math.toRadians(-90),
    roll: Cesium.Math.toRadians(0)
  }
});

scene.globe.enableLighting = true;
scene.skyBox.show = false;

```

在上述代码中，`camera`对象的`setView`方法用于设置地球的视图，包括位置、方向和缩放等参数。`destination`属性表示观察点的位置，使用经度、纬度和高度三个参数表示。`orientation`属性表示观察点的方向，包括航向、俯仰角和翻滚角三个参数。`scene`对象的`globe`属性和`skyBox`属性用于控制地球的外观和光照效果。

### 加载地图数据和图层

可以通过`viewer`对象的`imageryLayers`属性和`terrainProvider`属性来加载地图数据和图层。例如：

```
var viewer = new Cesium.Viewer('cesiumContainer');

var imageryLayers = viewer.imageryLayers;
imageryLayers.addImageryProvider(new Cesium.UrlTemplateImageryProvider({
  url: 'http://tile.stamen.com/watercolor/{z}/{x}/{y}.jpg',
  credit: 'Map tiles by Stamen Design, under CC BY 3.0. Data by OpenStreetMap, under ODbL.'
}));

var terrainProvider = new Cesium.CesiumTerrainProvider({
  url: 'https://assets.agi.com/stk-terrain/world',
  requestWaterMask: true,
  requestVertexNormals: true
});
viewer.terrainProvider = terrainProvider;

```

在上述代码中，`imageryLayers`属性是一个图层管理器，用于加载各种地图图层。可以通过`addImageryProvider`方法添加一个`ImageryProvider`对象，用于加载地图切片数据。`UrlTemplateImageryProvider`是一个常用的切片数据提供者

## 3.Viewer 构造参数

下面是Cesium中Viewer的一些常用构造参数介绍：

1. container：指定Viewer要渲染到的DOM容器。可以是一个HTML元素的ID、DOM元素对象或jQuery选择器。默认值是document.body。
2. imageryProvider：指定用于提供底图图层的对象。可以是Cesium提供的ImageryProvider对象，也可以是其他第三方提供的地图服务对象，如Google、Bing、天地图等。默认值是Cesium.WorldImageryProvider对象。
3. terrainProvider：指定用于提供地形数据的对象。可以是Cesium提供的TerrainProvider对象，也可以是其他第三方提供的地形服务对象，如地球之声、Mapbox等。默认值是Cesium.EllipsoidTerrainProvider对象。
4. animation：指定是否启用动画控件。默认值是true。
5. timeline：指定是否启用时间轴控件。默认值是true。
6. fullscreenButton：指定是否启用全屏控件。默认值是true。
7. vrButton：指定是否启用虚拟现实控件。默认值是false。
8. sceneMode：指定场景模式。可以是3D、2D或Columbus View模式。默认值是Cesium.SceneMode.SCENE3D。
9. scene3DOnly：指定是否只显示3D场景。默认值是false。
10. mapProjection：指定地图投影方式。可以是Web Mercator、WGS84或其他自定义投影方式。默认值是Cesium.WebMercatorProjection。
11. baseLayerPicker : false,是否显示图层选择器，右上角图层选择按钮
12. fullscreenButton : false,是否显示全屏按钮，右下角全屏选择按钮
13. geocoder : false,是否显示geocoder 小器件，右上角查询按钮
14. homeButton : false,是否显示 Home 按钮，右上角 home 按钮
15. sceneModePicker : false,是否显示 3D/2D 选择器，右上角按钮
16. navigationHelpButton : false,是否显示右上角的帮助按钮s
17. electionIndicator : false,是否显示选取指示器组件
18. infoBox : false,是否显示信息框
19. scene3DOnly : true,如果设置为 true，则所有几何图形以 3D 模式绘制以节约 GPU 资源
20. clock : new Cesium.Clock(),用于控制当前时间的时钟对象
21. shouldAnimate: true,自动播放动画控件
22. shadows: true,是否显示光照投射的阴影terrainShadows:Cesium.ShadowMode.RECEIVE_ONLY,地质接收阴影
23. sceneMode:Cesium.SceneMode.SCENE3D,//初始化渲染 3D 场景
24. terrainProviderViewModels:Cesium.createDefaultTerrainProviderViewModels(),可供BaseLayerPicker 选择的地形图层 ProviderViewModel 数组
25. selectedTerrainProviderViewModel : undefined,//当前地形图层的显示模型，仅 baseLayerPicker 设为true 有意义
26. imageryProviderViewModels:Cesium.createDefaultImageryProviderViewModels(),可供BaseLayerPicker 选择的图像图层 ProviderViewModel 数组

这些构造参数只是Cesium Viewer的一部分，还有很多其他参数可以配置，比如camera、globe、skyAtmosphere、imageryLayers等等。具体使用方法和详细参数可以参考Cesium官方文档。

viewer._cesiumWidget._creditContainer.style.display = "none";	// 去除版权信息

## 4.Cesium中Cesium3DTile属性

在Cesium中，Cesium3DTile是一种基于Web的三维地图数据格式，包含了大量的空间数据和属性信息。以下是Cesium3DTile常用的属性：

1.boundingVolume

boundingVolume属性定义了Cesium3DTile的包围盒，用于优化渲染性能。

2.geometricError

geometricError属性定义了Cesium3DTile的几何精度，即模型与真实世界之间的误差。

3.refine

refine属性用于控制Cesium3DTile的细节级别，支持三个值：'ADD'、'REPLACE'和'REFINE'。'ADD'表示当前节点是父节点的一个子节点；'REPLACE'表示当前节点代替父节点；'REFINE'表示当前节点与父节点拥有相同的空间范围，但更细节的几何信息。

4.content

content属性是Cesium3DTile的内容，包含了几何、纹理、材质等信息，以及其他自定义属性。

5.batchTable

batchTable属性是Cesium3DTile的批处理表格，用于存储自定义属性数据。

6.properties

properties属性是Cesium3DTile的属性列表，用于定义Cesium3DTile的属性名称和类型。

7.viewerRequestVolume

viewerRequestVolume属性定义了Cesium3DTile的可视化请求区域，用于优化Cesium3DTile的加载和渲染性能。

8.children

children属性是Cesium3DTile的子节点，用于构建Cesium3DTile的树状结构。

9.transform

transform属性是Cesium3DTile的坐标变换矩阵，用于将Cesium3DTile的坐标系转换为地球坐标系。

10.extras

extras属性是Cesium3DTile的额外属性，用于存储自定义的元数据。

以上是Cesium3DTile常用的属性，可以根据实际需求来选择使用。在使用Cesium3DTile时，建议先了解Cesium3DTile的结构和属性，再根据需求来进行操作。

## 4.Cesiumlab

官网（http://www.cesiumlab.com/）

CesiumLab是一个基于Cesium的开源Web GIS平台，它提供了一个易于使用的Web GIS平台，可用于构建三维可视化应用程序、地图和地理空间信息系统。CesiumLab使用Cesium的渲染引擎和图形库，可创建高度交互的三维场景和动态数据可视化。CesiumLab的主要功能包括：

1. 地图：支持各种不同的地图投影、地形和影像服务，提供全球范围内的地图数据。
2. 数据可视化：支持各种不同的数据格式和数据源，包括3D Tiles、GeoJSON、KML、CSV、Shapefile等。
3. 地理空间分析：支持地理空间查询、缓冲区分析、路径规划、空间统计等。
4. 可视化工具：支持图层控制、标注、测量、时间轴、动画、天气等可视化工具。
5. 开发者工具：支持自定义脚本、自定义样式、自定义数据源、自定义工具等。

CesiumLab具有开源、跨平台、高性能、可扩展性等特点，可应用于各种不同的领域和行业，如地图制图、军事防卫、城市规划、航空航天、能源资源、物流运输等。CesiumLab已经成为了一个受欢迎的开源GIS平台，吸引了全球众多开发者和用户的关注和支持。

## 5.IIS以及Nginx发布3Dtiles模型

### 1.IIS发布

要在IIS上发布Cesium 3D Tiles模型，可以按照以下步骤进行：

1. 将Cesium 3D Tiles模型文件夹复制到Web服务器的网站目录下。假设Cesium 3D Tiles模型存储在D:\Cesium3DTiles\example目录中，可以将该目录复制到网站目录，如C:\inetpub\wwwroot\example。
2. 打开IIS管理器，在左侧面板中选择“Sites”节点，右键单击要发布Cesium 3D Tiles模型的网站，选择“Add Virtual Directory”。
3. 在“Add Virtual Directory”窗口中，输入虚拟目录的别名，例如“example”，然后将物理路径指向步骤1中的Cesium 3D Tiles模型文件夹，如“C:\inetpub\wwwroot\example”。
4. 点击“OK”按钮，完成虚拟目录的添加。
5. 验证发布结果。打开浏览器，输入网站的URL，后跟虚拟目录的别名，例如http://localhost/example。如果一切正常，将会显示Cesium 3D Tiles模型的内容。

需要注意的是，Cesium 3D Tiles模型是由大量的小文件组成的，因此需要在Web服务器上启用静态文件压缩和缓存功能，以提高性能和减少网络流量。此外，还需要配置正确的CORS（跨域资源共享）规则，以确保Cesium 3D Tiles模型可以从不同的域名和端口访问。

具体步骤可以访问：该博客[如何使用IIS发布3dtiles模型 - 大数据 - 亿速云 (yisu.com)](https://www.yisu.com/zixun/550348.html)

### 2.Nginx发布

1. 将Cesium 3D Tiles模型文件夹复制到Web服务器的网站目录下。假设Cesium 3D Tiles模型存储在/opt/Cesium3DTiles/example目录中，可以将该目录复制到网站目录，如/usr/share/nginx/html/example。
2. 打开Nginx配置文件，通常位于/etc/nginx/nginx.conf。在http节点中添加以下配置：

```
bashCopy codeserver {
    listen 80;
    server_name example.com;
    root /usr/share/nginx/html;

    location /example {
        alias /usr/share/nginx/html/example;
        add_header Access-Control-Allow-Origin *;
        add_header Access-Control-Allow-Methods "GET, OPTIONS";
        add_header Access-Control-Allow-Headers "DNT,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type";
        add_header Access-Control-Allow-Credentials true;
    }
}
```

其中，listen指定了监听的端口，server_name指定了服务器的域名或IP地址，root指定了服务器的根目录，location指定了Cesium 3D Tiles模型的虚拟目录，alias指定了Cesium 3D Tiles模型的物理路径，add_header指定了CORS规则，用于解决跨域问题。

1. 保存并关闭Nginx配置文件，重新加载Nginx配置：

```
Copy codesudo nginx -t
sudo systemctl reload nginx
```

1. 验证发布结果。打开浏览器，输入网站的URL，后跟虚拟目录的别名，例如http://example.com/example。如果一切正常，将会显示Cesium 3D Tiles模型的内容。

需要注意的是，Nginx默认启用静态文件压缩和缓存功能，以提高性能和减少网络流量。如果需要自定义Nginx的压缩和缓存配置，可以参考Nginx的文档进行操作。此外，还需要确保Nginx的安全性和性能稳定性，例如启用SSL证书、设置请求限制等。

http://localhost:8888/qxsy/guazhou/tileset.json

## 6.Cesium中ImageryProvider分类

在Cesium中，ImageryProvider是用于提供地球表面图像的接口。Cesium支持多种类型的ImageryProvider，每种类型的提供器都支持不同的地图服务和数据源。以下是Cesium中常用的ImageryProvider分类：

1. ArcGisMapServerImageryProvider：用于连接Esri的ArcGIS Map Server服务，支持多种地图服务，如矢量地图、卫星地图、地形地图等。
2. BingMapsImageryProvider：用于连接Bing Maps服务，支持全球卫星地图、道路地图、混合地图等。
3. GoogleEarthImageryProvider：用于连接Google Earth服务，支持卫星地图、道路地图、地形地图等。
4. SingleTileImageryProvider：用于加载单张静态图像作为图层，常用于加载静态地图或地形数据。
5. TileCoordinatesImageryProvider：用于加载预定义范围内的切片地图数据，可用于自定义地图数据源。
6. TileMapServiceImageryProvider：用于连接标准的WMTS（Web Map Tile Service）服务，支持多种地图服务，如OpenStreetMap、Mapbox等。
7. UrlTemplateImageryProvider：用于加载可变地址的切片地图数据，常用于自定义地图数据源。

以上是Cesium中常用的ImageryProvider分类，每种ImageryProvider都有自己的特点和应用场景，具体使用可以参考Cesium的官方文档和示例代码。

### 1.Cesium中ImageryProvider分类及其代码实现

1. ArcGisMapServerImageryProvider

ArcGisMapServerImageryProvider用于连接Esri的ArcGIS Map Server服务，支持多种地图服务，如矢量地图、卫星地图、地形地图等。

```
var imageryProvider = new Cesium.ArcGisMapServerImageryProvider({
    url: 'https://services.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer'
});

viewer.imageryLayers.addImageryProvider(imageryProvider);

```

1. BingMapsImageryProvider

BingMapsImageryProvider用于连接Bing Maps服务，支持全球卫星地图、道路地图、混合地图等。

```
var imageryProvider = new Cesium.BingMapsImageryProvider({
    url: 'https://dev.virtualearth.net',
    key: 'Your Bing Maps Key',
    mapStyle: Cesium.BingMapsStyle.AERIAL_WITH_LABELS
});

viewer.imageryLayers.addImageryProvider(imageryProvider);

```

1. GoogleEarthImageryProvider

GoogleEarthImageryProvider用于连接Google Earth服务，支持卫星地图、道路地图、地形地图等。

```
var imageryProvider = new Cesium.GoogleEarthImageryProvider({
    url: 'https://kh.google.com',
    channel: 't'
});

viewer.imageryLayers.addImageryProvider(imageryProvider);

```

1. SingleTileImageryProvider

SingleTileImageryProvider用于加载单张静态图像作为图层，常用于加载静态地图或地形数据

```
var imageryProvider = new Cesium.SingleTileImageryProvider({
    url: 'path/to/image.png',
    rectangle: Cesium.Rectangle.fromDegrees(-75.0, 39.0, -71.0, 42.0)
});

viewer.imageryLayers.addImageryProvider(imageryProvider);

```

1. TileCoordinatesImageryProvider

TileCoordinatesImageryProvider用于加载预定义范围内的切片地图数据，可用于自定义地图数据源。

```
var imageryProvider = new Cesium.TileCoordinatesImageryProvider({
    rectangle: Cesium.Rectangle.fromDegrees(-180.0, -90.0, 180.0, 90.0),
    tileWidth: 256,
    tileHeight: 256,
    maximumLevel: 5,
    tilingScheme: new Cesium.GeographicTilingScheme()
});

viewer.imageryLayers.addImageryProvider(imageryProvider);

```

1. TileMapServiceImageryProvider

TileMapServiceImageryProvider用于连接标准的WMTS（Web Map Tile Service）服务，支持多种地图服务，如OpenStreetMap、Mapbox等。

```
var imageryProvider = new Cesium.TileMapServiceImageryProvider({
    url: 'https://tile.openstreetmap.org',
    fileExtension: 'png',
    maximumLevel: 18,
    credit: 'OpenStreetMap contributors'
});

viewer.imageryLayers.addImageryProvider(imageryProvider);

```



## 7.Cesium中Entity 实体介绍

在Cesium中，Entity是指在三维场景中的物体，可以是点、线、面、模型、传感器等。每个Entity可以包括一个或多个属性，例如位置、方向、大小、颜色、材质、标签等。Entity是Cesium的核心对象之一，用于描述三维场景中的实体，提供了对场景中物体的创建、更新和删除等操作。

### 1.Entity对象具有以下属性：

1. id：每个Entity都有一个唯一的id。
2. name：Entity的名称。
3. position：Entity的位置，可以是笛卡尔坐标系或地理坐标系。
4. orientation：Entity的方向，可以是四元数或欧拉角。
5. velocity：Entity的速度。
6. modelMatrix：Entity的变换矩阵，用于描述Entity的缩放、旋转和平移。
7. billboard：Entity的贴图。
8. label：Entity的标签。
9. polyline：Entity的折线，用于连接多个点。
10. polygon：Entity的多边形，用于填充多个点组成的区域。
11. ellipse：Entity的椭圆，用于描述圆形或椭圆形的物体。
12. corridor：Entity的走廊，用于描述一个长方形的区域。
13. cylinder：Entity的圆柱体，用于描述一个圆柱体。
14. box：Entity的立方体，用于描述一个立方体。
15. sphere：Entity的球体，用于描述一个球体。
16. availability：Entity的可用性。
17. description：Entity的描述信息。
18. properties：Entity的自定义属性。

Entity对象还可以响应鼠标事件，例如鼠标点击、双击、移动等，可以通过监听Entity对象的相应事件来实现交互功能。

在Cesium中，Entity是描述三维场景中实体的重要对象，可以使用Entity来创建、更新和删除场景中的物体，并且可以添加自定义属性和交互功能。