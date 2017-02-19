title: android feast
date: 2016-01-14
categories: Linux
tags: [advanced, play]
---
![Android Feast](pic/Android_Feast.png)
我的设备我做主，我的地盘我是老大……

## SDK
adb（Android Debug Bridge），Win下面一般装个驱动，下载exe就可以，稍微全一点的下载个androidSDK。Ubuntu下几条命名就可以[`$ apt-get install ubuntu-device-flash phablet-tools`](https://developer.ubuntu.com/en/start/ubuntu-for-devices/installing-ubuntu-for-devices/)
注：我的识别稍有问题，连手机前后执行两次`lsusb`，连手机后多出来的一行："Bus 003 Device 008: ID **29a9**:701a"，主要是找这个ID，还是上代码吧：
```shell
$ cat ~/.android/adb_usb.ini 
0x29a9

$ sudo adb devices
List of devices attached 
37c0c28f	device
```
`adb`有了，`fastboot`也有了，fastboot是标准的安卓刷机工具，然而你在中国，标准很多时候是标准不可用。


## YunOS
我爸在家就看个电视，过分么？  广电总局敛财，YunOS作伥，然后仅以此部分献给我的两个周末。
后门是什么：我爸说，后门就是我看电视的应用默默的都被更新掉了。我要不要感谢下，让我爸都对后门理解的如此深刻。
闲话少叙，那个时候网上有个流传的压缩包，里面有个bat，我就下载打开瞅了瞅，GET新技能：
```shell
adb connect 0.0.0.0:5555
adb shell pm block com.wei.hu.zuo.chang
```
原来电视盒子可以用adb远程连接，pm是package manage，我就adb连上盒子，然后把升级等乱七八糟的该block的block掉，用电脑直接adb install了几个apk应用。电视又可以正常看了…

### GET OUT
看了大约5天吧，一点都不消停，真是的…  害我连着两礼拜回家。
这回是很多应用都没有了，但是当贝市场还在，先看电视。第二天习惯性的先去盒子的官网看了看，厂家在云盘放出了ROM和刷机工具，这下没什么顾虑的了……
直接root，然后统统给我滚出去，电视淘宝什么鬼，走了您勒，不送。我尝试装了第三方桌面，自带的也没放过，然后果然被玩坏了……
软件问题都不是问题，双公头USB线，懒的出去买，快递太慢，直接自己动手，旧的线找两根剪断按颜色接上，找来以前用的带指示灯的充电头两个，测试了下（一个插上家用电源，另一个充电头灯正常亮表示没有问题，USB线是四根，两根电源两根数据，灯亮表示电源的两根没有错）。
然后正常刷机，下载rom稍微久点，刷机不足五分钟。
 ROOT-->UNINSTALL-->INSTALL  两个市场，两三点播，两三直播，找了找没有设计用来替换的桌面，作罢。该滚的都滚了，以后永不升级，我的地盘我做主。

结果是：电视猫转换成了系统应用，整个默认桌面都是空荡荡的，装了个第三方桌面，唯一不足是home键没绑定，止戈为武，鸣金收兵。

## JianGuo
“第三方预装应用都能卸载”，我真的想相信这句话，结果大家都知道，我想多了。只好要得可口自己动手，毕竟最近学习了不少新技能。
开启开发者模式，常用的命令如下：
```shell
adb shell ps
adb shell pm list package
adb shell pm block xx.xx.xx  # before android 5.0
adb shell pm hide xx.xx.xx  # android 5.0+
```
local shell权限不够，需要连上电脑，开启USBDebug，可以成功hide不想要的拉圾，如搜狗广告输入法。锤子以前内置触宝输入法，后面升级到2.5.0后内置了与之匹配的250输入法，我为此升级付出的代价是使用省电模式一天多。

### 中立
我不粉也不黑，但我想说点啥。。。

* 安全中心不安全：锤子的安全中心，平心而论是下了功夫的，从短信联系人位置信息到联网，都可以直接管，然而有一条，锤子家的不管，锤子家的权限全开。锤子家定制的权限全开，搜狗输入法加个后缀变成定制的，权限全开，安全中心管不着。
我想说的是，三权独立有点大，但一个小小手机敢不敢不这样……

* 清理好玩么：左手清理右手充电宝，好玩么？安卓的诱导安装和唤起链我不想说，搜狗输入法我确定取消了启用，然而一次又一次被活动在后台，清理是为了测试唤醒么？

* 农历是中文：中文外强制隐藏农历，多么鸡肋的设计…  要看农历的你还怕他看到地道的，谷歌英文日历农历就很地道，好的需求SE是多么的重要~

## jar 甜点
最后给大餐加点料，[View and control your android device on PC](https://github.com/xSAVIKx/AndroidScreencast)。  `adb devices`显示连接到设备后，从github上下载上述jar，然后`java -jar androidscreencast-0.0.5.1S.jar`
除了慢点，功能都有了，看到的java大牛，让梦想飞起来吧~

## END
手机慢，电池不够用么？  这年头电池很不错了，谁能告诉我，明明能作出好东西，为什么没有真正做出来几个好东西…
