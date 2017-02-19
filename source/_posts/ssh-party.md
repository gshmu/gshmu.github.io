title: ssh party
date: 2016-01-21
categories: Linux
tags: [advanced]
---
SSH你是不是每天都在用，ssh可是一大家，今天开派对，首先清点下：
```shell
$ ssh  # 双击Tab
ssh               ssh-argv0         sshd              ssh-import-id-gh  ssh-keyscan
ssh-add           ssh-askpass       sshfs             ssh-import-id-lp  sshmitm
ssh-agent         ssh-copy-id       ssh-import-id     ssh-keygen        sshow
```
有没有惊呆，居然有这么多。。。

## man
派对开场是man老师介绍了下出场的各位，这一大家果然各个身怀绝技啊。如果有什么不懂的，大家私下询问man老师吧，man老师为人好的没话说，除了讲一口地道的英语……

- ssh vs sshd 黄金组合
- ssh-keygen 私钥公钥对了，生成修改，不容小瞧
- ssh-agent 私钥认证
- ssh-add 添加私钥认证
- ssh-copy-id 添加自己的公钥到指定主机，需要开启密码登录(首次)
- ssh-import-id 在线批量添加公钥
- sshfs fisesystem，通过ssh挂载文件
- ssh-askpass 界面询问密码

例：首先生成公钥对，ssh-copy-id将公钥拷贝到某台机器上；ssh-add将私钥添加到agent，此处需要输入一次密码，然后再次使用私钥无需输入密码。在Linux下，私钥默认仅当前用户有读写权限，不符合这个权限的私钥是不被认可的。

添加同事公钥：`$ cat ~/.ssh/pub/id.pub | ssh 10.7.14.39 'cat >> ~/.ssh/authorized_keys'`

修改私钥密码：`$ ssh-keygen -f .ssh/id_xxx -p`

## .ssh
- authorized_keys  默认认证公钥文件，可修改
- known_hosts  保存的hosts认证
- rc  登录ssh是，会自动执行这个脚本。
- config  如下：

```shell
cat ~/.ssh/config
ControlMaster auto
    ControlPath /tmp/ssh_mux_%h_%p_%r
ControlPersist 4h

Host 10.65.200.50
    IdentityFile ~/.ssh/id_rsa
    User root

Host 10.65.200.*
    IdentityFile ~/.ssh/Identity
    User root
    Port 50002

Host *
    User root
    Port 22
```

首先是配置开启共享的长链接，默认设置4小时，好处是第二次连同一台设备基本秒连，还有scp已链接设备速度也会大大加快。支持通配符配置不同用户，不同端口，使用不同密钥，配置好后，只需要ssh ip 即可登录。

#### config 插曲
```shell
$ cat .pip/pip.conf 
[global]
download_cache = ~/.pip/cache

$ cat .gitconfig 
[user]
        name = name
        email = name@mail.com
[http]
        # proxy = socks5://127.0.0.1:1080
        proxy = https://127.0.0.1:8080
[https]
        # proxy = socks5://127.0.0.1:1080
        proxy = https://127.0.0.1:8080
[pull]
        default = current
[push]
        default = current
[alias]
        last = log -1 HEAD
[color]
        status = auto
        diff = auto
        branch = auto
        interactive = auto
[core]
        excludesfile = ~/.config/.gitignore
```
- pip 启用了cache，第二次装同样的包，virtualenv虚拟环境装包，能快多少快多少
- git 配置了默认用户，操作习惯，还有全局ignore，默认使用代理。

## END
在这一家人的协助下，只要是网络可达的ip，只需要ssh ip 就可以登录，cssh 同时多个ip还可以一起登录，==为不折腾而战！==  注：对应配置windows下都有，xshell等工具密钥需要导出也是安全措施的一种。
