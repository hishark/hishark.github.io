---
title: 利用 OkHttp 请求网络
date: 2018-03-27 16:02:17
tags:
- OkHttp
- Android
- Gson
categories: 学习笔记
thumbnail: 
---
HttpClient已经被亲爸抛弃了，那就来拥抱OkHttp吧。其余部分都和[Android客户端访问Tomcat服务器端](http://hishark.cc/2018/03/26/Android客户端访问Tomcat服务器端/)一致，只需要改动LoginActivity和LoginUtil即可。
<!--more-->

#### LoginActivity.java

```java
public class LoginActivity extends AppCompatActivity {
    /**
     * 定义控件
     */
    EditText et_username,et_password;
    Button bt_login;

    String userName,passWord;

    String strResult="";

    //Handler用来从子线程往主线程传输数据
    private Handler handler = new Handler() {
        public void handleMessage(Message msg) {
            strResult = msg.obj.toString();
            DialogUtil.createDialog(strResult,LoginActivity.this).show();

            super.handleMessage(msg);
        }
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_login);

        et_username = (EditText)this.findViewById(R.id.username);
        et_password = (EditText)this.findViewById(R.id.password);
        bt_login = (Button)this.findViewById(R.id.login);

        bt_login.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                userName = et_username.getText().toString().trim();
                passWord = et_password.getText().toString().trim();
                if(userName==null||userName.equals("")||passWord==null||passWord.equals("")){
                    Toast.makeText(getApplicationContext(),"请输入完整的登录信息", Toast.LENGTH_SHORT).show();
                }else{
                    //实例化登录工具类
                    LoginUtil lu = new LoginUtil();

                    //把handler对象传到子线程去，然后子线程通过handler把数据发回主线程，更新UI
                    lu.getDataAsync(userName,passWord,handler);
                }
            }
        });
    }
}
```
#### LoginUtil.java

```java
public  class LoginUtil {

    //模拟器用10.0.2.2，真机用无线局域网适配器ip——192.168.137.1
    private static String URL="http://10.0.2.2:8080/15Struts2-16-Struts-server/loginActivity.action";

    public String result = "";

    public void getDataAsync(String userName,String passWord,final Handler handler)  {
        //实例化OkHttpClient
        OkHttpClient client = new OkHttpClient();
        //创建表单请求体
        FormBody.Builder formBody = new FormBody.Builder();

        /**
         * 传递键值对参数
         * key一定要和LoginActivityAction里面的变量同名！！！一定要同名！！！
         */
        formBody.add("userName",userName);
        formBody.add("passWord",passWord);

        //创建Request对象
        Request request = new Request.Builder()
                .url(URL)
                .post(formBody.build())
                .build();

        /**
         * Get的异步请求，不需要跟同步请求一样开启子线程
         * 但是回调方法还是在子线程中执行的
         * 所以要用到Handler传数据回主线程更新UI
         */
        client.newCall(request).enqueue(new Callback() {
            @Override
            public void onFailure(Call call, IOException e) {
            }

            //回调的方法执行在子线程
            @Override
            public void onResponse(Call call, Response response) throws IOException {
                if(response.isSuccessful()){

                    //得到Json键值对{“key”:“value”}
                    String temp = response.body().string();
                    Log.d("test",temp);

                    //利用Gson解析Json键值对
                    Test test = new Gson().fromJson(temp,Test.class);
                    result = test.getMessage();

                    //通过handler传递数据到主线程
                    Message msg = new Message();
                    msg.obj = result;
                    handler.sendMessage(msg);
                }else{
                    result="error";
                }
            }
        });
    }

    static class Test{
        private String message;
        public String getMessage() {
            return message;
        }
        public void setMessage(String message) {
            this.message = message;
        }
    }

}
```

<hr>
#### 踩坑

<ol>
<li>如果报错<font color="#FF8C00"><code>FATAL EXCEPTION: OkHttp Dispatcher java.lang.IllegalStateException: closed</code></font>，检查<font color="#FF8C00"><code>response.body().string()</code></font>是否使用了多次，这个只能用一次。原因：从源码中可以发现调用一次<font color="#FF8C00"><code>.string</code></font>方法后又有close方法，流会被关闭，所以会报错。</li>
<li>直接在主线程中实例化一个<font color="#FF8C00"><code>Handler</code></font>对象传给<font color="#FF8C00"><code>LoginUtil</code></font>工具类，在工具类中<font color="#FF8C00"><code>OkHttp</code></font>的异步请求会有一个回调方法是在子线程中执行，拿到网络请求结果之后直接通过<font color="#FF8C00"><code>Handler</code></font>传回主线程更新<font color="#FF8C00"><code>UI</code></font>即可。*AsyncTask未解决，应该哪一步出了点错，下次试一下。*</li>
<li>一开始想学之前用<font color="#FF8C00"><code>HttpClient</code></font>那样从<font color="#FF8C00"><code>Entity</code></font>中拿到<font color="#FF8C00"><code>Json</code></font>对象结果<font color="#FF8C00"><code>OkHttp</code></font>的<font color="#FF8C00"><code>Response</code></font>没有<font color="#FF8C00"><code>getEntity</code></font>噢。查了查发现<font color="#FF8C00"><code>Gson</code></font>很方便很好用。</li>
<li>往表单请求体<font color="#FF8C00"><code>FormBody</code></font>中传递键值对时，要注意<font color="#FF8C00"><code>key</code></font>的值要和服务器端写的<font color="#FF8C00"><code>LoginActivityAction</code></font>中的变量同名噢不然得不到数据- -，有两个字母忘记大写了坑了我半天。</li>
</ol>

#### TIPS

1. 以上是Struts2框架，SSM把URL最后改为`@RequestMapping`设置的名字即可。