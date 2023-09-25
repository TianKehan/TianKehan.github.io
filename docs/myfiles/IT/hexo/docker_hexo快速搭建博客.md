---
layout: post
title:  "docker+hexo快速搭建博客网站"
date:   2023-09-14 5:14:12 +0800
categories: zjp update
---
```
docker pull spurin/hexo
docker run -d -p 8080:4000 935d3dd4f0d8
docker exec -it 929b447efd4d /bin/bash
hexo s

```
#docker+hexo快速搭建博客网站
## docker部署node容器


```
为方便调试，本文通过docker部署node容器进行本地测试，dockerfile如下：

```
mkdir -p ~/app/hexo-debug
cd ~/app/hexo-debug
vim Dockerfile
```

```
FROM node:14
maintainer lc

# 构建参数
ARG WORK_PATH="/hexo"

# 设置时区
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' >/etc/timezone

# 替换为阿里源并安装必要工具
RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list  \
    && apt update -y \
    && apt-get install -y curl vim telnet

# 解决vim中文乱码、ll命令
RUN echo "syntax on \nset termencoding=utf-8 \nset encoding=utf8 \nset fileencodings=utf8,ucs-bom,gbk,cp936,gb2312,gb18030" >> ~/.vimrc  \
 && echo "alias ll='ls $LS_OPTIONS -l'" >> ~/.bashrc

# 安装hexo
RUN npm install hexo-cli -g

#设置工作目录
WORKDIR $WORK_PATH

# 继承基础镜像
ENTRYPOINT ["docker-entrypoint.sh"]
CMD [ "node" ]
```

-   制作镜像

```
docker build -t hexo-debug:node14 .
```

-   启动hexo调试容器

```
# 启动容器，并挂载目录
cd ~/app/hexo-debug
docker run -dit  -p 4000:4000 --name hexo-debug -v ${PWD}/docker-mnt:/hexo hexo-debug:node14
```

-   进入容器

```
# 查看容器列表
docker ps -a

# 进入容器
docker exec -it hexo-debug bash
```

## 初始化[hexo](https://so.csdn.net/so/search?q=hexo&spm=1001.2101.3001.7020)

-   初始化hexo

```
# 初始化命令，blog为文件夹名
hexo init blog

# 进入文件夹
cd blog

# 删除.github文件夹
rm -rf .github

# 安装
npm install

# 启动本地服务器
hexo s -g 
```
![](assets/2023-09-25-22-07-26.png)

-   在控制台开放4000端口，访问测试

![](assets/2023-09-25-22-07-43.png)