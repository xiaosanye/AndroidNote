## support-annotations

Android Support 包之一的 support-annotations 是通过静态编译检测来提高代码质量的一个注解工具。

### @Nullable和@NonNull

>检测参数或者返回值是否可以为 null

>`@Nullable`和`@NonNull` 会分别检测一个变量、参数或者函数返回值是否为 null。如果一个函数的参数用 @NonNull 注解，当调用该函数指定该参数为 null 的时候，代码检测工具（Lint）会告诉你一个警告，该参数不能为 null。而 @Nullable 则表示可以为 null。


### 资源类型注解

>Android 开发中经常使用各种资源常量 R.XXX 来引用各种资源。例如 图片资源和字符串资源。这些常量都是 int 类型的，在代码检测的时候没法判断引用的资源是否有错误，比如本来需要一个字符串资源，结果在代码写的时候用了一个颜色资源，这种情况只有通过测试才能发现，有些极端情况可能测试也不容易发现。资源类型注解就是为了解决该问题的，资源注解包含如下几种：


>+ @AnimatorRes 表明该参数、变量或者函数返回值应该是一个 Animator 类型的资源
>+ @AnimRes 表明该参数、变量或者函数返回值应该是一个 Anim 类型的资源
>+ @AnyRes 表明该参数、变量或者函数返回值应该是一个任意类型的资源
>+ @ArrayRes 表明该参数、变量或者函数返回值应该是一个 Array 类型的资源
>+ @AttrRes 表明该参数、变量或者函数返回值应该是一个 attribute 类型的资源
>+ @BoolRes 表明该参数、变量或者函数返回值应该是一个布尔类型的资源
>+ @ColorInt 表明该参数、变量或者函数返回值应该是一个颜色值而不是颜色资源引用，例如应该是一个 AARRGGBB 的整数值。
>+ @ColorRes 表明该参数、变量或者函数返回值应该是一个 color 类型的资源，而不是颜色值。注意和 ColorInt 区别
>+ @DimenRes 表明该参数、变量或者函数返回值应该是一个 dimension 类型的资源
>+ @DrawableRes 表明该参数、变量或者函数返回值应该是一个 drawable 类型的资源
>+ @FractionRes 表明该参数、变量或者函数返回值应该是一个 fraction 类型的资源
>+ @IdRes 表明该参数、变量或者函数返回值应该是一个资源的 ID 类型
>+ @IntegerRes 表明该参数、变量或者函数返回值应该是一个整数类型的资源
>+ @InterpolatorRes 表明该参数、变量或者函数返回值应该是一个 interpolator 类型的资源
>+ @LayoutRes 表明该参数、变量或者函数返回值应该是一个 layout 布局文件类型的资源>+
>+ @MenuRes 表明该参数、变量或者函数返回值应该是一个 menu 类型的资源
>+ @PluralsRes 表明该参数、变量或者函数返回值应该是一个 plurals 类型的资源
>+ @RawRes 表明该参数、变量或者函数返回值应该是一个 raw 类型的资源
>+ @StringRes 表明该参数、变量或者函数返回值应该是一个字符串类型的资源
>+ @StyleableRes 表明该参数、变量或者函数返回值应该是一个 styleable 类型的资源
>+ @StyleRes 表明该参数、变量或者函数返回值应该是一个 style 类型的资源
>+ @TransitionRes 表明该参数、变量或者函数返回值应该是一个 transition 类型的资源
>+ @XmlRes 表明该参数、变量或者函数返回值应该是一个 XML 类型的资源


### 线程注解类型

`线程注解`用来检测一个函数是否在指定类型的线程中执行。

有四个：
+ @UiThread
+ @MainThread
+ @WorkerThread
+ @BinderThread

>注意： 其中 @UiThread 和 @MainThread 是可替换用的， 大部分应用中，这两个是一样的。

如果一个类中的所有函数都在同一个线程内执行，可以在 类名称上面用这个注解即可。



### 权限注解类型

@`RequiresPermission` 用来表明该函数执行需要一个或者多个权限，如果你没有声明这些权限，则会给出警告。

```java
@RequiresPermission(Manifest.permission.SET_WALLPAPER)
public abstract void setWallpaper(Bitmap bitmap) throws IOException;

@RequiresPermission(allOf = {
Manifest.permission.READ_HISTORY_BOOKMARKS,
Manifest.permission.WRITE_HISTORY_BOOKMARKS})
public static final void updateVisitedHistory(ContentResolver cr, String url, boolean real) {
…
}

@RequiresPermission(anyOf = {
Manifest.permission.READ_HISTORY_BOOKMARKS,
Manifest.permission.WRITE_HISTORY_BOOKMARKS})
public static final void updateHistory(ContentResolver cr, String url, boolean real) {
…
}


Read more: http://blog.chengyunfeng.com/?p=771#ixzz4vq5m3GJ6

```

> 如果只要满足多个权限中的一个，用 `anyOf；` 如果要满足多个权限，用 `allOf`.


### 返回值是否使用检测注解

@CheckResults 用来检测函数的返回值是否被使用了，如果没有使用则说明可能不应该调用这个函数，可以给出建议使用哪个函数。例如，新的 Android SDK 中就在 checkPermission 函数中使用如下注解：

```java
@CheckResult(suggest=”#enforcePermission(String,int,int,String)”)
public abstract int checkPermission(@NonNull String permission, int pid, int uid);

```

如果你调用了 checkPermission 函数，但是并没有使用其返回值，则很有可能你是想申请一个权限而不是检查是否有这个权限，所以 suggest 参数建议你使用 enforcePermission 函数来申请权限。如果你确实想检查是否有这个权限，则通常你会判断 checkPermission 的返回值来确定是否有这个权限。

### 确保调用 super 函数的注解

@CallSuper 来表明重写这个函数需要调用 super 父函数。如果你忘记了调用，则会提醒你。比如 Activity 的onCreate 函数需要代用 super.onCreate().

### 数值常量注解

>+ @`IntRange` 是用来表明整数型参数的取值范围的，比如 下面的 setAlpha 函数的参数 alpha 的取值范围应该为 0 到 255，其他值都是非法的；
public void setAlpha(@IntRange(from=0,to=255) int alpha) { … }

>+ @`FloatRange` 同样是表明浮点数范围的，例如：
public void setAlpha(@FloatRange(from=0.0, to=1.0) float alpha) {…}

>+ @`Size` 是用来表明数组类型参数的长度的，可以用 @Size(min=1) 来指定数组的最小长度，@Size(2) 则表明该数组参数必须是2. 例如：、

```java
int[] location = new int[3];
button.getLocationOnScreen(@Size(min=1) location);
```

### 创建枚举类型注解

如果一个参数、变量的取值是几个常量中的一个，则可以用 @`IntDef` 和 @`StringDef` 注解来自定义一个常量枚举类型注解。使用方式如下所示：

```java
import android.support.annotation.IntDef;
…
public abstract class ActionBar {
…
//定义所接受的常量值
@IntDef({NAVIGATION_MODE_STANDARD, NAVIGATION_MODE_LIST, NAVIGATION_MODE_TABS})

//告诉编译器该注解不会在 .class 文件中存在
@Retention(RetentionPolicy.SOURCE)

//定义 NavigationMode 注解
public @interface NavigationMode {}

//Declare the constants
public static final int NAVIGATION_MODE_STANDARD = 0;
public static final int NAVIGATION_MODE_LIST = 1;
public static final int NAVIGATION_MODE_TABS = 2;

//Decorate the target methods with the annotation
@NavigationMode
public abstract int getNavigationMode();

//Attach the annotation
public abstract void setNavigationMode(@NavigationMode int mode);
```

>上面的 @NavigationMode 注解使用了 @IntDef 来定义该注解所限定了一些常量值。 当你用 @NavigationMode 注解时，则说明这个参数或者函数返回值需要是 @IntDef 中定义的常量值其一 (NAVIGATION_MODE_STANDARD, NAVIGATION_MODE_LIST, 或者 NAVIGATION_MODE_TABS).


**除了定义具体的常量值以外，还可以通过 `flag` 参数来指定一个模式，例如下面的 DisplayOptions注解定义该类型必须满足依 DISPLAY_ 开头的一个模式。**

```
import android.support.annotation.IntDef;

@IntDef(flag=true, value={
DISPLAY_USE_LOGO,
DISPLAY_SHOW_HOME,
DISPLAY_HOME_AS_UP,
DISPLAY_SHOW_TITLE,
DISPLAY_SHOW_CUSTOM
})
@Retention(RetentionPolicy.SOURCE)
public @interface DisplayOptions {}


```













































#
