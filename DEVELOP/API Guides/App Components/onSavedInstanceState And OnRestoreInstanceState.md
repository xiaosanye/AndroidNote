onSavedInstanceState()和onRestoreInstanceState() **并不是** activity生命周期的方法。

>+ onSaveInstanceState()会在onPause()或onStop()之前执行
>+ onRestoreInstanceState()会在onStart()和onResume()之间执行。

当应用遇到意外情况（内存不足，用户直接按home键）由**系统直接销毁一个Activity**时，onSaveInstanceState()就会调用.

但是当**用户主动销毁activity**，如按back键，或直接执行finish(),这种情况下onSaveInstanceState()就不会执行，因为这种情况下，用户的行为决定了不需要保存Activity的状态。

**那么onRestoreInstanceState()会跟onSaveInstanceState()成对出现吗？**

>答案是不会成对出现，onSaveInstanceState()需要调用的时，activity可能销毁，也可能没有销毁，只有在activity销毁重建的时候onRestoreInstanceState()才会调用。

**在onSaveInstanceState()中默认情况下具体干些什么？**

>默认情况下默认会自动保存Activity中的某些状态，比如activity中各种UI的状态，因此在activity被“系统”销毁和重建的时候，这些Ui的状态会默认保存，但是**前提条件是Ui控件必须制定id**,如果没有指定id的话，UI的状态是无法保存的。


**总结下Activity数据的保存和恢复：**

>activity中保存数据有两种方式
>+ onPause()
>+ onSaveInstance(bundle)

>恢复数据也有两种途径
>+ onCreate(Bundle)
>+ onRestoreInstanceState(budle)

>默认情况下onSaveInstanceSate()和onRestoreInstanceState()会对UI状态进行保存和恢复，
如果需要保存其他数据可以在onSaveInstanceState()，onPause()保存，
但是如果是**持久化的数据得通过onPause()保存(google推荐)**。
