- [简谈百度坐标反转至WGS84的三种思路](https://www.cnblogs.com/naaoveGIS/p/6245206.html)

# 1.背景

基于百度地图进行数据展示是目前项目中常见场景，但是因为百度地图是基于BD09坐标系的，GPS坐标（WGS84）或者其他常见的标准坐标是无法准确在地图上进行展示的，但是互联网在线情况下，百度提供了将WGS84经纬度转换成百度经纬度坐标的API，这里不再对其进行研究（离线情况下也有专门方法解决）。这里，我们探讨，如何将在百度上获取的百度坐标数据反转成WGS84坐标。

目前有三种通用方法来解决此问题，分别是算法逼近、误差逼近和格网逼近方法。

# 2.算法逼近方法

百度地图坐标系的背景为首先使用国测局制定的GCJ-02,对地理位置进行首次加密，然后再利用其自创的BD-09进行二次加密措施。所以基于算法的逼近，也是进行这样的反解步骤：首先将BD09坐标转换成GCJ02坐标，然后再将GCJ02坐标反算成WGS84坐标。

以下为基于算法反解的详细代码：

 ![img](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/656746-20170103155210644-1482989726.png)

![img](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/656746-20170103155226566-1295329133.png)

# 3.误差逼近方法

A点为百度坐标点，假设此时我们将其看作一个WGS84坐标点A1，利用百度提供的在线WGS84坐标转换成百度经纬度坐标系的API，可得到A1’百度坐标，此时A1’与A1之间的坐标差为L。假设百度地图在2L范围的坐标其反转误差大致相同，则我们将真实的百度坐标A做L标准差的线性加减得到A’，最后A’则为百度坐标A反转所得的WGS84坐标。

​                                      ![img](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/656746-20170103155243362-21191489.png)

详细代码如下：

 ![img](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/656746-20170103155257706-581617249.png)

# 4.网格逼近算法

该方法我在之前的博客中详细介绍过：http://www.cnblogs.com/naaoveGIS/p/5342177.html。

其流程大致为：

a.将指定范围以100M（或更小）划分成若干格网。

b.建立各个格网的四角坐标中WGS84坐标与百度坐标之间的对应关系。

c.判断待转换的百度点落在哪个网格中，获取该格网的四角坐标对应的WGS84坐标。

按照该点在格网的权重算出其WGS84坐标后转换完毕。

​                          ![img](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/656746-20170103155308050-2094522980.png)

# 5.误差对比

此三种方法皆为逼近，误差是无法避免的，对这三种算法的误差做了初步的统计，如下：

 ![img](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/656746-20170103155321597-1715310601.png)

首先对比了误差逼近方法和算法逼近方法，可见他们的平均误差均在10M上下，其中算法逼近方法比误差逼近方法稍微精度高一些。

而网格方法是一种误差很稳定的方法，以100M的网格划分为例，其误差是厘米级的，具体如下：

​                           ![img](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/656746-20170103155328941-1262771857.png)

# 6.总结

当精度要求不高，并且需要快速部署情况下，首推算法逼近方法。当需要高精度方法时，还是需要使用网格逼近方法。