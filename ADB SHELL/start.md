```shell
10/13 09:13:44: Launching app
$ adb push /home/moma/moma/moma-project/android/Panda/app/build/outputs/apk/app-debug.apk /data/local/tmp/com.moma.panda
$ adb shell pm install -r "/data/local/tmp/com.moma.panda"
	pkg: /data/local/tmp/com.moma.panda
Success

$ adb shell am start -n "com.moma.panda/com.moma.panda.course.home.MainActivity" -a android.intent.action.MAIN -c android.intent.category.LAUNCHER -D
Connecting to com.moma.panda
Connected to the target VM, address: 'localhost:8621', transport: 'socket'
Disconnected from the target VM, address: 'localhost:8621', transport: 'socket'
```


```shell
0/13 09:18:51: Launching app
No apk changes detected since last installation, skipping installation of /home/moma/moma/moma-project/android/Panda/app/build/outputs/apk/app-debug.apk
$ adb shell am force-stop com.moma.panda
$ adb shell am start -n "com.moma.panda/com.moma.panda.course.home.MainActivity" -a android.intent.action.MAIN -c android.intent.category.LAUNCHER -D
Waiting for application to come online: com.moma.panda | com.moma.panda.test
Waiting for application to come online: com.moma.panda | com.moma.panda.test
Connecting to com.moma.panda
Connected to the target VM, address: 'localhost:8620', transport: 'socket'
```






















#
