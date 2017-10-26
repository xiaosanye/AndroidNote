[Android View框架的draw机制](http://www.cnblogs.com/xyhuangjinfu/p/5435277.html)

### 带着问题来思考整个draw过程。

#### 1、系统为什么要有draw过程？

View框架在经过了`measure`过程和`layout`过程之后，就已经确定了每一个View的`尺寸`和`位置`。那么接下来，也是一个重要的过程，就是`draw`过程，draw过程是用来`绘制View`的过程，它的作用就是**使用`graphic`框架提供的各种绘制功能**，绘制出当前View想要的样子。


#### 2、draw过程都干了点什么事？

View框架中，`draw`过程主要是绘制`View的外观`。`ViewGroup`除了负责绘制自己之外，还需要负责绘制所有的`子View`。而不含子View的View对象，就负责绘制自己就可以了。

draw过程的主要流程如下：

+ 1、绘制 `backgroud`（drawBackground）     
+ 2、如果需要的话，保存`canvas`的`layer`，来准备`fading`（不是必要的步骤）
+ 3、绘制view的`content`（`onDraw方法`）
+ 4、绘制`children`（`dispatchDraw方法`）
+ 5、如果需要的话，绘制`fading edges`，然后`还原layer`（不是必要的步骤）
+ 6、`绘制装饰器`、比如`scrollBar`（`onDrawForeground`）


### 源代码分析






















#
