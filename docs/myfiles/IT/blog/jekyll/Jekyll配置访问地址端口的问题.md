---
layout: post
title:  "Jekyll修改端口"
date:   2023-09-14 5:14:12 +0800
categories: zjp update
---

jekyll 默认开启地址端口 `127.0.0.1:4000` 在使用虚拟机时即使做端口转发也无法访问

解决方法

## 1\. `_config.yml`中配置ip 端口,添加上：

```
host: 0.0.0.0
port: xxxx
```

## 2.`nginx`端口转发

```
server {
      listen       80;
      server_name name.darklost.me;
       location / {
          proxy_pass   http://127.0.0.1:port;
     }
   }
```

## 3 `jekyll`加启动参数

`start.sh`

```
jekyll s --watch --host 0.0.0.0 --port 4000 -B
```

`stop.sh`

```
pkill -f jekyll
```

___