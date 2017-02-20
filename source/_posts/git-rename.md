title: git_rename
date: 2014-10-28
categories: Git
tags: [git]
---
## Why
项目多了，难免会有重命名的时候，重命名本身没什么问题，可是加上gitignore中的`*.pyc`或`*~`可能会出现些问题…

### Q
重命名的时候一般不会有问题，可是在分支切换的同时，由于存在ignore的文件，分支的切换并不会那么正确。
往往会多出重命名前或重命名后的文件夹，多的原因就是文件夹下有被忽略的临时文件。

原因很简单，所以解决也不难，删除多余的文件夹，一切正常了。

## 总结
git在重命名文件夹后切换分支可能由于ignore临时文件的存在多出重命名前后的文件夹。