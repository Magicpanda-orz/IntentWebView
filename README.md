# IntentWebView
Lab5
## 实验五：Intent
### 自定义WebView验证隐式Intent的使用
### 本实验通过自定义WebView加载URL来验证隐式Intent 的使用。 
实验包含两个应用：   
第一个应用：获取URL地址并启动隐式Intent的调用。  
第二个应用：自定义WebView来加载URL


## 代码及截图
### 主要代码：
#### MainActivity.java
```
public class MainActivity extends AppCompatActivity {
    private Intent intent;
    private Button button;
    private EditText edit_url;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        button = (Button) findViewById(R.id.bu_load_web);
        edit_url = (EditText) findViewById(R.id.edit_url);
        button.setOnClickListener(new View.OnClickListener(){

            @Override
            public void onClick(View v){
                passData();
            }
        });
    }

    public void passData(){
        // Intent intent = new Intent(this, WebViewLoadWeb.class);
        Intent intent = new Intent();
        intent.setAction("com.example.panda.intentwebview.START_ACTIVITY");
        intent.putExtra("url",edit_url.getText().toString());
        startActivity(intent);
    }
}
```
#### MyWebView.java
```
public class MyWebView extends AppCompatActivity {
    WebView webView;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.myview_layout);
        webView = (WebView)findViewById(R.id.wv_webview);
        Intent intent = getIntent();
        String url = intent.getStringExtra("url");
        loadWeb(url);
    }

    public void loadWeb(String url){
        //String url = "https://www.baidu.com/";
        //此方法可以在webview中打开链接而不会跳转到外部浏览器
        webView.setWebViewClient(new WebViewClient());
        webView.loadUrl(url);
    }

    @Override
    public boolean onKeyDown(int keyCode, KeyEvent event) {
        //重写onKeyDown，当浏览网页，WebView可以后退时执行后退操作。
        if(keyCode == KeyEvent.KEYCODE_BACK && webView.canGoBack()){
            webView.goBack();
            return true;
        }
        return super.onKeyDown(keyCode, event);
    }
}
```
### 结果截图：
![image](https://github.com/Magicpanda-orz/IntentWebView/blob/master/img/lab5_1.PNG)  
![image](https://github.com/Magicpanda-orz/IntentWebView/blob/master/img/lab5_2.PNG) 
![image](https://github.com/Magicpanda-orz/IntentWebView/blob/master/img/lab5_3.PNG) 
##  
