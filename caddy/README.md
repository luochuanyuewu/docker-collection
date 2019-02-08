## 说明
假设docker命令在一个sites文件夹下执行。

sites包含多个文件夹，每个文件夹是一个网站，同时要在Caddyfile里配置好多站点

单站点的话，直接把网站源文件也放在这个路径下吧

Caddyfile存在于sites文件夹下

```
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
第一个v是映射证书文件夹

第二个v是映射配置

第三个v是映射站点根文件夹，类似apache的RootDocument

实际上端口暴露443即可

此docker中/srv路径是站点根目录，类似于Apache的DocumentRoot。而这里我们把当前路径绑定到/srv中。

root的值其实是相对于DocumentRoot的。

假设我的当前路径有两个文件夹分别对应两个网站，一个是aliblog，一个是cdn。

运行上面的docker命令配合下面的Caddyfile配置即可完成同一主机两个站点。

```
luochuanyuewu.com {
    root /srv/aliblog
}

cdn.luochuanyuewu.com {
    root /srv/cdn
}
```

