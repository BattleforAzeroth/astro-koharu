---
title: 解锁、刷机、ROOT
link: jie-suo-shua-ji-root
date: 2023-6-10 19:04:21
categories:
  - - 刷机相关
cover: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/Magisk.cover.png
tags:
  - 刷机
---

:::info
以下为本人解 BL 锁、刷机、刷 ROOT 的记录，手机型号为`Redmi K60 pro`
持续施工中...
:::
# 解 BL 锁
[官方解锁](https://www.miui.com/unlock/index.html)
{% links %}
- site: 官方解锁
  url: https://www.miui.com/unlock/index.html
desc: MIUI 官方解锁工具
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icons/MIUI.png
  color: "#f76600"
  {% endlinks %}

在`开发者选项`中找到`设备解锁状态`，对于新机而言，需要绑定小米账号并等待 7 天

#F76600
# 刷机
{% links %}
- site: 小米 ROM
url: https://xiaomirom.com/
desc: 包含众多小米官方 ROM
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icons/MIUI.png
  color: "#f76600"
  {% endlinks %}


## 线刷
[线刷工具](https://xiaomirom.com/download-xiaomi-flash-tool-miflash)
推荐：[小米线刷报错问题及解决方法](https://miuiver.com/miflash-problem-list/)

## 卡刷
卡刷比线刷方便，一般选择下载 TWRP，注意要下载相同 Android 版本的 TWRP，然后到 fastboot 模式刷入

# ROOT
采用安装 Magisk 的方式获取 ROOT，参考[Magisk 安装](/post/magiskan-zhuang)
TWRP:arrow_right:安装:arrow_right:切换到刷入 Image 模式，手动选择修补后的 img 文件:arrow_right:选择 Boot 分区刷入