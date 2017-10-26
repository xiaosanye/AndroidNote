






#


paint的基本绘制方法已经在前面的基本图形绘制中讲解了，这里做的是进阶讲解，讲解paint的一些进阶方法。例如：`setStrokeCap`，`setStrokeJoin`，`setPathEffect`等。

#### 网址
+ [paint进阶 ](http://blog.csdn.net/cquwentao/article/details/51374994)

####1.setStrokeCap(Paint.Cap cap)
cap是帽子的意思，这里的意思是设置线帽子，什么是线帽呢，就是一个线段结束后的额外部分。

**他们传入的参数分别是**：
>+ BUTT    (0),//无线帽
>+ ROUND   (1),//圆形线帽
>+ SQUARE  (2);//方形线帽

```java
Paint paint = new Paint();
paint.setColor(Color.BLUE);
paint.setStrokeWidth(50);

paint.setStrokeCap(Paint.Cap.BUTT);
canvas.drawLine(100, 100, 800, 100, paint);

paint.setStrokeCap(Paint.Cap.ROUND);
canvas.drawLine(100, 300, 800, 300, paint);

paint.setStrokeCap(Paint.Cap.SQUARE);
canvas.drawLine(100, 500, 800, 500, paint);
```

#### 2.setStrokeJoin(Paint.Join join)
从join处可以知道，这里设置的是线段的连接处的样式，那么Join有哪些呢
**他们传入的参数分别是**：
>+ MITER   (0),//锐角连接
>+ ROUND   (1),//圆弧连接
>+ BEVEL   (2);//斜接（把锐角替换成斜边）


```java
Paint paint = new Paint();
paint.setStyle(Paint.Style.STROKE);
paint.setColor(Color.BLUE);
paint.setStrokeWidth(50);

Path path = new Path();

path.moveTo(100, 100);
path.rLineTo(800, 0);
path.rLineTo(0, 200);
paint.setStrokeJoin(Paint.Join.MITER);
canvas.drawPath(path, paint);

paint.setStrokeJoin(Paint.Join.ROUND);
path.moveTo(100, 500);
path.rLineTo(800, 0);
path.rLineTo(0, 200);
canvas.drawPath(path, paint);

paint.setStrokeJoin(Paint.Join.BEVEL);
path.moveTo(100, 1000);
path.rLineTo(800, 0);
path.rLineTo(0, 200);
canvas.drawPath(path, paint);
```

####3. setPathEffect(PathEffect effect)
effect代表效果，这里明显是要设置路径的效果。





#
