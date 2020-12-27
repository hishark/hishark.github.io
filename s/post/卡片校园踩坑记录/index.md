这次开发过程中碰到的问题都扔这，看最后能不能破百哦哈哈

<!--more-->

1. 标签云的属性要记得设置，只设置宽高运行时会报错。

2. 登录成功后，按返回键出去后再进来又要登录，[解决方法](https://blog.csdn.net/li15225271052/article/details/62884597)，重写onKeyDown即可。

3. 登录界面如果用了`TextInputLayout`，那么获取到EditText输入值的语句要放在登录按钮的点击事件里，不知道为什么，玄学。[这个人能发现也是无敌](https://blog.csdn.net/tmaskboy/article/details/41047997)。

4. GridView的Item居中直接在getView里面动态设置即可

5. 使用同类多个视图解析器，比如jsp视图解析器，直接在Controller里设置好路径就好了，不要在springMVC.xml里用order设置优先级，没有用噢。
   ```java
   ModelAndView mav=new ModelAndView();
   mav.setViewName("userCURD/UserList");
   ```

6. MySQL-Front导出的sql代码会按照数据库目前表格顺序排序，这样可能会导致找不到外键关联的表的问题。

7. eclipse pull下来的时候报错`checkout conflict with files`，右键项目`Team->Advanced->Assume Unchanged`，然后再pull即可。（这个方法是忽略了自己的修改，如果不想忽略就是别的情况了）

8. 莫名其妙的404问题直接删了Tomcat新建一个就好了，没有什么是删掉一个垃圾汤姆猫不能解决的，如果不能，就删两遍：）

9. 数据库表里字段为user_sno，javabean里属性为User，在mapper.xml中使用association即可。

10. html和js忘了个精光，页面加载时就调用函数用这个
   ```jsp
   <script type="text/javascript">
   window.onload = function()
   {
      showAtRight('${c}')
   }
   </script>
   ```

11. 如果右边加载的内容显示页里面有css，必须放在主页index.jsp才起作用。

12. 用json时如果找不到`.fromObject`方法，看一下导的json包是`net.sf.json.JSONObject`还是`org.json.JSONObject`。如果是后者，换成前者即可。

13. 水平的线性布局不能用layout_gravity使控件居右，用weight即可。

14. Handler可以定义多个啦智障。

15. 捷豹那个intent传递数据的问题，因为传的不是Object，传过来的实际上是HashMap。还需要注意的是在两个Activity之间传送数据时，需要读或者写其他的bean数据的话，这些bean需要实现Serializable序列化接口。（有几个就实现几个，不要漏了）
    ```java
    intent.putExtra("BookPost",BookPostResult.get(i));
    currentBookPost = (HashMap<String,Object>)getIntent().getSerializableExtra("BookPost");
    ```

16. 自定义标题栏，使用Toolbar时，最左边总会有一点间距，设置`app:contentInsetStart="0dp"`即可。

17. 从数据库查出时间JSON为下面的代码，想直接按照以前的方法用Gson解析出时间，解析不出来。用其他的办法，利用阿里的fastjson得到time的值。然后再`Timestamp = new Timestamp(1524323880000L)`即可。有个坑，千万要记得加L，不加L会默认为int，就会报错说太长啦。加个L表示就会作为Long类型来处理了。
   ```json
   {"date":21,"day":6,"hours":23,"minutes":18,"month":3,"nanos":0,"seconds":0,"time":1524323880000,"timezoneOffset":-480,"year":118}
   ```

18. Java不支持范型数组。

19. controller改变了，一定要重启服务器才能看到改变。

20. MyBatis要求如果参数为String的话，不管接口方法的形参是什么，在Mapper.xml中引用时需要改变为_parameter才能识别。(您可真坑- -)
   ```xml
	<select id="getUserBySno" parameterType="String" resultType="User">
		select * from user_info where user_sno= #{_parameter}
	</select>
   ```
21. 当前用户自定义一个静态类保存就好了。

22. TextView设置字体颜色
   ```java
   textview.setTextColor(Color.parseColor("#757575"));
   ```
23. `FloatingActionButton`默认会使用配置中`colorAccent`的颜色，所以如果想自定义`FloatingActionButton`的背景颜色就去`styles.xml`中自定义一个style即可。
   ```xml
   <style name="DaiFloatingButton">
        <item name="colorAccent">@color/colorPrimary</item>
    </style>
	```
	```java
	<android.support.design.widget.FloatingActionButton
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:theme="@style/DaiFloatingButton"
	/>
	```
24. 报错【You need to use a Theme.AppCompat theme (or descendant) with this activity.】解决方法：将AndroidManifest.xml文件中关于Activity的主题配置改一下即可。()
   ```xml
   <activity
            android:name=".activity.MainActivity"
            android:label="@string/title_activity_main"
            android:theme="@style/Theme.AppCompat.Light.NoActionBar">
   </activity>
   ```
25. [ListView实现item内部控件的点击事件](https://blog.csdn.net/weixin_41828085/article/details/79571728)。把Button换成ImageButton就行不通了，查了一下ImageButton的父类居然不是Button，而是ImageView。

26. 睡了一个午觉起来突然被世界抛弃，tomcat莫名其妙一直无法运行，删了重新来也没用我真的崩溃。弄了一下午也没弄好好烦哦T T。终于解决了呜呜呜！也没报错，启动过程就一直卡在log4j的三条警告那里，查了一下午资料都没法解决。以前的struts2和ssm的项目也都无法运行。把汤姆猫删了重装然后把项目重新从git导入，运行之前去tomcat根目录bin下面打开shutdown.bat。然后就OK啦！万岁可以睡个好觉了TUT。重装是第一生产力，谨记。好个球吧注解突然没法用了我要自杀。不自杀了重启eclipse就好了哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈。

27. 找到罪魁祸首了！！parameterMap！！！少了个属性也不报错就直接无法部署你这个垃圾！！！哇气死！！！

28. 服务器改了代码也不要重新启动啦，直接看着console等他reloading completed就好了。

29. 百事通这个模块真是无数的坑啊...`QuestionReplySQL.xml`里`questionreplyResultMap`这个结果集里面包括了`QuestionPost`和`User`，`QuestionPost`里面还包括了`User`，啧啧啧一环扣一环别忘了`QuestionPost`里的`User`，实践表明`association`可以嵌套。不然客户端取不到`QuestionPost`的`User`值噢。

30. 广播真是个好东西，我为啥把他给忘了。[利用广播在Activity之间传递数据](https://blog.csdn.net/jason0539/article/details/18075293)

31. 哇哈哈哈哈哈哈哈哈哈百事通搞定了！！

32. 数据库表中的id不要用int啊智障用String，然后生成随机字符串设置成id。

33. 调用相机时报错
    ```java
    java.lang.NullPointerException: Attempt to invoke virtual method 'android.content.res.XmlResourceParser android.content.pm.ProviderInfo.loadXmlMetaData(android.content.pm.PackageManager, java.lang.String)' on a null object reference
    ```
    记得检查一下manifests里面有没有注册provider。
    ```xml
    <provider
            android:name="android.support.v4.content.FileProvider"
            android:authorities="${applicationId}.provider"
            android:exported="false"
            android:grantUriPermissions="true">
            <meta-data
                android:name="android.support.FILE_PROVIDER_PATHS"
                android:resource="@xml/filepaths" />
    </provider>
    ```
34. 一个boolean可以解决的问题请你不要想的那么复杂- -

35. 之前没想到要FloatingActionButton下滑消失上滑出现，等想到要用的时候大多数都是`CoordinatorLayout`+`RecyclerView`的组合，之前用的都是ListView和GridView就懒得改了，找到这个FloatingActionButton无敌呀hiahiahia。https://github.com/makovkastar/FloatingActionButton

36. json转HashMap，借助fastjson。封装成一个工具类用很方便。
    ```java
    import com.alibaba.fastjson.JSON;
    import com.alibaba.fastjson.TypeReference;

    import java.util.HashMap;

    /**
    * Created by mac on 2018/5/29.
    */

    public class JsonUtil {

        /**
        * 将json转化成HashMap
        * @param jsonStr
        * @return
        */
        public static HashMap<String, Object> convertJsonStrToMap(String jsonStr){
                                                                                  
            HashMap<String, Object> hashmap = JSON.parseObject(jsonStr,new TypeReference<HashMap<String, Object>>(){} );
            return hashmap;
        }
    }
    ```
    然后如下步骤使用即可。
    ```java
    //从服务器取到Json键值对{“key”:“value”}
    String temp = response.body().string();
    JSONObject jsonObject=new JSONObject(temp);
    String jsonResult = jsonObject.get("key").toString();
    HashMap<String, Object> hashmap = JsonUtil.convertJsonStrToMap(jsonResult);
    ```
37. notifyDataSetChanged失效问题。http://www.bkjia.com/Androidjc/869179.html

38. apk运行崩溃问题，首先报错
    ```error
    java.lang.RuntimeException: Unable to get provider android.support.v4.content.FileProvider: java.lang.ClassNotFoundException: Didn't find class "android.support.v4.content.FileProvider" on path: DexPathList[[zip file "/data/app/***.apk"],nativeLibraryDirectories=[/data/app-lib/***-1, /vendor/lib, /system/lib]]
    ```
    找到解决方法https://blog.csdn.net/fangood/article/details/78726005
    自定义的MyApplication在manifest的application节点下添加name属性即可。(Myapplication在util目录下)
    ```java
    android:name=".util.MyApplication"
    ```
    然后又报错了┑(￣Д ￣)┍，报错如下
    ```error
    java.lang.RuntimeException: Unable to instantiate application package.MyApplication:java.lang.ClassNotFoundException: Didn't find class "package.MyApplication" on path:
    ```
    再次找到解决方法，有两种
    a. 直接Build-Build APK就可以得到apk https://blog.csdn.net/u013258802/article/details/76021714
    b. 直接把gradle改成2.2.3 https://blog.csdn.net/xufazhong/article/details/71155528
    >bingo~( •̀ ω •́ )y 卡片校园.apk GET！ 
