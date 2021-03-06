# VRVIU-AltPlayerSDK (Android)

[![](https://img.shields.io/badge/Powered%20by-vrviu.com-brightgreen.svg)](https://vrviu.com)

## 版本
V1.1.0

## 功能说明
支持点播以及直播功能，其中直播是网络主播实时推送的视频流，用户能够及时看到主播的画面。点播是播放云端或者本地的文件。

## 产品特点
* **播放器格式支持**：可以支持常见视频格式播放，也可以播放威尔云转码的视频，其中威尔云视频转码对视频编码算法在同样清晰度的前提下有更高的压缩率。

* **直播视频秒开**：通过优化播放器缓冲策略、网络加载等，该SDK可以实现秒开。

* **多协议支持**：支持HLS/FLV/MP4/本地文件播放等。

* **接口简单全面**：实现播放接口简单，可快速实现播放。提供播放器状态监听接口以及错误信息通知接口、日志接口、算法参数配置接口等。

* **解码性能强大**：支持H264、H265、AAC，支持4K视频硬件解码以及2K以下视频软件解码

* **多平台**：支持ARMV7、ARM64和X86平台

## 开发环境
Android studio

## 导入工程
### 1. 开发准备
下载最新的demo和sdk

### 2. 导入工程
##### 2.1 导入aar包
将aar包放到工程libs目录下，如图
![](https://github.com/vrviu-sdk/VRVIU-AltPlayer-Demo-Android)


修改build.gradle文件，确保添加

```gradle
repositories{
	flatDir{
		dirs 'libs'
	}
}
dependencies {
	compile(name:'vrviu-altplayer1.1.0', ext:'aar')
}
```

##### 2.2 配置工程权限
在AndroidManifest.xml中配置APP的权限，一般需要以下权限：

```xml
<uses-sdk android:minSdkVersion="21" android:targetSdkVersion="25" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS"/>
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
```

### 3. 引用SDK
##### 3.1 添加控件
在PlayActivity使用的布局文件中添加界面控件

```xml
<com.viu.player.AltVideoView
    android:id="@+id/surfaceView"
    android:layout_width="match_parent"
    android:scrollbars="none"
    android:layout_height="match_parent"
    android:visibility="visible"/>
```
##### 3.2 调用接口
在onCreate()中首先调用init接口实施鉴权，具体参数见表1.1，然后使用setUrl设置播放地址，使用start开始播放。

```java
videoView = (AltVideoView)findViewById(R.id.surfaceView);
videoView.init(mAppid,mAccessKey,mAccessKeyId,mBizId);
videoView.setUrl(uriString);
videoView.start();
```
##### 3.3 设置本地文件
```java
videoView.setDataSource(file);
```
##### 3.4 设置监听事件
```java
videoView.setOnErrorListener(this);
videoView.setOnVideoSizeChangedListener(this);
videoView.setOnInfoListener(this);
videoView.setOnPreparedListener(this);
videoView.setOnSeekCompleteListener(this);
videoView.setOnCompleteListener(this);
```
##### 3.5 暂停点播播放
```java
videoView.pause();
```
##### 3.6 点播播放时长
```java
videoView.getDuration();
```
##### 3.7 点播播放进度
```java
videoView.getCurrentPosition();
```
##### 3.8 点播跳转
```java
videoView.seekTo(msec);
```
##### 3.9 设置音量
```java
videoView.setVolume(left,right);
```
##### 3.10 设置点播播放速度
```java
videoView.setSpeed(1.0f);
```
##### 3.11 获取点播播放速度
```java
videoView.getSpeed();
```
##### 3.12 获取播放状态
```java
videoView.getPlayState();
```
##### 3.13 设置播放时屏幕常亮与否
```java
videoView.setScreenOnWhilePlaying(true);
```
##### 3.14 结束点播（直播）播放
```java
videoView.release();
```
### 4.检查混淆
```proguard
-keep class com.viu.player.** { *; }
```

## 账号鉴权参数表
 |参数|说明|是否必填|类型|
 |:---|:---|:---|:---|
 |AppId|分配给用户的ID，可通过 www.vrviu.com 填写表单或者联系客服申请|必填|String|
 |AccessKeyId|分配给用户的ID，可通过 www.vrviu.com 填写表单或者联系客服申请|必填|String|
 |BizId|分配给用户的ID，可通过 www.vrviu.com 填写表单或者联系客服申请|必填|String|
 |AccessKey|分配给用户的ID，可通过 www.vrviu.com 填写表单或者联系客服申请|必填|String