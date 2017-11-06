[TOC]




## 4.2 Tasks and Back Stack

**任务**      
>在 SDK中关于Task（guide/topics/fundamentals.html#acttask），有一个很好的比方，说，Task就相当于应用（application）的概念。在开发人员眼中，开发一个Android程序，是做一个个独门独户的组件，但对于一般用户而言，它们感知到的，只是一个运行起来的整体应用，这个整体背后，就是Task。  Task，简单的说，就是一组以栈的模式聚集在一起的Activity组件集合。它们有潜在的前后驱关联，新加入的Activity组件，位于栈顶，并仅有在栈顶的Activity，才会有机会与用户进行交互。而当栈顶的 Activity完成使命退出的时候，Task会将其退栈，并让下一个将跑到栈顶的Activity来于用户面对面，直至栈中再无更多 Activity，Task结束

**LaunchMode(启动模式)**
  1. **标准模式**
    1)`从task中启动Activity时，该Activity的新实例总是在当前task中创建.`
    2)每次启动Activity，都会创建该Activity类的新实例
    3)一个task中可以存在同一Activity的多个实例
    4)一个Activity的多个实例可以出现在多个task栈中
  2. **singleTop**
    1)如果启动模式设置为singleTop的Activity实例未处于栈顶，则其表现与启动模式设置为standard的Activity的表现一致
    2)如果启动模式设置为singleTop的Activity的实例位于任务栈的栈顶则，不会创建该Activity的新实例。只是调用位于栈顶的该Activity实例的onNewIntent方法，将新的intent传递给该实例。  
  3. **singleTask**
    1)设置为singleTask的Activity，具有全局唯一性，在Android系统中只能创建该Activity的一个实例。
    2)如果启动s设置为singleTask的Activity时，已经存在该Activity的实例，则将该实例之上的所有Activity实例释放，将该实例重新带回到栈顶，并调用器onNewIntent方法，将新的intent传递给该实例
    3)在创建设置为singleTask模式的Activity的实例时，如果当前task的taskAffinity与该Activity的taskAffinity一致，则直接在当前task中创建;如果当前task的taskAffinity值与该Activity的taskAffinity不一致则在新的任务中创建该Activity的实例。
  4. **singleInstance**
    1)`当创建设置为singleInstance模式的Activity时，总是在新的任务中创建`
    2)设置为SingleInstance模式的Activity，具有全局唯一性。在Android系统中只能存在该Activity的一个实例
    3)设置为singleInstance模式的Activity，总是单独在一个task中存在也就是说在该Activity所在的task栈中不可能存在其他的activity




### 4.2.1 Handling affinities

>该亲和力表示Activity更喜欢属于哪个task.

> + `By default`, all the activities from the same app have an affinity for each other. So, by default, all activities in the same app prefer to be in the same task.
>+ owever, `you can modify the default affinity for an activity`. Activities defined in different apps can share an affinity, or activities defined in the same app can be assigned different task affinities.

您可以**修改`<activity>`元素的taskAffinity属性指定任何给定Activity的亲和力**。

>The `taskAffinity` attribute takes a string value, which must be unique from `the default package name` declared in the `<manifest>` element, because the system uses that name to identify the default task affinity for the app.

**The affinity comes into play in two circumstances[亲和力在两种情况下发挥作用]:**

+ However, if the `intent` passed to `startActivity()` contains the `FLAG_ACTIVITY_NEW_TASK flag`, **the system looks for a different task to house the new activity**. **Often, it's a new task. However, it doesn't have to be.** If there's already an existing task with the same affinity as the new activity, the activity is launched into that task. If not, it begins a new task.






























#
