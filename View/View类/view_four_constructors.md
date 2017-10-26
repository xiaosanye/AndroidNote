### Android View类 四个构造函数详解

+ [Android View 四个构造函数详解 ](http://blog.csdn.net/zhao123h/article/details/52210732)


#### 先从android源码中把四个构造函数拉出来看看
1. 第一个构造函数
```java

/**
 * Simple constructor to use when creating a view from code.
 *
 * @param context The Context the view is running in, through which it can
 *        access the current theme, resources, etc.
 */  
public View(Context context)

```

2. 第二个构造函数
```java
/**
    * Constructor that is called when inflating a view from XML. This is called
    * when a view is being constructed from an XML file, supplying attributes
    * that were specified in the XML file. This version uses a default style of
    * 0, so the only attribute values applied are those in the Context's Theme
    * and the given AttributeSet.
    *
    * <p>
    * The method onFinishInflate() will be called after all children have been
    * added.
    *
    * @param context The Context the view is running in, through which it can
    *        access the current theme, resources, etc.
    * @param attrs The attributes of the XML tag that is inflating the view.
    * @see #View(Context, AttributeSet, int)
    */  
   public View(Context context, @Nullable AttributeSet attrs)  

```

3. 第三个构造函数
```java
/**
     * Perform inflation from XML and apply a class-specific base style from a
     * theme attribute. This constructor of View allows subclasses to use their
     * own base style when they are inflating. For example, a Button class's
     * constructor would call this version of the super class constructor and
     * supply <code>R.attr.buttonStyle</code> for <var>defStyleAttr</var>; this
     * allows the theme's button style to modify all of the base view attributes
     * (in particular its background) as well as the Button class's attributes.
     *
     * @param context The Context the view is running in, through which it can
     *        access the current theme, resources, etc.
     * @param attrs The attributes of the XML tag that is inflating the view.
     * @param defStyleAttr An attribute in the current theme that contains a
     *        reference to a style resource that supplies default values for
     *        the view. Can be 0 to not look for defaults.
     * @see #View(Context, AttributeSet)
     */  
    public View(Context context, @Nullable AttributeSet attrs, int defStyleAttr)  

```

4. 第四个构造函数
```java
/**
 * Perform inflation from XML and apply a class-specific base style from a
 * theme attribute or style resource. This constructor of View allows
 * subclasses to use their own base style when they are inflating.
 * <p>
 * When determining the final value of a particular attribute, there are
 * four inputs that come into play:
 * <ol>
 * <li>Any attribute values in the given AttributeSet.
 * <li>The style resource specified in the AttributeSet (named "style").
 * <li>The default style specified by <var>defStyleAttr</var>.
 * <li>The default style specified by <var>defStyleRes</var>.
 * <li>The base values in this theme.
 * </ol>
 * <p>
 * Each of these inputs is considered in-order, with the first listed taking
 * precedence over the following ones. In other words, if in the
 * AttributeSet you have supplied <code><Button * textColor="#ff000000"></code>
 * , then the button's text will <em>always</em> be black, regardless of
 * what is specified in any of the styles.
 *
 * @param context The Context the view is running in, through which it can
 *        access the current theme, resources, etc.
 * @param attrs The attributes of the XML tag that is inflating the view.
 * @param defStyleAttr An attribute in the current theme that contains a
 *        reference to a style resource that supplies default values for
 *        the view. Can be 0 to not look for defaults.
 * @param defStyleRes A resource identifier of a style resource that
 *        supplies default values for the view, used only if
 *        defStyleAttr is 0 or can not be found in the theme. Can be 0
 *        to not look for defaults.
 * @see #View(Context, AttributeSet, int)
 */  
public View(Context context, @Nullable AttributeSet attrs, int defStyleAttr, int defStyleRes)  

```

#### 构造函数的调用

**如果我们在继承了View类实现自定义类时，需要重写哪个构造函数？
回答这个问题，首先需要知道，在定义了View时，我们都调用了哪个构造函数。**

+ 当我们自定义一个View，且在布局文件中引用时，在系统初始化该View时，调用的是第二个构造函数，而且我还把第二个构造函数中的`attrs参数`也打了出来，可以看出其中的参数attrs是我们在xml中配置的参数。

+ 其实第一个构造函数用途并不大，主要是在java代码中声明一个View时所用，不过如果只用第一个构造函数，声明的View并没有任何的参数，基本是个空的View对象。


#### View的第三和第四个构造函数[本文的重点]

1. View的属性和主题

在说后两个构造函数之前，先说说View的属性，在View中有不同的属性，比如layout_width等，TextView还有textColor这些特有的属性，我们可以对这些属性进行不同的配置进而实现不同的效果。而且属性也可以在不同的位置进行配置。以TextView为例，**android:textColor这个属性可以在多个地方配置，可以直接写在xml中，可以在xml中以style的形式定义，这两种是我们平时见得较多的，其实还有一种背后的力量可以给属性赋值，那就是主题。**

我们在android中可以配置一个主题，从而使得一些View即使你不对其进行任何配置，它都会有一些已经默认赋值的属性，这就是主题的功劳。

>View类的后两个构造函数都是与主题相关的，也就是说，在你自定义View时，如果不需要你的View随着主题变化而变化，有前两个构造函数就OK了，但是如果你想你的View随着主题变化而变化，就需要利用后两个构造函数了。

2 属性赋值的优先级

当可以在多个地方赋值属性时，一个问题就不可避免的出现了：**优先级！！！**

一个属性可以在多个地方赋值:
+ xml定义
+ xml中引入style
+ theme中直接指定
+ defStyleAttr
+ defStyleRes
这5个地方。（后面会讲这几个地方的用处）

>【第二个问题】 属性在多个地方被赋值后，系统以哪个属性为准呢？

我将用一个实验，利用多个TextView整体说明属性赋值的优先级，这个实验将贯穿文章后面，我将分块讲解。

> 优先级: xml定义>style>theme


研究View是如何利用系统主题，这时候需要回到我们今天的主题：View的构造函数！！！！

View中如何体现主题的信息，需要就通过实验对View进行彻底探究。这是一个复杂的问题，需要看看View的第三和第四个构造函数，在看这两个构造函数时，就不可避免的看到两个让人懵b的参数：defStyleAttr和defStyleRes。这时引入我们的第三个问题。

>【第三个问题】 那么在View的第四个构造函数中的后面两个的参数都是什么意思呢？

第四个构造函数中第三个参数defStyleAttr，从名字就能看出，是一个`属性资源`。

这个属性资源跟主题有一个奇妙的协议：**只要在主题中对这个属性赋值，该View就会自动应用这个属性的值。**

再看看在第四个构造函数中有一个参数defStyleRes，这个参数是什么作用呢?

这个参数说，**只有在第三个参数defStyleAttr为0，或者主题中没有找到这个defStyleAttr属性的赋值时，才可以启用**。而且这个参数不再是Attr了，而是真正的style。其实这也是一种低级别的“默认主题”，即在主题未声明属性值时，我们可以主动的给一个style，使用这个构造函数定义出的View，其主题就是这个定义的defStyleRes（是一种写死的style，因此优先级被调低）。




















































＃
