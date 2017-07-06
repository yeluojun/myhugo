---
title: "Supervisor安装使用记录及遇到的坑"
date: 2017-06-25T11:13:44+08:00
tags: ["supervisor", "运维"]
---

初用Supervisor的记录：

*Supervisor是一个强大的进程管理工具，我只用了其中的一点皮毛功能*

<!--more-->

## 一.安装
>安装的方式有两种：一种是apt-get install supervisor(Ubuntu),另一种是用pip安装 pip install supervisor，
我用的方式一安装。工具分为两个部分 第一个是：supervisord 可以理解为服务端， 第二个第一个是：supervisorctl 可以理解为客户端

## 二.编写配置文件
创建了一个文件: /etc/supervisor/conf.d/dg.conf,内容如下：
```
[program:dgApp]
user = root
directory = /home/jun/deploy/go/dg-app
command = /home/jun/deploy/go/dg-app/dg-app
autostart = true
autorestart = true
startsecs = 5
redirect_stderr = true
stdout_logfile = /home/jun/deploy/go/dg-app/log/log.log

```
* program: 指明应用名称
* user: 指明用户 *(note: 遇到的坑在这里，我遇到的问题是用户不指明的话，会找不到sock,报一个no suck file 的错误）*
* command: 顾名思义，需要运行的命令
* autostart: （If true, this program will start automatically when supervisord is started.）
* autorestart: 自动重启（意外退出的时候）
* startsecs: 程序需要运行的时间来表明成功
* stdout_logfile: 输出日志到指定的地方 *（日志很重要）*

更多配置看这里：http://supervisord.org/configuration.html

*note: 必须在主配置文件/etc/supervisor/supervisor.conf里面include这个配置文件才能生效:*
```
[include]
files = /etc/supervisor/conf.d/*.conf

```

## 启动
* 先启动服务端：supervisord -c /etc/supervisor/supervisor.conf
* 启动客户端： supervisorctl reload

>如果：supervisord进程已经存在，重新启动的话，需要杀掉进程：
>先用 ps -ef | grep supervisord 查找出进程id, 然后 kill掉

*supervisorctl 其他的一些命令：*

* supervisorctl start "your app"  # 启动 app
* supervisorctl restart "your app" # 重新启动 app
* supervisorctl status "your app" # 查看app运行状态

## 总结：
supervisor初试记录。
