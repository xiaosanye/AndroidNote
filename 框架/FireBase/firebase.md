### 检查 Google Play 服务

依靠 `Play 服务 SDK` 运行的应用在访问 Google Play 服务功能之前，应始终检查设备是否拥有兼容的 Google Play 服务 APK。我们建议您在以下两个位置进行检查：主 `Activity` 的 `onCreate()` 方法中，及其`onResume()``方法中。**在 onCreate() 中检查可确保该应用在检查成功之前无法使用**。**在 onResume() 中检查可确保当用户通过一些其他方式返回正在运行的应用（比如通过返回按钮）时，检查仍将继续进行**。

>如果设备没有兼容的 Google Play 服务版本，您的应用可以调用 `GoogleApiAvailability.makeGooglePlayServicesAvailable()`以允许用户从 Play 商店下载 Google Play 服务。




















###
