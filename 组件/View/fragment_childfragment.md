### Fragment嵌套问题

自从Android3.0引入了Fragment之后，使用Activity去嵌套一些Fragment的做法也变得更加流行，这确实是Fragment带来的一些优点，比如说：Fragment可以使你能够将activity分离成多个可重用的组件，每个都有它自己的生命周期和UI，更重要的是Fragment解决了Activity间的切换不流畅，实现了一种轻量及的切换，但是在官方提供的android.support.v4包中，Fragment还是或多或少的存在一些BUG，今天就与大家分享一下这些BUG和解决方法。

`Case 1`：当使用Fragment去嵌套另外一些子Fragment的时候，我们需要去管理子Fragment，这时候需要调用`ChildFragmentManager`去管理这些子Fragment，由此可能产生的Exception主要是：
`Java.lang.IllegalStateException: No activity`

首先我们来分析一下Exception出现的原因：
通过DEBUG发现，当第一次从一个Activity启动Fragment，然后再去启动子Fragment的时候，存在指向Activity的变量，但当退出这些Fragment之后回到Activity，然后再进入Fragment的时候，这个变量变成null，这就很容易明了为什么抛出的异常是No activity

这个Exception是由什么原因造成的呢？如果想知道造成异常的原因，那就必须去看Fragment的相关代码，发现Fragment在detached之后都会被reset掉，但是它并没有对ChildFragmentManager做reset，所以会造成ChildFragmentManager的状态错误。

找到异常出现的原因后就可以很容易的去解决问题了，我们需要在Fragment被detached的时候去重置ChildFragmentManager，即：
```
@Override
 public void onDetach() {
   super.onDetach();
   try {
     Field childFragmentManager = Fragment.class
         .getDeclaredField("mChildFragmentManager");
     childFragmentManager.setAccessible(true);
     childFragmentManager.set(this, null);

   } catch (NoSuchFieldException e) {
     throw new RuntimeException(e);
   } catch (IllegalAccessException e) {
     throw new RuntimeException(e);
   }
 }
```
`Case 2`：当我们从一个Activity启动了一个Fragment，然后在这个Fragment中又去实例化了一些子Fragment，在子Fragment中去有返回的启动了另外一个Activity，即通过`startActivityForResult`方式去启动，这时候造成的现象会是，子Fragment接收不到`OnActivityResult`，如果在子Fragment中是以`getActivity.startActivityForResult`方式启动，那么只有Activity会接收到OnActivityResult，如果是以getParentFragment.startActivityForResult方式启动，那么只有父Fragment能接收（此时Activity也能接收），但无论如何子Fragment接收不到OnActivityResult。

这是一个非常奇怪的现象，按理说，应该是让子Fragment接收到OnActivityResult才对，究竟是什么造成的呢？这是由于某位写代码的员工抱怨没发奖金，稍稍偷懒了，少写了一部分代码，没有考虑到Fragment再去嵌套Fragment的情况。

我们来看看FragmentActivity中的代码：
```
protected void onActivityResult(int requestCode, int resultCode, Intent data)
 {
   this.mFragments.noteStateNotSaved();
   int index = requestCode >> 16;
   if (index != 0) {
     index--;
     if ((this.mFragments.mActive == null) || (index < 0) || (index >= this.mFragments.mActive.size())) {
       Log.w("FragmentActivity", "Activity result fragment index out of range: 0x" + Integer.toHexString(requestCode));

       return;
     }
     Fragment frag = (Fragment)this.mFragments.mActive.get(index);
     if (frag == null) {
       Log.w("FragmentActivity", "Activity result no fragment exists for index: 0x" + Integer.toHexString(requestCode));
     }
     else {
       frag.onActivityResult(requestCode & 0xFFFF, resultCode, data);
     }
     return;
   }

   super.onActivityResult(requestCode, resultCode, data);
 }
```
很显然，设计者把Fragment的下标+1左移16位来标记这个request是不是Fragment的，拿到result再解码出下标，直接取对应的Fragment，这样并没有去考虑对Fragment嵌套Fragment做一个Map映射，所以出现了这种BUG。

但是如果我们需要在OnActivityResult的时候处理一些事情的话，我们可以通过在子Fragment中以getParentFragment.startActivityForResult的方式来启动，然后在父Fragment中去接收数据，我们需要在子Fragment中提供一个方法，如：getResultData（Object obj），通过父Fragment中的子Fragment实例去调用这个方法，把相应的数据传过去，然后去更新子Fragment。

以上是在使用Fragment去嵌套Fragment的时候可能会遇到的BUG，了解了BUG存在的原因之后，就可以完美的解决问题。
