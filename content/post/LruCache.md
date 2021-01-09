---
title: LruCache
date: 2017-12-30 21:28:47
tags: 
- Android
categories: 
- 学习笔记
thumbnail:
---
一直拖着图片缓存的小视频没看今天看了一哈
梳理一下
<!--more-->
#### 创建一个LruCache
LruCache实际上是一个Map，指定它的键值对类型。
```java
private LruCache<String,Bitmap> mCaches;
```
#### 从缓存中获取数据
```java
public Bitmap getBitmapFromCache(String url){
	return mCaches.get(url);
}
```
#### 把图片添加到缓存
```java
public void addBitmapToCache(String url,Bitmap bitmap){
	//如果缓存中没有该图片就噗特进去
	if(getBitmapFromCache(url) == null){
		mCaches.put(url,bitmap);
	}
}
```

#### 获取最大内存
获取当前应用所可以使用的最大内存，并设置一个缓存的大小值来初始化LruCache。
```java
int maxMemory = (int) Runtime.getRuntime().maxMemory();
int cacheSize = maxMemory / 4;
mCaches = new LruCache<String,Bitmap>(cacheSize){
	@Override
	protected int sizeOf(String key,Bitmap value){
		// 在每次存入缓存的时候调用，告诉系统当前存的对象到底有多大
		// 所以返回一个实际的大小
		return value.getByteCount();
	}
}
```
#### 获取图片
```java
//获取图片的时候，第一步会去内存缓存中取出图片
Bitmap bitmap = getBitmapFromCache(url);
if(bitmap == null){
	//如果缓存中没有，就直接使用异步任务从网络上下载图片
}else{
	//如果缓存中有，就直接使用图片
}
```
#### 下载图片的同时保存至LruCache
```java
//在异步任务的下载逻辑中，还需要将下载完毕的图片保存到LruCache中
@Override
protected Bitmap doInBackground(String... params){
	String url = params[0];
	//从网络上获取图片
	Bitmap bitmap = getBitmapFromURL(url);
	if(bitmap != null){
		//将不在缓存的图片加入缓存
		addBitmapToCache(url,bitmap);
	}
	return bitmap;
}
```

>通过这个方法就可以把下载过的图片存入缓存
刷新时就不用每次都从网上下载
典型的"以内存换效率"
listview常用