## android中使用DisplayMetrics获取屏幕参数

--关于Density

int android.graphics.Bitmap.getDensity()，返回bitmap-density（密度）。默认的density就是当前display-density，除非当前应用程序不支持不同的screen-density。

在android.util.DisplayMetrics类中定义了一些变量和常量。


--常量DENSITY_XXX，

int类型，定义了不同级别的密度对应的dpi数值，

低密度，DENSITY_LOW，120，

中密度，DENSITY_MEDIUM，160，

高密度，DENSITY_HIGH，240，

超高密度，DENSITY_XHIGH，320，

默认密度，DENSITY_DEFAULT，160（即中密度）。

--变量widthPixels和heightPixels，

int类型，单位像素，display的absolute-width和absolute-height。


--变量density，

float类型，display的logic-density。是一个scaling-factor，用在Density-Independent-Pixel单位，一个dip就是一个像素。

160dpi的screen提供系统display的baseline。

因此，160dpi的screen-density值为1（160/160），120dpi的screen-density值为0.75（120/160）。

screen-1，已知240x320，1.5"x2" ，可以计算出densityDpi等于160。即240/1.5=160，或320/2=160。再通过densityDpi/160计算出density的值1.0。

screen-2，已知320x480，1.5"x2"，可以计算出densityDpi等于240。即320/1.5=240，或480/2=240。再通过densityDpi/160计算出density的值1.5。

--变量densityDpi，

int类型，dots-per-inch。

--关于分辨率和尺寸

分辨率是手机长和宽方向上的像素个数，

尺寸是指屏幕的实际物理大小，

手机尺寸手机尺寸115.5×61×12.45解析得长115.5毫米，宽61毫米，高12.45毫米。

1英寸（inch）等于2.54厘米，

--获取DisplayMetrics对象，再获取屏幕的参数

DisplayMetrics displaysMetrics = new DisplayMetrics();
getWindowManager().getDefaultDisplay().getMetrics(displaysMetrics);

--关于scaledDensity

float类型，一个scaling-factor，用于fonts显示，同density相同的值，除非由于基于font-size上的体验需要做微调。

--TyuMainApp.getApp().getResources().getDisplayMetrics()对象中的属性值

--本机上调试时记录的数据

DENSITY_DEFAULT    160   
DENSITY_DEVICE    240   
DENSITY_HIGH    240   
DENSITY_LOW    120   
DENSITY_MEDIUM    160   
DENSITY_TV    213   
DENSITY_XHIGH    320   
density: 1.5, sclaedDensity: 1.5
densityDpi: 240   
heightPixels: 800, widthPixels: 480

xdpi: 160.42105, ydpi: 160











#
