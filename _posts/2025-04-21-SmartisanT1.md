---
title: SMARTISAN T1 刷机教程和资源
date: 2025-04-21 19:00:00 +800
categories: [资源, 手机]
tags: [SMARTISAN]     # TAG names should always be lowercase
description: SMARTISAN Flashing Resources.
pin: false
image:
  path: /assets/image/posts/smartisan/T1.jpg
  alt: SMARTISAN T1
---

# 官方最新包

T1(3G):[https://dl2.smartisan.com/ota/t1/sfo/3.7.2/20180211/3.7.2-2018021111-user-sfo-b16e127f93.zip](http://dl2.smartisan.com/ota/t1/sfo/3.7.2/20180211/3.7.2-2018021111-user-sfo-b16e127f93.zip)
T1(4G):[https://dl2.smartisan.com/ota/t1/sfo_lte/3.7.2/20180211/3.7.2-2018021111-user-sfo_lte-ce47466d52.zip](http://dl2.smartisan.com/ota/t1/sfo_lte/3.7.2/20180211/3.7.2-2018021111-user-sfo_lte-ce47466d52.zip)

# Smartisan T1 (sfo) 底包、TWRP 及相关工具
链接：https://pan.quark.cn/s/e6c844278b53


## 写在前面

1.该手机的厂商不提供刷机保修，意味着刷机后你将失去保修资格，且需要自己承担失手造成故障的风险；

2.该手机无法通过工程线救砖，意味着一旦你失手很可能就无法挽救；

3.该手机首次刷机需要较强的动手能力，请先充分阅读本帖再决定是否继续刷机；

4.魔趣是原生系统，不包含（也不会加入）一步、大爆炸等 Smartisan OS 特色功能。如果你离不开他们，不建议你尝试魔趣。

## 准备工具

1.adb 和 fastboot 工具

2.降级包、解锁文件、TWRP 镜像、底包、魔趣 ROM 等相关资源，详见：[Smartisan T1 (sfo) 底包、TWRP 及相关工具](https://pan.quark.cn/s/e6c844278b53)

## 一、刷入 TWRP

1.将官方降级包 (注意区分 3G 和 4G 版)、底包 (3G/4G 通用)、魔趣 ROM (3G/4G 通用) 放到内置存储中；

2.进官方 Recovery，刷入官方降级包将系统降级到 2.6.7

3.关机，然后同时按住左下键、右上键、Home 键、电源键开机，直到见到 Fastboot Mode；

4.在电脑上执行下列命令 (其中 sec.img 替换成解锁文件的真实路径)：

```shell
fastboot flash security sec.img
```

5.同时按住左下键、右上键、Home 键、电源键，手机会在黑屏后再次进入 Fastboot Mode；
6.在电脑上执行下列命令 (其中 twrp.img 替换成 TWRP 镜像的真实路径)：

```shell
fastboot flash recovery twrp.img
```

7.再次同时按住左下键、右上键、Home 键、电源键，并在手机黑屏后迅速变成按住左上键、右下键、Home 键、电源键，即可进入 TWRP。

## 二、刷入魔趣

1.进 Wipe (清除)，把下面那个条条拖住向右划一下；

2.返回上一层，进 Install (安装)，刷入底包；

3.返回上一层 (不要重启)，再次进安装，刷入魔趣包；

4.刷完重启，完成。

## 如何刷回原厂 Smartisan OS 系统

1.下载官方卡刷包放到内置存储根目录；

2.在 TWRP 里 Wipe，然后刷入卡刷包。


## 视频教程：

[https://www.bilibili.com/video/BV1et411V72G/](https://www.bilibili.com/video/BV1et411V72G/)


# 原贴

Smartisan T1 魔趣刷入教程：
[https://web.archive.org/web/20220525205738/https://bbs.mokeedev.com/t/topic/14699](https://web.archive.org/web/20220525205738/https://bbs.mokeedev.com/t/topic/14699)