title: a cup of vps
date: 2015-12-08
categories: Linux
tags: [linux, config, deploy]
---
习惯了谷歌搜索，还真的离不开了…(本文后面更新过)

# Buy VPS
购买个VPS吧，选了款便宜点的，[bandwagon](https://bandwagonhost.com/) 19.9$/Y（支持支付宝付款），这个我是新来的，就不搬门弄斧了…
购买成功后，操作系统选Ubuntu16.04，和我现在用的一样，主要是方便，首次密码登录添加公钥，安卓可以使用JuiceSSH客户端。。。

## shadowsocks
先装个服务吧，本着不折腾的折腾原则。

### server
先启动个服务吧，脚本奉上：
```shell
apt-get update && apt-get -y install python-pip && pip install -U pip && pip install shadowsocks
```
安装完毕，可以直接用命令`ssserver`启动服务，推荐写个json，参数不懂问`man`老师，或者帮助，官网文档都可以。
```shell
echo '{
   "server":"0.0.0.0",
   "server_port":88,
   "password":"yourpassword",
    "timeout":300,
   "method":"aes-256-cfb",
   "fast_open": false
}
' > /etc/shadowsocks.json

ssserver -c /etc/shadowsocks.json
```
至此服务端启动OK，其中端口和密码自己设置。

### client
安装方式一样，只是启动的时候用`sslocal`命令，可以直接指定参数启动，也可以写个配置文件。
推荐火狐浏览器，因为火狐浏览器有单独的网络配置，而chrome等用的系统代理配置。

## nginx
大家对nginx和gunicorn（uwsgi的一种）一定不陌生，其中有个名词叫反向代理，我的理解nginx反向代理是，自己有的（像js，css之类的）直接给你，没有的，去找gunicorn取来后给你。

### Apply
“Nginx, Show me google homepage...” 没有取了来给我，哈哈哈 :) 
不要想太复杂，[Github](https://github.com/cuber/ngx_http_google_filter_module/blob/master/README.zh-CN.md)上有现成的（我不喜欢编译，但偶尔编译下还是可以滴），注有个组建我更新了下，然后configure命令修改后是下面这样的：(前两个版本号稍有更新)
```shell
apt-get -y install build-essential git gcc g++ make && mkdir wen.lu && cd wen.lu && git clone https://github.com/cuber/ngx_http_google_filter_module && git clone https://github.com/yaoweibin/ngx_http_substitutions_filter_module && wget "http://nginx.org/download/nginx-1.10.2.tar.gz" && tar xzvf nginx-1.10.2.tar.gz && wget "ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.39.tar.gz" && tar xzvf pcre-8.39.tar.gz && wget "http://zlib.net/zlib-1.2.8.tar.gz" && tar xzvf zlib-1.2.8.tar.gz &&  wget "https://www.openssl.org/source/openssl-1.1.0c.tar.gz" && tar xzvf openssl-1.1.0c.tar.gz && cd nginx-1.10.2 && \
./configure \
  --prefix=/opt/nginx-1.10.2 \
  --with-pcre=../pcre-8.39 \
  --with-openssl=../openssl-1.1.0c \
  --with-zlib=../zlib-1.2.8 \
  --with-http_ssl_module \
  --add-module=../ngx_http_google_filter_module \
  --add-module=../ngx_http_substitutions_filter_module && \
make && \
make install
```
下来修改下配置，修改的地方如下：
```
  resolver 8.8.8.8;
  location / {
    google on;
    google_language "ca"; 
  }
```
然后启动ngins，访问[My VPS HIDE]，久违的谷歌出现了。
http支持了，https如今也已经支持，使用Let's encrypt证书，使用证书需要域名，免费域名申请的较晚，所以https及证书支持较晚。

# the End
[all in one last.](https://github.com/m4free/vps)  感谢阅读，我本地代理默认监听0.0.0.0，局域网的小伙伴有福了哈。
