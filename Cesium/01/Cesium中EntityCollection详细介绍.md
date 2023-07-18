

# Cesium中EntityCollection及EntityCluster

[TOC]

## EntityCollection

### EntityCollection属性

在Cesium中，EntityCollection是一组Entity对象的集合，一个Entity对象通常代表三维场景中的一个可视化元素，例如模型、标注、图像等。EntityCollection是Entity的容器，可以方便地对其中的多个Entity对象进行操作，例如添加、删除、获取、更新等。

EntityCollection继承自Cesium的Event类，因此可以使用事件监听机制来处理EntityCollection中的操作。常用的事件包括entityAdded、entityRemoved、collectionChanged等。

使用EntityCollection可以轻松地在三维场景中添加多个Entity对象，例如：

```
javascriptCopy codevar viewer = new Cesium.Viewer('cesiumContainer');
var entities = viewer.entities;
var entityCollection = new Cesium.EntityCollection();
entities.add(entityCollection);

var entity1 = new Cesium.Entity({
    name : 'Entity 1',
    position : Cesium.Cartesian3.fromDegrees(-75.59777, 40.03883),
    billboard : {
        image : 'path/to/image.png'
    }
});

var entity2 = new Cesium.Entity({
    name : 'Entity 2',
    position : Cesium.Cartesian3.fromDegrees(-75.59777, 40.03883),
    model : {
        uri : 'path/to/model.gltf'
    }
});

entityCollection.add(entity1);
entityCollection.add(entity2);
```

在上述代码中，我们首先创建了一个EntityCollection对象，并将其添加到Viewer的entities中，然后创建了两个Entity对象，并将其添加到EntityCollection中。这样，我们就可以方便地在场景中同时展示多个元素。

除了添加Entity对象之外，EntityCollection还支持其他常用操作，例如：

- remove(entity): 从EntityCollection中删除指定的Entity对象。
- removeAll(): 从EntityCollection中删除所有Entity对象。
- contains(entity): 判断EntityCollection中是否包含指定的Entity对象。
- get(index): 获取EntityCollection中指定索引处的Entity对象。

总之，EntityCollection为我们在Cesium中管理多个Entity对象提供了便利，可以更好地组织和展示三维场景中的元素。

### EntityCollection 方法

在Cesium中，EntityCollection是一个对象集合，可以存储和管理一组实体对象，例如点、线、面等。EntityCollection允许用户添加、删除、更新和查询这些实体对象。以下是EntityCollection的一些常见方法：

1. add(entity): 向EntityCollection中添加实体对象。
2. remove(entity): 从EntityCollection中移除实体对象。
3. removeAll(): 移除所有实体对象。
4. get(index): 返回指定索引处的实体对象。
5. getLength(): 返回EntityCollection中实体对象的数量。
6. getOrCreateEntity(id): 返回指定ID的实体对象，如果不存在则创建一个新的实体对象并返回。
7. getById(id): 返回指定ID的实体对象，如果不存在则返回undefined。
8. contains(entity): 判断EntityCollection中是否包含指定的实体对象。
9. raiseToTop(entity): 将指定的实体对象移动到EntityCollection的顶部，使其显示在其他实体对象之上。

EntityCollection还可以监听实体对象的添加、删除、更新等事件，以便及时处理相关操作。例如，可以使用以下方法监听添加事件：

1. addEventListener(eventType, listener): 监听指定类型的事件。
2. removeEventListener(eventType, listener): 取消监听指定类型的事件。

在Cesium中，EntityCollection常常用于管理场景中的实体对象，例如添加、移除、更新等操作都可以通过EntityCollection进行管理和控制。同时，EntityCollection还提供了许多实用的方法和事件，使用户能够轻松地管理和操作实体对象。

## EntityCluster

EntityCluster是Cesium中的实体聚合类，用于对多个实体进行聚合和分组，以便更好地管理和控制它们。EntityCluster可以帮助您组织和优化您的场景，并为用户提供更好的交互体验。

EntityCluster类有以下属性、方法、事件和实例：

### 属性

- **clusterBillboards**：Boolean类型，指示是否聚合图标（billboards）。
- **clusterLabels**：Boolean类型，指示是否聚合标签（labels）。
- **clusterPoints**：Boolean类型，指示是否聚合点（points）。
- **enabled**：Boolean类型，指示实体聚合是否启用。

### 方法

- **destroy()**：销毁实体聚合对象，释放相关资源。
- **removeAll()**：从聚合对象中移除所有实体。
- **removeChild(child)**：从聚合对象中移除指定的实体。
- **update(clusterRadius, minimumClusterSize)**：更新聚合对象的属性。`clusterRadius`指定实体之间的距离，如果它们比这个距离更接近，则会被聚合。`minimumClusterSize`指定要聚合的实体的最小数量。

### 事件

- **clusterEvent**：每当聚合对象发生更改时触发，包括添加或删除实体。

### 实例

以下是创建EntityCluster的示例代码：

```
javascriptCopy codevar entityCluster = new Cesium.EntityCluster({
    clusterRadius: 80,
    minimumClusterSize: 3,
    enabled: true,
    clusterBillboards: true,
    clusterLabels: true,
    clusterPoints: true
});
```

这将创建一个实体聚合对象，将实体距离设置为80，并指定聚合实体的最小数量为3。此外，它还启用了实体聚合，并指定了聚合图标、标签和点。