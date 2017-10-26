+ 1、实例化Intent后，调用setFlag(int)方法，设置参数为Intent.FLAG_ACTIVITY_NO_ANIMATION，最后调用startActivity(Intent)。这种方法需要注意的是：不要调用finish()方法，否则activity还是使用默认的跳转效果。

  ```java
  Intent intent = new Intent();  
  intent.setFlags(Intent.FLAG_ACTIVITY_NO_ANIMATION);  
  intent.setClass(MainActivity.this, Text2.class);  
  startActivity(intent);  
  //this.finish(); //不要调用  
  ```
+ 2、调用startActivity(Intent)后，调用overridePendingTransition（int,int）方法，可设置两个参数都为0，或者在res文件夹下的anim目录下创建一个空的Tween Animation XML文件，然后设置overridePendingTransition的两个参数都是它。这个方法用于以自定义的动画方式跳转。

  ```java
  startActivity(new Intent(MainActivity.this, Text2.class));  
  //overridePendingTransition(0, 0);  
  overridePendingTransition(R.anim.empty,R.anim.empty);  
  ```
+ 3、在Manifest文件中声明Activity时，通过android:theme属性设置Activity的主题，可实现跳转动画的设置，这个方法同样需要创建Tween Animation XML文件。具体参考转载的博文：[Android中Activity的切换动画(非overridePendingTransition](https://my.oschina.net/u/1376187/blog/263331))







#
