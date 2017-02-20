title: chrome apk
date: 2016-01-15
categories: Linux
tags: [advanced, play]
---
![跟大牛一起玩chrome，奔跑吧APK](/pic/Ubuntu-chrome-apk.png)
[chromeos-apk](https://github.com/vladikoff/chromeos-apk):Run Android APKs on Chrome OS, OS X, Linux and Windows.  把安卓应用放到PC玩，有没有心动呢？然后一个不好的消息是，越不标准的应用越容易崩溃，比如某信和某宝。

## npm
[Node.js](http://nodejs.org/) 火了，npm和Node.js的关系，借用官方的话说：
>
“The npm command-line tool is bundled with Node.js. If you have it installed, then you already have npm too. If not, go download Node.js. ”

先装Node.js，这个不是不是本文重点，此处略过。

## [chromeos-apk](https://github.com/vladikoff/chromeos-apk)
主角出场了：`$ npm install chromeos-apk -g`，用法很简单，`$ chromeos-apk /path/to/file.apk`，执行成功后会在当前目录生成一个文件夹，名字如`com.app.android`，根据我的经验需要加上`--name com.xxx.android`就是根据生成的文件夹名，我还习惯加上`--scale`参数。

### APK
下载APK当然选择[Google Play](https://play.google.com/store/apps)，配合下载的网页[APK Downloader](https://apps.evozi.com/apk-downloader/)  即可下载谷歌市场应用，有人要为什么这么挑，因为这里的应用更加标准。举个简单的例子，你的微信经常会提醒更新，后台下载APK文件，而我去微信里面点击检查更新，会打开应用市场，这是看得见的区别。（如果还有问题，可以参考我2015-12-18的盟盟汇文章）

## ARChon runtime
[Download the runtime](http://archon-runtime.github.io/)根据你的系统下载对应的版本，解压到某个目录。

## chrome
建议使用最新的稳定版，打开[chrome扩展页](chrome://extensions/)。开启开发者模式，点击load unpackkd extension，先加载前面解压的运行环境整个文件夹，然后加载你转换的APK的文件夹，然后点击运行… 大家都有民生的银行卡，我用民生的手机银行客户端为例，如图：

## END
跟大牛有肉吃，至于问我为什么要这么大费周章，没人喜欢折腾，真的……  只是，以前手机内存小，庙太小，容不下大神，再加上安卓那令人发指的唤醒链，有些应用不想往手机装。最后还有个原因是我用Linux，Linux下出名的通讯问题大家都听过吧，可惜是鹅厂应用太不标准了！！！
