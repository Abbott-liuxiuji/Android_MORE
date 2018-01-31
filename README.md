# Android_MORE
***
###1、 系统适配（基于android 7.1系统适配）
重点一    第三方加固引起的兼容性

“ 
问题描述：

现在主流加固服务提供商，诸如梆梆加固、百度加固和360加固，他们提供的早期方案都无法兼容Android 7.0/7.1 平台，app多产生crash以及黑屏问题，这类错误大多是由于脱壳失败导致。这个一般在app启动的早期发生native crash，很多都crash在对应的加固so的backtrace里面。

”
解决方法：

及时更新到加固服务提供商最新的方案，如果怀疑与加固服务有关系，可以用加固跟非加固应用做对比测试，对于加固引起的问题及时更新最新方案或者找服务商解决。

重点二    native  so兼容性

“ 
问题描述：

多见于加载so失败，上层报UnsatisfiedLinkError 异常，由于google在Android 7.0 以后对so做了更加严格的限制，对于非标准so，比如section header缺失或者dynamic table中数据项不对，会直接崩溃，对于这类问题，可以过滤linker的log查看logcat-s linker。



相关的log信息：


xxx.so has invalid e_phnum  

-----程序头项数不对

xxx.so has no section headers   

-----结头丢失

xxx.so .dynamic section header was not found

-----动态结区丢失

xxx.so .dynamic section has invalid link(%d) sh_type: %d (expected SHT_STRTAB)  

-----结头表里面dynamic section 对应的sh_link字段非法，这里正常应该是字符串表，如果不是字符串表，就会报错。

xxx.so has invalid offset/size of .dynamic section  

-----动态结区offset 校验失败

xxx.so: has text relocations 

-----so有text 重定位section，对于targetSDK>22 会报错。

”
解决方法：

规范app自身lib下的so格式，按标准格式进行，对so加保护的请更新保护方案，对于引用其他服务商so有问题的，及时更新服务商so版本。

重点三    支付SDK兼容性

“ 
问题描述：

大部分常用的支付类SDK，如移动支付SDK、联通支付SDK、游戏SDK等，其早期版本都无法兼容安卓7.0/7.1系统，往往会导致apk产生闪退、黑屏等异常。SDK类异常往往发生在应用启动早期，且调试log较少，而且一些app可能有反调试功能，backtrace刷不出来，但是您可以通过应用在异常之前加载的最后一个so文件来进行判断，如果最后一个so是SDK里面包含的，请联系相关SDK服务商。

”
解决办法：

如果出现问题，请确认最新版SDK是否还有问题。并及时与SDK服务商沟通解决。

重点四    Webview兼容适配

“ 
问题描述：

安卓7.0/7.1默认使用55版本的Webview，可能不兼容部分基于低版本Webview实现的代码。

”
解决办法：

如果您的应用中有使用WebView实现的逻辑，请在安卓7.1上的机器，做一下点检。点检的重点 : 应用启动、网页加载、网页滑动、页内跳转、页内动画执行效果、视频播放和全屏等。看是否有网页打不开、闪退、花屏、卡顿等异常，如发现问题，请基于新版本Webview，重新适配您的代码。

重点五    Toast类型使用

“ 
问题描述：

Android 7.1规范了对Toast类型窗口的使用，同UID的进程不允许同时显示两个Toast类型的窗口，否则会造成黑屏、ANR或停止运行等异常。

”
解决办法：

1. 第三方app尽量不要重写Toast窗口，直接使用Toast组件，这样会按队列处理Toast，不会同时显示两个Toast窗口。

2. 若app需要重写窗口，比如做悬浮等效果，不要用Toast类型，可以使用TYPE_SYSTEM_ALERT类型。



相关的log信息：

WindowManager: Adding more than one toast window for UID at a time

重点六    SharedPreferences的使用

“ 
问题描述：

为了提高app数据的安全性，Android 7.0后对SharedPreferences两种访问模式MODE_WORLD_READABLE和MODE_WORLD_WRITEABLE进行了限制。若应用targetSDK>24，继续使用这两种模式，会抛SecurityException，导致应用异常。

”
解决办法：

官网推荐开发者可以多使用ContentProvider, BroadcastReceiver和Service进行数据共享。



相关的log信息：

AndroidRuntime：FATAL EXCEPTION：Thread-9

AndroidRuntime：Process：com.solomo.azt，PID：830

AndroidRuntime：java.lang.SecurityException：MODE_WORLD_READABLE no longer supported

AndroidRuntime：at android. app.ContextImpl.checkMode(ContextImpl.java：2137)

AndroidRuntime：at android. app.ContextImpl.getSharedPreferences(ContextImpl.java：354)

重点七    FileUri的使用

“ 
问题描述：

由于一些app可能没有权限去访问app设置的file uri，Android 7.0后，不建议app使用file uri，即file://共享给另外一个app，否则会抛FileUriExposedException，导致应用异常。

”
解决办法：官网推荐使用content://代替file://



相关的log信息：

System.err：android. os.FileUriExposedException：file：///storage/emulated/0/temp.jpg exposed beyond app through ClipData. Item. getUri()

System.err：at android.os.StrictMode.onFileUriExposed(StrictMode.java：1799)

System.err：at android.net.Uri.checkFileUriExposed(Uri.java：2346)

System.err：at android.content.ClipData.prepareToLeaveProcess(ClipData.java：845)

System.err：at android.content.Intent.prepareToLeaveProcess(Intent.java：9044)

重点八    分屏功能适配建议

“ 
问题描述：

Android N 支持分屏功能，对于未配置的应用，安卓可强制在分屏模式下开启，但会影响用户体验及手机稳定性。

”
解决办法：请详细参考官方文档

https://developer.android.google.cn/guide/topics/ui/multi-window.html进行适配。



建议：

1. 分屏后，应用的窗口会变小。因此，应用的布局中的控件尽量不要写成固定的值，否则可能会导致分屏后，界面显示不全。组件的布局应采用自适应窗口大小的布局方式。

2. 尽量采用可滑动的控件。如果界面采用的是不可滑动的布局方式，分屏后由于窗口大小改变，则原本可显示完整的界面会被切割，但因为界面不可上下/左右滑动，用户将无法继续操作。

重点九    权限说明

“ 
问题描述：

从Android M开始，系统引入了运行时权限，对于targetSDK>=23的应用，且保护级别为“危险”的权限，不仅仅需要在Manifest中进行申明，同时还需要在调用相关的API前，进行对应的权限检查。在没有权限情况下，先动态申请该权限，否则将会出现Security Excption等权限异常，导致应用发生崩溃或功能异常。

”
解决办法：

确保在调用需要危险权限的API时，检查权限是否允许，没有允许的情况下，请求权限允许。详情请仔细阅读谷歌的开发文档，理解运行时权限的概念和作用，并参考其示例。

参考：https://developer.android.com/guide/topics/permissions/index.html

重点十    NDK使用公开NDK API

“ 
问题描述：

从 Android 7.0开始，系统将阻止应用动态链接非公开 NDK 库，这种库可能会导致应用崩溃。此行为变更旨在为跨平台更新和不同设备提供统一的应用体验。即使代码可能不会链接私有库，但应用中的第三方静态库可能会这么做。因此，所有引用so的应用都应该进行检查，确保其不会在 Android 7.0 以上的设备运行崩溃。

”
解决办法:

参考链接https://developer.android.com/about/versions/nougat/android-7.0-changes.html#ndk，重新规范设计您的so。
