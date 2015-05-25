---------
config bash for work well

#### 声明
本文不是介绍bash(shell)配置的，花几分钟时间配置下你的Linux，你将收获不止多少个几分钟，同时还有份好的心情。
关注你的工具，工具将会更好的给你服务。

### 唤醒历史命令补全
将下述代码复制粘贴到`~/.bashrc`文件(~/.profile 或 ~/.bash_aliases 等shell自动加载的文件)。
重启bash，然后输入部分命令再使用上下键试试。
```
bind '"\e[A": history-search-backward'
bind '"\e[B": history-search-forward'
```

### 很长又很常用的命令
虽说bash本身支持CTRL+R搜索历史，换醒历史命令补全后更是如虎添翼，但所谓术业有专攻。
`alias pyc='find . -type f -name "*.pyc" -exec rm {} \;'`
功能就不多说了，删除当前目录下所有pyc文件。
`alias wd='cd /var/www/your/path'`

那些常用又很长的目录，至于为什么是wd，参考命令`pwd`，当然可以设置成任何你喜欢的，提醒，设置之前查看下`type`。
```
function sp(){
	if [ -z $1 ]; then
		echo "Need Process Name!"
	else
		ps -auxww | grep "$1" | grep -v grep
	fi
}
if [-f /usr/share/bash-completion/completions/complete]; then
    . /usr/share/bash-completion/completions/complete
    complete -F _complete sp
else
    echo "No comlpete for function sp()."
fi
```

定义一个函数sp，查看指定进程。这还不够，添加自动完成，不能用Tab的函数不是好函数！


### PS1
有些提示符看着又丑又占地方，自己修改个吧，我的：
[`^_^:~$ `](http://bashrcgenerator.com/)
> export PS1="\[\e[00;37m\]\n\[\e[0m\]\[\e[00;34m\]^_^\[\e[0m\]\[\e[01;31m\]:\[\e[0m\]\[\e[00;36m\]\w\[\e[0m\]\[\e[01;33m\]\\$\[\e[0m\]\[\e[00;37m\] \[\e[0m\]"

点击上面的提示符 or [bashrcgenerator](http://bashrcgenerator.com/)，定制一个属于自己的提示符吧。
（注：`export`一个常量`PS1`，所以有必要放在`PS1`赋值的后边，以便不被覆盖。）


## 总结
最后的最后，有个不幸的消息告诉大家，[alias.sh](http://alias.sh)网站居然关闭了！
```
bind '"\e[A": history-search-backward'
bind '"\e[B": history-search-forward'

alias pyc='find . -type f -name "*.pyc" -exec rm {} \;'
alias wd='cd /var/www/your/path'

function sp(){
	if [ -z $1 ]; then
		echo "Need Process Name!"
	else
		ps -auxww | grep "$1" | grep -v grep
	fi
}
if [-f /usr/share/bash-completion/completions/complete]; then
    . /usr/share/bash-completion/completions/complete
    complete -F _complete sp
else
    echo "No comlpete for function sp()."
fi
```
这部分我给你了，怎么更好的使用，请自行思考。
