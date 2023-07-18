# Cesium坐标系介绍

[TOC]

Cesium是一个3D地图引擎，它使用笛卡尔坐标系来描述3D空间中的位置和方向。在Cesium中，地球的中心被定义为原点，坐标轴被定义如下：

- X轴：指向经度为0度的位置，向东为正方向。
- Y轴：指向纬度为0度的位置，向北为正方向。
- Z轴：指向地球的北极点，垂直于地球表面向外为正方向。

Cesium中的坐标系是右手坐标系，即将右手的大拇指指向X轴的正方向，食指指向Y轴的正方向，中指指向Z轴的正方向，当这三个手指弯曲的方向与坐标系正方向相同，那么这就是一个右手坐标系。

Cesium中有两种常用的坐标系：笛卡尔坐标系和地理坐标系。

- 笛卡尔坐标系：在Cesium中，位置用笛卡尔坐标系表示，使用三个数字表示在X、Y和Z轴上的偏移量。坐标系的原点位于地球的中心。因此，这些坐标通常是负的。单位通常是米。
- 地理坐标系：地理坐标系是一种基于经度和纬度的坐标系，它使用度数来表示位置。在Cesium中，地理坐标可以通过将经度、纬度和高度值传递给`Cartographic`对象来表示。其中经度和纬度是以度数表示的，高度值可以是以米或其他单位表示的。Cesium将地理坐标转换为笛卡尔坐标以在地球表面上进行可视化。

Cesium还支持多种坐标系转换和操作，例如将地理坐标转换为笛卡尔坐标，将笛卡尔坐标转换为地理坐标，计算两点之间的距离等。这些功能可以通过Cesium中的`Cartesian3`和`Cartographic`对象来实现。

## 笛卡尔坐标系

Cesium中的笛卡尔坐标系是一个三维笛卡尔坐标系，其中每个点都由三个坐标轴上的数字表示。这三个坐标轴是x、y和z。它们通常表示空间中的长度、宽度和高度。

在Cesium中，笛卡尔坐标系的原点是地球的中心。x轴指向经度为0度的位置，y轴指向经度为90度东的位置，z轴指向北极。此坐标系是右手系，即如果您将右手的拇指指向x轴，食指指向y轴，中指指向z轴，则其他手指的方向表示正方向。

在Cesium中，`Cartesian3`对象表示三维笛卡尔坐标系中的点，其中每个点由x、y和z坐标值表示。例如，以下是在Cesium中创建`Cartesian3`对象的示例：

```
javascriptCopy codevar x = 1000;
var y = 2000;
var z = 3000;

var cartesian = new Cesium.Cartesian3(x, y, z);
```

在这个示例中，我们创建了一个名为`cartesian`的`Cartesian3`对象，并在构造函数中提供了x、y和z坐标值。这个点的笛卡尔坐标是(1000, 2000, 3000)。

笛卡尔坐标系在Cesium中用于表示三维场景中的几何图形，例如模型、相机位置和方向以及其他场景元素。

## 地理坐标系

Cesium中的地理坐标系是一个二维经纬度坐标系，通常用于表示地球表面的位置。地理坐标系使用经度和纬度度数表示位置，通常用度数（degree）作为单位，其中经度值介于-180度到180度之间，纬度值介于-90度到90度之间。

在Cesium中，`Cartographic`对象表示地理坐标系中的点，由经度、纬度和高度三个值组成。例如，以下是在Cesium中创建`Cartographic`对象的示例：

```
javascriptCopy codevar longitude = Cesium.Math.toRadians(-75.59777);
var latitude = Cesium.Math.toRadians(40.03883);
var height = 1000;

var cartographic = new Cesium.Cartographic(longitude, latitude, height);
```

在这个示例中，我们创建了一个名为`cartographic`的`Cartographic`对象，并在构造函数中提供了经度、纬度和高度三个值。我们使用`Cesium.Math.toRadians()`方法将经度和纬度值转换为弧度，以便在`Cartographic`对象中使用。

地理坐标系在Cesium中用于表示地球表面的位置，例如地形、建筑物和其他地球上的特征。它通常与笛卡尔坐标系一起使用，以便将地球上的位置转换为三维笛卡尔坐标系中的点。

## 地理坐标转换为笛卡尔坐标代码

在Cesium中，可以使用`Cartographic`和`Ellipsoid`对象将地理坐标转换为笛卡尔坐标。`Cartographic`对象包含经度、纬度和高度值，`Ellipsoid`对象表示地球的形状和大小。

以下是将地理坐标转换为笛卡尔坐标的代码示例：

```
javascriptCopy code// 定义地理坐标
var longitude = -75.59777;
var latitude = 40.03883;
var height = 0;

// 创建Cartographic对象
var cartographic = Cesium.Cartographic.fromDegrees(longitude, latitude, height);

// 获取椭球体对象
var ellipsoid = viewer.scene.globe.ellipsoid;

// 将Cartographic对象转换为笛卡尔坐标
var cartesian = ellipsoid.cartographicToCartesian(cartographic);
```

在这个示例中，我们首先定义了地理坐标的经度、纬度和高度值。然后，使用`Cesium.Cartographic.fromDegrees()`方法创建一个`Cartographic`对象。接着，我们获取当前场景中的椭球体对象，并使用`ellipsoid.cartographicToCartesian()`方法将`Cartographic`对象转换为笛卡尔坐标。最终，我们得到了该地理坐标的笛卡尔坐标值。

## 笛卡尔坐标转换为地理坐标

在Cesium中，可以使用`Cartographic`和`Ellipsoid`对象将笛卡尔坐标转换为地理坐标。`Cartographic`对象包含经度、纬度和高度值，`Ellipsoid`对象表示地球的形状和大小。

以下是将笛卡尔坐标转换为地理坐标的代码示例：

```
javascriptCopy code// 定义笛卡尔坐标
var cartesian = new Cesium.Cartesian3(1622363.762473216, -5053963.416943614, 3575778.7116152966);

// 获取椭球体对象
var ellipsoid = viewer.scene.globe.ellipsoid;

// 将笛卡尔坐标转换为Cartographic对象
var cartographic = ellipsoid.cartesianToCartographic(cartesian);

// 获取经度、纬度和高度值
var longitude = Cesium.Math.toDegrees(cartographic.longitude);
var latitude = Cesium.Math.toDegrees(cartographic.latitude);
var height = cartographic.height;
```

在这个示例中，我们首先定义了一个笛卡尔坐标。然后，使用`viewer.scene.globe.ellipsoid`获取当前场景中的椭球体对象。接着，我们使用`ellipsoid.cartesianToCartographic()`方法将笛卡尔坐标转换为`Cartographic`对象。最后，我们通过`Cesium.Math.toDegrees()`方法将经度和纬度值转换为度数，从`Cartographic`对象中获取高度值，得到了该笛卡尔坐标的地理坐标值。