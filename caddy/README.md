# Caddy web服务器

## 说明

Caddy是golang开发的web服务器，可以自动https，个人用来替代apache等类似web服务器。

- [官方文档](https://caddyserver.com/docs)
- [Docker](https://hub.docker.com/r/abiosoft/caddy)

## 示例

### 多网站

假设当前working directory是sites文件夹

sites包含多个文件夹，每个文件夹是一个网站，同时要在Caddyfile里配置好多站点,Caddyfile存在于sites文件夹下

Caddyfile内容:

```bash
luochuanyuewu.com {
    root /srv/aliblog
}

cdn.luochuanyuewu.com {
    root /srv/cdn
}
```

表示luochuanyuewu.com这个网站的根目录在/srv/aliblog下，cnd.luochuanyuewu.com这个网站的根目录在/srv/cdn下。

然后是Docker命令：

```bash
docker run -d \
--name sites  \
-v $HOME/.caddy:/root/.caddy \
-v $(pwd)/Caddyfile/:/etc/Caddyfile \
-v $(pwd):/srv \
-p 80:80 \
-p 443:443 \
-p 2015:2015 \
abiosoft/caddy
```

第一个v是映射证书文件夹(很重要，否则很容易超过tls限制)

第二个v是映射配置

第三个v是映射站点根文件夹，类似apache的RootDocument，将sites文件夹映射到了容器中的/srv路径。

如果站点配置里写的是域名而不是localhost:xxx，那么实际上端口暴露443即可，如果指定的站点时localhost:xxx，那么caddy实际上是以非https运行的（所以端口在2015）

此docker中/srv路径是站点根目录，类似于Apache的DocumentRoot。而这里我们把当前路径绑定到/srv中。

假设我的当前路径有两个文件夹分别对应两个网站，一个是aliblog，一个是cdn。

运行上面的docker命令配合下面的Caddyfile配置即可完成同一主机两个站点。

## 反向代理
