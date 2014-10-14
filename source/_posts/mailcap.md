title: mailcap
date: 2014-10-13
categories: Linux
tags: [config]
---
`Tencent === Trash`，微云下载的文件总是用gedit打开，firefox如是说。有谁能想到，腾讯微云下载的文件有着一样错误的`Content-Type: "application/octet-stream"`

### `The Way to fix it`
Ubuntu 下，命令行执行：
```
echo 'application/octet-stream; nautilus --no-default-window --no-desktop %s; test=test -n "$DISPLAY"' >> ~/.mailcap
```
其实就是向家目录下`.mailcap`文件追加上述命令单引号内中的内容。（文件不存在则新建）

### reason
微云下载文件时，HTTP Response headers，中使用了不是Trash不可能使用的`Content-Type: "application/octet-stream"`，这是什么鬼文件，系统说他不认识，你试试gedit吧。

上面的解决方法是，`application/octet-stream`类型的文件用nautilus打开（在文件夹中显示），之所以没有定义到确定的应用，因为我常用的有zip和pdf两种，只好折中使用nautilus了。

## 总结
firefox中下载的文件总是用gedit打开，我气愤不止一次了。我用Linux，为什么用QQ，因为有人用QQ，为什么是微云，因为有用QQ发的文件，我只好借用微云，然后浏览器下载下来。

### 感谢IRC: `Cork`
