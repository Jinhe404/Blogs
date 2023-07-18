# Cesium中material 材质

[TOC]

Cesium中的Material（材质）用于定义3D对象的外观，包括颜色、透明度、纹理、着色器等。Material是一种特殊类型的Globe或Primitive属性，可以应用于Primitive（图元）对象、3D Tiles中的Batch、GeometryInstance以及其他几乎所有具有几何形状的对象。Cesium提供了多种类型的材质，以满足不同场景的需求，例如ColorMaterial、ImageMaterial、PolylineArrowMaterial等。

下面是Material类中的主要属性和方法：

### 属性

- `materialType`：返回Material的类型，例如ColorMaterial、ImageMaterial等。
- `uniforms`：返回Material的Uniform属性。
- `vertexShaderSource`：返回Material的Vertex Shader代码。
- `fragmentShaderSource`：返回Material的Fragment Shader代码。
- `translucent`：返回Material是否为半透明材质。
- `closed`：返回Material是否为封闭材质。
- `fabric`：返回Material的Canvas 2D绘图上下文。

### 方法

- `isTranslucent()`：返回Material是否为半透明材质。
- `isClosed()`：返回Material是否为封闭材质。
- `isConstant()`：返回Material是否为常量材质。
- `isDestroyed()`：返回Material是否已销毁。
- `destroy()`：销毁Material对象。
- `getShaderProgram(context, sceneMode, closed)`：获取Material对象的Shader程序。
- `isTranslucent()`：返回Material是否为半透明材质。
- `isClosed()`：返回Material是否为封闭材质。
- `isConstant()`：返回Material是否为常量材质。
- `isDestroyed()`：返回Material是否已销毁。
- `destroy()`：销毁Material对象。
- `getShaderProgram(context, sceneMode, closed)`：获取Material对象的Shader程序。
- `getShaderProgram()`：获取Material对象的Shader程序。
- `isTranslucent()`：返回Material是否为半透明材质。
- `isClosed()`：返回Material是否为封闭材质。
- `isConstant()`：返回Material是否为常量材质。
- `isDestroyed()`：返回Material是否已销毁。
- `destroy()`：销毁Material对象。
- `getShaderProgram(context, sceneMode, closed)`：获取Material对象的Shader程序。

Material类还提供了许多其他的属性和方法，可根据实际需求进行查阅和使用。在使用Material时，需要根据不同的场景和需求选择合适的类型，并设置相关属性和方法，以达到期望的效果。