---
title: Kubuntu 22.04安装
link: kubuntu-22.04an-zhuang
date: 2022-10-10 21:39:51
categories:
  - - Linux
cover: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/Kubuntu%E5%AE%89%E8%A3%85.cover.png
tags:
  - Linux
  - Kubuntu
  - 双系统
---

:::info
以下为本人删除 Linux 双系统并安装 Kubuntu 22.04 的记录，作为 Ubuntu+KDE 的解决方案
:::
:::info
本次是在我的笔记本原有 Windows 系统的基础上安装双系统的记录，且用[空硬盘]{.label .success}安装 Kubuntu
:::
# 删除原有双系统
先在 Windows 中将之前的 Arch 系统[删除:broken_heart:]{.label .danger}，腾出硬盘空间
1. 右键开始菜单，打开磁盘管理
2. 选择要删除的主分区并右键删除
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/Kubuntu%E5%AE%89%E8%A3%85.%E5%88%A0%E9%99%A4%E7%A3%81%E7%9B%98.png#pic_center)

3. EFI 分区是无法直接删除的，在 cmd 中输入`diskpart`
```raw 命令提示符
diskpart
```
4. 在 diskpart 中查看磁盘列表
```raw diskpart
list disk
```
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/Kubuntu%E5%AE%89%E8%A3%85.diskpart.1.png#pic_center)

5. 选择 EFI 分区所在的磁盘
```raw diskpart
sel disk 0
```
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/Kubuntu%E5%AE%89%E8%A3%85.diskpart.2.png#pic_center)

6. 查看磁盘分区表
```raw diskpart
list partition
```
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/Kubuntu%E5%AE%89%E8%A3%85.diskpart.3.png#pic_center)

7. 选择要删除的 EFI 分区
:::danger
注意看清楚，不要选错
:::
```raw diskpart
sel partition 1
```
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/Kubuntu%E5%AE%89%E8%A3%85.diskpart.4.png#pic_center)

8. 设置分区 id，将选定分区转换为`FAT32`分区
```raw diskpart
set id=ebd0a0a2-b9e5-4433-87c0-68b6b72699c7
```
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/Kubuntu%E5%AE%89%E8%A3%85.diskpart.5.png#pic_center)

9. 此时可以按第二步中的方法，将 EFI 分区删除
# 修复启动项
:::warning
该步骤的意义是避免 Windows 无法启动
如果开机时可以选择启动方式，该步骤也可以后续再进行
通常情况下，删除 Ubuntu 系统后需要解决此问题
:::
因为 Ubuntu 安装后在 Windows 的 EFI 分区增加了 Ubuntu 的启动项，需要清理，也是导致删除双系统后无法进入 Windows 的可能原因
1. 选择 Windows EFI 分区所在的磁盘
```raw diskpart
sel disk 1
```

2. 查看磁盘分区表
```raw diskpart
list partition
```
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/Kubuntu%E5%AE%89%E8%A3%85.diskpart.6.png#pic_center)

3. 选择 Windows EFI 分区
```raw diskpart
sel partition 1
```

4. 分配盘符
```raw diskpart
assign letter = P
```
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/Kubuntu%E5%AE%89%E8%A3%85.diskpart.7.png#pic_center)

5. 分配盘符后不能直接打开，以管理员权限打开 cmd（开始菜单搜索 cmd，右键以管理员身份运行）
先输入刚才分配的盘符
```raw 命令提示符
P:
```
进入 EFI 文件夹
```raw 命令提示符
cd EFI
```
显示子目录
```raw 命令提示符
dir /b
```
删除 ubuntu 文件夹
```raw 命令提示符
rmdir /s/q ubuntu
```
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/Kubuntu%E5%AE%89%E8%A3%85.diskpart.8.png#pic_center)

# 准备好启动 U 盘
1. 从[官网](https://kubuntu.org/)下载镜像，还需要一个 Rufus 工具
{% links %}
- site: Kubuntu 官网下载
url: https://kubuntu.org/getkubuntu/
desc: 点击进入 Kubuntu 官网下载界面
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icons/Kubuntu.png
  color: "#007ac2"
- site: Rufus 官网下载
url: https://rufus.ie/zh/
desc: 点击进入 Rufus 官网下载界面
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icons/rufus.png
  color: "#3f4555"
  {% endlinks %}
2. 制作启动盘
:::warning
不是直接复制到 U 盘哦！
:::
在 Rufus 中选择下载好的 iso 镜像，核对无误后点击开始即可
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/Kubuntu%E5%AE%89%E8%A3%85.refus.png#pic_center)

3. 在 BIOS（我的电脑是[F10]{.kbd .red}）里设置启动顺序，优先 U 盘
如果在启动时可以选择启动方式也可以（我的电脑是[F9]{.kbd .red}）
# 开始安装
现在都是傻瓜式安装了，也不需要手动分区，就不展示了
:::warning
安装时千万不要选错硬盘哦！
:::