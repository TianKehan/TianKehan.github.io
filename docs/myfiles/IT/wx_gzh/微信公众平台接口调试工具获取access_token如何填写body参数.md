---
layout: post
title:  "微信公众平台接口调试工具获取access_token如何填写body参数"
date:   2023-10-01 16:19:12 +0800
categories: jekyll update
---
```
{
    "grant_type": "client_credential",
    "appid": "APPID",
    "secret": "APPSECRET",
    "force_refresh": false
} 

```

可参考文档：
[微信公众平台接口调试工具获取access_token](https://developers.weixin.qq.com/doc/offiaccount/Basic_Information/getStableAccessToken.html)
