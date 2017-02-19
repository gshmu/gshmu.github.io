title: lvs bug
date: 2016-01-29
categories: Linux
tags: [lvs, bug]
---
lvs是网络负载均衡常用的一种方式，然而今天的重点并不是lvs，而是一个隐含的坑……

## Error
打开网页报表页面，显示有问题。然后是(firefox+chrome)*2，四种模式访问都有问题！注：四种模式——乘2是使用隐私模式，no cache，no cookies …，这个是相对清空浏览器缓存一种优雅的方式，还有一种是不清空强制刷新Ctrl+F5方式。

## Try VM again
一切正常，一切正常有没有。。。

### add-ons
是插件作怪么，[Firefox addons](about:addons)/[chrome extensions](chrome://extensions/)，共同的插件没几个，晒图一张吧(仅Enable的插件)：
![suggest add-ons](pic/My-Add-ons.png)
既然说到了插件，说说优雅排查插件问题的方法（禁用插件重启），如图：
![disable add-ons restart](pic/add-ons-disable.png)

## …
浏览器debug，日志错误之类，此处略过半小时…

### lvs
时间刚好，wanglei5来上班了，王哥来瞅瞅：你的web有没有lvs...
先是堡垒机前置机远程桌面，分别访问了两个不同地址，果然问题在这里。然后堡垒机登录有问题那台机器后台，上代码：
```shell
Last login: Mon Dec 28 17:57:45 2015 from 172.16.58.xx
touch: cannot touch `/var/log/history/20160129-root.log': Read-only file system
/usr/bin/chattr: No such file or directory while trying to stat /var/log/history/20160129-root.log
-bash: /var/log/history/20160129-root.log: Read-only file system
```

## END
问题找到了，LVS后面两台机器一台出了点问题，奇葩问题给个奇葩解决方案吧。考虑到目前这个系统访问量使用量都很少，所以决定下来关闭lvs和一台web，外加一条转发规则，省点儿资源是点儿资源，何乐而不为。（本文晒了火狐浏览器积攒下的长的常用插件，和一些相对优雅的操作，需要自取。）最后感谢wanglei5，Best wishes！
