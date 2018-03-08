### Android 混合开发对H5 兼容适配

***
###场景：

近期因项目需要，对android工程中部分业务采用webview的方式加载。因场景运用不同对技术要求也异样，现在根据不同场景描述适配过程。

***

###场景一：通过webview浏览简单的HTML静态界面

对于简单的业务场景，建议使用系统API原声WebVIew。

***

###场景二：通过webview浏览复杂的业务HTML

因HTML界面中使用大量的“<iframe>”标签。因android系统webview支持问题。最新的android webview内核为chromewebview。

1、需要在webview重写shouldOverrideUrlLoading方法。并返回false。

2、设置setJavaScriptEnabled(true);

示例：

//webview 判断页面加载过程  

webview.setWebChromeClient(new WebChromeClient()){

​      @Override

​     public void onProgressChanged(WebView view,int newProgress){

​     if(newProgress == 100){

​        progressDialog.dismiss();

​      }else{

​      }

}});

//webview 支持iframe 

webview.setWebViewClient(new WebViewClient()){

​      @Override

​     public boolean shouldOverrideUrlLoading(WebView view, String url){

​      return false

}});

***

### 场景三：通过webview浏览复杂的前端界面，对画质图片要求比较高

对于改场景，如果对WebGL有要求的话，建议直接放弃使用android 系统对webview的使用。因系统问题，建议使用第三方组件：

腾讯X5Webview

### 













### 




