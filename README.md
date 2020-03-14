
# RaftLink��Ϣ�����ն� WebApp���ָ��

![xiaofu.png](xiaofu.png)
  
###### Guangzhou Fuhai Software Technology Co., Ltd.
###### �������ں�����������޹�˾ ��Ʒ
[Company website http://www.wifi-town.com](https://www.wifi-town.com/)


#### Histroy
|Version|Revision|Author|Date|
|:----- |:-------|:-----|----- |
|v1.0 |First initial version|Easion|2019-08-26 |
|v1.1 |���Ӷ���������API��2.18�¼��Ժ�|Easion|2020-03-14 |


> ��վ: 
**kuaipin.wifi-town.com**

> Ĭ�ϲ��Ի������°汾�������ַ��
**https://kuaipin.wifi-town.com/kp/connect.html**


## 1. ����
  [RaftLink](https://raftlink.1688.com/)�ǹ������ں�����������޹�˾��ע���̱�.
  
RaftLink��Ϣ�����ն��ǻ��ڰ�׿����Ϣ����Ӧ�á��û������Զ�����ҳ���õ�Ƭ����Ƶ�������͵Ķ�ý���ļ�������ʽ��Ĭ�ϵİ���ÿ6Сʱһ��ʱ��Σ���ȫ�컮�ֳ�4��ʱ��Σ�ÿ��ʱ��ο��Բ�����ͬ�����ݡ�
  
RaftLink��Ϣ�����ն˿�֧��2��������Ļ�����ǽ����û�����WebApp�ķ�ʽ����������Ϣ����Ӧ�ã�����ͨ��WEB JavaScript����ʵ�ֲ�ͬ��Ļ���л������ŵ��Ķ�ȡ���޸ġ��ı�ת�����ȹ��ܡ��ǳ��ʺϲ�������Angular/Vue/ReactJS+WebSocket�������������ĵ�ҳ��Ϣ����ϵͳ��
  
�����豸�ṩJavaScriptתnative���ܣ�������΢�Ź��ںŵ�JSAPI���ܣ�ͨ��JS�������ԭ���ײ�ʵ�֣��豸��ƫ����WEB�Եײ�������ܵĲٿأ��Ӷ�������ɲ�Ʒ�����߲����ٵ���������
    
    ���������豸�����ṩ����ͨ�û�����JS����Ȩ�޲����������ߵ���Դ������ӿڵ�ǩ��У�������
    
[RaftLink�豸�����ַ](https://raftlink.1688.com/)
 
  - 
 ## 1.���������

��������⣬�ɴ� [https://kuaipin.wifi-town.com](https://kuaipin.wifi-town.com) ���������ļ���
```html
<head>
<--- ʡ��������Ϣ   --->
<script src="https://kuaipin.wifi-town.com/kp/dsbridge.js"> </script>
<script src="https://kuaipin.wifi-town.com/kp/fly.js"></script>
<script src="https://kuaipin.wifi-town.com/kp/engine-wrapper.js"></script>
<script src="https://kuaipin.wifi-town.com/kp/adapter.js"></script>
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
  
**JSBridge��֧���¼��ص�**
```mermaid
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

#### 2.2.1 ��̵���
```js
var sysInfo = JSBridge.getSystemInfoSync();
console.log("getSystemInfoSync "+ JSON.stringify(sysInfo) );
```

Ӧ��
```json
{
	"last_version": 42,
	"last_demos": "֧�ֶ�����ʾ",
	"DeviceID": "r1hWbFsnN1558053123",
	"DeviceQR": "http://kuaipin.wifi-town.com/api/serial_query/N1C6K56GCL#BIND_r1hWbFsnN1558053123",
	"serial": "N1C6K56GCL",
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
		"name": "������Ļ"
	}, {
		"id": 1,
		"name": "HDMI ��Ļ"
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

#### 2.2.2 �����ֶ�˵��
|�ֶ�|˵��|
|:----- |:------|
| versioncode| ��ǰ����İ汾��|
| last_version|  ��ǰ���µĹ̼��汾|
| last_demos|  �̼���������|
| DeviceID|�ƶ˷�����豸Ψһ����|
| DeviceQR| �豸��Ϣ��ѯ�����ע���ά��|
| serial| Ӳ��Ψһ���к�|
| DeviceRole| �豸���ͣ����ڲ�ͬ����;��Ĭ��Ϊlan���̶�|
| slaveScreen| �����Ĳ��ŵ�ID|
| ip| �豸��IP��ַ|
| port| �豸WEB���ʶ˿�|
| expired| �����Ȩ�Ƿ��Ѿ�����|
| wifiEnabled| �Ƿ�ʹ��WIFI|
| model| ��׿��Ʒmodel|
| product| ��׿��ƷID|
| display| ��ʾ��Ϣ|
| sdk_int| ��׿SDK�汾��|
| dpi| ��Ļ��ʾ�ܶȣ�������|
| widthPixels| ����Ļ���أ�������|
| bluetoothEnabled| �Ƿ�����������|
| downloadTimeout |  Ĭ���������ʱ(��������)|
| mobileDataEnabled |  �Ƿ��Ѿ�����4G������������|
| mainScreen | ������ǰ���ŵ�ID  |
| slaveScreen | ��̨��ǰ���ŵ�ID(Ĭ�����أ��ɼ���)  |
| presentationScreen | �������Ի����£�������Ļ��ǰ���ŵ�ID  |
| displayCount | ������ʾ�����£���Ļ����  |
| displayList | ������ʾ�����£�������Ļ��Ϣ  |


��Ƶ�Ĳ��ŵ�ID�ֱ���0��1��2��3.��Ӧ00:00-23:59:59ÿ6СʱΪһ�ε�4��ʱ��Ρ�
�������Ե�ǰ��Ҫ����ƽ̨ΪRK3288��֧���Զ����֡�Ͷ�͡�


### 2.3 ��ѯ����״̬

#### 2.3.1 ��̼ܹ�
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

```json
{
	"connected": true,
	"type": "4g",
	"simOperator": "46001",
	"networkType": "LTE",
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

#### 2.3.2 �����ֶ�˵��
|�ֶ�|˵��|
|:----- |:------|
| connected | �����Ƿ��Ѿ����� |
| type | ��ǰ�������ͣ���wifi,lte |
| networkType | �ƶ���������,��2g,3g,4g |
| simOperator | �ƶ�������Ӫ��ID |
| traffic | ����ͳ��,��λΪ�ֽ������߱��ĸ��� |

### 2.4 ������Ļ�л�

#### 2.5.1 ���
```js
JSBridge.scrollPage('slave');
setTimeout(function(){
	JSBridge.scrollPage('main');
},60000)
```

ע�⣺����Ļ��WEBҳ���л�������ҳ�棬�������뽹���Ѿ��ı䡣
JS�����ܻ�ȡ�û��İ�����Ϣ����ʹ������߼����ҳ����лء�

#### 2.4.1 �������˵��
|�ֶ�|˵��|
|:----- |:------|
| main|  �л�������|
| slave| �л������� |
| toggle| ����ģʽ |


### 2.5 �̼�����

#### 2.5.1 ��̼ܹ�
```js
JSBridge.fwUpdate();
```
�Զ���ת���������棬������°汾���Զ��������������������ʼ���档
�ɸ��ݻ�ȡϵͳ��ϢAPI���ж��Ƿ���Ҫ֧�����������

### 2.6 ���ŵ��Ķ�ȡ������

#### 2.7.1 ��̼ܹ�
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

/*�������ص����أ���Ƶ/ͼƬ����ͬ���Ľṹ*/
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
���ŵ�֧�����ߵ��ļ�����http https��ͷ��Э�飬������ΪͼƬ������Ƶ��
�����������ʱ����������ؽ����Զ�������غ�������

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

#### 2.6.2 �����ֶ�˵��
|�ֶ�|˵��|
|:----- |:------|
| channel|  ���ŵ�ID����ΧΪ0-3,14|
| data | ���ŵ����ݣ���дnull��ʾɾ�����ŵ� |
| data.name| ���� |
| data.media_type| ���ͣ��ֱ��� uri,media,slideshow|
| data.local| �Ƿ���ñ��ص��ļ����� |
| data.data | �������� |

### 2.7 WebP2P


#### ngrok����������̳̣�
[https://luozm.github.io/ngrok](https://luozm.github.io/ngrok)


#### 2.7.1 ���

����/����web�������
```js

var opt = {};
opt.host = "webp2p.example.com";
opt.domain = sysInfo.DeviceID;
opt.port = 1234;

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

```json
{
	"status": 0,
	"host": "webp2p.example.com",
	"domain": "Buo7QUnd415539",
	"port": 1234,
	"autoboot": false
}
```

ֹͣweb�������:
```js
JSBridge.stopWebP2P();
```


#### 2.7.2 ����/����ֶ�˵��
|�ֶ�|˵��|
|:----- |:------|
| host|  NGROK����������ַ|
| port| NGROK�����������Ӷ˿� |
| domain| ��ǰ������������ |
| autoboot| �Ƿ񿪻��Զ������˷��� |
| focus| �Ƿ�ǿ��(force)���� |

### 2.8 ���̿ռ�

#### 2.8.1 ���
```js
var disk = JSBridge.getDiskSpace();
$("#total" ).html("�洢 ����" + disk.free + "M,�ܹ�" + disk.total+"M");
```

��ȡ��ǰ�豸�洢�ռ�������Ϣ����λΪM�����ֽڣ�

```json
 {"total":12345,"free":11685}
```

### 2.9 ��ȡWifi AP�б�

#### 2.9.1 ���
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

��ȡ���õ�AP�б�

### 2.10 �˳�����(�Զ�����)

#### 2.10.1 ���
```js
JSBridge.exitProgram();
```
�˳���ǰ�������޸��˲��ŵ����ɵ��ô�API����������������µĲ��ŵ��ļ��ء�


### 2.11 �ػ�

#### 2.11.1 ���
```js
JSBridge.powerOff();
```



### 2.12 ����

#### 2.12.1 ���
```js
JSBridge.reboot();
```

### 2.13 ����ת����

#### 2.13.1 ���
```js
JSBridge.Speak("��� ����");
```

### 2.14 ��������

#### 2.14.1 ���
```js
JSBridge.setVolume({type:'notify', val: '7'});
```


#### 2.14.2 ����/����ֶ�˵��
|�ֶ�|˵��|
|:----- |:------|
| type |  notifyΪ֪ͨ������musicΪý������ |
| vol| ��������������ջ�ȡϵͳ��Ϣ��������Χ��д,incΪ���ӣ�decΪ���� |

### 2.15 MDNS��ѯ

#### 2.15.1 ���
```js
JSBridge.startLocalServiceDiscovery({type: "_hap._tcp."}, function(list){
	console.log("startLocalServiceDiscovery "+ JSON.stringify(list) );
});
```
��ѯ�Ľ����2.1�½�ע���MDNS�ص�������


### 2.16 ִ������

#### 2.16.1 ���
```js
JSBridge.doExecCommand("/system/xbin/cpustats");
```
����ָ������͵�һ���߳��첽ִ�У����Բ�֧�ַ���������ݡ�



### 2.16 TTS����

#### 2.16.1 ���
```js
var voiceSample = {};

voiceSample = JSBridge.getVioceSetting();
voiceSample.speaker = '0';
voiceSample.volume = '9';
voiceSample.speed = '5';
voiceSample.pitch = '5';

voiceSample = JSBridge.getVioceSetting();
console.log("getVioceSetting "+ JSON.stringify(voiceSample) );
voiceSample.speaker = '110'; //��Сͯ����ж�ͯ����
var newSetting = {data: voiceSample};
JSBridge.vioceSetting(newSetting, function(res){
	console.log("vioceSetting "+ JSON.stringify(res) );
	if (res.result == 0)
	{
		JSBridge.Speak('TTS�����Ѿ�����,����������Ч');
	}
	else{
		JSBridge.Speak('TTS�����Ѿ�ɾ��');
	}
});

//ɾ��
newSetting = {data: null};
JSBridge.vioceSetting(newSetting, function(res){
	console.log("vioceSetting "+ JSON.stringify(res) );
	if (res.result == 0)
	{
		JSBridge.Speak('TTS�����Ѿ�����,����������Ч');
	}
	else{
		JSBridge.Speak('TTS�����Ѿ�ɾ��');
	}
});

```
���ðٶ�����tts����Ч������


#### 2.17.2 ����/����ֶ�˵��

ȡֵ��ο�[�ٶ�TTS�ĵ�](https://ai.baidu.com/docs#/TTS-Android-SDK/top)

|�ֶ�|˵��|
|:----- |:------|
| volume|  ������ȡֵ0-15��|
| speed| ���٣�ȡֵ0-15 |
| pitch| ������ȡֵ0-15��Ĭ��Ϊ5����� |
| speaker| ���������� |

��ע��������������Ϊ�ַ���
ɾ��data��дnull����Ϊ��

#### ����
console.log�������������ϵͳ��־logcat�С�
���¼��web����̨���˵�չ����������־��Ŀ¼��   


### 2.18 ��ȡ������Ϣ

#### 2.18.1 ���
```js
var vols = JSBridge.getVolumeSync();
```

��ȡ��ǰ�豸������Ϣ��volΪϵͳ����������������������˼��⡣

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

### 2.18 ��ȡ���������ô洢�ļ��б�

#### 2.18.1 ���
```js
var path = 'picture';
var fileList = JSBridge.getFloderContents(path + '/');
```

��ȡ��ǰָ��Ŀ¼(����ΪString)���ļ��б�,��Ƭ�ϴ�Ϊpicture,��ƵΪvideo,PDFΪpdf��

```json
[{
	"path": "picture/bg-9.jpg",
	"filename": "bg-9.jpg",
	"size": 395203,
	"id": 1,
	"time": 1565775738000
}]
```
#### 2.3.2 �����ֶ�˵��
|�ֶ�|˵��|
|:----- |:------|
| path | ·�� |
| filename | �ļ��� |
| size | �ļ���С |
| id | ��� |
| time | �ļ�����޸�UNIXʱ�������λ���� |


### 2.18 ɾ���ļ�

#### 2.18.1 ���
```js
JSBridge.removeFile("picture/bg-9.jpg");
```

ɾ���趨���ļ�




## 3. FAQ
  
####  3.1����Ҫ����һЩAPI ���������ύ
   ��ͨ���·����ʼ��������������͸������ߡ�


## 4.0 ��ϵ������
----

```sh
email: root@wifi-town.com
QQ: 1694900623
```

**Thank you!**


