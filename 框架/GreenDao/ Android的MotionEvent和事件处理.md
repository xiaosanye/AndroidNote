 Android的MotionEvent和事件处理 http://blog.csdn.net/huaxun66/article/details/52352469


 动作常量：
 MotionEvent.ACTION_DOWN：当屏幕检测到第一个触点按下之后就会触发到这个事件。
 MotionEvent.ACTION_MOVE：当触点在屏幕上移动时触发，触点在屏幕上停留也是会触发的，主要是由于它的灵敏度很高，而我们的手指又不可能完全静止（即使我们感觉不到移动，但其实我们的手指也在不停地抖动）。
 MotionEvent.ACTION_POINTER_DOWN：当屏幕上已经有触点处于按下的状态的时候，再有新的触点被按下时触发。
 MotionEvent.ACTION_POINTER_UP：当屏幕上有多个点被按住，松开其中一个点时触发（即非最后一个点被放开时）触发。
 MotionEvent.ACTION_UP：当触点松开时被触发。
 MotionEvent.ACTION_OUTSIDE: 表示用户触碰超出了正常的UI边界.
 MotionEvent.ACTION_SCROLL：android3.1引入，非触摸滚动，主要是由鼠标、滚轮、轨迹球触发。
 MotionEvent.ACTION_CANCEL：不是由用户直接触发，由系统在需要的时候触发，例如当父view通过使函数onInterceptTouchEvent()返回true,从子view拿回处理事件的控制权时，就会给子view发一个ACTION_CANCEL事件，子view就再也不会收到后续事件了。
