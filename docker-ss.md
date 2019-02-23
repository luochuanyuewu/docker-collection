## 启用SS服务端
在你自己的国外的安装了docker的Vps/或者云服务器上操作。

``` bash
$docker run -dt --name ssserver -p 6443:6443 -p 6500:6500/udp mritd/shadowsocks -m "ss-server" -s "-s 0.0.0.0 -p 6443 -m chacha20 -k test123 --fast-open" -x -e "kcpserver" -k "-t 127.0.0.1:6443 -l :6500 -mode fast2"
```
其中test123是密码，可以换成你的，端口绑定按需更改。

## 启动SS客户端

在你自己的装了Docker的电脑上操作。

``` bash
$docker run -dt --name ssclient -p 1080:1080 mritd/shadowsocks -m "ss-local" -s "-s 127.0.0.1 -p 6500 -b 0.0.0.0 -l 1080 -m chacha20 -k test123 --fast-open" -x -e "kcpclient" -k "-r SSSERVER_IP:6500 -l :6500 -mode fast2"
```
其中test123是密码，可以换成你的，端口绑定按需更改。

谷歌浏览器配合SwitchOmega插件，配置代理为Socks5，监听127.0.0.1:1080

[参考链接](https://hub.docker.com/r/mritd/shadowsocks) 


