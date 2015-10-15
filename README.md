## baiduPush-android
cordova(ionic/phonegap) plugin: "com.xishiyi7.baidupush"
###### plugin desc(插件功能描述)
 * 在js端使用run方法，可以实现js调用android native，同时可以启动baidu push各个接口的广播监听；
 * 在js端使用start方法，可以实现js端启动baidu push绑定服务，如果success，则触发baidu push bind广播，回调js中的bind方法，你可以在bind方法中添加具体操作；
 * 如果bind已成功，当有消息到达时，会触发onNotificationArrived中的广播，此时回调js中的sendPushResult方法，你可以在sendPushResult方法中添加具体操作；
 * 如果点击消息，会触发onNotificationClicked中的广播，此时回调js中的sendBackgroundPushResult方法，你可以在sendBackgroundPushResult方法中添加具体操作；
 * 以上js回调都支持参数传递
 * 以上广播监听也都支持参数传递
 
 
## Usage
the plugin exposes the following method:

```javascript(BaiduPush.js)
// run plugin "com.xishiyi7.baidupush"
cordova.plugins.baiduPush.run(success,error);
// start, bind baidu push 
cordova.plugins.baiduPush.start(success,error);
// stop, unbind baidu push 
cordova.plugins.baiduPush.stop(success,error);
// resume baidu push
cordova.plugins.baiduPush.resume(success,error);
```
## File

```java 
// BaiduPush.java
 1.you should replace the key in first.(你应该先把代码中的key替换成你申请的百度应用key)

 2.there are three boradcast,"bind"/"onNotificationArrived"/"onNotificationClicked". we can use it to callback js in function. (代码里动态注册了三个广播，分别对应“绑定服务”、“消息到达”、“消息点击”,当监听到广播时，我们可以触发相应的广播事件来回调js，可以在相应的js中写操作进行下一步操作)

// PushReceiver.java
 1.when bind successed, i save the device data to your device "com.xishiyi7/Files/pushInfo.txt", and then , i trigger the boradcast "bind".(当绑定成功，我把返回的数据存储在设备的"com.xishiyi7/Files/pushInfo.txt"文件中，可以方便用户在js中读取，同时触发绑定广播，方便用户在js中回调相应操作)

 2.when onNotificationArrived, i trigger the boradcast "onNotificationArrived".(当消息到达，触发onNotificationArrived，回调js方法)

 3.when onNotificationClicked, i trigger the boradcast "onNotificationClicked".(当点击消息，触发onNotificationClicked，回调js方法)

 4.when onMessage, i write two function -- the app run in front or run in background.when it run in front,default. when it run in background, i will make a notify to display message,make it looks like "onNotificationArrived".(当使用透传传递消息时，此处有两种走向，应用运行在前台，则默认透传，运行在后台，则自己定义一个消息，让它看起来像是非透传的消息)
 
// libs 
you should put "libs" into "platforms/android/libs".(你应该把lib放在"platforms/android/libs"下面，此为百度云推送引用的包)
```

## Example
```use
// when you do something, like demo button click event
function demoClick(){
  cordova.plugins.baiduPush.run(success,error);
  cordova.plugins.baiduPush.start(success,error);
  cordova.plugins.baiduPush.stop(success,error);
  cordova.plugins.baiduPush.resume(success,error);
}
```

## CallBack
```
this plugin support the "bind"、"onNotificationArrived"、"onNotificationClicked" callback, you should add some code in index.html like this or use event broadcast. eg.
 1. getPushFrontResult(param,count);
 
 2. getPushBackgroundResult(param,count);
```
