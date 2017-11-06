[TOC]



# [CoordinatorLayout与滚动的处理](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2015/0717/3196.html)


相关网页：
+ [Design Support Library](https://guides.codepath.com/android/Design-Support-Library)



>CoordinatorLayout 实现了多种Material Design中提到的滚动效果。目前这个框架提供了几种不用写动画代码就能工作的方法，这些效果包括：


+ **让浮动操作按钮上下滑动，为Snackbar留出空间。**

+ **扩展或者缩小Toolbar或者头部，让主内容区域有更多的空间。**

+ **控制哪个view应该扩展还是收缩，以及其显示大小比例，包括视差滚动效果动画。**


## 浮动操作按钮与Snackbar

>`CoordinatorLayout`可以用来配合浮动操作按钮的 `layout_anchor` 和 `layout_gravity`属性创造出浮动效果，**layout_anchor 指定参照物, anchorGravity 指定相对于参照物的位置，设置为 bottom|right则表示将FloatingActionButton放置于参照物的右下角**。

>只要使用CoordinatorLayout作为基本布局，将自动产生向上移动的动画。浮动操作按钮有一个 默认的 behavior来检测Snackbar的添加并让按钮在Snackbar之上呈现上移与Snackbar等高的动画。

```xml
<android.support.design.widget.CoordinatorLayout
        android:id="@+id/main_content"
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

   <android.support.v7.widget.RecyclerView
         android:id="@+id/rvToDoList"
         android:layout_width="match_parent"
         android:layout_height="match_parent">
   </android.support.v7.widget.RecyclerView>

   <android.support.design.widget.FloatingActionButton
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="bottom|right"
        android:layout_margin="16dp"
        android:src="@mipmap/ic_launcher"
        app:layout_anchor="@id/rvToDoList"
        app:layout_anchorGravity="bottom|right|end"/>
 </android.support.design.widget.CoordinatorLayout>
```

## Toolbar的扩展与收缩

首先需要确保你不是使用已经过时的ActionBar。务必遵循 使用ToolBar作为actionbar这篇文章的指南。同样，这里也需要CoordinatorLayout作为主布局容器。

```xml
<android.support.design.widget.CoordinatorLayout xmlns:android="http://schemas.android.com/apk/res/android"
 xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/main_content"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fitsSystemWindows="true">

      <android.support.v7.widget.Toolbar
                android:id="@+id/toolbar"
                android:layout_width="match_parent"
                android:layout_height="?attr/actionBarSize"
                app:popupTheme="@style/ThemeOverlay.AppCompat.Light" />

</android.support.design.widget.CoordinatorLayout>
```

## 响应滚动事件

**接下来，我们必须使用一个容器布局：AppBarLayout来让Toolbar响应滚动事件**

```xml
<android.support.design.widget.AppBarLayout
        android:id="@+id/appbar"
        android:layout_width="match_parent"
        android:layout_height="@dimen/detail_backdrop_height"
        android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar"
        android:fitsSystemWindows="true">

  <android.support.v7.widget.Toolbar
                android:id="@+id/toolbar"
                android:layout_width="match_parent"
                android:layout_height="?attr/actionBarSize"
                app:popupTheme="@style/ThemeOverlay.AppCompat.Light" />

 </android.support.design.widget.AppBarLayout>
```

>注意：根据官方的谷歌文档，AppBarLayout目前必须是第一个嵌套在CoordinatorLayout里面的子view（现在貌似不是这样子，正确的理解是：AppBarLayout必须是CoordinatorLayout的直接子View）。


然后，我们需要定义AppBarLayout与滚动视图之间的联系。
在RecyclerView或者任意支持嵌套滚动的view比如NestedScrollView上添加 app:layout_behavior。support library包含了一个特殊的字符串资源@string/appbar_scrolling_view_behavior，它的值为 android.support.design.widget.AppBarLayout$ScrollingViewBehavior ，指向 AppBarLayout.ScrollingViewBehavior，用来通知AppBarLayout 这个特殊的view何时发生了滚动事件，这个behavior需要设置在触发滚动事件的view之上。

```xml
<android.support.v7.widget.RecyclerView
        android:id="@+id/rvToDoList"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:layout_behavior="@string/appbar_scrolling_view_behavior">
```

当CoordinatorLayout发现RecyclerView中定义了这个属性，它会搜索自己所包含的其他view，看看是否有view与这个behavior相关联。AppBarLayout.ScrollingViewBehavior描述了RecyclerView与AppBarLayout之间的依赖关系。RecyclerView的任意滚动事件都将触发AppBarLayout或者AppBarLayout里面view的改变。
























































































#
