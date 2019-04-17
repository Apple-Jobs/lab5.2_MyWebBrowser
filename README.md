# lab5.2_MyWebBrowser

## 实验内容：

Android实验五_Intent，本代码创建了Android工程，并在工程中通过自定义WebView加载URL来验证隐式Intent的使用。

## 关键代码：
```
    <uses-permission android:name="android.permission.INTERNET" />
```

```
        <activity android:name=".WebViewActivity">
            <intent-filter>
                <action android:name="com.action.webview"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <category android:name="com.action.webviewcategory"/>

            </intent-filter>
        </activity>
```

```
public class MainActivity extends AppCompatActivity {
    private Button button;
    private EditText editText;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        button = findViewById(R.id.button);
        editText = findViewById(R.id.editText);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent intent = new Intent("com.action.webview");
                String url = "http://" + editText.getText().toString();
                intent.addCategory("com.action.webviewcategory");
                intent.putExtra("url", url);
                startActivity(intent);
            }
        });
    }
}

```

```
public class WebViewActivity extends AppCompatActivity {

    private WebView webView;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_web_view);
        webView = findViewById(R.id.webview);
        String url = getIntent().getExtras().getString("url");
        webView.loadUrl(url);
        webView.setWebViewClient(new WebViewClient() {
            @Override
            public boolean shouldOverrideUrlLoading(WebView view, String url) {
                view.loadUrl(url);
                return true;
            }
        });

        WebSettings settings = webView.getSettings();
        settings.setJavaScriptEnabled(true);
        settings.setCacheMode(WebSettings.LOAD_CACHE_ELSE_NETWORK);
    }
}
```

## 实验结果：
![Image text](https://github.com/Apple-Jobs/img-folder/blob/master/web521.png)<br>
![Image text](https://github.com/Apple-Jobs/img-folder/blob/master/web522.png)<br>

