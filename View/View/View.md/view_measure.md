Android中View框架的工作机制中，主要有三个过程：

+ 1、View树的测量（measure）Android View框架的measure机制

+ 2、View树的布局（layout） Android View框架的layout机制

+ 3、View树的绘制（draw）Android View框架的draw机制

View框架的工作流程为：测量每个View大小（measure）-->把每个View放置到相应的位置（layout）-->绘制每个View（draw）。


### measure过程 [http://www.cnblogs.com/xyhuangjinfu/p/5435201.html]
#### 1.系统为什么要有measure过程？

 开发人员在绘制UI的时候，基本都是通过XML布局文件的方式来配置UI，而每个View必须要设置的两个群属性就是layout_width和layout_height，这两个属性代表着当前View的尺寸。

 所以这两个属性的值是必须要指定的，这两个属性的取值只能为三种类型：

>+ 1、固定的大小，比如100dp。
>+ 2、刚好包裹其中的内容，wrap_content。
>+ 3、想要和父布局一样大，match_parent / fill_parent。

由于Android希望提供一个更优雅的GUI框架，所以提供了自适应的尺寸，也就是 wrap_content 和 match_parent 。

试想一下，那如果这些属性只允许设置固定的大小，那么每个View的尺寸在绘制的时候就已经确定了，所以可能都不需要measure过程。但是由于需要满足自适应尺寸的机制，所以需要一个measure过程。


#### 2、measure过程都干了点什么事？

由于上面提到的自适应尺寸的机制，所以在用自适应尺寸来定义View大小的时候，View的真实尺寸还不能确定。但是View尺寸最终需要映射到屏幕上的像素大小，所以measure过程就是干这件事，把各种尺寸值，经过计算，得到具体的像素值。measure过程会遍历整棵View树，然后依次测量每个View真实的尺寸。具体是每个ViewGroup会向它内部的每个子View发送measure命令，然后由具体子View的`onMeasure()`来测量自己的尺寸。最后测量的结果保存在View的`mMeasuredWidth`和`mMeasuredHeight`中，保存的数据单位是像素。


#### 4.那么ViewGroup是如何向子View传递限制信息的？

谈到传递限制信息，那就是MeasureSpec类了，该类贯穿于整个measure过程，用来传递父布局对子View尺寸测量的约束信息。简单来说，该类就保存两类数据。

>+ 1、子View当前所在父布局的具体尺寸。
>+ 2、父布局对子View的限制类型。

那么限制类型又分为三种类型：

1、`UNSPECIFIED`，不限定。意思就是，子View想要多大，我就可以给你多大，你放心大胆的measure吧，不用管其他的。也不用管我传递给你的尺寸值。（其实Android高版本中推荐，只要是这个模式，尺寸设置为0）

2、`EXACTLY`，精确的。意思就是，根据我当前的状况，结合你指定的尺寸参数来考虑，你就应该是这个尺寸，具体大小在MeasureSpec的尺寸属性中，自己去查看吧，你也不要管你的content有多大了，就用这个尺寸吧。

3、`AT_MOST`，最多的。意思就是，根据我当前的情况，结合你指定的尺寸参数来考虑，在不超过我给你限定的尺寸的前提下，你测量一个恰好能包裹你内容的尺寸就可以了。



### measure 源代码分析
在View的源代码中，提取到了下面一些关于measure过程的信息。

我们知道，**整棵View树**的`根节点`是`DecorView`，它是一个FrameLayout，所以它是一个ViewGroup，所以**整棵View树的测量是从一个ViewGroup对象的measure方法开始的**。


### View中相关方法：

##### measure

**开始测量一个View有多大，parent会在参数中提供约束信息，实际的测量工作是在onMeasure()中进行的，该方法会调用`onMeasure()`方法，所以只有onMeasure能被也必须要被override。**

```Java
public final void measure(int widthMeasureSpec, int heightMeasureSpec);
```

**父布局会在自己的onMeasure方法中，调用child.measure** ，这就把measure过程转移到了子View中。

##### onMeasure
```java
/** 具体测量过程，测量view和它的内容，来决定测量的宽高（mMeasuredWidth  mMeasuredHeight ）。该方法中必须要调用setMeasuredDimension(int, int)来保存该view测量的宽高。 */
protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec);
```

子View会在该方法中，根据父布局给出的限制信息，和自己的content大小，来合理的测量自己的尺寸。

##### setMeasuredDimension

```java
/** 保存测量结果 */
protected final void setMeasuredDimension(int measuredWidth, int measuredHeight);
```

当View测量结束后，把测量结果保存起来，具体保存在`mMeasuredWidth`和`mMeasuredHeight`中。





















### ViewGroup中相关方法：





#
