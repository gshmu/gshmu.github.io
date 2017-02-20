title: remote debugger
date: 2015-07-02
categories: Python
tags: [python, debug, idea]
---
你没有看错，Python Remote Debugger with PyCharm！本文是基于Python IDE：[PyCharm](https://www.jetbrains.com/pycharm/)，主要介绍 Remote Debugger 的在 PyCharm 中的配置使用，本文希望传递一个消息，**远程是可在IDE调试的**，也希望大家能在以后的工作中调试起来…。

## Debug Configurations
先上图：
![Debug Configurations](/pic/Run-Debug-Configurations.png)
* 1： 这是一个django服务的示例
* 2： 选择的是服务器（Remote）运行环境interpreter
* 3： **本地和远端path mapping**

### SSH
SSH最基本的通讯协议，服务器和测试服务器没有不开的吧。

### Remote Interpreter
Interpreter 解释器，使用python的对虚拟环境`virtualenv`应该都不陌生，我们首先需要一个和服务器一样的运行环境。
![Setting add Interpreter](/pic/Settings_add.png)
按照顺序操作到4，点击Add Remote(如下图)，SSH配置完点OK。
![Configure Remote Python Interpreter](/pic/Configure-Remote-Python-Interpreter.png)
初次连接可能弹出提醒，确认即可，然后会回到设置主界面，切记点击**Apply**和**OK**。

### config mapping etc
![Configure Server](/pic/Configure-Server.png)
单击向下的那个箭头，然后编辑配置，就回到了最开始那个图，配置好后用debug方式启动就可以远程调试了，吼吼

## Linux
远程调试已经完了，你可以很方便的在你本地以调试方式启动服务，在本地设置断点，然后使用服务器ip访问，捕获到断点是不成问题的，修改代码，PyCharm 也有同步的功能，但我还是喜欢下面的~

### sshfs
Linux，所以直接挂载测试服务器文件：
`$ sshfs -o idmap=user root@10.65.200.151:/opt/disk2/var/www/V6.3.1 /local/mount/point`
直接将服务器目录挂载到本地，实质就一份文件。(避免和线上配置可能的冲突)
附：取消挂载的命令`$ fusermount -u $point`

### Windows
感谢`永哥`，在windows下实现了，给大家扫雷了。在用户目录下新建`.ssh`文件夹和`known_hosts`文件，不然远程环境会无法建立。
虽然用不了sshfs，但是可以sftp的，配置远程文件时，需要明确选下如图，虽然选后路径不变:
![Remote Host File](/pic/Remote_File.png)
不选的话，远程文件可能不识别，识别后远程文件显示为绿色。

## 总结
本文希望能传递一个消息：**远程是可调试的！**希望大家以后能用起来，以后如何用好还请大家思考。最后，欢迎任何反馈。
