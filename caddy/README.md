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
-p 80:2015 \
abiosoft/caddy
```

第一个v是映射证书文件夹

第二个v是映射配置

第三个v是映射站点根文件夹，类似apache的RootDocument

暴露端口80