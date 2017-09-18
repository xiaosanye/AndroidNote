ListView自身带了单选、多选模式，可通过listview.setChoiceMode来设置：

```java
listview.setChoiceMode(ListView.CHOICE_MODE_MULTIPLE);//开启多选模式
listview.setChoiceMode(ListView.CHOICE_MODE_SINGLE);//开启单选模式
listview.setChoiceMode(ListView.CHOICE_MODE_NONE);//默认模式
listview.setChoiceMode(ListView.CHOICE_MODE_MULTIPLE_MODAL);//没用过，不知道用来干嘛的
```

**实现单选**

需要设置：
```java
listview.setChoiceMode(ListView.CHOICE_MODE_SINGLE);
```

ListView控件还需要指定一个selector:
```xml
android:listSelector="@drawable/checkable_item_selector"
```

```xml
<selector xmlns:android="http://schemas.android.com/apk/res/android">  
    <item android:drawable="@color/c1" android:state_pressed="true"/>  
    <item android:drawable="@color/c1" android:state_checked="true"/>  
    <item android:drawable="@color/c2"/>  
</selector>  
```





























3
