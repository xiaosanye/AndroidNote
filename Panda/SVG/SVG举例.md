[SVG](http://www.w3school.com.cn/svg/)
## 一、SVG举例

```xml
<?xml version="1.0" standalone="no"?>

<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN"
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">

<circle cx="100" cy="50" r="40" stroke="black"
stroke-width="2" fill="red"/>

</svg>

```

> * 第一行包含了 XML 声明。请注意 `standalone` 属性！该属性规定此 SVG 文件是否是“独立的”，或含有对外部文件的引用。
> * standalone="no" 意味着 SVG 文档会引用一个外部文件 - 在这里，是 DTD 文件。
> * 第二和第三行引用了这个外部的 SVG DTD。该 DTD 位于 “http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd”。该 DTD 位于 W3C，含有所有允许的 SVG 元素。


SVG 代码以`<svg>`元素开始，包括开启标签`<svg>`和关闭标签`</svg>`。这是根元素。width 和 height 属性可设置此 SVG 文档的宽度和高度。`version` 属性可定义所使用的 SVG 版本，`xmlns` 属性可定义 SVG 命名空间。

+ <circle> 用来创建一个圆。
+ cx 和 cy 属性定义圆中心的 x 和 y 坐标。如果忽略这两个属性，那么圆点会被设置为 (0, 0)。
+ r 属性定义圆的半径。
+ stroke 和 stroke-width 属性控制如何显示形状的轮廓。我们把圆的轮廓设置为 2px 宽，黑边框。
+ fill 属性设置形状内的颜色。我们把填充颜色设置为红色。



## 二、SVG形状

SVG 有一些预定义的形状元素，可被开发者使用和操作。

+ 矩形 <rect>
+ 圆形 <circle>
+ 椭圆 <ellipse>
+ 线 <line>
+ 折线 <polyline>
+ 多边形 <polygon>
+ 路径 <path>

### `<Rect>`

```xml
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN"
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">

<rect width="300" height="100"
style="fill:rgb(0,0,255);stroke-width:1;
stroke:rgb(0,0,0)"/>

</svg>
```

+ rect 元素的 width 和 height 属性可定义矩形的高度和宽度
+ style 属性用来定义 CSS 属性
+ CSS 的 fill 属性定义矩形的填充颜色（rgb 值、颜色名或者十六进制值）
+ CSS 的 stroke-width 属性定义矩形边框的宽度
+ CSS 的 stroke 属性定义矩形边框的颜色


+ x 属性定义矩形的左侧位置（例如，x="0" 定义矩形到浏览器窗口左侧的距离是 0px）
+ y 属性定义矩形的顶端位置（例如，y="0" 定义矩形到浏览器窗口顶端的距离是 0px）
+ CSS 的 fill-opacity 属性定义填充颜色透明度（合法的范围是：0 - 1）
+ CSS 的 stroke-opacity 属性定义笔触颜色的透明度（合法的范围是：0 - 1）

+ CSS 的 opacity 属性定义整个元素的透明值（合法的范围是：0 - 1）
+ rx 和 ry 属性可使矩形产生圆角。


#### 其他标签比较简单，这里不做说明了；下面讲解一个最重要的SVG形状：`SVG路径`

### SVG路径 `<path>`

<path> 标签用来定义路径。

>下面的命令可用于路径数据：
> + M = moveto
> + L = lineto
> + H = horizontal lineto
> + V = vertical lineto
> + C = curveto
> + S = smooth curveto
> + Q = quadratic Belzier curve
> + T = smooth quadratic Belzier curveto
> + A = elliptical Arc
> + Z = closepath

>注释：以上所有命令均允许小写字母。大写表示绝对定位，小写表示相对定位。
















#
