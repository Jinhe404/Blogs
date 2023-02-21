![img](https://img-blog.csdnimg.cn/img_convert/e0239a75f96830e577eef736ebcad965.png)

### 

# Cesium开发面试题

### 

## 1、请简要介绍一下Cesium的基本功能。

答：Cesium是一款3D地球可视化引擎，可以在Web浏览器中显示高度真实感的3D地球场景，包括地形、地表纹理、3D建筑、水域等。它提供多种漫游和导航方式，支持多种地形和影像数据格式，以及3D Tiles、CZML等技术，可以用于实时位置追踪、天文数据显示、地下和空中场景等应用场景。



##  2、请解释一下Cesium中的3D Tiles技术是什么，以及它的作用是什么。

答：3D Tiles是一种用于高效地加载和显示大规模的3D地球数据的技术，可以将复杂的3D数据分层并进行高度优化。Cesium中的3D Tiles技术可以支持大规模的3D地球数据，包括城市、建筑、地形等，提高了数据的加载速度和显示效率。



##  3、CZML是Cesium中的一个数据格式，它是什么，以及它用于描述什么样的场景？

答：CZML（Cesium Language）是一种描述和显示动态的地球场景的数据格式，它可以用于描述航班轨迹、气象数据、卫星运行轨迹等。CZML中可以包含实体的位置、速度、方向等信息，以及可视化效果的设置。



##   4、请解释一下Cesium中的ImageryProvider是什么，以及它的作用是什么。

答：ImageryProvider是Cesium中的一个数据提供器，用于提供地图和影像数据。它可以从多种来源获取数据，比如Web Map Service（WMS）、Web Map Tile Service（WMTS）等，并在地球表面上显示出来。通过使用ImageryProvider，开发者可以轻松地获取并显示各种地图和影像数据。



## 5、如何加载飞线

答：1、创建polyLine实体

2、计算带有弧度效果的点集数组作为polyline的positions属性参数



## 6、如何设置飞线动效材质

答：1、创建cesium自定义材质类

2、创建shader，原理是通过贴图UV移动来实现流光效果



## 7、如何在cesium地球上添加柱状图

答：1、创建entity实体，使用box属性；

2、dimensions设置长宽；

3、position设置中心点位置；

4、heightReference属性设置贴地属性；



## 8、如何让柱状图跟随数据变化

答：1、创建SampledPositionProperty对象

2、在不同的时间点绑定对应的值

将填充好的SampledPositionProperty赋值给dimensions，实现位置随时间的偏移

## 9、如何加载天气图的效果

答：1、使用Wind3D类实现

实现原理是将nc格式的数据解析之后运用primitive绘制

​    2、Cesium官网有github的分享案例，需要修改鼠标事件影响该类绘制时的显示隐藏

## 10、如何给cesium地球替换表面图层

答：1、主要是在viewer的imageryLayers地图层级内对单独的layer图层的显示隐藏或者添加与移除，imageryLayers有add与remove方法

```
2、viewer.imageryLayers.addImageryProvider(layer, num);
viewer.imageryLayers.remove(viewer.imageryLayers.get(num), true);
```

主要是这两个API
3、注意不同的地图图层加载会有对应的投影方式，比如web墨卡托投影和wgs84



## 11、cesium如何进行坐标转换

```
答：1、//经纬度转屏幕坐标

LngLatToSceenCoordinates(lng, lat) {

let cartesian3 = Cesium.Cartesian3.fromDegrees(lng, lat);

let cartesian2 = Cesium.SceneTransforms.wgs84ToWindowCoordinates(

viewer.scene,

cartesian3

);

return cartesian2;

},

2、 //笛卡尔坐标转经纬度坐标

Cartesian3ToLngLat(cartesian) {

let cartographic =

viewer.scene.globe.ellipsoid.cartesianToCartographic(cartesian);

let c_height = viewer.camera.positionCartographic.height;

//将地图坐标（弧度）转为十进制的度数

let lat_String = Cesium.Math.toDegrees(cartographic.latitude).toFixed(6);

let log_String = Cesium.Math.toDegrees(cartographic.longitude).toFixed(6);

return [

parseFloat(log_String),

parseFloat(lat_String),

parseFloat(c_height),

];

},
```

## 12、cesium如何实现标记的添加

答：1、创建entity实体对象使用billboard对象场景图标挥着使用billboard collection使用primitive创建

## 13、cesium如何实现鼠标拾取弹窗功能

答：1、创建new Cesium.ScreenSpaceEventHandler(canvas)对象

2、注册鼠标点击事件
3、使用let pick = viewer.scene.pick(movement.position); 选取当前的entity

## 14、如何设置cesium中的抗锯齿方法

答：1、使用fxaa方法，效果较差

2、使用msaa方法，但需要浏览器支持webGL2的api方法


![qrcode_for_gh_e879ec750214_258.jpg](https://bexp.135editor.com/files/users/498/4980660/202302/k5PHuh8T_I5qb.jpg?auth_key=1677427199-0-0-d90c72020ea7995dbf533d91bb976f8c)

