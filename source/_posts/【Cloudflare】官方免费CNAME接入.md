---
title: 【Cloudflare】官方免费CNAME接入
tags:
  - Web
  - Cloudflare
categories: Web
date: 2023-04-20 13:56:25
---
# 功能简介
使用CloudFlare for SaaS功能CNAME接入CloudFlare。
> Cloudflare SaaS官方公告：[https://blog.cloudflare.com/zh-cn/waf-for-saas-zh-cn/](https://blog.cloudflare.com/zh-cn/waf-for-saas-zh-cn/ "https://blog.cloudflare.com/zh-cn/waf-for-saas-zh-cn/")

CloudFlare中一个完全接入的域名即为一个zone，点进去包括套餐、安全等等都是针对这一主域名配置的，官方SaaS功能针对的是你服务的客户，开放这项功能允许使用他们自己的域名直接附加在你的zone里，享受你zone包含的安全、加速等功能。

# 配置接入
## 订阅CloudFlare for SaaS
打开一个域名，选择【SSL/TLS】下的【自定义主机名】，点击【启用CloudFlare for SaaS】后根据指示绑定外币卡或者PayPal，订阅CloudFlare for SaaS功能。
![订阅SaaS](https://pic7.58cdn.com.cn/nowater/webim/big/n_v284235f79b6ce4f088e4ed76b654497c0.jpg)
## 设置源站
选择一个承载的域名zone点进去，在【DNS】下解析一个子域名作为回退源域名，必须开启小橙云(代理)。
![解析](https://pic4.58cdn.com.cn/nowater/webim/big/n_v28568d0b9933a4dfabb5b88b65bcfcdcc.png)

然后进入【SSL/TLS】下的【自定义主机名】，首先要设置附加上域名的回退源，输入刚才设置的子域名并点击添加回退源，会同步这个子域名设置的源站作为后续在此接入域名的源站。
![回退源](https://pic2.58cdn.com.cn/nowater/webim/big/n_v29cd6125000af40239cffef242454b1e8.png)

## 添加自定义主机名
点击【添加自定义主机名】，输入你要添加的未在CF接入的子域名，选择TXT验证。
![自定义主机名](https://pic3.58cdn.com.cn/nowater/webim/big/n_v2149256d383ea48e797df43af0d20ca79.png)

## 验证域名所有权
![TinySnap-2023-04-20-14.29.58.png](https://pic6.58cdn.com.cn/nowater/webim/big/n_v24fc5d90783be49c5a7a00c74bcfd684b.png)
按要求解析证书和主机名两个TXT记录，解析生效后10分钟左右即可验证通过，到此这个SaaS域名就正确的添加到了你的zone中并接入了CF。

## SaaS域名解析
添加进去的SaaS域名，CF不会给你明确的CNAME指向，可以直接CNAME到你刚刚设置的回退源域名比如origin.ysl.cm

防火墙规则、页面规则，直接将添加进的域名输入其中即可圈定范围，完成对于其细则的设置。
