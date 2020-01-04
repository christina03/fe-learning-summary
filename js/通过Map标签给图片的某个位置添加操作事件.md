# 通过Map标签给图片的某个位置添加操作事件

示例：
```
<img src="./img.png" usemap="#imgMap">
<map name="imgMap" id="imgMap">
    <area shape="rect|circle|poly" coords="#" href="url">
</map>
```
> img 元素中的 "usemap" 属性引用 map 元素中的 "id" 或 "name" 属性（根据浏览器），所以我们同时向 map 元素添加了 "id" 和 "name" 属性。

所有坐标都是相对于图片左上角的位置的。

其中coords相对于不同shape值的参数：
```
<area shape="rect" coords="x1,y1,x2,y2" href="url">
//(x1,y1)=Upper Left,(x2,y2)=Lower Right表示矩形左上或者右下的坐标。
```

```
<area shape="circle" coords="x,y,r" href="url">
//(x,y)为圆心坐标，以及半径
```
```
<area shape="poly" coords="x1,y1,x2,y2,x3,y3..." href="url">
//表示多边形，所有顶点的坐标
```
> 注释：如果某个 area 标签中的坐标和其他区域发生了重叠，会优先采用最先出现的 area 标签。浏览器会忽略超过图像边界范围之外的坐标。
