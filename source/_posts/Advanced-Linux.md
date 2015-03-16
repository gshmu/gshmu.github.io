title: Advanced Linux
date: 2015-03-10
categories: Linux
tags: [Linux, Advanced, GRUB]
---
本文介绍几个Ubuntu进阶的操作。

## 先晒晒我信攥的电脑
* CPU：E3-1231 V3 (3.4GHz*8 志强四核八线程)
* 内存：Kingston 8G (骇客神条 1866MHz)
* 主板：ASUS B85-PLUS R2.0
* 显卡：NVIDIA GeForce GT 730

CPU，内存没得说，显卡很一般，Linux用完全足够了，如果想超频主板可用Z97K，我不超频也足够了

## 显卡驱动
志强CPU不集成GPU，所以需要独立显卡，显卡驱动是避免不了的。[更多关于显卡的介绍，推荐](https://linuxtoy.org/archives/compare-linux-driver-support-between-three-major-gpus.html)

### 官方闭源驱动
官网按型号下载驱动，然后进入命令行(tty1-6)，关闭Xorg，`sh`装驱动，然后启动Xorg。
```
sudo service lightdm stop
sudo sh NVIDIA-Linux-x86_64-346.35.run 
sudo service lightdm start 
```

### 包管理器直接装
`sudo apt-get install nvidia-331 nvidia-prime nvidia-settings`
331是我装时候仓库中最新的。

### 装完后，不测试下？
工具： glxgears
奇怪，人家都说是评分多少万，为啥我的几乎定在60FPS？ 原来是设置里开了，垂直同步，取消后评分正常。

## GRUB2 引导
（Ubuntu 14.04下）grub引导选项主要是由/boot/grub/grub.cfg控制的，不过这个文件是自动生成的，我们一般编辑/etc/default/grub，然后通过命令`sudo update-grub`应用改动。

### 常用选项
* 启动顺序 `GRUB_DEFAULT` 默认是0
* 延时时间 `GRUB_TIMEOUT` 就是显示grub菜单的时间（单系统默认不显示，开机按Shift即可。）
* 想开机进命令行修改 `GRUB_CMDLINE_LINUX_DEFAULT="text"`
* 添加内核参数 `GRUB_CMDLINE_LINUX=""` 添加你想加的参数，如`reboot=a`

无论修改什么，都别忘了修改后更新grub！

## 新内核
说道内核，你知道你的内核版本么？还记得命令`uname -r`吧。

### 编译内核
我编译过内核，那是因为第一次主板有问题，关机后自动重启，我由于设备教新，所以怀疑驱动等问题。按照wiki我尝试修改了CPU选项和电源选项，不过后来确认是主板问题，跑华硕售后，确认主板有问题，然后换了主板。我不敢大言不惭教大家编译内核，我想说的是新内核源里就有，用新内核不一定需要自己编译。还有我想说的是编译过程比较久，我3.4GHz*8的主频，需要1h这么久。

### 装新内核
就不教大家装包了，大家都会。不过我想提醒大家的是，装新内核时有几个包需要统一装，不要漏了哪个。
`apt-get install linux-headers-x.xx linux-headers-x.xx-generic linux-image-x.xx-generic linux-image-extra-x.xx-generic` 四个包，x.xx是版本号，自行替换。

目前源里版本更新到3.16.0-31了，Linux内核最新版本已经到4.0了，告诉大家个好消息，4.0版本以后，Linux再也不要求大家重启了，厌倦了Windows反复重启的可要牢记哦。

## 总结
最后再次提醒大家修改grub设置后，不要忘记update-grub哦。
