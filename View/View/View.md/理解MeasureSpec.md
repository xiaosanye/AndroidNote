### 理解MeasureSpec

`MeasureSpec`代表一个`32`位int值，高2位代表`SpecMode`，低30位代表`SpecSize`，`SpecMode`是指测量模式，而`specSize`是指在某种测量模式下的规格大小。

`MeasureSpec`通过`SpecMode`和`SpecSize`打包成`int`值来避免过多对象内存分配，为了方便操作，其提供了打包和解包的方法。`SpecModel`和`SpecSize`也是一个int值，一组`SpecMode`和`SpecSize`可以打包为一个`MeasureSpec`，而一个`MeasureSpec`可以通过解包的形式来得出其原始的`SpecMode`和`SpecSize`，需要注意的是这里提到的`MeasureSpec`是指`MeasureSpec`所代表的`int值`，而并非`MeasureSpec`本身。

specMode有三类，每一类都表示特殊的含义，如下所示:
>+ UNSPECIFIED
>+ EXACTLY
>+ AT_MOST









#
