## **1.** **Viewer** **构造参数介绍**

```
var viewer = new Cesium.Viewer( 'cesiumContainer', { animation : false,//是否创建动画小器件，左下角仪表
baseLayerPicker : false,//是否显示图层选择器，右上角图层选择按钮fullscreenButton : false,//是否显示全屏按钮，右下角全屏选择按钮
geocoder : false,//是否显示geocoder 小器件，右上角查询按钮
homeButton : false,//是否显示 Home 按钮，右上角 home 按钮sceneModePicker : false,//是否显示 3D/2D 选择器，右上角按钮navigationHelpButton : false,//是否显示右上角的帮助按钮selectionIndicator : false,//是否显示选取指示器组件
timeline : false,//是否显示时间轴infoBox : false,//是否显示信息框
scene3DOnly : true,//如果设置为 true，则所有几何图形以 3D 模式绘制以节约 GPU 资源
clock : new Cesium.Clock(),//用于控制当前时间的时钟对象shouldAnimate: true,	//自动播放动画控件
shadows: true,//是否显示光照投射的阴影terrainShadows:Cesium.ShadowMode.RECEIVE_ONLY,//地质接收阴影sceneMode:Cesium.SceneMode.SCENE3D,//初始化渲染 3D 场景
selectedImageryProviderViewModel : undefined,//当前图像图层的显示模型，仅 baseLayerPicker 设为true 有意义
imageryProviderViewModels	:	Cesium.createDefaultImageryProviderViewModels(),//	可	供
BaseLayerPicker 选择的图像图层 ProviderViewModel 数组
imageryProvider : new Cesium.UrlTemplateImageryProvider( {
url : 'http://mt1.google.cn/vt/lyrs=s&hl=zh-CN&x={x}&y={y}&z={z}&s=Gali/'
} ),//图像图层提供者，仅baseLayerPicker 设为false 有意义

selectedTerrainProviderViewModel : undefined,//当前地形图层的显示模型，仅 baseLayerPicker 设为
true 有意义
terrainProviderViewModels	:	Cesium.createDefaultTerrainProviderViewModels(),//	可	供
BaseLayerPicker 选择的地形图层 ProviderViewModel 数组

terrainProvider : new Cesium.EllipsoidTerrainProvider(),//地形图层提供者，仅 baseLayerPicker 设为
false 有意义
skyBox : new Cesium.SkyBox({ sources : {
positiveX : '/xxxxxx/px.jpg', negativeX : '/xxxxxx/mx.jpg', positiveY : '/xxxxxx/py.jpg', negativeY : '/xxxxxx/my.jpg', positiveZ : '/xxxxxx/pz.jpg', negativeZ : '/xxxxxx/mz.jpg'
}
}),//用于渲染星空的 SkyBox 对象
fullscreenElement : document.body,// 全 屏 时 渲 染 的 HTML 元 素 , shoSources : new Cesium.DataSourceCollection()	//需要进行可视化的数据源的集合
wRenderLoopErrors : false,//如果设为true，将在一个 HTML 面板中显示错误信息
data} );
```

```
viewer._cesiumWidget._creditContainer.style.display = "none";	// 去除版权信息
```

8.Viewer 分辨率resolutionScale
获取或设置渲染分辨率的比例因子。小于 1.0 的值可以提高在功能较弱的设备上的性能，而
大于 1.0 的值将以更高的速度渲染分辨率，然后缩小，从而提高视觉保真度。
例如，如果小部件的布局尺寸为 640x480，则将该值设置为 0.5 将使场景渲染为 320x240， 然后在设置时放大，将其设置为 2.0 将导致场景渲染为 1280x960，然后缩小比例。

通俗的说就是需要多少个屏幕像素去渲染一个 css 像素，屏幕分辨率越高，屏幕分辨率就越大，就可以使用更多的屏幕像素去显示一个 css 像素，当然这就需要更好的显卡作为支撑了。

useBrowserRecommendedResolution
指示是否使用浏览器建议的分辨率的布尔标志。

如果为 true，则忽略浏览器的设备像素比，而使用 1.0，基于 CSS 像素而不是设备像素的有效渲染。这可以改善在像素密度较高、功能较弱的设备上的性能。如果为 false，则渲染将以设备像素为单位。resolutionScale 仍将生效，无论布尔标志是真是假。

![image-20230718094950228](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20230718094950228.png)

### ViewportQuad

与视口对齐的四边形。可以作为公司的 logo 进行渲染。

material
视口四边形的表面外观。这可以是多个内置对象之一，也可以是使用 FabricMaterial 编写的自定义材质 。

```
默认材质为 Material.ColorType.
viewportQuad.material.uniforms.color = new Cesium.Color(1.0, 1.0, 0.0, 1.0); viewportQuad.material = Cesium.Material.fromType(Cesium.Material.StripeType);
BoundingRectangle 定义四边形在视口中的位置。
rectangle
viewportQuad.rectangle = new Cesium.BoundingRectangle(0, 0, 80, 40);
```

确定是否将显示视口四边形图元。默认值：true show

场景视锥，渲染帧率，地形，几何体监控
viewer.extend(Cesium.viewerCesiumInspectorMixin);

![image-20230718095143364](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20230718095143364.png)

### viewerCesiumInspectorMixin

性能监控狗

```

viewer.extend(Cesium.viewerPerformanceWatchdogMixin, {

lowFrameRateMessage : 'Why is this going so <em>slowly</em>?'});
```

## 2.Entity 实体

### **1)** **Entity** 的公共属性

| id           | String                                                       | 此对象的唯一标识符。如果未提供，则将生成GUID。 |
| ------------ | ------------------------------------------------------------ | ---------------------------------------------- |
| name         | String                                                       | 要显示给用户的可读名称。它不必是唯一的。       |
| availability | [TimeIntervalCollection](http://cesium.xin/cesium/cn/Documentation1.72/TimeIntervalCollection.html) | 与此对象相关联的可用性（如果有）。             |
| show         | Boolean                                                      | 一个布尔值，指示是否显示该实体及其子代。       |
| description  | [Property](http://cesium.xin/cesium/cn/Documentation1.72/Property.html) \| string | 一个字符串属性，用于为此实体指定HTML 描述。    |
| position     | [PositionProperty](http://cesium.xin/cesium/cn/Documentation1.72/PositionProperty.html) \| [Cartesian3](http://cesium.xin/cesium/cn/Documentation1.72/Cartesian3.html) | 指定实体位置的属性。                           |
| orientation  | [Property](http://cesium.xin/cesium/cn/Documentation1.72/Property.html) | 指定实体方向的属性。                           |
| viewFrom     | [Property](http://cesium.xin/cesium/cn/Documentation1.72/Property.html) | 用于查看该对象的建议初始偏移量。               |
| parent       | [Entity](http://cesium.xin/cesium/cn/Documentation1.72/Entity.html) | 要与此实体相关联的父实体。                     |
| properties   | [PropertyBag](http://cesium.xin/cesium/cn/Documentation1.72/PropertyBag.html) \|undefined | 与此实体相关联的任意属性。                     |

### 2)Entity 的公共方法

addProperty (propertyName)

向此对象添加属性。添加属性后，就可以用 Entity＃definitionChanged 观察并合成与 CompositeEntityCollection

computeModelMatrix (time, result ) → Matrix4

在指定时间为实体的转换计算模型矩阵。如果方向或位置返回未定义未定义。

isAvailable (time) → Boolean

给定时间，如果此对象在该时间内应该有数据，则返回 true。

merge (source)

将此对象上每个未分配的属性分配给该值提供的源对象具有相同属性

removeProperty (propertyName)

删除了以前用 addProperty 添加的属性。

### 3)Entity 的 Graphics

| billboard | [BillboardGraphics](http://cesium.xin/cesium/cn/Documentation1.72/BillboardGraphics.html) \| [BillboardGraphics.ConstructorOptio](http://cesium.xin/cesium/cn/Documentation1.72/BillboardGraphics.html) ns | 与此实体相关联的广告牌。           |
| --------- | ------------------------------------------------------------ | ---------------------------------- |
| box       | [BoxGraphics](http://cesium.xin/cesium/cn/Documentation1.72/BoxGraphics.html) \| [BoxGraphics.ConstructorOptions](http://cesium.xin/cesium/cn/Documentation1.72/BoxGraphics.html) | 与该实体关联的框。                 |
| corridor  | [CorridorGraphics](http://cesium.xin/cesium/cn/Documentation1.72/CorridorGraphics.html) \| [CorridorGraphics.ConstructorOption](http://cesium.xin/cesium/cn/Documentation1.72/CorridorGraphics.html) s | 与此实体相关联的走廊。             |
| cylinder  | [CylinderGraphics](http://cesium.xin/cesium/cn/Documentation1.72/CylinderGraphics.html) \| [CylinderGraphics.ConstructorOptions](http://cesium.xin/cesium/cn/Documentation1.72/CylinderGraphics.html) | 要与此实体相关联的圆柱体。         |
| ellipse   | [EllipseGraphics](http://cesium.xin/cesium/cn/Documentation1.72/EllipseGraphics.html) \| [EllipseGraphics.ConstructorOptions](http://cesium.xin/cesium/cn/Documentation1.72/EllipseGraphics.html) | 与此实体相关联的椭圆。             |
| ellipsoid | [EllipsoidGraphics](http://cesium.xin/cesium/cn/Documentation1.72/EllipsoidGraphics.html) \| [EllipsoidGraphics.ConstructorOption](http://cesium.xin/cesium/cn/Documentation1.72/EllipsoidGraphics.html) s | 与此实体相关联的椭球。             |
| label     | [LabelGraphics](http://cesium.xin/cesium/cn/Documentation1.72/LabelGraphics.html) \| [LabelGraphics.ConstructorOptions](http://cesium.xin/cesium/cn/Documentation1.72/LabelGraphics.html) | 与此实体相关联的options.label。    |
| model     | [ModelGraphics](http://cesium.xin/cesium/cn/Documentation1.72/ModelGraphics.html) \| [ModelGraphics.ConstructorOptions](http://cesium.xin/cesium/cn/Documentation1.72/ModelGraphics.html) | 与此实体相关联的模型。             |
| tileset   | [Cesium3DTilesetGraphics](http://cesium.xin/cesium/cn/Documentation1.72/Cesium3DTilesetGraphics.html) \| [Cesium3DTilesetGraphics.Co](http://cesium.xin/cesium/cn/Documentation1.72/Cesium3DTilesetGraphics.html) nstructorOptions | 要与此实体相关联的 3D Tiles 图块。 |

| path           | [PathGraphics](http://cesium.xin/cesium/cn/Documentation1.72/PathGraphics.html) \| [PathGraphics.ConstructorOptions](http://cesium.xin/cesium/cn/Documentation1.72/PathGraphics.html) | 与此实体相关联的路径。             |
| -------------- | ------------------------------------------------------------ | ---------------------------------- |
| plane          | [PlaneGraphics](http://cesium.xin/cesium/cn/Documentation1.72/PlaneGraphics.html) \| [PlaneGraphics.ConstructorOptions](http://cesium.xin/cesium/cn/Documentation1.72/PlaneGraphics.html) | 与此实体相关联的平面。             |
| point          | [PointGraphics](http://cesium.xin/cesium/cn/Documentation1.72/PointGraphics.html) \| [PointGraphics.ConstructorOptions](http://cesium.xin/cesium/cn/Documentation1.72/PointGraphics.html) | 与该实体关联的点。                 |
| polygon        | [PolygonGraphics](http://cesium.xin/cesium/cn/Documentation1.72/PolygonGraphics.html) \| [PolygonGraphics.ConstructorOptions](http://cesium.xin/cesium/cn/Documentation1.72/PolygonGraphics.html) | 要与此实体相关联的多边形。         |
| polyline       | [PolylineGraphics](http://cesium.xin/cesium/cn/Documentation1.72/PolylineGraphics.html) \| [PolylineGraphics.ConstructorOptions](http://cesium.xin/cesium/cn/Documentation1.72/PolylineGraphics.html) | 与此实体相关联的折线。             |
| polylineVolume | [PolylineVolumeGraphics](http://cesium.xin/cesium/cn/Documentation1.72/PolylineVolumeGraphics.html) \| [PolylineVolumeGraphics.Cons](http://cesium.xin/cesium/cn/Documentation1.72/PolylineVolumeGraphics.html) tructorOptions | 要与此实体相关联的polylineVolume。 |
| rectangle      | [RectangleGraphics](http://cesium.xin/cesium/cn/Documentation1.72/RectangleGraphics.html) \| [RectangleGraphics.ConstructorOpti](http://cesium.xin/cesium/cn/Documentation1.72/RectangleGraphics.html) ons | 与此实体相关联的矩形。             |
| wall           | [WallGraphics](http://cesium.xin/cesium/cn/Documentation1.72/WallGraphics.html) \| [WallGraphics.ConstructorOptions](http://cesium.xin/cesium/cn/Documentation1.72/WallGraphics.html) | 与该实体关联的墙。                 |

### point 点

效果：

![image-20230718095545283](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20230718095545283.png)

属性：

![image-20230718095602719](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20230718095602719.png)

clone ( result ) → BillboardGraphics

复制此实例。

merge (source)

将此对象上每个未分配的属性分配给该值提供的源对象具有相同属性。

### Billboard 广告牌 

|      |                                                            |
| ---- | ---------------------------------------------------------- |
|      | ![img](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/wps9.png) |

billboard 的特性会随着场景的旋转移动来改变自身的朝向

属性：

![image-20230718095657923](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20230718095657923.png)

lone ( result ) → BillboardGraphics

复制此实例。 

merge (source)

将此对象上每个未分配的属性分配给该值提供的源对象具有相同属性。

###  Box 盒子

属性：

![image-20230718095940125](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20230718095940125.png)

方法：

clone ( result ) → BillboardGraphics

复制此实例。

merge (source)

将此对象上每个未分配的属性分配给该值提供的源对象具有相同属性。

### Corridor 走廊

属性：

![image-20230718100032010](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20230718100032010.png)

classificationType，则用来描述是否只贴地形（ClassificationType.TERRAIN），或者只贴 3dtiles

数据（ClassificationType.CESIUM_3D_TILE），或者二者都贴（ClassificationType.BOTH）

方法：

clone ( result ) → BillboardGraphics

复制此实例。

merge (source)

将此对象上每个未分配的属性分配给该值提供的源对象具有相同属性。

### cylinder 椎体

clone ( result ) → CylinderGraphics
复制此实例。

merge (source)
将此对象上每个未分配的属性分配给该值提供的源对象具有相同属性。

### ellipse 圆与椭圆

属性：

![image-20230718101537737](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20230718101537737.png)

```
classificationType，则用来描述是否只贴地形（ClassificationType.TERRAIN），或者只贴 3dtiles
数据（ClassificationType.CESIUM_3D_TILE），或者二者都贴（ClassificationType.BOTH）

```

方法：

clone ( result ) → EllipseGraphics
复制此实例。

merge (source)
将此对象上每个未分配的属性分配给该值提供的源对象具有相同属性。

### ellipsoid 球体与椭球体

![image-20230718101613755](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20230718101613755.png)

属性：

![image-20230718101623893](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20230718101623893.png)

方法：

clone ( result ) → EllipsoidGraphics
复制此实例。

merge (source)
将此对象上每个未分配的属性分配给该值提供的源对象具有相同属性。

### label 标签

属性：

![image-20230718101913904](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20230718101913904.png)

方法：

clone ( result ) → LabelGraphics
复制此实例。

merge (source)

将此对象上每个未分配的属性分配给该值提供的源对象具有相同属性。

### model 模型

![image-20230718102001669](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20230718102001669.png)

属性：

![image-20230718102010262](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20230718102010262.png)

方法：

clone ( result ) → ModelGraphics
复制此实例。

merge (source)
将此对象上每个未分配的属性分配给该值提供的源对象具有相同属性。

### path 路径

属性：

![image-20230718102039062](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20230718102039062.png)

### plane 平面

![image-20230718104119564](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20230718104119564.png)

### polygon 多边形

![image-20230718104139680](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20230718104139680.png)

```
classificationType，则用来描述是否只贴地形（ClassificationType.TERRAIN），或者只贴 3dtiles
数据（ClassificationType.CESIUM_3D_TILE），或者二者都贴（ClassificationType.BOTH）
```

## 3.EntityCollection

### 1)EntityCollection 属性

id : String
获取此集合的全局唯一标识符。

owner : DataSource | CompositeEntityCollection
获取此实体集合的所有者，即。创建它的数据源或复合实体集合。

show : Boolean
获取此实体集合是否应为显示。如果为 true，则仅在以下情况下显示每个实体:它自己的 show
属性也是如此。

values : Array.< Entity >
获取集合中的 Entity 实例的数组。此数组不应直接修改。

### 2)EntityCollection 方法

add (entity) → Entity
将实体添加到集合中。

computeAvailability () → TimeInterval
计算集合中实体的最大可用性。如果集合包含无限可用数据和非无限数据的混合，它只会返   回与非无限数据有关的时间间隔。返回数据是无限的，将返回一个无限的时间间隔。

contains (entity) → Boolean
如果提供的实体在此集合中，则返回 true，否则返回 false。

getById (id) → Entity |undefined
获取具有指定 ID 的实体。

getOrCreateEntity (id) → Entity
获取具有指定 ID 的实体，或者创建一个实体并将其添加到集合（如果不存在）。

remove (entity) → Boolean
从集合中删除实体。

removeAll ()
从集合中删除所有实体。

removeById (id) → Boolean
从集合中删除具有提供的 ID 的实体。

resumeEvents ()
恢复立即引发 EntityCollection＃collectionChanged 事件添加或删除项目时。事件暂停时进行的任何修改调用此函数时，将作为单个事件触发。该函数是引用计数的，并且可以安全地多   次调用是 EntityCollection＃resumeEvents 的相应调用。
Throws:
DeveloperError :不能在 suspendEvents 之前调用 resumeEvents。

suspendEvents ()
防止引发 EntityCollection＃collectionChanged 事件直到对 EntityCollection＃resumeEvents

进行相应的调用为止将会引发一个涵盖所有已暂停操作的事件。这允许有效地添加和删除许   多项目。只要存在，就可以安全地多次调用此函数是 EntityCollection＃resumeEvents 的相应调用。大批量操作时，临时禁用事件可以提高性能。

## 4.EntityCluster

定义屏幕空间对象（广告牌，点，标签）的聚集方式。

### 1)EntityCluster 属性

| enabled            | 布尔值 | false | 可选是否启用群集。                 |
| ------------------ | ------ | ----- | ---------------------------------- |
| pixelRange         | 数字   | 80    | 可选扩展屏幕空间边界框的像素范围。 |
| minimumClusterSize | 数字   | 2     | 可选可以群集的最小屏幕空间对象。   |
| clusterBillboards  | 布尔值 | true  | 可选是否将实体的广告牌聚类。       |
| clusterLabels      | 布尔值 | true  | 可选是否将实体的标签聚类。         |
| clusterPoints      | 布尔值 | true  | 可选是否将实体的点聚类。           |

### 2)EntityCluster 方法

destroy ()
销毁此对象拥有的 WebGL 资源。销毁对象可以确定性释放 WebGL 资源，而不是依赖垃圾回收器破坏此对象。

### 3)EntityCluster 事件

```
Cesium.EntityCluster.newClusterCallback (clusteredEntities, cluster)
一个事件监听器函数，用于设置集群样式。
clusteredEntities	集群中包含的实体的数组。
cluster	包含广告牌，标签和点属性的对象。
```

### 4)EntityCluster 实例

```
// The default cluster values. dataSource.clustering.clusterEvent.addEventListener(function(entities, cluster) {
cluster.label.show = true;
cluster.label.text = entities.length.toLocaleString();
});
```

## 5.EntityView 相机跟踪实体

构造器

| entity    | [Entity](https://cesium.com/learn/cesiumjs/ref-doc/Entity.html) |                 | 用相机跟踪的实体。     |
| --------- | ------------------------------------------------------------ | --------------- | ---------------------- |
| scene     | [Scene](https://cesium.com/learn/cesiumjs/ref-doc/Scene.html) |                 | 要使用的场景。         |
| ellipsoid | [Ellipsoid](https://cesium.com/learn/cesiumjs/ref-doc/Ellipsoid.html) | Ellipsoid.WGS84 | 用于定向相机的椭球体。 |

属性
boundingSphere
对象的边界球体。

ellipsoid
用于定向相机的椭球体。

entity
用相机跟踪的实体。

scene : Scene
跟踪对象的场景。

方法
update(time, boundingSphere)
应该调用每个动画帧来更新相机到最新的设置。