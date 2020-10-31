---
title: Glide大法好
date: 2018-03-09 13:03:01
tags: 
- Android
categories: 学习笔记
thumbnail:
---
项目突然要加几个界面
然后打开了将近两个月没摸过的的AS
findViewById都给忘了我怕是智障

真是开张大吉呢一运行就OOM
记得上学期被这个鬼东西烦到爆炸
搜了很多图片加载的工具类都没有用
然后就自己压缩图片让他勉强显示

现在回头看我可能是猪吧
Glide这么美好的库为什么上学期没发现
简直是居家旅行必备产品啊呜呜呜
导个包然后用上这一句
什么OOM给我见鬼去886
<!--more-->
```java
compile 'com.github.bumptech.glide:glide:3.7.0';

Glide.with(Context).load(ImageId).into(ImageView);

```
另外如果是网络加载图片
就
```java
Glide.with(this).load(url).into(imageView);
```

赶项目过程还碰到点问题
记一下

#### RecycleView设置点击事件

我一开始以为会提供
结果还要自定义的噢

1. 自定义接口
2. 在适配器中声明接口
3. 在适配器的构造方法中添加自定义接口
4. 在<font color="#FF8C00">`onCreateViewHolder()`</font>中给item的view对象设置点击监听
5. 在<font color="#FF8C00">`onBindViewHolder()`</font>中给view设置tag以作为参数传递到监听回调方法中
6. 在<font color="#FF8C00">`onClick()`</font>中将监听传递给自定义接口
7. 在Activity或fragment中声明自定义的监听接口
8. 将接口作为参数传入啊适配器的构造方法中即可

流程是酱紫
具体代码要用再搜

#### 获取res/drawable目录下的图片Uri

```java
/**
  * 得到资源文件中图片的Uri
  * @param context 上下文对象
  * @param id 资源id
  * @return Uri
  */
public Uri getUriFromDrawableRes(Context context, int id){
     Resources resources = context.getResources();
     String path =
	 ContentResolver.SCHEME_ANDROID_RESOURCE + "://" 
	 + resources.getResourcePackageName(id) + "/"
     + resources.getResourceTypeName(id) + "/"
     + resources.getResourceEntryName(id);
     return Uri.parse(path);
}
```

#### AS预览

![](https://ws1.sinaimg.cn/large/0068SXX6gy1fp6j1lgx1mj30eh0c1glv.jpg)
BTW用了这么久预览
一直没有打开过右边这个的我
简直是暴殄天物

