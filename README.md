
# RaftLink��Ϣ�����ն� WebApp���ָ��

![xiaofu.png](https://www.dropbox.com/s/jq6b9tn9ngzd2oz/xiaofu.png?dl=0&raw=1)
  
###### Guangzhou Fuhai Software Technology Co., Ltd.
###### �������ں�����������޹�˾ ��Ʒ
[Company website http://www.wifi-town.com](https://www.wifi-town.com/)


#### Histroy
|Version|Revision|Author|Date|
|:----- |:-------|:-----|----- |
|v1.0 |First initial version|Easion|2019-08-08 |


> ��վ: 
**kuaipin.wifi-town.com**


## 1. ����
  [RaftLink](https://raftlink.1688.com/)�ǹ������ں�����������޹�˾��ע���̱�.
  
    RaftLink��Ϣ�����ն��ǻ��ڰ�׿����Ϣ����Ӧ�á��û������Զ�����ҳ���õ�Ƭ����Ƶ�������͵Ķ�ý���ļ�������ʽ��Ĭ�ϵİ���ÿ6Сʱһ��ʱ��Σ���ȫ�컮�ֳ�4��ʱ��Σ�ÿ��ʱ��ο��Բ�����ͬ�����ݡ�
  
    RaftLink��Ϣ�����ն˿�֧��2��������Ļ�����ǽ����û�����WebApp�ķ�ʽ����������Ϣ����Ӧ�ã�����ͨ��WEB JavaScript����ʵ�ֲ�ͬ��Ļ���л������ŵ��Ķ�ȡ���޸ġ��ı�ת�����ȹ��ܡ�
  
    �����豸�ṩJavaScriptתnative���ܣ�������΢�Ź��ںŵ�JSAPI���ܣ�ͨ��JS�������ԭ���ײ�ʵ�֣��豸��ƫ����WEB�Եײ�������ܵĲٿأ��Ӷ�������ɲ�Ʒ�����߲����ٵ���������
    ���������豸�����ṩ����ͨ�û�����JS����Ȩ�޲����������ߵ���Դ������ӿڵ�ǩ��У�������
    
[RaftLink�豸�����ַ](https://raftlink.1688.com/)
 
���������ǶԸ�������޸�:
  - ����RaftLink���ͨѶ��ܣ���Ȼ���浥�������мܹ���
  - �ṩUI���û��������в�����
  - �ṩ�ӿڸ��û��ϴ��ű������á�
  - �ṩAPI���û����Դ����Լ���WEB�ڵ㡣
  - ��ȫ���libc�ķ�װAPI����socket�ȡ�
  - ��Ϊ������ṩ�豸API��HomeKit���ء�
  - NodeJS���ݲ㣬�� Buffer,FS,EventEmitter,jsonfile��ģ��API��
  - �ṩ���ڲ���API
  - �ṩmosquitto��libcurl��װAPI��
  - 
 ## 1.���������

��������⣬�ɴ�https://kuaipin.wifi-town.com/kp/���������ļ���
```html
<head>
<--- ʡ��������Ϣ   --->
<script src="/kp/dsbridge.js"> </script>
<script src="/kp/fly.js"></script>
<script src="/kp/engine-wrapper.js"></script>
<script src="/kp/adapter.js"></script>
</head>
```

����Ƿ�֧��JSBridge
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

 ## 2.���API
  
**���ӵ�RaftLink�������磬�����������fuhai.gw�����豸IP��ַ:**
```mermaid
������룺
Ӧ��-->> �ɰ�װӦ��-->>RaftLink Javascript Engine-->չ������^-->�����װ��ť
```
#### ע��ص�
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
	//JSBridge.Speak('�ҵ�HomeKit�豸!');
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

### 2.2 ��ѯϵͳ��Ϣ

#### 2.2.1 ����
```js
var sysInfo = JSBridge.getSystemInfoSync();
console.log("getSystemInfoSync "+ JSON.stringify(sysInfo) );
```

#### 2.2.1 �����ֶ�˵��
|�ֶ�|˵��|
|:----- |:------|
| |  |
| |  |
| |  |

### 2.2 ��ѯ����״̬

#### 2.2.1 ��̼ܹ�
```js
function queryNetState()
{
    var netinfo = JSBridge.getNetworkInfo();
	console.log("netinfo "+ JSON.stringify(netinfo) );
	if (netinfo.connected === true)
	{
	  console.log("�Ѿ����ӵ�����");
	}
	else{
	  console.log("�����ѶϿ�");
	}
}
```


### 2.2 ��ѯ����״̬

#### 2.2.1 ��̼ܹ�
```js
function queryNetState()
{
    var netinfo = JSBridge.getNetworkInfo();
	console.log("netinfo "+ JSON.stringify(netinfo) );
	if (netinfo.connected === true)
	{
	  console.log("�Ѿ����ӵ�����");
	}
	else{
	  console.log("�����ѶϿ�");
	}
}
```

### 2.2 ������Ļ�л�

#### 2.2.1 ���
```js
JSBridge.scrollPage('slave');
setTimeout(function(){
	JSBridge.scrollPage('main');
},60000)
```
#### 2.2.1 �������˵��
|�ֶ�|˵��|
|:----- |:------|
| main|  �л�������|
| slave| �л������� |


### 2.2 �̼�����

#### 2.2.1 ��̼ܹ�
```js
JSBridge.fwUpdate();
```


### 2.2 ��ѯ����״̬

#### 2.2.1 ��̼ܹ�
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

#### 2.2.1 ��̼ܹ�
```js

var opt = {};
opt.host = "webp2p.wifi-town.com";
opt.domain = sysInfo.DeviceID;
opt.port = 6443;

var p2pInfo = JSBridge.getWebP2pInfoSync();
if (p2pInfo.autoboot !== true)
{		
	//opt.autoboot = false; //�����Զ�����
	opt.focus = false; //ǿ�Ʊ���		
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


### 2.2 ���̿ռ�

#### 2.2.1 ���
```js
var disk = JSBridge.getDiskSpace();
$("#total" ).html("�洢 ����" + disk.free + "M,�ܹ�" + disk.total+"M");
```


### 2.2 ��ȡWifi AP�б�

#### 2.2.1 ���
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


>��ͼ�������������ҳ�棺.



���������û��ϴ����ֽű����ֱ��ǡ�������ű����������ݽű����������ر���������ļ���.

|����|����|
|:----- |:------|
|������ű�|ϵͳĬ�����еĽű��ļ� |
|���ݽű�|������ű������ڻ��߳��ּ��ش��󣬼��������ݽű������������ѻָ����ű��������� |
|���ر���������ļ�|�û��ϴ��������ļ���·��ͨ��ȫ�ֱ���scriptConfigFile���ʣ������json��ʽ����ͨ��jsonfile���н������߱��� |


#### 2.2 ����
console.log�������������ϵͳ��־logcat�С�
���¼��web����̨���˵�չ����������־��Ŀ¼��   

#### 2.2 ���ϻָ�
�ű�����������־�д�ӡ����Ķ�ջ��Ϣ���ɸ��ݶ�ջ��ʾ��Ϣ�����޸ġ�



## 3. FAQ
  
####  3.1�ҵĽű���Ҫ�����������ļ�����ô�죿
   ��ͨ��curlģ������js�ű����浽���أ��������ű����롣

#### 3.2 fs ģ��֧��ģ��NODEJS���첽API��
  ��֧��
  
## 4.0 ��ϵ������
----

```sh
email: root@wifi-town.com
QQ: 1694900623
```

**Thank you!**


