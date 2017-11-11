### 滑动冲突问题，触摸事件拦截处理
http://www.cnblogs.com/android-blogs/p/5794867.html

>解决的方法是写一个自定义ScrollView拦截子View的滑动事件

```java
@Override
   public boolean onInterceptTouchEvent(MotionEvent ev) {
       return true;
}
```


### 禁止RecycleView的滑动
http://blog.csdn.net/lengqi0101/article/details/52874762
http://blog.csdn.net/u011374875/article/details/51744448








#
