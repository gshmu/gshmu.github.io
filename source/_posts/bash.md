title: bash
date: 2014-09-05
categories: Linux
tags: [bash]
---
my bash

#### 声明
本文不是介绍bash的，当然也不含有bash历史，本文写的很随意，如果你不喜欢这些，请移步。
有高见，欢迎来IRC： `/join #zh-cn`

### PS1
整一个个性的提示符`PS1`，我的提示符：
[`^_^:~$ `](http://bashrcgenerator.com/)
> export PS1="\[\e[00;37m\]\n\[\e[0m\]\[\e[00;34m\]^_^\[\e[0m\]\[\e[01;31m\]:\[\e[0m\]\[\e[00;36m\]\w\[\e[0m\]\[\e[01;33m\]\\$\[\e[0m\]\[\e[00;37m\] \[\e[0m\]"

点击上面的提示符 or [bashrcgenerator](http://bashrcgenerator.com/)，定制一个属于自己的提示符吧。
使用该提示符，将生成的代码复制粘贴到`~/.bashrc`文件即可。（其实是`export`一个常量`PS1`，所以有必要放在`PS1`赋值的后边，以便生效。）

### 唤醒历史命令补全
将下述代码复制粘贴到`~/.bashrc`文件，然后输入部分命令再使用上下键试试。
> bind '"\e[A": history-search-backward'

> bind '"\e[B": history-search-forward'

### 控制命令
* `;`: 组合多个命令，按循序执行。
* `&`: 使命令开启一个子Shelll并在后台执行。
* `&&`: 前面命令成功后，执行后边命令。
* `||`: 前面命令执行失败后，执行后边的命令。

### 重定向
* `>`: 重定向输出。（新建，会覆盖）
* `>>`: 重定向追加输出。（追加，会新建）
* `<`: 重定向输入，一般从文件读入等。
* `<<`: `！`不知道，没用过。
* `|`: 管道，不解释了。`*****`五星级。

## .bashrc at Ubuntu
```
alias ga='git add'
alias gb='git branch'
alias gc='git commit'
alias gd='git diff'
alias gf='git fetch'
alias gl='git log'
alias gs='git status'
alias go='git checkout'

export PS1="\[\e[00;37m\]\n\[\e[0m\]\[\e[00;34m\]^_^\[\e[0m\]\[\e[01;31m\]:\[\e[0m\]\[\e[00;36m\]\w\[\e[0m\]\[\e[01;33m\]\\$\[\e[0m\]\[\e[00;37m\] \[\e[0m\]"

. /usr/share/bash-completion/completions/git  # about my git completions
__git_complete ga _git_add
__git_complete gb _git_branch
__git_complete gc _git_commit
__git_complete gd _git_diff
__git_complete gf _git_fetch
__git_complete gl _git_log
__git_complete go _git_checkout
```

经过一番折腾，激活了git的自动完成，有自动完成的别名才有意义。

