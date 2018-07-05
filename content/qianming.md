android 签名信息获取方法

首先要生成签名证书，要记住签名密码 

然后通过命令工具，cd 到签名存储的文件夹

最后执行：keytool -list -v -keystore cloudkey.jks 

