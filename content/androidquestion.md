##1、 java.lang.NoClassDefFoundError 问题解决！！！

问题场景：因我的工程使用gRPC，需要引入 compile 'org.conscrypt:conscrypt-android:1.1.2' 安全认证；在导入第三方分享平台包时，出现该问题，对于该问题
原因千千万，而我使用的是直接重新方法。

解决方法：看清问题，不是 ClassNotFoundException 异常，是 NoClassDefFoundError；
第一步：重新构建Application，并在配置文件引入。
第二部：重写 attachBaseContext 方法
    
    @Override 
    protected void attachBaseContext(Context base) {
        super.attachBaseContext(base);
        MultiDex.install(base);
    }
##2、Android studio 编译java类爆红，但项目可以运行

解决方法：
第一步：打开Android studio，选择项目后，点击File，找到菜单栏中 Invalidate Caches/Restart
第二步：在弹出的对话框中点击Invalidate and Restart就可以了，他会自动清理缓存并重启Android studio

##3、APP 原生代码传值到HTML 异常
解决JS报错chromium: [INFO:CONSOLE(1)] "Uncaught TypeError:

解决方法：


