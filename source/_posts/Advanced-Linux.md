title: Advanced-Linux
date: 2015-03-10
categories: Linux
tags: [Linux, Advanced]
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


## 总结
