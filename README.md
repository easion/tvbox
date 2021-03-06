
# RaftLink信息发布终端 WebApp编程指南

![xiaofu.png](xiaofu.png)
  
###### Guangzhou Fuhai Software Technology Co., Ltd.
###### 广州市孚海软件技术有限公司 出品
[Company website http://www.wifi-town.com](https://www.wifi-town.com/)


#### Histroy
|Version|Revision|Author|Date|
|:----- |:-------|:-----|----- |
|v1.0 |First initial version|Easion|2019-08-26 |
|v1.1 |增加多屏环境等API见2.18章及以后|Easion|2020-03-14 |


> 网站: 
**kuaipin.wifi-town.com**

> 默认测试环境最新版本请访问网址：
**https://kuaipin.wifi-town.com/kp/connect.html**


## 1. 概论
  [RaftLink](https://raftlink.1688.com/)是广州市孚海软件技术有限公司的注册商标.
  
RaftLink信息发布终端是基于安卓的信息发布应用。用户可以自定义网页、幻灯片、视频三种类型的多媒体文件播出方式，默认的按照每6小时一个时间段，将全天划分成4个时间段，每个时间段可以播出不同的内容。
  
RaftLink信息发布终端可支持2个虚拟屏幕，我们建议用户采用WebApp的方式开发您的信息发布应用，可以通过WEB JavaScript代码实现不同屏幕的切换、播放单的读取和修改、文本转语音等功能。非常适合采用类似Angular/Vue/ReactJS+WebSocket技术方案构建的单页信息发布系统。
  
我们设备提供JavaScript转native功能，它类似微信公众号的JSAPI功能，通过JS代码调用原生底层实现，设备更偏重于WEB对底层基本功能的操控，从而快速完成产品的上线并快速迭代开发。
    
    由于我们设备并非提供给普通用户，对JS调用权限并不检查调用者的来源，无需接口的签名校验操作。
    
[RaftLink设备购买地址](https://raftlink.1688.com/)
 
  - 
 ## 1.导入基础库

导入基础库，可从 [https://kuaipin.wifi-town.com](https://kuaipin.wifi-town.com) 下载下面文件。
```html
<head>
<--- 省略其他信息   --->
<script src="https://kuaipin.wifi-town.com/kp/dsbridge.js"> </script>
<script src="https://kuaipin.wifi-town.com/kp/fly.js"></script>
<script src="https://kuaipin.wifi-town.com/kp/engine-wrapper.js"></script>
<script src="https://kuaipin.wifi-town.com/kp/adapter.js"></script>
</head>
```

检查是否支持JSBridge
```js
var engine = EngineWrapper(dsbAdapter)
fly.engine = engine;

if (JSBridge.hasNativeMethod("getSystemInfoSync"))
{
	console.log("Your browser was running JSBridge!");
}
else{
	alert("Your browser not supported JSBridge!");
}
```

 ## 2.编程API
  
**JSBridge可支持事件回调**
```mermaid
```
#### 注册回调
```js
function bridgeEventHandle(e)
{
	console.log("Event handle " + JSON.stringify(e) );
}
function onLocalServiceLost(e)
{
	console.log("onLocalServiceLost handle " + JSON.stringify(e) );
}
function onLocalServiceFound(e)
{
	//JSBridge.Speak('找到HomeKit设备!');
	console.log("onLocalServiceFound handle " + JSON.stringify(e) );
}
function onLocalServiceDiscoveryStop(e)
{
	console.log("onLocalServiceDiscoveryStop handle " + JSON.stringify(e) );
}
function onLocalServiceResolveFail(e)
{
	console.log("onLocalServiceResolveFail handle " + JSON.stringify(e) );
}
function onLocalServiceResolved(e)
{
	console.log("onLocalServiceResolved handle " + JSON.stringify(e) );
}

JSBridge.register('bridgeEventHandle', bridgeEventHandle);
JSBridge.register('onLocalServiceFound', onLocalServiceFound);
JSBridge.register('onLocalServiceResolved', onLocalServiceResolved);
JSBridge.register('onLocalServiceLost', onLocalServiceLost);
JSBridge.register('onLocalServiceDiscoveryStop', onLocalServiceDiscoveryStop);
```

### 2.2 查询系统信息

#### 2.2.1 编程调用
```js
var sysInfo = JSBridge.getSystemInfoSync();
console.log("getSystemInfoSync "+ JSON.stringify(sysInfo) );
```

应答
```json
{
	"last_version": 42,
	"last_demos": "支持多屏显示",
	"DeviceID": "r13bFs123",
	"DeviceQR": "http://kuaipin.wifi-town.com/api/serial_query/N326GCL#BIND_r13bFs123",
	"serial": "N326GCL",
	"downloadTimeout": 40,
	"email": "test@envcat.com",
	"DeviceRole": "lan",
	"mobileDataEnabled": false,
	"mainScreen": 2,
	"slaveScreen": 14,
	"presentationScreen": 16,
	"ip": "192.168.8.118",
	"port": 8080,
	"expired": false,
	"presentationEnabled": false,
	"wifiEnabled": true,
	"wifiState": 3,
	"displayCount": 2,
	"displayList": [{
		"id": 0,
		"name": "内置屏幕"
	}, {
		"id": 1,
		"name": "HDMI 屏幕"
	}],
	"ssid": "",
	"WiFiIP": 0,
	"mac": "A2:25:90:BE:CB:96",
	"network": -1,
	"model": "rk3288",
	"product": "rk3288",
	"sdk_int": 27,
	"brand": "rockchip",
	"display": "rk3288-userdebug 8.1.0 OPM8.181005.003 120911 test-keys",
	"version": "1.42",
	"versioncode": 42,
	"dpi": 220,
	"widthPixels": 1920,
	"heightPix": 1014,
	"scaledDensity": 1.375,
	"density": 1.375,
	"bluetoothEnabled": true
}
```

#### 2.2.2 返回字段说明
|字段|说明|
|:----- |:------|
| versioncode| 当前软件的版本号|
| last_version|  当前最新的固件版本|
| last_demos|  固件更新内容|
| DeviceID|云端分配的设备唯一编码|
| DeviceQR| 设备信息查询、软件注册二维码|
| serial| 硬件唯一序列号|
| DeviceRole| 设备类型，用于不同的用途，默认为lan，固定|
| slaveScreen| 从屏的播放单ID|
| ip| 设备的IP地址|
| port| 设备WEB访问端口|
| expired| 软件授权是否已经过期|
| wifiEnabled| 是否使用WIFI|
| model| 安卓产品model|
| product| 安卓产品ID|
| display| 显示信息|
| sdk_int| 安卓SDK版本号|
| dpi| 屏幕显示密度，可设置|
| widthPixels| ，屏幕像素，可设置|
| bluetoothEnabled| 是否启用了蓝牙|
| downloadTimeout |  默认下载最大超时(所有任务)|
| mobileDataEnabled |  是否已经启用4G流量上网功能|
| mainScreen | 主屏当前播放单ID  |
| slaveScreen | 后台当前播放单ID(默认隐藏，可激活)  |
| presentationScreen | 多屏异显环境下，其他屏幕当前播放单ID  |
| displayCount | 多屏显示环境下，屏幕个数  |
| displayList | 多屏显示环境下，所有屏幕信息  |


主频的播放单ID分别是0，1，2，3.对应00:00-23:59:59每6小时为一段的4个时间段。
多屏异显当前主要测试平台为RK3288，支持自动发现、投送。


### 2.3 查询网络状态

#### 2.3.1 编程架构
```js
function queryNetState()
{
    var netinfo = JSBridge.getNetworkInfo();
	console.log("netinfo "+ JSON.stringify(netinfo) );
	if (netinfo.connected === true)
	{
	  console.log("已经连接到网络");
	}
	else{
	  console.log("网络已断开");
	}
}
```

```json
{
	"connected": true,
	"type": "LTE",
	"simOperator": "46001",
	"networkType": "4g",
	"traffic": {
		"mobileRxBytes": 0,
		"mobileRxPackets": 0,
		"mobileTxBytes": 0,
		"mobileTxPackets": 0,
		"totalRxBytes": 953567,
		"totalRxPackets": 970,
		"totalTxBytes": 90479,
		"totalTxPackets": 729
	}
}
```

#### 2.3.2 返回字段说明
|字段|说明|
|:----- |:------|
| connected | 网络是否已经连接 |
| type | 当前网络类型，如wifi,lte |
| networkType | 移动网络类型,如2g,3g,4g |
| simOperator | 移动网络运营商ID |
| traffic | 流量统计,单位为字节数或者报文个数 |

### 2.4 主从屏幕切换

#### 2.5.1 编程
```js
JSBridge.scrollPage('slave');
setTimeout(function(){
	JSBridge.scrollPage('main');
},60000)
```

注意：当屏幕从WEB页面切换到其他页面，由于输入焦点已经改变。
JS将不能获取用户的按键消息，请使用软件逻辑完成页面的切回。

#### 2.4.1 输入参数说明
|字段|说明|
|:----- |:------|
| main|  切换到主屏|
| slave| 切换到从屏 |
| toggle| 触发模式 |


### 2.5 固件升级

#### 2.5.1 编程架构
```js
JSBridge.fwUpdate();
```
自动跳转到升级界面，如果有新版本将自动升级，否则会重启到初始界面。
可根据获取系统信息API来判断是否需要支持这个操作。

### 2.6 播放单的读取与设置

#### 2.7.1 编程架构
```js

var plBrowser = {};
plBrowser.media_type = "uri";
plBrowser.name = "js";
plBrowser.local = true;
plBrowser.demos = "js wrote";
plBrowser.uri = "https://www.solidot.org";
plBrowser.tiresTime = 12;
plBrowser.data = {};

var plPics = {};
plPics.media_type = "slideshow";
plPics.name = "js";
plPics.local = true;
plPics.demos = "js slideshow";
plPics.slideshowType = "default";
plPics.slideshowInterval = 10;
plPics.data = {};

var plVid = {};
plVid.media_type = "media";
plVid.name = "js";
plVid.local = true;
plVid.demos = "js video";
plVid.data = {};

/*网络下载到本地，视频/图片都是同样的结构*/
var httpVid = {};
httpVid.media_type = "media";
httpVid.name = "js http";
httpVid.demos = "http video";
httpVid.data = [
  {path: 'http://kuaipin.wifi-town.com/file123.jpg',
	name: 'My Photo', keyid: 'file123', filesize: 123009},
  {path: 'http://kuaipin.wifi-town.com/file124.jpg',
	name: 'My Photo2', keyid: 'file124', filesize: 163014}
];

if (sysInfo.slaveScreen !== undefined)
{
	var plinfo = JSBridge.getPlayListSync({channel: sysInfo.slaveScreen});
	var plSample = {};
	
	plSample.channel = sysInfo.slaveScreen;
	plSample.data = plPics;
	JSBridge.setPlayList(plSample,function(result){
		console.log("result "+ JSON.stringify(result) );
	});
	console.log("getPlayListSync "+ JSON.stringify(plinfo) );
}

```
播放单支持在线的文件，如http https开头的协议，如类型为图片或者视频。
在软件启动的时候会启动下载界面自动完成下载和重启。

```json
{
	"channel": 14,
	"data": {
		"media_type": "media",
		"name": "js",
		"local": true,
		"demos": "js video",
		"data": {}
	}
}
```

#### 2.6.2 返回字段说明
|字段|说明|
|:----- |:------|
| channel|  播放单ID，范围为0-3,14|
| data | 播放单内容，填写null表示删除播放单 |
| data.name| 名称 |
| data.media_type| 类型，分别是 uri,media,slideshow|
| data.local| 是否采用本地的文件内容 |
| data.data | 网络内容 |

### 2.7 WebP2P


#### ngrok服务器部署教程：
[https://luozm.github.io/ngrok](https://luozm.github.io/ngrok)


#### 2.7.1 编程

启动/保存web反向代理
```js

var opt = {};
opt.host = "webp2p.example.com";
opt.domain = sysInfo.DeviceID;
opt.port = 1234;

var p2pInfo = JSBridge.getWebP2pInfoSync();
if (p2pInfo.autoboot !== true)
{		
	//opt.autoboot = false; //开机自动启动
	opt.focus = false; //强制保存		
}
else{
	console.log("getWebP2pInfoSync "+ JSON.stringify(p2pInfo) );
}

if (p2pInfo.running !== true)
{
	JSBridge.startWebP2P(opt, function(result){
		console.log("startWebP2P "+ JSON.stringify(result) );
	});
}
```

```json
{
	"status": 0,
	"host": "webp2p.example.com",
	"domain": "Buo7QUnd415539",
	"port": 1234,
	"autoboot": false
}
```

停止web反向代理:
```js
JSBridge.stopWebP2P();
```


#### 2.7.2 输入/输出字段说明
|字段|说明|
|:----- |:------|
| host|  NGROK服务主机地址|
| port| NGROK服务主机连接端口 |
| domain| 当前主机的子域名 |
| autoboot| 是否开机自动启动此服务 |
| focus| 是否强制(force)保存 |

### 2.8 磁盘空间

#### 2.8.1 编程
```js
var disk = JSBridge.getDiskSpace();
$("#total" ).html("存储 空闲" + disk.free + "M,总共" + disk.total+"M");
```

获取当前设备存储空间用量信息，单位为M（兆字节）

```json
 {"total":12345,"free":11685}
```

### 2.9 获取Wifi AP列表

#### 2.9.1 编程
```js
JSBridge.onGetWifiList(function(list){
	var select = $('#wifilist');
	$('option', select).remove();
	for (var i=0; i<list.length; i++)
	{
		console.log("onGetWifiList "+ JSON.stringify(list[i]) );
		$('#wifilist').append('<option value="'+list[i].ssid+'" selected="selected">'
		+list[i].ssid+' '+list[i].level+'</option>');
	}
});
```

获取可用的AP列表

### 2.10 退出程序(自动重启)

#### 2.10.1 编程
```js
JSBridge.exitProgram();
```
退出当前程序，如修改了播放单，可调用此API，可在重启后完成新的播放单的加载。


### 2.11 关机

#### 2.11.1 编程
```js
JSBridge.powerOff();
```



### 2.12 重启

#### 2.12.1 编程
```js
JSBridge.reboot();
```

### 2.13 文字转语音

#### 2.13.1 编程
```js
JSBridge.Speak("你好 世界");
```

### 2.14 设置音量

#### 2.14.1 编程
```js
JSBridge.setVolume({type:'notify', val: '7'});
```


#### 2.14.2 输入/输出字段说明
|字段|说明|
|:----- |:------|
| type |  notify为通知音量，music为媒体音量 |
| type |  system为系统音量，alarm为闹钟音量 |
| type |  ring为铃声音量，voice_call为电话音量 |
| vol| 音量参数，请参照获取系统信息的音量范围填写,inc为增加，dec为减少 |

### 2.15 MDNS查询

#### 2.15.1 编程
```js
JSBridge.startLocalServiceDiscovery({type: "_hap._tcp."}, function(list){
	console.log("startLocalServiceDiscovery "+ JSON.stringify(list) );
});
```
查询的结果见2.1章节注册的MDNS回调函数。


### 2.16 执行命令

#### 2.16.1 编程
```js
JSBridge.doExecCommand("/system/xbin/cpustats");
```
上面指令会推送到一个线程异步执行，所以不支持返回输出数据。



### 2.16 TTS设置

#### 2.16.1 编程
```js
var voiceSample = {};

voiceSample = JSBridge.getVioceSetting();
voiceSample.speaker = '0';
voiceSample.volume = '9';
voiceSample.speed = '5';
voiceSample.pitch = '5';

voiceSample = JSBridge.getVioceSetting();
console.log("getVioceSetting "+ JSON.stringify(voiceSample) );
voiceSample.speaker = '110'; //度小童（情感儿童声）
var newSetting = {data: voiceSample};
JSBridge.vioceSetting(newSetting, function(res){
	console.log("vioceSetting "+ JSON.stringify(res) );
	if (res.result == 0)
	{
		JSBridge.Speak('TTS配置已经更新,重启程序生效');
	}
	else{
		JSBridge.Speak('TTS配置已经删除');
	}
});

//删除
newSetting = {data: null};
JSBridge.vioceSetting(newSetting, function(res){
	console.log("vioceSetting "+ JSON.stringify(res) );
	if (res.result == 0)
	{
		JSBridge.Speak('TTS配置已经更新,重启程序生效');
	}
	else{
		JSBridge.Speak('TTS配置已经删除');
	}
});

```
设置百度语音tts声音效果方案


#### 2.17.2 输入/输出字段说明

取值请参考[百度TTS文档](https://ai.baidu.com/docs#/TTS-Android-SDK/top)

|字段|说明|
|:----- |:------|
| volume|  音量，取值0-15，|
| speed| 语速，取值0-15 |
| pitch| 音调，取值0-15，默认为5中语调 |
| speaker| 语音播放者 |

请注意上面数据类型为字符串
删除data填写null或者为空

#### 调试
console.log的输出将保存在系统日志logcat中。
请登录到web控制台，菜单展开后点击“日志”目录。   


### 2.18 获取音量信息

#### 2.18.1 编程
```js
var vols = JSBridge.getVolumeSync();
```

获取当前设备音量信息，vol为系统音量，其他类型照字面意思理解。

```json
{
	"vol_max": 7,
	"vol_current": 7,
	"music_max": 15,
	"music_current": 0,
	"alarm_max": 7,
	"alarm_current": 7,
	"notification_max": 7,
	"notification_current": 7,
	"ring_max": 7,
	"ring_current": 7,
	"voice_call_max": 5,
	"voice_call_current": 5
}
```

### 2.19 获取机顶盒内置存储文件列表

#### 2.19.1 编程
```js
var path = 'picture';
var fileList = JSBridge.getFloderContents(path + '/');
```

获取当前指定目录(参数为String)的文件列表,照片上传为picture,视频为video,PDF为pdf。

```json
[{
	"path": "picture/bg-9.jpg",
	"filename": "bg-9.jpg",
	"size": 395203,
	"id": 1,
	"time": 1565775738000
}]
```
#### 2.3.2 返回字段说明
|字段|说明|
|:----- |:------|
| path | 路径 |
| filename | 文件名 |
| size | 文件大小 |
| id | 编号 |
| time | 文件最后修改UNIX时间戳，单位毫秒 |


### 2.20 删除文件

#### 2.20.1 编程
```js
JSBridge.removeFile("picture/bg-9.jpg");
```

删除设定的文件,sd卡路径从/mnt/sdcard/Cabinet/开始




### 2.21 清理缓存

#### 2.21.1 编程
```js
JSBridge.destroyCache();
```

删除应用缓存、以及清理浏览器缓存、历史记录等信息。

### 2.22 打开应用

#### 2.22.1 编程
```js
JSBridge.openApp("android.settings.SETTINGS");
```

打开指定路径的应用程序或者设置界面

### 2.23 设定下载超时

#### 2.23.1 编程
```js
JSBridge.setDownloadTimeout("30");
```

设定下载播放单内媒体文件最大超时时间，单位为秒，目前暂支持字符串格式的数字

### 2.24 打开/设置跑马灯文字内容

#### 2.24.1 编程
```js
JSBridge.setMarquee("你好 世界");
```

设定跑马灯文字，如需要关闭跑马灯，参数可输入"//close"。


### 2.25 向播放单实时添加/插播新条目(默认不保存)

#### 2.25.1 编程
```js
var newItem = {
	"playlist": 16,
	"uri": "http://cdn.wifi-town.com/mypic.jpg",
	"path": "mypic.jpg",
	"name": "Demo Add"
};
JSBridge.addPlayListFile(newItem);
```

向播放单实时添加新条目(默认不保存),新条目会尽快安排播出，但不保存到当前播放单，
需要调用savePlayListFiles才能保存。

#### 2.25.2 输入字段说明
|字段|说明|
|:----- |:------|
| playlist | 该条目对应的播放单ID |
| path | 文件下载后保存名称 |
| uri | 文件在互联网的地址 |
| name | 文件展示名称 |



### 2.26 实时查询当前在播的节目列表

#### 2.26.1 编程
```js
var allList = JSBridge.getRealTimePlayListSync();
```

应答
```json
{
	"timeID": 3,
	"slave": {
		"id": 14,
		"currentElement": 0,
		"playType": "uri",
		"local": true,
		"playName": "connect web",
		"uri": "https://kuaipin.wifi-town.com/kp/connect.html",
		"files": 0,
		"elements": []
	},
	"main": {
		"id": 3,
		"currentElement": 0,
		"playType": "pdf",
		"local": false,
		"playName": "js",
		"files": 2,
		"elements": [{
			"type": 2,
			"key": 0,
			"name": "快屏-简介.pdf",
			"uri": "http://cdn.wifi-town.com/xx.pdf",
			"path": "xx.pdf"
		}, {
			"type": 2,
			"key": 1,
			"name": "快屏云柜 - 微信智能存包柜产品介绍.pdf",
			"uri": "http://cdn.wifi-town.com/xx2.pdf",
			"path": "xx2.pdf"
		}]
	},
	"presentation": {
		"id": -1,
		"currentElement": 0,
		"playType": "uri",
		"local": false,
		"playName": "默认网页",
		"uri": "https://kuaipin.wifi-town.com/kp_lan",
		"files": 0,
		"elements": []
	}
}

```

实时查询当前在播的节目列表,根据节目单显示区域可分为main,slave,presentation三组。
#### 2.26.3 显示区域说明
|字段|说明|
|:----- |:------|
| timeID | 主屏前端节目单ID，根据时间段确定 |
| main | 主屏默认显示的前端节目单 |
| slave | 默认不显示的后端节目单，可通过JSBridge.scrollPage('slave')切换到前端 |
| presentation | 多屏环境下，其他屏幕显示的节目单 |


### 2.27 向播放单实时删除已存在条目(默认不保存)

#### 2.27.1 编程
```js
var who = {playlist: 14, key: 0};
JSBridge.removePlayListFile(who);
```

向播放单中删除指定编号的节目。
#### 2.27.2 输入字段说明
|字段|说明|
|:----- |:------|
| playlist | 该条目对应的播放单ID |
| key | 节目的编号， 可通过getRealTimePlayListSync获取节目的key字段 |


### 2.28 保存播放单

#### 2.28.1 编程
```js
var who = {playlist: 14};
JSBridge.savePlayListFiles(who);
```

保存通过removePlayListFile/addPlayListFile临时添加、移除的内容同步到设定的播放单


### 2.29 启用4G网络流量开关

#### 2.29.1 编程
```js
var state = {enabled: true};
JSBridge.setMobileDataEnabled(state);
```

注意：由于安卓不同版本策略的不同，可能有些平台无法工作，需要通过调用openApp进入设置界面手动设置。


### 2.30 启用Wifi开关

#### 2.30.1 编程
```js
var state = {enabled: true};
JSBridge.setWifiEnabled(state);
```

注意：由于安卓不同版本策略的不同，可能有些平台无法工作，需要通过调用openApp进入设置界面手动设置。



### 2.30 启停多屏显示开关

#### 2.30.1 编程
```js
var state = {enabled: true};
JSBridge.setPresentationEnabled(state);
```

启停多屏显示开关, 此API当前只是修改运行参数，需要调用应用重启功能来加载新配置



### 2.31 设置RK3288平台的定时开关机功能

#### 2.31.1 编程
```js
var state = {lockTime: "22:00", startTime:"06:00"};
JSBridge.setRK3288Clock(state);
```

设置RK3288平台的定时开关机功能，需要主板开发商的板子兼容56iq标准

#### 2.31.2 输入字段说明
|字段|说明|
|:----- |:------|
| lockTime | 关机时间 |
| startTime | 开机时间 |




### 2.32 发送按键

#### 2.32.1 编程
```js
var state = {action: "press", key:"3"};
JSBridge.postKey(state);
```

发送虚拟按键到安卓系统

#### 2.32.2 action输入字段说明
|字段|说明|
|:----- |:------|
| press | 按键类型为按压 |
| down | 按键类型为按下 |
| up | 按键类型为松开 |

key 字符串，兼容安卓API“KeyEvent.keyCodeFromString”即可，参考：
https://developer.android.com/reference/android/view/KeyEvent#keyCodeFromString(java.lang.String)




### 2.33 下载文件

#### 2.33.1 编程
```js
var fileInfo = {
	"url": "https://html5videoformatconverter.com/data/images/happyfit2.mp4",
	"file": "happyfit2.mp4",
	"timeout": 8000
};
JSBridge.downloadFile(fileInfo, function(value){
	console.log("Download progress: " + value + "%");
});
```

下载url所指向的文件到file设定的存储目录,回调函数为下载百分比。

#### 2.32.2 输入字段说明
|字段|说明|
|:----- |:------|
| url | 文件在互联网上地址，仅支持http/https协议 |
| file | 文件在机顶盒上的存储路径,sd卡路径从/mnt/sdcard/Cabinet/开始 |
| timeout | 最大超时，单位毫秒 |


## 3. FAQ
  
####  3.1我需要增加一些API 可以怎样提交
   可通过下方的邮件，将您的需求发送给开发者。


## 4.0 联系开发者
----

```sh
email: root@wifi-town.com
QQ: 1694900623
```

**Thank you!**


