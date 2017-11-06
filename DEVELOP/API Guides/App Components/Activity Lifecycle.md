onCreate()


onStart()
>When the activity enters the Started state, the system invokes this callback. The onStart() call makes the activity visible to the user, as the app prepares for the activity to enter the foreground and become interactive.

当活动进入“开始”状态时，系统将调用此回调。该onStart()通话使活动对用户可见，因为应用程序准备活动进入前台并成为交互式。

>该方法是应用程序初始化维护UI的代码的位置。它还可以注册一个BroadcastReceiver 监视UI中反映的更改。

pnResume()

>This is the state in which the app interacts with the user.

这是应用程序与用户进行交互的状态。

> The app stays in this state until something happens to take focus away from the app. Such an event might be, for instance, receiving a phone call, the user’s navigating to another activity, or the device screen’s turning off.


>If the activity returns to the Resumed state from the Paused state, the system once again calls onResume() method. For this reason, you should implement onResume() to initialize components that you release during onPause(). For example, you may initialize the camera as follows:

```java
@Override
public void onResume() {
    super.onResume();  // Always call the superclass method first


    // Get the Camera instance as the activity achieves full user focus
    if (mCamera == null) {
        initializeCamera(); // Local method to handle camera init
    }
}
```

＞As such, you should implement onResume() to initialize components that you release during onPause(), and perform any other initializations that must occur each time the activity enters the Resumed state. For example, you should begin animations and initialize components that the activity only uses when it has user focus.



您应该实现onResume()初始化您在onPause()发布的组件 ，并执行每次活动进入恢复状态时必须发生的任何其他初始化。例如，您应该开始动画并初始化活动仅在用户关注时才使用的组件。



onPause()

>The system calls this method as the first indication that the user is leaving your activity (though it does not always mean the activity is being destroyed). Use the onPause() method to pause operations such animations and music playback that should not continue while the Activity is in the Paused state, and that you expect to resume shortly.

使用该onPause()方法暂停Activity在暂停状态期间不应该继续的动画和音乐播放的操作，并且您希望很快恢复。

>You can use the onPause() method to release system resources, such as broadcast receivers, handles to sensors (like GPS), or any resources that may affect battery life while your activity is paused and the user does not need them.

>For example, if your application uses the Camera, the onPause() method is a good place to release it. The following example of onPause() is the counterpart to the onResume() example above, releasing the camera that the onResume() example initialized.

您可以使用该onPause()方法释放系统资源，例如广播接收器，传感器（例如GPS）的手柄，或任何可能影响电池寿命的资源，而您的活动暂停，用户不需要它们。

例如，如果您的应用程序使用相机，该 onPause()方法是释放它的好地方。以下示例onPause()是上述示例 的对应 onResume()，释放onResume()示例初始化的摄像头。

```java
@Override
public void onPause() {
    super.onPause();  // Always call the superclass method first


    // Release the Camera because we don't need it when paused
    // and other activities might need to use it.
    if (mCamera != null) {
        mCamera.release();
        mCamera = null;
    }
}

```


onStop()


>In the onStop() method, the app should release almost all resources that aren't needed while the user is not using it. For example, if you registered a BroadcastReceiver in onStart() to listen for changes that might affect your UI, you can unregister the broadcast receiver in onStop(), as the user can no longer see the UI. It is also important that you use onStop() to release resources that might leak memory, because it is possible for the system to kill the process hosting your activity without calling the activity's final onDestroy() callback.

在该onStop()方法中，应用程序应该释放几乎所有的用户不需要的资源。例如，如果您注册一个BroadcastReceiver 在onStart()侦听可能会影响用户界面的变化，你可以注销在广播接收器 onStop()，因为用户不再能看到的UI。同样重要的是，您可以使用 onStop()释放可能泄漏内存的资源，因为系统可能会在不调用活动最终onDestroy()回调的情况下终止托管活动的进程


onDestroy()


onRestart()






## Coordinating activities[协调活动]

>当一个活动启动另一个活动时，他们都会经历生命周期过渡。第一个活动停止运行并进入暂停或停止状态，而另一个活动被创建。如果这些活动共享保存到光盘或其他地方的数据，请务必了解在创建第二个活动之前，第一个活动不会完全停止。相反，启动第二个的过程与停止第一个的过程重叠。

生命周期回调的顺序是很好的定义的，特别是当两个活动在同一个进程（应用程序）中，另一个是启动另一个。以下是活动A启动活动B时发生的操作顺序：

+ 活动A的onPause()方法执行。
+ 活动B的onCreate()， onStart()和 onResume()方法执行顺序。（活动B现在有用户关注。）
+ 然后，如果活动A在屏幕上不再可见，则其onStop()方法将执行。
这种可预测的生命周期回调序列允许您管理从一个活动到另一个活动的信息转换。



## Saving and restoring activity state

#### Save your activity state

当您的活动开始停止时，系统调用该 onSaveInstanceState() 方法，以便您的活动可以使用键值对集合来保存状态信息。此方法的默认实现将保存关于活动视图层次结构状态的临时信息，例如EditText窗口小部件中的文本或窗口小部件的滚动位置 ListView。您的应用程序应该实现 onSaveInstanceState() 回调后的onPause() 方法，和之前 onStop()。不要实现这个回调onPause()。

>Caution: You must always call the superclass implementation of onSaveInstanceState() so the default implementation can save the state of the view hierarchy.


>Note: In order for the Android system to restore the state of the views in your activity, each view must have a unique ID, supplied by the android:id attribute.

>To save persistent data, such as user preferences or data for a database, you should take appropriate opportunities when your activity is in the foreground. If no such opportunity arises, you should save such data during the onStop() method.

要保存持久性数据（例如用户首选项或数据库的数据），您应该在活动处于前台时采取适当的机会。如果没有这样的机会，你应该在onStop()方法中保存这样的数据 。



#### Restore your activity state


>When your activity is recreated after it was previously destroyed, you can recover your saved state from the Bundle that the system passes to your activity. Both the onCreate() and onRestoreInstanceState() callback methods receive the same Bundle that contains the instance state information.

>Because the onCreate() method is called whether the system is creating a new instance of your activity or recreating a previous one, you must check whether the state Bundle is null before you attempt to read it. If it is null, then the system is creating a new instance of the activity, instead of restoring a previous one that was destroyed.


```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState); // Always call the superclass first


    // Check whether we're recreating a previously destroyed instance
    if (savedInstanceState != null) {
        // Restore value of members from saved state
        mCurrentScore = savedInstanceState.getInt(STATE_SCORE);
        mCurrentLevel = savedInstanceState.getInt(STATE_LEVEL);
    } else {
        // Probably initialize members with default values for a new instance
    }
    ...
}
```

>Instead of restoring the state during onCreate() you may choose to implement onRestoreInstanceState(), which the system calls after the onStart() method. The system calls onRestoreInstanceState() only if there is a saved state to restore, so you do not need to check whether the Bundle is null:

而不是恢复状态， onCreate()您可以选择实现 onRestoreInstanceState()，系统在onStart()方法后调用 。系统onRestoreInstanceState() 只有在保存状态恢复时才调用 ，所以您不需要检查是否Bundle为空：


```java
public void onRestoreInstanceState(Bundle savedInstanceState) {
    // Always call the superclass so it can restore the view hierarchy
    super.onRestoreInstanceState(savedInstanceState);


    // Restore state members from saved instance
    mCurrentScore = savedInstanceState.getInt(STATE_SCORE);
    mCurrentLevel = savedInstanceState.getInt(STATE_LEVEL);
}
```

>注意：始终调用超类实现， onRestoreInstanceState() 所以默认实现可以恢复视图层次结构的状态。











































#
