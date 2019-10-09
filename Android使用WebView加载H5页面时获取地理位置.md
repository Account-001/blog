# Android系统下，使用WebView控件加载H5页面，如何做H5页面才能获取地理位置？
### H5页面获取地址位置参考代码
```jscript
navigator.geolocation.getCurrentPosition(showPosition);

function showPosition(position){
  x.innerHTML="Latitude: " + position.coords.latitude +
  "<br />Longitude: " + position.coords.longitude;
}
```

### Android部分
#### 权限：AndroidManifest.xml
添加如下几行：

```xml
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
    <uses-permission android:name="android.permission.INTERNET"/>
```

#### 代码部分
先在界面上加入一个WebView控件，命名为webView1。
```java
public class MainActivity extends AppCompatActivity {

    private WebChromeClient mWebChromeClient = new WebChromeClient() {
        @Override
        public void onGeolocationPermissionsShowPrompt(final String origin, final android.webkit.GeolocationPermissions.Callback callback) {
            callback.invoke(origin, true, false);
            super.onGeolocationPermissionsShowPrompt(origin, callback);
        }
    };

    private WebViewClient mWebView = new WebViewClient(){
        @Override
        public void onReceivedSslError (WebView view, SslErrorHandler handler, SslError error) {
            handler.proceed();
        }

        @Override
        public boolean shouldOverrideUrlLoading(WebView view, String url) {
            view.loadUrl(url);
            return true;
        }

    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        WebView webview = findViewById(R.id.webView1);
        webview.setWebChromeClient(mWebChromeClient);
        webview.setWebViewClient(mWebView);

        WebSettings webSettings = webview.getSettings();
        webSettings.setJavaScriptEnabled(true);

        //启用地理定位
        webSettings.setGeolocationEnabled(true);
        // 启用数据库
        webSettings.setDatabaseEnabled(true);
        String dir = this.getApplicationContext().getDir("database", Context.MODE_PRIVATE).getPath();
        // 设置定位的数据库路径
        webSettings.setGeolocationDatabasePath(dir);
        // 设置存储
        webSettings.setDomStorageEnabled(true);

        // 加载h5页面
        webview.loadUrl("https://lite.zuogj.com/h5_lty/webh5.html");
    }
}
```