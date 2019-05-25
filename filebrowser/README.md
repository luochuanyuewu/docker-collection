# filebrowser

提供基于web的文件管理

## 在Docker中安装

```bash
docker run \
    -v $(pwd)/content:/srv \
    -v $(pwd)/filebrowser.db:/database.db \
    -v $(pwd)/.filebrowser.json:/.filebrowser.json \
    -p 8080:80 \
    filebrowser/filebrowser
```

默认.filebrowser.json配置:

```json
{
  "port": 80,
  "baseURL": "",
  "address": "",
  "log": "stdout",
  "database": "/database.db",
  "root": "/srv"
}
```

[参考](https://filebrowser.xyz/installation)

## 使用caddy代理filebrowser

改变baseurl（也可以在.filebrowser.json中配置）

```bash
filebrowser config set --baseurl /admin
```

然后Caddyfile配置（以下两种方式都可以）

```bash
example.com

proxy /admin 127.0.0.1:8080
```

```bash
localhost:2015/admin

proxy / 127.0.0.1:8080
```

[官方参考](https://filebrowser.xyz/installation/caddy)

[Caddy反向代理教程](https://medium.com/bumps-from-a-little-front-end-programmer/caddy-reverse-proxy-tutorial-faa2ce22a9c6)