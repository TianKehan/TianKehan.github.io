---
layout: post
title:  "ChatGPT不耗余额，不用API Key接入个人微信"
date:   2023-09-28 16:19:12 +0800
categories: jekyll update
---
[ChatGPT不耗余额，不用API Key接入个人微信，很简单用免费的服务器就行，一个GitHub项目](https://www.youtube.com/watch?v=twIWGbNeI48) 

-

工具链接：

GitHub项目地址：WechatGPTBot
亚马逊领的12月免费云服务器（新加坡ubuntu）
Xshell
操作指令
1.下载项目并获取access_token

    1.1 xshell连接ubuntu
进入root权限	sudo -i
更新软件仓库	sudo apt-get update
    1.2 下载项目（ubuntu自带git无需下载，其他系统没有的自己安装） 

# 获取项目
git clone https://github.com/CJ-cooper6/WechatGPTBot.git

# 进入项目目录
cd WechatGPTBot
    1.3 获取并替换access_token 

        访问 https://chat.openai.com/chat 成功登录之后, 打开浏览器开发者工具 (F12) -> 刷新页面- > Network 找到 /api/auth/session 请求, 得到 accessToken

# 替换config.json中access_token
 

2.运行程序并保护进程

安装docker	sudo snap install docker

必须要进入bot文件夹运行守护程序+sudo超级管理员权限
sudo docker build -t wechatgptbot .
sudo docker-compose up -d
sudo docker-compose logs --tail=10 wechatgptbot
        扫码登录、换微信时重新运行上面的代码就行 

