---
title: Android客户端访问Tomcat服务器端
date: 2018-03-26 14:47:24
tags: 
- Android
- Tomcat
- Struts
- HttpClient
categories: 学习笔记
---
终于学会客户端访问服务端啦，JSON可以说是媒婆吧(●ˇ∀ˇ●)，记录一下总感觉没过几天就会忘了OTZ。另外HttpClient已经被谷歌亲爹抛弃啦，添添说学会一个再举一反三就好，之后再自学一下怎么用OkHttp。
<!--more-->

#### 服务器端

##### 导包

放到WEB-INF/lib下
<center>![](https://ws1.sinaimg.cn/large/0068SXX6gy1fpq8o4qlw5j30hm05q3yr.jpg)</center>

##### 定义抽象方法loginCheck

```java
public interface UserService {
	boolean loginCheck(String userName,String passWord);
}
```

##### 实现loginCheck

```java
public class UserServiceImpl implements UserService {
	DbConnection  db=new DbConnection();
	ResultSet rs=null;

	@Override
	public boolean loginCheck(String userName, String passWord) {
		// TODO Auto-generated method stub
		boolean bl=false;
		
		/*
		 * 这里只是走个流程 查个名字出来就好
		 */
		String strSql="select * from user_table where userName='"+userName+"'";
		
		rs=db.executeQuery(strSql);
		try {
			while(rs.next()){
				bl=true;
				break;
			}
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		return bl;
	}

}
```

##### 创建LoginActivityAction

```java
public class LoginActivityAction extends ActionSupport {
	/*
	 * 用户名和密码
	 */
	String userName;
	String passWord;
	
	UserService us = new UserServiceImpl();
	
	/*
	 * 得到response对象,通过这个来响应客户端的请求 （把JSON返回给客户端）
	 */
	HttpServletResponse response = ServletActionContext.getResponse();
	
	public String getUserName() {
		return userName;
	}
	public void setUserName(String userName) {
		this.userName = userName;
	}
	public String getPassWord() {
		return passWord;
	}
	public void setPassWord(String passWord) {
		this.passWord = passWord;
	}
	
	/*
	 * 没有返回值啦！是void！
	 * 处理客户端LoginActivity过来的登录信息
	 * 成功不成功的信息全靠JSON传递
	 * 不需要跟之前一样返回字符串啥的
	 */
	public void loginActivity() {
		/*
		 * 这里的JSONObject和客户端的JSONObject导的不是同一个包
		 */
		JSONObject jsonObject = new JSONObject();
		
		if(us.loginCheck(userName, passWord)) {
			jsonObject.put("message", "欢迎"+userName+"这位胖友！");
		}else {
			jsonObject.put("message", "老哥你谁？？？");
		}

		/*
		 * 先封装成text即字符串 再转换成JSON
		 * 安卓Activity的中文显示只认UTF-8！GBK不可以哦
		 * 这里是指在客户端显示的编码格式
		 */
		response.setContentType("text/json;charset=utf-8");
		
		/*
		 * 这里是指在网络传输过程中的编码方式
		 */
		response.setCharacterEncoding("utf-8");
		
		/*
		 * 用管道流传东西啦
		 * 把JSON转换成byte再传
		 * 编码方式UTF-8！
		 */
		try {
			byte[] bytes = jsonObject.toString().getBytes("utf-8");
			
			//把字节数组写入输出流
			response.getOutputStream().write(bytes);
			
			//设置传输内容的长度，方便response处理
			response.setContentLength(bytes.length);
			
			//清空缓存（把缓存里的全部发出去
			response.getOutputStream().flush();
			
			//用完要关啦
			response.getOutputStream().close();
			
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		};
		
	}
}

```

##### 在sturts.xml中进行配置

```xml
<!-- 客户端和服务端交互要定义新的命名空间 -->
<package name="activity" namespace="/" extends="json-default">
    <!-- result的type现在就只有json了 -->
    <action name="loginActivity" class="jxnu.edu.cn.x3321.action.LoginActivityAction"
    method="loginActivity">
    	<!-- result没有名字 因为loginActivity返回为空  但是type是json！只能是json！-->
    	<result type="json">
    		<!-- 这里是空的！因为所有的数据都在json里头！struts自动记录了从哪来到哪去 -->
    	</result>
    </action>
</package>
```

####  客户端

##### 编写访问服务器端的工具类LoginUtil

```java
public class LoginUtil {

    //模拟器用10.0.2.2，真机用无线局域网适配器ip——192.168.137.1
    private static String URL="http://192.168.137.1:8080/15Struts2-16-Struts-server/loginActivity.action?";
    public String loginToServer(String userName,String passWord){
        String result="";
        String strURL=URL+"userName="+userName+"&passWord="+passWord;

        HttpClient hc=new DefaultHttpClient();
        HttpPost request=new HttpPost(strURL);
        HttpResponse response=null;
        try {
            response=hc.execute(request);
            if(response.getStatusLine().getStatusCode()==200){
                //取得服务器传来的响应
                HttpEntity entity=response.getEntity();

                //这里仍然乱码，还要继续还原成json对象
                String strJson=EntityUtils.toString(entity,"utf-8");

                if(strJson!=null){
                    JSONObject jsonObject=new JSONObject(strJson);
                    result=jsonObject.getString("message").toString();
                }
            }else{
                result="没有网络或服务器连接不上";
            }
        } catch (Exception e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
        return result;
    }
}
```

##### 创建LoginActivity

```java
public class loginActivity extends AppCompatActivity {
    /**
     * 定义控件
     */
    EditText et_username,et_password;
    Button bt_login;

    String userName,passWord;
    String strResult="";

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
                    //异步任务访问网络更方便啦
                    new AsyncTask<String,Void, String>() {
                        @Override
                        protected String doInBackground(String... params) {
                            // TODO Auto-generated method stub
                            /*
                             * 利用编写的LoginUtil工具类访问服务器端
                             */
                            LoginUtil lu=new LoginUtil();
                            strResult=lu.loginToServer(userName, passWord);

                            //这里返回的值传给下面的onPostExecute与主线程产生交互
                            return strResult;
                        }

                        protected void onPostExecute(String strResult) {
                            /**
                             * 和主线程进行交互
                             * 可以直接访问界面上的东西
                             * 对话框要在这里产生
                             */
                            AlertDialog.Builder bd = new AlertDialog.Builder(loginActivity.this);
                            bd.setTitle("提示信息");
                            bd.setMessage(strResult);
                            bd.setPositiveButton("OK", null);
                            bd.create().show();
                        }
                    //execute里面为空，因为LoginUtil里已经定义好访问地址了
                    }.execute("");
                }
            }
        });
    }
}
```

####  实现效果

<center><img src="http://p3as6e9rs.bkt.clouddn.com/QQ%E5%9B%BE%E7%89%8720180326160633.gif" width="" height="100"></center>
  
####  访问方式

##### 安卓模拟器访问

IP为10.0.2.2

##### 真机访问

使用Android真机连接的Wifi的IP地址进行访问
我这里电脑开了热点给手机用
直接ipconfig查到ip就ok了
<center>![](https://ws1.sinaimg.cn/large/0068SXX6gy1fpqal8pwnzj30et03hwee.jpg)</center>
IP为192.168.137.1

<hr>

####  TIPS
1. sql注入攻击
如果sql语句为<font color='#FF8C00'>`select * from user_table where username = '' and password = ''`</font>会很危险，有username就可以登入了，添添说会被老板炒鱿鱼的哈哈哈哈哈
2. 导包
有六个包别漏了，添添debug了大半个上午结果是少导了个包OTZ
3. <font color='#FF8C00'>`URL="http://192.168.137.1:8080/15Struts2-16-Struts-server/loginActivity.action?";`</font>这里的loginActivity是Action的name属性，不是Action的文件名。
4. 权限
记得去Manifest添加访问网络的权限。
