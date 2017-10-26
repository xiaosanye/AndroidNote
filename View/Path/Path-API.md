## 一.Path常用方法表

>去除了在API21(即安卓版本5.0)以上才添加的方法

|作用|相关方法|备注|
|----|----|-----|
|移动起点|	moveTo|	移动下一次操作的起点位置
|设置终点	|setLastPoint	|重置当前path中最后一个点位置，如果在绘制之前调用，效果和moveTo相同
|连接直线	|lineTo	|添加上一个点到当前点之间的直线到Path
|闭合路径	|close	|连接第一个点连接到最后一个点，形成一个闭合区域
|添加内容	|addRect, addRoundRect, addOval, addCircle, addPath, addArc, arcTo|	添加(矩形， 圆角矩形， 椭圆， 圆， 路径， 圆弧) 到当前Path (注意addArc和arcTo的区别)
|是否为空	|isEmpty	|判断Path是否为空
|是否为矩形	|isRect	|判断path是否是一个矩形
|替换路径	|set|	用新的路径替换到当前路径所有内容
|偏移路径	|offset	|对当前路径之前的操作进行偏移(不会影响之后的操作)
|贝塞尔曲线	|quadTo, cubicTo|	分别为二次和三次贝塞尔曲线的方法
|rXxx方法	|rMoveTo, rLineTo, rQuadTo, rCubicTo	|不带r的方法是基于原点的坐标系(偏移量)，rXxx方法是基于当前点坐标系(偏移量)
|填充模式	|setFillType, getFillType, isInverseFillType, toggleInverseFillType	|设置,获取,判断和切换填充模式
|提示方法	|incReserve	|提示Path还有多少个点等待加入(这个方法貌似会让Path优化存储结构)
|布尔操作(API19)	|op	|对两个Path进行布尔运算(即取交集、并集等操作)
|计算边界|	computeBounds	|计算Path的边界
|重置路径	|reset, rewind|	清除Path中的内容(reset相当于重置到new Path阶段，rewind会保留Path的数据结构)
|矩阵操作	|transform	|矩阵变换


>API21 以后的方法
