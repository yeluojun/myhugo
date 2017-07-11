---
title: "Ruby环境搭建记录"
date: 2016-06-29T12:22:21+08:00
tags: ["Ruby", "Rails", "环境搭建"]
categories: ["Ruby"]
---

## Ruby on Rails 环境搭建记录 - Ubuntu 16.04

<!--more-->

## 一. 安装rvm
RVM 是 Ruby版本管理工具，功能强大，Ruby开发基本都能用上它。



__安装RVM:__
```
$ gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
$ curl -sSL https://get.rvm.io | bash -s stable

# 如果上面的连接失败，可以尝试:
$ curl -L https://raw.githubusercontent.com/wayneeseguin/rvm/master/binscripts/rvm-installer | bash -s stable
```

__使用RVM:__
```
$ source ~/.rvm/scripts/rvm
```
> 如果RVM安装到了 /usr/local 位置：`$ source /usr/local/rvm/scripts/rvm`  
> 如果安装正确，运行 `$ rvm -v` 将会出现版本号等信息。



__更新RVM到最新版本:__
```
$ rvm get stable
```

----
## 二. 安装Ruby

列出rvm管理的软件及版本:
```
$ rvm list known
```
安装 Ruby - 比如安装Ruby 2.4.1 :
```
$ rvm install 2.4.1
```
列出已经安装的Ruby版本：
```
$ rvm list
```

----
## 三.使用Ruby

__设置默认使用的 Ruby 版本：__
```
$ rvm use 2.4.1 --default
```
> 也可以不默认使用， 把 `--default` 去掉就可以。

查看Ruby版本：
```
$ ruby -v
ruby 2.4.1 ...

$ gem -v
2.1.6
```

__安装Bundler:__

```
$ gem install bundler
```

----

## 四. 安装Rails

```
$ gem install rails
```
查看rails版本：
```
$ rails -v
```
