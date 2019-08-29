
# RaftLink信息发布终端 安装说明

![xiaofu.png](xiaofu.png)
  
###### Guangzhou Fuhai Software Technology Co., Ltd.
###### 广州市孚海软件技术有限公司 出品
[Company website http://www.wifi-town.com](https://www.wifi-town.com/)


#### Histroy
|Version|Revision|Author|Date|
|:----- |:-------|:-----|----- |
|v1.0 |First initial version|Easion|2019-08-26 |


> 网站: 
**kuaipin.wifi-town.com**


## 1. 概论
  [RaftLink](https://raftlink.1688.com/)是广州市孚海软件技术有限公司的注册商标.
  
RaftLink信息发布终端是基于安卓的信息发布应用。用户可以自定义网页、幻灯片、视频三种类型的多媒体文件播出方式，默认的按照每6小时一个时间段，将全天划分成4个时间段，每个时间段可以播出不同的内容。

在安装或者卸载操作前，您需要在您的PC或者Mac电脑上安装adb软件。请参考网络相关说明。播放器终端在启动的时候，屏幕左上角会显示出设备的IP，您可以尝试通过adb来连接它。
如果您还没有安装这个软件，可通过上级路由器的DHCP客户端列表获取设备的IP地址。

#### 连接指令
假设播放器终端的当前IP地址为192.168.1.22
```bash
adb connect 192.168.1.22
```
  
## 2. 卸载旧版本
```bash
adb uninstall com.wifitown.cabinet
```

## 3. 安装

假设您得到的安装文件是rl-screen.apk
```bash
adb install rl-screen.apk
```

## 4.0 联系开发者
----

```sh
email: root@wifi-town.com
QQ: 1694900623
```

**Thank you!**


