---
title: "通过ss来看看外面的世界"
date: 2017-05-07T12:40:02+08:00
tags: ["shadowsocks", "翻墙"]
categories: ["shadowsocks"]
---

## 一. 安装并运行ss

<!--more-->

好吧，客户端的安装非常简单：

* 运行： `apt-get update`, `apt-get install shadowsocks`
* 修改你的配置文件： /etc/shadowsocks/config.json:  

```
{
    "server":"xx.xx.xx.xx",
    "server_port":"xxx",
    "local_address":"127.0.0.1",
    "local_port":1080,
    "password":"xxxxx",
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open":false
}

```
* 前台运行：`sslocal -c /etc/shadowsocks/config.json`  
  或者后台运行：`nohup sslocal -c /etc/shadowsocks/config.json &`  
  或者用 `supervisor` 跑也行

## 二. 配置Chrome浏览器）

* 安装 `SwitchyOmega`插件
* 安装插件 —— 新建情景模式 —— 选择代理服务器 —— 代理协议SOCKS5 —— 代理服务器：127.0.0.1 —— 代理端口：1080 —— 应用选项
* 好了浏览器右上方会有一个新奇的圈圈图表，点击一下，选择你刚刚配置的代理就可以了。

## 三. 命令行翻墙
* 安装：proxychains: `apt-get install proxychains`
* 修改配置文件 `/etc/proxychains.conf`, 把socks4注释掉，加上 `socks5  127.0.0.1 1080` ：  
```
  # socks4        127.0.0.1 9050
  socks5  127.0.0.1 1080
```
* 使用代理时在命令前面加上`proxychains`即可，比如： `proxychains curl google.com`
