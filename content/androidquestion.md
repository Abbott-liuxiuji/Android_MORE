##1、 java.lang.NoClassDefFoundError 问题解决！！！

问题场景：因我的工程使用gRPC，需要引入 compile 'org.conscrypt:conscrypt-android:1.1.2' 安全认证；在导入第三方分享平台包时，出现该问题，对于该问题
原因千千万，而我使用的是直接重新方法。

解决方法：看清问题，不是 ClassNotFoundException 异常，是 NoClassDefFoundError；
第一步：重新构建Application，并在配置文件引入。
第二部：重写 attachBaseContext 方法
     /**
     * 解决 java.lang.NoClassDefFoundError
     * @param base
     */
    @Override protected void attachBaseContext(Context base) {
        super.attachBaseContext(base);
        MultiDex.install(base);
    }
