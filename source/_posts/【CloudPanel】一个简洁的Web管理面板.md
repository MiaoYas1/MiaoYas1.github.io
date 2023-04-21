---
title: 【CloudPanel】一个简洁的Web管理面板
tags:
  - Web
  - CloudPanel
categories: Web
date: 2023-04-20 02:25:14
---
> 这个面板不能说是最完美的，简洁，功能够用，并且支持中文，维护者也有持续在迭代更新，就个人用户而言，搞个VPS搭建网站程序，CloudPanel是一个不错的选择。

**注意：仅支持Debian/Ubuntu系统**

![仪表板](https://s2.loli.net/2023/04/21/PvRadLOEy6i4BxI.jpg)

> 官方Demo [点击查看官方Demo](https://demo.cloudpanel.io/ "点击查看官方Demo")

# 安装CloudPanel面板
官方安装说明[点这里](https://www.cloudpanel.io/docs/v2/getting-started/other/ "点这里")
登录系统后，先执行以下命令更新一下
```shell
apt update && apt -y upgrade && apt -y install curl wget sudo
```
然后进入官方页面：[点击这里](https://www.cloudpanel.io/docs/v2/getting-started/other/ "点击这里")

![系统选择](https://i.328888.xyz/2023/04/20/iFolvy.jpeg)

选择正确的操作系统，以及适合你的数据库引擎，复制命令后回到SSH客户端执行即可开始安装

安装完毕后，即可通过 你的服务器IP:8443 访问管理后台，(需要提前在防火墙放行8443端口)

此时应尽快创建面板的管理员账户。由于初始化安装完成后，任何人拿到以上网址都能登录和操作，所以需要尽快完成管理员账户的创建。

# WordPress性能优化
## 启用Varnish加速
面板后台-网站群-网站管理- Varnish Cache，开启Varnish Cache，并在WordPress后台安装CLP Varnish Cache Plugin插件进行相应配置。如果网站更新频率不高，可以适当拉长缓存更新时长（Cache Lifetime）。
## 开启页面速度
面板后台-网站群-网站管理- 设置，拉到下方，打开页面速度并保存，网站图片会自动转变为Webp格式并缓存
## 使用Redis缓存
在WordPress插件页面搜索并安装 Redis 缓存插件 - Redis Object Cache
跳转到设置 - Redis，点击 Enable Object Cache 按钮开启即可。

**Varnish Cache和Redis只能开启一个，不能同时开启**