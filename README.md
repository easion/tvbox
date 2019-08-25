
# RaftLink信息发布终端 WebApp编程指南

![xiaofu.png](https://www.dropbox.com/s/jq6b9tn9ngzd2oz/xiaofu.png?dl=0&raw=1)
  
###### Guangzhou Fuhai Software Technology Co., Ltd.
###### 广州市孚海软件技术有限公司 出品
[Company website http://www.wifi-town.com](https://www.wifi-town.com/)


#### Histroy
|Version|Revision|Author|Date|
|:----- |:-------|:-----|----- |
|v1.0 |First initial version|Easion|2019-08-08 |


> 网站: 
**kuaipin.wifi-town.com**


## 1. 概论
  [RaftLink](https://raftlink.1688.com/)是广州市孚海软件技术有限公司的注册商标.
  
    RaftLink信息发布终端是基于安卓的信息发布应用。用户可以自定义网页、幻灯片、视频三种类型的多媒体文件播出方式，默认的按照每6小时一个时间段，将全天划分成4个时间段，每个时间段可以播出不同的内容。
  
    RaftLink信息发布终端可支持2个虚拟屏幕，我们建议用户采用WebApp的方式开发您的信息发布应用，可以通过WEB JavaScript代码实现不同屏幕的切换、播放单的读取和修改、文本转语音等功能。
  
    我们设备提供JavaScript转native功能，它类似微信公众号的JSAPI功能，通过JS代码调用原生底层实现，设备更偏重于WEB对底层基本功能的操控，从而快速完成产品的上线并快速迭代开发。
    由于我们设备并非提供给普通用户，对JS调用权限并不检查调用者的来源，无需接口的签名校验操作。
    
[RaftLink设备购买地址](https://raftlink.1688.com/)
 
下面是我们对该软件的修改:
  - 融入RaftLink软件通讯框架，仍然保存单进程运行架构。
  - 提供UI给用户配置运行参数。
  - 提供接口给用户上传脚本和配置。
  - 提供API让用户可以创建自己的WEB节点。
  - 更全面的libc的封装API，如socket等。
  - 作为输入端提供设备API给HomeKit网关。
  - NodeJS兼容层，如 Buffer,FS,EventEmitter,jsonfile等模拟API。
  - 提供串口操作API
  - 提供mosquitto，libcurl封装API。
  - 
 ## 1.导入基础库

导入基础库，可从https://kuaipin.wifi-town.com/kp/下载下面文件。
```html
<head>
<--- 省略其他信息   --->
<script src="/kp/dsbridge.js"> </script>
<script src="/kp/fly.js"></script>
<script src="/kp/engine-wrapper.js"></script>
<script src="/kp/adapter.js"></script>
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
  
**连接到RaftLink所在网络，在浏览器输入fuhai.gw或者设备IP地址:**
```mermaid
点击进入：
应用-->> 可安装应用-->>RaftLink Javascript Engine-->展开倒立^-->点击安装按钮
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

#### 2.2.1 调用
```js
var sysInfo = JSBridge.getSystemInfoSync();
console.log("getSystemInfoSync "+ JSON.stringify(sysInfo) );
```

#### 2.2.1 返回字段说明
|字段|说明|
|:----- |:------|
| |  |
| |  |
| |  |

### 2.2 查询网络状态

#### 2.2.1 编程架构
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


### 2.2 查询网络状态

#### 2.2.1 编程架构
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

### 2.2 主从屏幕切换

#### 2.2.1 编程
```js
JSBridge.scrollPage('slave');
setTimeout(function(){
	JSBridge.scrollPage('main');
},60000)
```
#### 2.2.1 输入参数说明
|字段|说明|
|:----- |:------|
| main|  切换到主屏|
| slave| 切换到从屏 |


### 2.2 固件升级

#### 2.2.1 编程架构
```js
JSBridge.fwUpdate();
```


### 2.2 查询网络状态

#### 2.2.1 编程架构
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
plPics.demos = "js wrote";
plPics.slideshowType = "default";
plPics.slideshowInterval = 10;
plPics.data = {};

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
### 2.2 WebP2P

#### 2.2.1 编程架构
```js

var opt = {};
opt.host = "webp2p.wifi-town.com";
opt.domain = sysInfo.DeviceID;
opt.port = 6443;

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


### 2.2 磁盘空间

#### 2.2.1 编程
```js
var disk = JSBridge.getDiskSpace();
$("#total" ).html("存储 空闲" + disk.free + "M,总共" + disk.total+"M");
```


### 2.2 获取Wifi AP列表

#### 2.2.1 编程
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


>下图是软件基本配置页面：.



程序允许用户上传三种脚本，分别是“主程序脚本”，“备份脚本”，“本地保存的配置文件”.

|类型|作用|
|:----- |:------|
|主程序脚本|系统默认运行的脚本文件 |
|备份脚本|主程序脚本不存在或者出现加载错误，即启动备份脚本，可用于灾难恢复、脚本自身升级 |
|本地保存的配置文件|用户上传的配置文件，路径通过全局变量scriptConfigFile访问，如果是json格式，可通过jsonfile进行解析或者保存 |


#### 2.2 调试
console.log的输出将保存在系统日志logcat中。
请登录到web控制台，菜单展开后点击“日志”目录。   

#### 2.2 故障恢复
脚本出错，会在日志中打印出错的堆栈信息，可根据堆栈提示信息进行修改。



## 3. FAQ
  
####  3.1我的脚本需要导入其他的文件，怎么办？
   可通过curl模块下载js脚本保存到本地，再重启脚本导入。

#### 3.2 fs 模块支持模拟NODEJS的异步API吗
  不支持
  
## 4.0 联系开发者
----

```sh
email: root@wifi-town.com
QQ: 1694900623
```

**Thank you!**


