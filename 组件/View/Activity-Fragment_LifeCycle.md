### Activity 回收问题

如果系统内存不足、或者切换横竖屏、或者app长时间在后台运行，**Activity都可能会被系统回收，然后Fragment并不会随着Activity的回收而被回收，从而导致Fragment丢失对应的Activity。**

某种原因系统回收MainActivity——FragmentA被保存状态未被回收——再次点击app进入——首先加载的是未被回收的FragmentA的页面——由于MainActivity被回收，系统会重启MainActivity，FragmentA也会被再次加载——页面出现混乱，因为一层未回收的FragmentA覆盖在其上面——（假如FragmentA使用到了getActivity()方法）会报空指针，出现crash。

**原理虽然有点绕，但是解决办法很简单：**
MainActivity重写onSaveInstanceState方法，将super.onSaveInstanceState(outState);注释掉，让其不再保存Fragment的状态，达到其随着MainActivity一起被回收的效果！

**在Android开发中，如果我们用到V4包里面的Fragment，在应用被切换到后台的时候，Activity可能被回收，但是创建的所有Fragment则会被保存到Bundle里面**

如果从最近使用的应用里面点击我们的应用，系统会恢复之前被回收的Activity，这个时候FragmentActivity在oncreate里面也会做Fragment的恢复。但是此时恢复出的Fragment，在调用getActivity的时候会返回null，具体什么原因还没详细研究，这里我的解决方法是在恢复Fragment之前把保存Bundle里面的数据给清除，也就是保存的Fragment信息，然后自己重新replace。
```
if(arg0 != null)
        {
            String FRAGMENTS_TAG = "Android:support:fragments";
            // remove掉保存的Fragment
            arg0.remove(FRAGMENTS_TAG);
        }

注：如果是FragmentActivity则在 onCreate之前添加如下
if (savedInstanceState != null) {
      savedInstanceState.putParcelable(“android:support:fragments”, null);
}

super.onCreate(savedInstanceState);

如果是actvity
改成是“android:fragments"
```


### Activity 生命周期
![图片描述](images/activity-lifecycle.png)

### Fragment 生命周期
![图片描述](images/fragment-lifecycle.png)

Activity被销毁的两中情况

Activity被销毁的情况大致可分为两种。
+ 一是正常行为。如当用户按了手机的back键或者activity调用自己的finish（）方法而被销毁。
+ 另一种是非正常行为。如activity处于stop状态而且长期没有被使用，或者是前台的activitiy需要更多的资源因此系统必须关闭后台进程以回收内存。

**原理：**
Android中的进程是托管的，当系统进程空间紧张的时候，会依照优先级自动进行进程的回收。由此带来三个问题：
1. 回收规则:  什么时候回收与回收哪一个？
2. 避免误杀:  如何阻止被回收？
3. 数据恢复与保存:  被回收了怎么办？

Android将进程分为6个等级,它们按优先级顺序由高到低依次是:
1. 前台进程( FOREGROUND_APP)
2. 可视进程(VISIBLE_APP )
3. 次要服务进程(SECONDARY_SERVER )
4. 后台进程 (HIDDEN_APP)
5. 内容供应节点(CONTENT_PROVIDER)
6. 空进程(EMPTY_APP)

**特征：**
1. 如果一个进程里面同时包含service和可视的activity，那么这个进程应该归于可视进程，而不是service进程。
2. 另外，如果其他进程依赖于它的话，一个进程的等级可以提高。例如，一个A进程里的service被绑定到B进程里的组件上，进程A将总被认为至少和B进程一样重要。
3. 系统中的phone服务被划分到前台进程而不是次要服务进程.
