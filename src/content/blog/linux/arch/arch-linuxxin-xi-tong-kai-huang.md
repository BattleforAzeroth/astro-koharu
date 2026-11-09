---
title: Arch Linux新系统开荒
link: arch-linuxxin-xi-tong-kai-huang
date: 2023-3-24 21:31:20
categories:
  - - Linux
    - Arch
cover: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/Arch.cover.png
tags:
  - Linux
  - Arch Linux
  - 双系统
---

:::info
以下为本人安装 Arch 系统后，安装软件和解决一些小毛病的记录
持续施工中...
:::

# 写在最前
## 区域设置
:::warning
不进行此步骤可能导致的问题：QQ、微信等输入中文无法上词
如果在安装系统时已经设置过可以跳过此步
:::
编辑`/etc/locale.gen`文件，取消美式英语和中国简体前的注释：
```bash
vim /etc/locale.gen
```
:::primary no-icon
...
#en_SG ISO-8859-1
en_US.UTF-8 UTF-8
#en_US ISO-8859-1
...
#zh_CN.GBK GBK
zh_CN.UTF-8 UTF-8
#zh_CN GB2312
...
:::
生成 Locale，并设置整个系统使用的区域设置：
```bash
sudo locale-gen
sudo localectl set-locale LANG=zh_CN.UTF-8
```
locale.conf 的变更会在下次登录时生效，要立刻应用新的设置的话，可以运行：
```bash
sudo unset LANG
sudo source /etc/profile.d/locale.sh
```
# 安装日常软件
## `yay`包管理器
`yay`包管理器是安装 AUR 软件包的前提，强烈建议安装
+++danger 先确保已经开启`Multilib`仓库和`archlinuxcn`仓库
:::warning
如果在安装系统时已经设置过可以跳过此步
:::
编辑`/etc/pacman.conf`，取消对应行前面的注释：
```bash
sudo vim /etc/pacman.conf
```

- [ ] ~~#[multilib]~~{.danger}
- [ ] ~~#Include = /etc/pacman.d/mirrorlist~~{.danger}
- [x] [multilib]
- [x] Include = /etc/pacman.d/mirrorlist

然后插入：
```bash
[archlinuxcn]
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
```
更新一下源，再导入 GPG key：
```bash
sudo pacman -Sy
sudo pacman -S archlinuxcn-keyring
```
+++
```bash
sudo pacman -S yay
```
建议隔一段时间使用以下命令同步更新软件包：
```bash
yay -Syu
```

## 安装搜狗输入法
### 安装 fcitx 及搜狗输入法
```bash
yay -S fcitx fcitx-qt5 fcitx-configtool fcitx-sogoupinyin
```
注销或重启后，右键选择启用搜狗输入法
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/Arch.fcitx.png#pic_center)
:::warning
在输入框内，默认切换输入法快捷键是[Ctrl]{.kbd .red}+[空格]{.kbd .red}，显示搜狗拼音输入法、能正常使用代表安装成功！
:::

### 解决搜狗输入法不能在 Konsole、Kate 等软件中使用
修改`/etc/profile`：
```bash
sudo vim /etc/profile
```

并插入以下语句：
```bash
#fcitx
export XIM_PROGRAM=fcitx
export XIM=fcitx
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
```
注销或重启即可

## 安装 QQ
### 安装新架构 QQ
推荐安装新架构 QQ：
```bash
yay -S linuxqq
```
### 安装旧架构 QQ
旧架构 QQ 采用 wine 容器实现
```bash
yay -S deepin-wine-qq
```
运行应用菜单中创建的 QQ 快捷方式，开始安装（建议安装时不更改目录）
偶然发现运行快捷方式闪退，输入以下命令进行安装：
```bash
/opt/apps/com.qq.im.deepin/files/run.sh -d
```
如发生问题，可参考该项目的[GitHub 仓库](https://github.com/vufa/deepin-wine-qq-arch#%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98%E5%8F%8A%E8%A7%A3%E5%86%B3)：
{% links %}
- site: deepin-wine-qq-arch
  url: https://github.com/vufa/deepin-wine-qq-arch#%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98%E5%8F%8A%E8%A7%A3%E5%86%B3
desc: 点击进入 Github 仓库界面查看常见问题解决方法
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icons/GitHub.png
  color: "#24292f"
{% endlinks %}

## 安装浏览器
安装火狐浏览器：
```bash
sudo pacman -S firefox
```
安装 Chrome 浏览器
```bash
yay -S google-chrome
```

## 安装显卡驱动
### 安装 Nvidia 闭源显卡驱动
首先确定显卡型号，我的 1660Ti 不新不旧，正好适合安装闭源驱动
最新的显卡也许需要安装`nvidia-beta`和`nvidia-utils-beta`，以及较老的显卡可参考[Arch Wiki](https://wiki.archlinux.org/title/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#%E5%AE%89%E8%A3%85)
{% links %}
- site: NVIDIA-Arch Wiki
  url: https://wiki.archlinux.org/title/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#%E5%AE%89%E8%A3%85
desc: 点击进入 Arch Wiki
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icons/Archlinux.png
  color: "#0f94d2"
{% endlinks %}
根据内核选择安装，如对于`linux`内核安装`nvidia`（如果是`linux-lts`，对应`nvidia-lts`）：
```bash
sudo pacman -S nvidia
```
### 安装 intel 核芯显卡驱动
仍然建议先参考[Arch Wiki](https://wiki.archlinuxcn.org/wiki/Intel_%E5%9B%BE%E5%BD%A2%E5%A4%84%E7%90%86%E5%99%A8#%E5%AE%89%E8%A3%85)
```bash
sudo pacman -S mesa lib32-mesa vulkan-intel lib32-vulkan-intel
```

# 安装编程软件、环境
## 安装 JetBrains 系列软件
### 安装`Toolbox`
:::info
由于本人需要安装多款 JetBrains 系列软件，采取先安装`Toolbox`，并借助此工具安装、管理`IDEA`、`PyCharm`、`Android Studio`等软件
:::
安装方法有从[AUR 仓库安装](https://aur.archlinux.org/packages/jetbrains-toolbox)和[官网安装](https://www.jetbrains.com/zh-cn/toolbox-app/)：
{% links %}
- site: JetBrains Toolbox-AUR 仓库页面
url: https://aur.archlinux.org/packages/jetbrains-toolbox
desc: 点击进入 AUR 仓库检查更新时间
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icons/Archlinux.png
  color: "#0f94d2"
- site: JetBrains Toolbox 官网
url: https://www.jetbrains.com/zh-cn/toolbox-app/
desc: 点击进入 JetBrains Toolbox 官网下载界面
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icons/toolbox.png
color: "#c01fd9"
{% endlinks %}
建议从 AUR 仓库安装，但如果 AUR 仓库未及时更新版本可考虑从官网安装（从 AUR 仓库链接中检查更新时间 Last Updated）
```bash
yay -S jetbrains-toolbox
```
下载完成后打开此工具，下载所需软件，后续可以更新，需要使用多款 JetBrains 系列软件时非常方便！（经测试`Android Studio`需要设置代理才能下载）

### 激活诀窍
{% links %}
- site: https://jetbra.in/s
  url: https://jetbra.in/s
desc: 点击进入网页下载 jetbra.zip
color: "#ea606e"
{% endlinks %}
打开上述网页后选择一个有效链接并进入，根据上方提示信息点击下载`jetbra.zip`文件
解压后放在你想放的位置，执行`install.sh`文件，例如此时终端的位置是`jetbra`的父目录：
```bash
sh jetbra/scripts/install.sh
```
注销或重启后，在之前的网站上找到对应软件，点击下方的`Copy to clipboard`按钮，并看到`Copied!`提示
打开 IDE，粘贴激活码，呈绿色，此时可点击`Activate`激活

### 解决 fcitx、搜狗输入法的输入框不随光标移动问题
:::info
这个是简单粗暴的解决办法，直接下载他人编译好的 jbr 而非自己编译
:::
以下为[jbr 下载地址](https://github.com/RikudouPatrickstar/JetBrainsRuntime-for-Linux-x64/releases)和[官方替换教程](https://intellij-support.jetbrains.com/hc/en-us/articles/206544879-Selecting-the-JDK-version-the-IDE-will-run-under)：
{% links %}
- site: jbr 下载地址
url: https://github.com/RikudouPatrickstar/JetBrainsRuntime-for-Linux-x64/releases
desc: 点击进入 Github Releases 界面下载
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icons/GitHub.png
  color: "#24292f"
- site: JetBrains 官方替换教程
url: https://intellij-support.jetbrains.com/hc/en-us/articles/206544879-Selecting-the-JDK-version-the-IDE-will-run-under
desc: 点击查看 JetBrains 官方替换教程
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icons/JetBrains.png
color: "#000000"
{% endlinks %}
例如（注意看文章时间，请根据后续看版本号的方法下载++对应版本++{.dot}的 jbr 文件），下载`jbr_jcef-17.0.6-linux-x64-b829.5.tar.gz`
解压后放在你想放的位置，得到了文件夹`jbr_jcef-17.0.6-linux-x64-b829.5`
对于每个 IDE，打开后选择：`帮助`:arrow_right:`查找操作`（快捷键[Ctrl]{.kbd .red}+[Shift]{.kbd .red}+[A]{.kbd .red}）
输入`choose`，选择`选择IDE的启动Java运行时...`
点击新建右边的文本框:arrow_right:`添加自定义运行时...`:arrow_right:`添加JDK...`:arrow_right:然后选择刚才解压后的文件夹
:::danger
目前发现 Android Studio 可能导致 IDE 无法启动
发生意外导致 IDE 无法启动时，在~/.config/Google/AndroidStudio2021.3 文件夹中删除 studio.jdk 文件。类似地，其他 IDE 对应目录在~/.config/JetBrains 中
:::
## 安装 Anaconda 环境
```bash
yay -S anaconda
```
取消 anaconda 在终端中默认使用 base 环境（可选）：
```bash
conda config --set auto_activate_base false
```
## 安装 Docker
```bash
yay -S docker
```
启用 Docker 服务
```bash
sudo systemctl start docker
sudo systemctl enable docker
```
将用户加入 Docker 组
```bash
sudo gpasswd -a $USER docker
```
更新 Docker 组
```bash
newgrp docker
```

## 安装 Node.js 以及 NPM
```bash
sudo pacman -S nodejs npm
```

# 安装工具
## 安装图片查看器
安装`Gwenview`
```bash
sudo pacman -S gwenview
```

## 安装解压缩软件
安装`Ark`：
```bash
sudo pacman -S ark
```

## 安装文本编辑器
安装`Kate`
```bash
sudo pacman -S kate
```

# 辅助功能
## 解决 Arch 和 Windows 双系统时间不同步
在 Windows 系统中，以管理员权限打开 cmd（开始菜单搜索 cmd，右键以管理员身份运行）
```raw 命令提示符
reg add "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation" /v RealTimeIsUniversal /d 1 /t REG_DWORD /f
```
## 自动挂载 Windows 某磁盘
:::info
这源于我个人经验也推荐这种存储文件的方式
Windows 分为系统盘、文件盘和软件盘，软件盘的软件基本只能在 Windows 下运行，文件盘包括文件资料和代码仓库，只需启动 Linux 时自动挂载文件盘（不自动也可以，但是每次启动需要点一次，麻烦）
:::
首先需要下载`ntfs-3g`工具：
```bash
sudo pacman -S ntfs-3g
```
从 KDE 自带的 Dolphin 文件管理器中观察到手动挂载通常会挂载到`/run/media/maomao/Files`目录（`maomao`是用户名），于是尝试设置自动挂载到这个目录
先查看 Windows 磁盘的分区：
```bash
sudo fdisk -l
```
找到 Windows，确定磁盘对应的分区（此例中是`/dev/nvme0n1p4`）
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/Arch.fdisk.png#pic_center)

修改`/etc/fstab`文件：
```bash
sudo vim /etc/fstab
```
增加以下语句（请看情况修改++分区++{.dot}（第 1 个参数）和++挂载点++{.dot}（第 2 个参数））
```bash
/dev/nvme0n1p4 /run/media/用户名/磁盘卷标（磁盘名称） ntfs-3g defaults 0 0
```
上面简单配置即可使用，高级参数设置可参考[Arch Wiki](https://wiki.archlinux.org/title/NTFS-3G_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#%E9%85%8D%E7%BD%AE)
{% links %}
- site: NTFS-3G-Arch Wiki
  url: https://wiki.archlinux.org/title/NTFS-3G_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#%E9%85%8D%E7%BD%AE
desc: 点击进入 Arch Wiki
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icons/Archlinux.png
  color: "#0f94d2"
{% endlinks %}

# 系统美化
## GRUB 界面美化
从以下网站中挑选一个 GRUB 主题
{% links %}
- site: GNOME-LOOK
  url: https://www.gnome-look.org/browse?cat=109&ord=rating
desc: 点击查看 GNOME-LOOK GRUB 主题
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icons/Gnome.png
  color: "#282828"
  {% endlinks %}
以`Dark Matter GRUB Theme`为例，安装这个主题，在适当的位置下载并构建：
```bash
git clone --depth 1 https://gitlab.com/VandalByte/darkmatter-grub-theme.git && cd darkmatter-grub-theme
sudo python3 darkmatter-theme.py --install
```
后续按提示安装即可
