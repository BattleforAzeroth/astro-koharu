---
title: Magisk安装
link: magiskan-zhuang
date: 2023-6-10 19:04:21
categories:
  - - 刷机相关
cover: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/Magisk.cover.png
tags:
  - 刷机
---

:::info
以下为本人安装 Magisk 的记录，手机型号为`Redmi K60 pro`
持续施工中...
:::

# 安装 Magisk
{% links %}
- site: Magisk
  url: https://github.com/topjohnwu/Magisk
desc: 官方 Magisk github 仓库
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icons/Magisk.png
  color: "#00b09d"
{% endlinks %}
前往[Releases 页面](https://github.com/topjohnwu/Magisk/releases)，下载 APK 安装包并安装

## 修补 init_boot
### 提取 init_boot
`init_boot.img`线刷包中可以找到，而卡刷包需要从`payload.bin`中提取（现在 Magisk 也可以自动使用`payload.bin`进行修补）
### 修补 init_boot
打开 Magisk，选择 Magisk 安装，点击选择并修补一个文件，选择`init_boot.img`文件，修补完成后直接刷入修补后的 init_boot
默认修补后文件位置在`Downloads`文件夹，使用 TWRP 刷入（线刷理论也可）
