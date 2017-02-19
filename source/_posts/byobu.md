title: byobu startup
date: 2017-02-19
categories: Linux
tags: [config, byobu]
---
相信很多人都知道byobu，Ubuntu下很赞的终端管理工具，很方便的管理多个窗口，还支持窗口分屏，也支持多个窗口执行同样的命令（这点和`cssh`有一比），还可在服务器端保留你的工作状态，可以极大的提高效率。

## byobu
让进程在后台运行，注销后而不退出，你或许知道`nohup`，但这个也是`byobu`的最基本功能之一，与`nohup`相比，`byobu`给人更熟悉的感觉。久而久之，我就喜欢上了，可是如何在VPS上开机/重启后自动执行指定命令呢？

### code
配置相关的我看了不少资料，也尝试了不少。最后写了如下shell:
```shell
#!/usr/bin/env bash
# byobu
cd /root/
byobu new-session -d -n - "your command one"
byobu new-window -n - "your command ..."
byobu new-window -n - "your command ..."
byobu new-window -n - "your command ..."
```
这个脚本在登录后，执行下，确实能达到预想的效果，但是自动执行却不可以。。。

## ssh
最后无奈之下使用了简单粗暴的办法，在`/etc/rc.local`中添加一行：
`ssh -p22222 -i /root/.ssh/id_rsa root@localhost /etc/init.d/gshmu.sh`

### default shell
如果想ssh登录默认使用byobu，可以修改`/etc/passwd`中指定的默认shell。注意：默认的shell还有`/bin/false`和`/usr/sbin/nologin`daemon专用的，禁止登录用的。还有一种`/bin/rbash`，改天有时间，容我细细道来。

# END
程序猿都是有偏执的，预想的事情终于实现了，VPS重启后，登录上去的界面好熟悉。
