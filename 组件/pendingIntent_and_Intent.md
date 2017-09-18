### Intent和PendingIntent的区别

intent英文意思是意图，pending表示即将发生或来临的事情。
PendingIntent这个类用于处理即将发生的事情。比如在通知Notification中用于跳转页面，但不是马上跳转。

Intent 是及时启动，intent 随所在的activity 消失而消失。

Intent 是及时启动，intent 随所在的activity 消失而消失。
PendingIntent 可以看作是对intent的包装，通常通过getActivity,getBroadcast ,getService来得到pendingintent的实例，当前activity并不能马上启动它所包含的intent,而是在外部执行 pendingintent时，调用intent的。正由于pendingintent中 保存有当前App的Context，使它赋予外部App一种能力，使得外部App可以如同当前App一样的执行pendingintent里的 Intent， 就算在执行时当前App已经不存在了，也能通过存在pendingintent里的Context照样执行Intent。另外还可以处理intent执行后的操作。常和alermanger 和notificationmanager一起使用。
Intent一般是用作Activity、Sercvice、BroadcastReceiver之间传递数据，而Pendingintent，一般用在 Notification上，可以理解为延迟执行的intent，PendingIntent是对Intent一个包装。 





























#
