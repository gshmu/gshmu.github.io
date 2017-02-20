title: wake on lan/wan
date: 2016-01-11
categories: Config
tags: [config, wol, play]
---
我是怎么远程开启我家电脑的WOL：远程登录后只要没有限制，大家都会关机，然而今天我们讨论的话题是远程开机——WakeOnLan…

## APP
WOL这款应用是跨平台的，github上有个用perl写的，原先perl写的不支持域名，不过你可以找到我修改后支持域名的那款。
那次分享我使用的手机远程开启我家电脑，之所以选择手机是因为手机方便，选择的应用是：net.mafro.android.wakeonlan (Google Play 的应用id，搜WOL有好几款，我选这个的原因是小，需要权限少)

### Let's GO
在应用界面配上我家路由器的IP(我用DDNS有一个免费域名)，Port还有需要开机的MAC，如下图：
![WOL APP](/pic/Wake_On_Lan.png)
填好表单，点击发送，会产生一个“Magic Packet”，并发出…

### DDNS
TP-LINK路由器一般默认就有，注册账号，在路由器配置自动登录即可，我家宽带是拨号上网，没有固定IP(但庆幸的是是一个外网IP，电信曾 调整成内网映射IP，我投诉后又恢复成外网IP)，DDNS负责登录后将路由器外网地址映射到一个域名上，如我的是xxx.oicp.net，通 过DNS查询就获得了路由器的真实地址，为了保证可用性，我将路由联网模式改成了：总是连接，而不是默认的按需连接(按需连接，只会在内部有网络 访问时才路由器才真正联网，我需要从外部连，所以改成总是)

### Magic Packet
具体定义请参考维基百科，一个具有特殊头部的UDP包，主要信息是网卡MAC信息重复三次

## UDP转发
发出的“Magic Packet”通过网络到达了路由器，如果你家路由器支持广播，那么恭喜你，你将该条消息直接在路由器内网广播即可，默认端口是9或者7…
如果不支持广播，先是设置端口转发，你家电脑需要设置静态IP，或者通过路由器绑定一个IP，同时你还需要ARP绑定，一切配置 OK，“Magic Packet”可以到达电脑网卡了…

## Wake
问题成功从Wake On Wan 转化成 Wake On Lan，进入电脑BIOS设置下，允许网卡唤醒(只要你家的电脑不是古董，这个功能应该都有，还有就是网卡也需要支持)，如图：
![BIOS SETTING](/pic/BIOS_WOL.BMP)
注：Windows 可能需要进系统，网卡设置允许“Magic Package”魔包唤醒，如下图：
![Windows SETTING](/pic/OS_WOL.png)

## 安全&应用
Lan是相对安全的，路由器可以通过MAC过滤，不要泄漏你的MAC等信息。这个仅能开机和关机，对于几乎不会关机的服务器来说，开机没什么不安 全的。（确保你的PC像服务器那样安全）
最佳应用是用在托管机房的远程开机，我们机房的测试机等也可以采用……

# 总结
本文从手机发出UDP包，简述了远程开机原理及实现，如果你需要配置远程开机，可能需要将整个过程倒过来，先在局域网内广播唤醒，最后用手机数据 流量或其他电脑远程唤醒(开机或从待机欢迎)。