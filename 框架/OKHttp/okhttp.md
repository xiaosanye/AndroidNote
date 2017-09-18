### OKhttp

http://www.jiangwenrou.com/okhttp%E7%BC%93%E5%AD%98%E6%B5%85%E6%9E%90.html

尽管Google在大部分安卓版本中推荐使用HttpURLConnection，但是这个类相比HttpClient实在是太难用，太弱爆了。
OkHttp是一个相对成熟的解决方案，据说Android4.4的源码中可以看到HttpURLConnection已经替换成OkHttp实现了。所以我们更有理由相信OkHttp的强大。

OkHttp 处理了很多网络疑难杂症：会从很多常用的连接问题中自动恢复。如果您的服务器配置了多个IP地址，当第一个IP连接失败的时候，OkHttp会自动尝试下一个IP。OkHttp还处理了代理服务器问题和SSL握手失败问题。

使用 OkHttp 无需重写您程序中的网络代码。OkHttp实现了几乎和java.net.HttpURLConnection一样的API。如果你用了 Apache HttpClient，则OkHttp也提供了一个对应的okhttp-apache 模块。



### okhttp 缓存策略
+ http://www.cnblogs.com/android-blogs/p/5438110.html 剖析OkHttp缓存机制
+ https://m.aliyun.com/yunqi/articles/78102  OkHttp 3.7源码分析（四）
+ http://www.jianshu.com/p/9cebbbd0eeab  OkHttp3源码分析[缓存策略]

https://m.aliyun.com/yunqi/articles/78102

http://www.jianshu.com/p/e3d32c016c32

http://blog.csdn.net/iigeoxiaoyang/article/details/52605131?locationNum=13

### Retrofit+OkHttp的缓存机制

链接：http://www.jianshu.com/p/e3d32c016c32

在响应请求之后在 data/data/<包名>/cache 下建立一个response 文件夹，保持缓存数据。
这样我们就可以在请求的时候，如果判断到没有网络，自动读取缓存的数据。
同样这也可以实现，在我们没有网络的情况下，重新打开App可以浏览的之前显示过的内容。
也就是：判断网络，有网络，则从网络获取，并保存到缓存中，无网络，则从缓存中获取。



### 缓存实现方式

#### 1. 先开启OkHttp缓存

在Retrofit2.0版本之后，Retrofit底层自动依赖了OkHttp，所以我们不用重复依赖Okhttp了

```
File httpCacheDirectory = new File(MyApp.mContext.getCacheDir(), "responses");
int cacheSize = 10 * 1024 * 1024; // 10 MiB
Cache cache = new Cache(httpCacheDirectory, cacheSize);

OkHttpClient client = new OkHttpClient.Builder()
        .addInterceptor(REWRITE_CACHE_CONTROL_INTERCEPTOR)
        .cache(cache).build();
```
这一步是设置缓存路径，以及缓存大小，其中addInterceptor是我们第二步的内容。

#### 2. 设置OkHttp拦截器

主要是拦截操作，包括控制缓存的最大生命值，控制缓存的过期时间
两个操作都是在 Interceptor 中进行的

主要是拦截操作，包括控制缓存的最大生命值，控制缓存的过期时间
两个操作都是在`Interceptor`中进行的

+ 通过`CacheControl`控制缓存数据
```java
CacheControl.Builder cacheBuilder = new CacheControl.Builder();

cacheBuilder.maxAge(0, TimeUnit.SECONDS);//这个是控制缓存的最大生命时间

cacheBuilder.maxStale(365,TimeUnit.DAYS);//这个是控制缓存的过时时间

CacheControl cacheControl = cacheBuilder.build();
```
+ 设置拦截器
```java
Request request = chain.request();
 if(!StateUtils.isNetworkAvailable(MyApp.mContext)){
   request = request.newBuilder()
   .cacheControl(cacheControl) .build();
 }
Response originalResponse = chain.proceed(request);
if (StateUtils.isNetworkAvailable(MyApp.mContext)) {
  int maxAge = 60; // read from cache
  return originalResponse.newBuilder()
  .removeHeader("Pragma")
  .header("Cache-Control", "public ,max-age=" + maxAge) .build();
} else
{ int maxStale = 60 * 60 * 24 * 28; // tolerate 4-weeks stale
  return originalResponse.newBuilder()
  .removeHeader("Pragma")
  .header("Cache-Control", "public, only-if-cached, max-stale=" + maxStale)
  .build();
}
```

















###
