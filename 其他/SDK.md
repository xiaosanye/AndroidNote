## SDK介绍

### SDk目录结构
`system-images:`


`add-ones`：里面保存这一些附加的库，第三放公司为Android平台开发的附加功能系统。比如GoogleMaps等等第三方的。（一开始此包内容为空)

`bulid-tools`：构建项目的时候用到的工具，当你新建android项目的时候会用到这个包。我尝试过如果没有此包你新建的项目会报错。还包括一些编译的工具。

`docs`：SDK文档，对各种控件。类的官方说明。可以在里面找到所有的开发文档，index.html（为导航页）建议在火狐浏览器脱机状态下打开。

`extra`：该文件下存放了Google提供的USB驱动、Intel提供的硬件加速等附件工具包

`platform-tools`：该文件夹下存放了Android平台的相关工具比如adb.exe、sqlite3.exe

`tools`：里面放了大量的Android开发、调试的工具和platform—tools有些重复都是与开发有关的工具

`platforms`：platform是SDK里面最重要的文件，这个里面可以有许多不同版本的SDK，有的时候我们在导入项目的时候发现导入后没有SDK，就是因为这里面没有我们导入项目编译时的SDK我们需要在这里面加入SDK或者在项目的根目录下的project.properties里面讲target改为platforms里面有的版本重新编译即可。这里面有SDK对于的版本。每个版本下面又有许多文件组成看图。还有就是如果你在布局文件中编写没有错但是试图预览不了，可能是由于你选择的版本有问题。

`system-images`：上面讲了这里面放的是创建Android虚拟机时的镜像文件

`soruce`：里面存放的是源码，如果你想要ctrl+点击对于类查看源码的化这个必须存在了。 
