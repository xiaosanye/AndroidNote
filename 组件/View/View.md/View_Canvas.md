Android中使用`图形处理引擎`，`2D部分是android SDK内部自己提供`，`3D部分是用Open GL ES 1.0`。
`大部分2D使用的api`都在`android.graphics`和`android.graphics.drawable`包中。他们提供了图形处理相关的： `Canvas、ColorFilter、Point(点)和RetcF(矩形)`等，还有一些动画相关的：`AnimationDrawable`、 `BitmapDrawable`和`TransitionDrawable`等。以图形处理来说，我们最常用到的就是在一个View上画一些图片、形状或者自定义的文本内容，这里我们都是使用Canvas来实现的。你可以获取View中的Canvas对象，绘制一些自定义形状，然后调用`View. invalidate`方法让View重新刷新，然后绘制一个新的形状，这样达到2D动画效果。下面我们就主要来了解下Canvas的使用方法。



canvas提供的绘制图形的方法都是以draw开头的，我们可以查看api:
