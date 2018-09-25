---
title: "Lunix 命令记录"
date: 2018-08-03T11:40:57+08:00
draft: true
---

<!--more-->

## Lunix 命令记录

### 文件同步

> 文件从服务器同步到本地
>

```
rsync -avhzP deploy@example.com:~/projects/example/tmp(服务器) public(本地)/

```
* `-avhzP` 一堆参数，参见 <http://man.linuxde.net/rsync/>


### 文件查看


> tail 命令常用于日志分析


* tail -f 循环输出, 常用于监控

* tail -n 从倒数第几行开始输出

  >
  ```
  touch a.log

  tail -n 1000 b.log > a.log  # 表示从b中取出最新1000行数据输入到a.log文件里

  ```

### 杂七杂八

* df -h 查看硬盘使用

* sudo nethogs 查看进程的流量

* sudo nload 查看总流量


