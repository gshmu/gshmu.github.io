title: multi-system
date: 2016-01-12
categories: Config
tags: [config, sys, linux]
---
中文名：《我把双系统放入vBox并行》
![WIN7HD](pic/win7hd.png)
双系统同时运行：宿主机Ubuntu，虚拟机DELL9020原装“正版”Win7。

## Linux
我用Linux办公，不喜盗版讨厌弹窗等等，不过我觉得用Linux是不需要理由的。领来新机直接U盘装Ubuntu 14.04 x64，看到大家用Windows居多，所以本着有备无患留下了Windows，grub直接引导就变成双系统，硬盘分区如下：

```bash
~$ lsblk 
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0 931.5G  0 disk 
├─sda1   8:1    0   100M  0 part 
├─sda2   8:2    0 196.7G  0 part 
├─sda3   8:3    0     1K  0 part 
├─sda5   8:5    0 186.3G  0 part /
└─sda6   8:6    0 279.4G  0 part /home

```
可恶的Windows占用了两个主分区，一个是所谓的boot。我把Linux装到了逻辑分区，这个无所谓了，grub大叔能叫起床就OK了。（sda3是逻辑分区的标识，Linux我只分了两个，还预留了200G的空白分区，备用）

## Win
我不用Windows系统，一直都是Ubuntu一个系统，最多考试什么需要IE的场合用下。然而有一天，小鬼（一个不支持Linux的所谓互联网大公司，不支持也就罢了，源里还有个不能用的软件拉嘲讽）作祟，Web版本也不让用了，开源大神一度辛苦抓包维护的pidgin插件lwqq不能用了。
最不折腾的方案是虚拟机了，然而我一个懒人，懒得下镜像，懒得装盗版系统，懒得下直接下不确定安全的vmdk/vdi文件用，就想用现成的系统。有句话叫：没有最不到，只有想不到。虚拟的磁盘文件都可以，然而我有真的，不用白不用。
### 折腾
我最不喜欢折腾，Linux下我不会在乎系统多起个服务进程的，但是Windows没用的开机启动，用不着的服务关一个少一个，少一个系统就少一份维护。我真的最不喜欢折腾，软件都是直接装源里的，除非有bug不想忍时才偶尔编译安装新版本。

## 开工
首先创建一个类似链接文件的虚拟机磁盘文件，命令如下：
```bash
vboxmanage internalcommands createrawvmdk -filename /path/to/new/vmlink/file/Win7HD.vmdk -rawdisk /dev/sda -partitions 1,2 -mbr /path/to/mbr/win7.mbr -relative
```
### MBR
大家都知道MBR，我就不卖弄了，有真的最好，没有真的弄个假的先凑合下吧。安装完Linux后我的MBR默认引导GRUB，可以导出一份（dd/fdisk/gdisk等等），也可以先搞个假的512bytes 二进制文件。（虚拟机可以有自己的MBR，赞赞）
### chmod
默认`/dev/sda*`是没有写权限的，so (作为一个懒人，必须搞个自动的: `update-rc.d`)
```bash
sudo chmod o+rw /dev/sda1 /dev/sda2
```
建议用命令，也可以自己写个sh放到对应的/etc/rc?.d/下面（利用rc.d启动级别，密码可以跳过。）

## VBox
含有自己mbr的虚拟机磁盘镜像文件建立好了，如下：
```bash
$ ll Win7HD*
-rw------- 1 gshmu gshmu 65536  5月  5  2015 Win7HD-pt.vmdk
-rw------- 1 gshmu gshmu   857  1月 11 08:52 Win7HD.vmdk
```
下来当然创建虚拟机，同时添加磁盘文件（注：仅需要添加Win7HD.vmdk这一个文件就好）
### FIX
如果你的mbr是真的，如我在装Ubuntu之前备份了mbr这步可以跳过。修复MBR对大家不是什么难题，最方便的是在虚拟机中挂载个iso镜像文件，启动顺序设置CD优先启动。
我挂载了个PE的iso文件，进入PE直接修复引导…
取消挂载的iso文件，或者改下顺序，然后，重启~  双系统一起运行，竣工 吼吼！
### Other
* 网络：虚拟机网络建议选择NAT模式，然后给虚拟机分配个IP。起初我的双系统是同样的IP，不会存在冲突，现在只好再申请一个IP分配上，使用NAT方便宿主机和虚拟机通信。
* 软件：Windows虚拟机下输入法我用小狼毫，通讯软件我用Lite版本。
* 操作：起初我尝试过用远程登录虚拟机的方式，因为虚拟机快捷键是系统级别的，远程桌面可以降到软件级，方便统一操作，但还是鸡肋。最后修改虚拟机设置“Auto Capture Keyboard”，结合工作空间Workspaces给虚拟机单用一个工作空间。

## END
本文介绍了借助vbox并行运行双系统的实践，提供了Linux下部分关键命令。我想做一款IM，一款立足Linux的IM，一款和世界共通的IM，然而在“鸡犬之声相闻（lǎo sǐ bù xiāng wǎng lái）”的中国（中：通假字），很难作出这样的IM，有很多做好的却又被不可用。最后的最后给无数开源贡献者点个赞…
