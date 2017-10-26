https://juejin.im/post/5937e1c8570c35005b7b262a?utm_source=tuicool&utm_medium=referral

## Handling Lifecycles

android.arch.lifecycle包提供的类和接口，让您建立生命周期感知组件，可以自动根据当前活动或片段的生命周期调整他们的行为成分。

>Open the build.gradle file for your app or module and add the artifacts that you need as dependencies:
>+ For Lifecycles, add:
implementation "android.arch.lifecycle:runtime:1.0.3" // not necessary if you are using Support Library 26.1+ or lifecycle:extensions
>+ annotationProcessor "android.arch.lifecycle:compiler:1.0.0-rc1" // not needed if you are using the DefaultLifecycleObserver from common-java8 artifact.
>+ For Lifecycles Java8 Lanaguage support, add:
implementation "android.arch.lifecycle:common-java8:1.0.0-rc1"


大部分是在Android框架定义的应用程序组件都连接到他们的生命周期。这些生命周期都是由操作系统或框架的代码在你的程序运行管理。它们是Android工作的核心，您的应用程序必须尊重它们。如果不这样做，可能会触发内存泄漏甚至应用程序崩溃。

想象一下，我们有一个显示屏幕上设备位置的Activity。常见的实现可能如下所示：

```java
class MyLocationListener {
    public MyLocationListener(Context context, Callback callback) {
        // ...
    }

    void start() {
        // connect to system location service
    }

    void stop() {
        // disconnect from system location service
    }
}

class MyActivity extends AppCompatActivity {
    private MyLocationListener myLocationListener;

    public void onCreate(...) {
        myLocationListener = new MyLocationListener(this, (location) -> {
            // update UI
        });
  }

    public void onStart() {
        super.onStart();
        myLocationListener.start();
    }

    public void onStop() {
        super.onStop();
        myLocationListener.stop();
    }
}
```

即使这样看起来很好，在实际的应用程序，你有太多这样的调用，onstart()和onstop()方法变得非常大。

此外，某些组件无法在onstart()刚刚开始。如果我们需要在开始位置观察之前检查一些配置呢？这是可能的，在某些情况下，活动结束后停止检查完成，这意味着mylocationlistener.start()叫做后mylocationlistener.stop()称，基本上保持联系永远。


>android.arch.lifecycle包提供的类和接口，帮助你解决这些问题的弹性和孤立的方式。


###　Lifecycle

生命周期是一个类，它包含组件生命周期状态的信息（如活动或片段），并允许其他对象观察此状态。

生命周期主要通过二枚举为其相关组件的生命周期状态跟踪。




事件
>从框架和生命周期类中分发的生命周期事件。这些事件映射到活动和片段中的回调事件。

状态

>生命周期对象跟踪的组件的当前状态。
















































































#
