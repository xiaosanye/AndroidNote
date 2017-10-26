Android assets的作用：

1： 可以用来实现html5+javascript+android的混合开发中，一般html5和javascript以及相关资源可以存放在Assets文件夹内。

2：可以放一些资源文件


创建成功后你再去build.gradle文件看一下，有如下代码可创建成功了

" sourceSets { main { assets.srcDirs = ['src/assets', 'src/assets/'] } } "


1.加载assets目录下的网页：

//加载assets/win8_Demo/目录下的index.html网页

webView.loadUrl("file:///android_asset/win8_Demo/index.html");

说明：这种方式可以加载assets目录下的网页，并且与网页有关的css，js，图片等文件也会的加载

2.访问assets目录下的资源文件：

AssetManager.open(String filename)，返回的是一个InputSteam类型的字节流，这里的filename必须是文件比如（aa.txt；img/semll.jpg）

3.获取assets的文件及目录名：

//获取assets目录下的所有文件及目录名，content（当前的上下文如Activity，Service等ContextWrapper的子类的都可以）

String fileNames[] =context.getAssets().list(path);


4.将assets下的文件复制到SD卡：
```java
/**
 *  从assets目录中复制整个文件夹内容
 *  @param  context  Context 使用CopyFiles类的Activity
 *  @param  oldPath  String  原文件路径  如：/aa
 *  @param  newPath  String  复制后路径  如：xx:/bb/cc
 */
public void copyFilesFassets(Context context,String oldPath,String newPath) {                    
         try {
        String fileNames[] = context.getAssets().list(oldPath);//获取assets目录下的所有文件及目录名
        if (fileNames.length > 0) {//如果是目录
            File file = new File(newPath);
            file.mkdirs();//如果文件夹不存在，则递归
            for (String fileName : fileNames) {
               copyFilesFassets(context,oldPath + "/" + fileName,newPath+"/"+fileName);
            }
        } else {//如果是文件
            InputStream is = context.getAssets().open(oldPath);
            FileOutputStream fos = new FileOutputStream(new File(newPath));
            byte[] buffer = new byte[1024];
            int byteCount=0;               
            while((byteCount=is.read(buffer))!=-1) {//循环从输入流读取 buffer字节        
                fos.write(buffer, 0, byteCount);//将读取的输入流写入到输出流
            }
            fos.flush();//刷新缓冲区
            is.close();
            fos.close();
        }
    } catch (Exception e) {
        // TODO Auto-generated catch block
        e.printStackTrace();
        //如果捕捉到错误则通知UI线程
                   MainActivity.handler.sendEmptyMessage(COPY_FALSE);
    }                           
}
```

5.使用assets目录下的图片资源：


```java
InputStream is=getAssets().open("wpics/0ZR424L-0.jpg");
Bitmap bitmap=BitmapFactory.decodeStream(is);
imgShow.setImageBitmap(bitmap);
```

6.播放assets目录下的音乐

首先，获取通过openFd()的方法获取asset目录下指定文件的AssetFileDescriptor对象。
其次，通过MediaPlayer对象的setDataSource (FileDescriptorfd, longoffset, long length)方法加载音乐文件。

最后，调用prepare方法准备音乐，start方法开始播放音乐。
