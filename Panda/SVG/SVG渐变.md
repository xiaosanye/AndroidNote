## SVG渐变

SVG 渐变必须在 <defs> 标签中进行定义。

>渐变是一种从一种颜色到另一种颜色的平滑过渡。另外，可以把多个颜色的过渡应用到同一个元素上。


### SVG 线性渐变

>`<linearGradient>` 可用来定义 SVG 的线性渐变。

>`<linearGradient>` 标签必须嵌套在 `<defs>` 的内部。`<defs>` 标签是 definitions 的缩写，它可对诸如渐变之类的特殊元素进行定义。

>线性渐变可被定义为`水平`、`垂直`或`角形`的渐变：


>+ 当 y1 和 y2 相等，而 x1 和 x2 不同时，可创建水平渐变
>+ 当 x1 和 x2 相等，而 y1 和 y2 不同时，可创建垂直渐变
>+ 当 x1 和 x2 不同，且 y1 和 y2 不同时，可创建角形渐变


```xml
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN"
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">

<defs>
<linearGradient id="orange_red" x1="0%" y1="0%" x2="100%" y2="0%">
<stop offset="0%" style="stop-color:rgb(255,255,0);
stop-opacity:1"/>
<stop offset="100%" style="stop-color:rgb(255,0,0);
stop-opacity:1"/>
</linearGradient>
</defs>

<ellipse cx="200" cy="190" rx="85" ry="55"
style="fill:url(#orange_red)"/>

</svg>
```

>**代码解释**：

>+ `<linearGradient>` 标签的 id 属性可为渐变定义一个唯一的名称
>+ fill:url(#orange_red) 属性把 ellipse 元素链接到此渐变
>+ `<linearGradient>` 标签的 x1、x2、y1、y2 属性可定义渐变的开始和结束位置
>+ 渐变的颜色范围可由两种或多种颜色组成。每种颜色通过一个 `<stop>` 标签来规定。offset 属性用来定义渐变的开始和结束位置。



### SVG 放射性渐变

> <radialGradient> 用来定义放射性渐变。

> <radialGradient> 标签必须嵌套在 <defs> 中。<defs> 标签是 definitions 的缩写，它允许对诸如渐变等特殊元素进行定义。

```java
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN"
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">

<defs>
<radialGradient id="grey_blue" cx="50%" cy="50%" r="50%"
fx="50%" fy="50%">
<stop offset="0%" style="stop-color:rgb(200,200,200);
stop-opacity:0"/>
<stop offset="100%" style="stop-color:rgb(0,0,255);
stop-opacity:1"/>
</radialGradient>
</defs>

<ellipse cx="230" cy="200" rx="110" ry="100"
style="fill:url(#grey_blue)"/>

</svg>
```

>**代码解释**：
>+ `<radialGradient> `标签的 id 属性可为渐变定义一个唯一的名称.
>+ fill:url(#grey_blue) 属性把 ellipse 元素链接到此渐变.
>+ cx、cy 和 r 属性定义外圈，
>+ 而 fx 和 fy 定义内圈 渐变的颜色范围可由两种或多种颜色组成。
>+ 每种颜色通过一个 `<stop> `标签来规定。offset 属性用来定义渐变的开始和结束位置。



#
