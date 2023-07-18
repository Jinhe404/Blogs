## Cesium中Math介绍

Cesium中包含了许多数学计算方法，用于处理地球表面的坐标转换、距离计算、矩阵变换等操作。下面是一些常用的Cesium数学模块和方法的介绍：

`Cesium.Math`模块：这是Cesium中最基本的数学模块，包含了许多常用的数学计算方法，例如：

- `Cesium.Math.toRadians(degrees)`：将角度转换为弧度。
- `Cesium.Math.toDegrees(radians)`：将弧度转换为角度。
- `Cesium.Math.clamp(value, min, max)`：将一个值限制在指定范围内。
- `Cesium.Math.lerp(start, end, t)`：计算在两个值之间插值的值。
- `Cesium.Math.nextPowerOfTwo(n)`：计算大于或等于给定值的下一个2的幂。
- `Cesium.Math.randomBetween(min, max)`：生成一个指定范围内的随机数。

`Cesium.Ellipsoid`模块：这个模块包含了地球椭球体的定义和相关的计算方法，例如：

- `Cesium.Ellipsoid.WGS84`：表示WGS84标准椭球体。
- `Cesium.Ellipsoid.cartesianToCartographic(cartesian)`：将笛卡尔坐标系中的点转换为地理坐标系中的点。
- `Cesium.Ellipsoid.cartographicToCartesian(cartographic)`：将地理坐标系中的点转换为笛卡尔坐标系中的点。
- `Cesium.Ellipsoid.scaleToGeodeticSurface(cartesian)`：将笛卡尔坐标系中的点投影到地球表面。
- `Cesium.Ellipsoid.geodeticSurfaceNormal(cartesian)`：计算给定点的地球表面法线向量。

`Cesium.Cartesian3`模块：这个模块表示笛卡尔坐标系中的点，包含了许多与点相关的计算方法，例如：

- `Cesium.Cartesian3.fromDegrees(longitude, latitude, height, ellipsoid)`：根据经纬度和高度创建一个点。
- `Cesium.Cartesian3.distance(point1, point2)`：计算两个点之间的距离。
- `Cesium.Cartesian3.normalize(vector, result)`：将向量归一化为单位向量。
- `Cesium.Cartesian3.cross(left, right, result)`：计算两个向量的叉积。
- `Cesium.Cartesian3.dot(left, right)`：计算两个向量的点积。

`Cesium.Matrix4`模块：这个模块表示4x4矩阵，包含了许多与矩阵相关的计算方法，例如：

- `Cesium.Matrix4.IDENTITY`：表示4x4单位矩阵。
- `Cesium.Matrix4.fromArray(array, startingIndex, result)`：从数组中创建一个矩阵。
  - `array`：包含矩阵元素的数组。
  - `startingIndex`：数组中矩阵元素的起始索引。
  - `result`：可选参数，输出结果的矩阵对象。
- `Cesium.Matrix4.toArray(matrix, result)`：将矩阵的元素存储到一个数组中。
  - `matrix`：要转换的矩阵对象。
  - `result`：可选参数，输出结果的数组对象。
- `Cesium.Matrix4.multiply(left, right, result)`：计算两个矩阵的乘积。
  - `left`：左边的矩阵对象。
  - `right`：右边的矩阵对象。
  - `result`：可选参数，输出结果的矩阵对象。
- `Cesium.Matrix4.multiplyTransformation(left, right, result)`：计算两个变换矩阵的乘积。
  - `left`：左边的矩阵对象。
  - `right`：右边的矩阵对象。
  - `result`：可选参数，输出结果的矩阵对象。
- `Cesium.Matrix4.multiplyByTranslation(matrix, translation, result)`：将矩阵和一个平移向量相乘。
  - `matrix`：要进行乘法计算的矩阵对象。
  - `translation`：要加入到矩阵中的平移向量。
  - `result`：可选参数，输出结果的矩阵对象。
- `Cesium.Matrix4.multiplyByUniformScale(matrix, scale, result)`：将矩阵和一个统一缩放因子相乘。
  - `matrix`：要进行乘法计算的矩阵对象。
  - `scale`：缩放因子。
  - `result`：可选参数，输出结果的矩阵对象。
- `Cesium.Matrix4.inverse(matrix, result)`：计算矩阵的逆矩阵。
  - `matrix`：要求逆矩阵的矩阵对象。
  - `result`：可选参数，输出结果的矩阵对象。
- `Cesium.Matrix4.transpose(matrix, result)`：计算矩阵的转置矩阵。
  - `matrix`：要求转置矩阵的矩阵对象。
  - `result`：可选参数，输出结果的矩阵对象。

​	`Cesium.Matrix4.extractRotation(matrix, result)`：从矩阵中提取出旋转部分的矩阵。

- `matrix`：要从中提取旋转矩阵的矩阵对象。
- `result`：可选参数，输出结果的矩阵对象。如果没有提供，则会创建一个新的矩阵对象。

1. `Cesium.Matrix4.multiplyByPoint(matrix, cartesian, result)`：将一个点与矩阵相乘。
   - `matrix`：要进行乘法计算的矩阵对象。
   - `cartesian`：要乘以矩阵的点的笛卡尔坐标对象。
   - `result`：可选参数，输出结果的笛卡尔坐标对象。
2. `Cesium.Matrix4.multiplyByVector(matrix, vector, result)`：将一个向量与矩阵相乘。
   - `matrix`：要进行乘法计算的矩阵对象。
   - `vector`：要乘以矩阵的向量对象。
   - `result`：可选参数，输出结果的向量对象。
3. `Cesium.Matrix4.computePerspectiveFieldOfView(fovY, aspectRatio, near, far, result)`：计算透视投影矩阵。
   - `fovY`：视场角，以弧度表示。
   - `aspectRatio`：视口宽高比。
   - `near`：近平面距离。
   - `far`：远平面距离。
   - `result`：可选参数，输出结果的矩阵对象。
4. `Cesium.Matrix4.computeOrthographicOffCenter(left, right, bottom, top, near, far, result)`：计算正交投影矩阵。
   - `left`：左平面距离。
   - `right`：右平面距离。
   - `bottom`：底部平面距离。
   - `top`：顶部平面距离。
   - `near`：近平面距离。
   - `far`：远平面距离。
   - `result`：可选参数，输出结果的矩阵对象。

这些方法和属性是Matrix4模块中的一部分，可以帮助开发者对矩阵进行计算和转换。





scripts/shrec/datasets/shrec_16/dog1/train