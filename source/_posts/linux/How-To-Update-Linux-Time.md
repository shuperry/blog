---
title: 如何更新并自动同步 Linux 时间
date: 2017-02-07 15:02:12
updated:
tags:
  - linux
  - ntpdate
categories: linux
comments: true # 开启回复功能
toc: false # 开启自动生成目录
---
　　很多人经常会发现 Linux 的时间不知道什么时候就不对了，如果刚好是作为某个业务系统的后台或数据库服务器的话就会引来一系列的麻烦，系统里很多数据的时间不对了，对排错和处理数据也会带来相当的工作量，这篇文章主要是讲解如何更新并自动同步 Linux 的时间。
<!--more-->

#### 只更新一次时间：

---

##### 安装 ntp 工具

```bash
$ yum install ntp -y
```

##### 同步一次服务器时间

``` bash
$ ntpdate -u us.pool.ntp.org
```

#### 自动同步时间:

---

##### 设置定时同步时间任务，每 10 分钟执行一次

``` bash
$ crontab -e
```

**注: 在打开的窗口中输入 `*/10 * * * * /usr/sbin/ntpdate -u us.pool.ntp.org`。**

##### 如果发现上一步操作中提示没有 `crontab`, 则请先执行此步骤安装 `crontab` 服务后再执行上一步操作

``` bash
$ yum  install -y vixie-cron
```

有些同学可能会问，时区的问题怎么处理？别急，下面附带时区相关操作。

##### 查看服务器时区

``` bash
$ date -R
```

**注: 如果时区是 `+0800` 则表示为东八区，在国内的同学就不用去修改时区了。**

##### 修改服务器时区

``` bash
$ rm -rf /etc/localtime
$ ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

**注: 以上操作是将当前时区修改为上海时区。**
