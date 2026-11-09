---
title: Arch Linux双系统安装
link: arch-linuxshuang-xi-tong-an-zhuang
date: 2023-10-09 17:12:37
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
以下为本人在安装 Windows 系统后，安装 Arch 系统的记录
:::
:::warning
推荐以下 2 个安装教程，前者为 Arch Wiki。但由于 Arch Wiki 有些过于详细、繁琐、具备可选择性，反而有时因为漏看、没能理解或不了解如何选择而造成安装错误，本文旨在通过最简洁的步骤，不纠结地快速完成安装，更倾向于安装后再处理琐碎事务，也尽量少涉及原理，毕竟以下 2 个教程中已经讲得很详细了。
:::
:::danger
Arch Linux 系统安装较为繁琐，建议新手先了解 Linux 系统、vim 编辑器，预留出充足的时间和耐心再开始安装
Arch Linux 相较 Ubuntu 更轻量、更多可选择性，软件包管理系统更强大，Wiki 丰富且有中文论坛，个人认为安装部分软件比 Ubuntu 更快捷方便，也更加喜欢滚动更新的方式
:::
{% links %}
- site: Arch Wiki
  url: https://wiki.archlinuxcn.org/wiki/%E5%AE%89%E8%A3%85%E6%8C%87%E5%8D%97
desc: 点击进入 Arch Linux 中文安装指南
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icon/Archlinux.png
  color: "#0f94d2"
- site: Arch Linux 简明指南
url: https://arch.icekylin.online/guide/rookie/basic-install.html
desc: 点击进入 Arch Linux 安装指南
color: "#ea606e"
{% endlinks %}

# 安装准备
1. 建议准备 U 盘，下载镜像并制作启动盘，制作步骤[参考](/post/kubuntu-22.04an-zhuang/#准备好启动U盘)
{% links %}
- site: Arch Downloads
  url: https://archlinux.org/download/
desc: 点击进入 Arch Linux 下载界面
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icon/Archlinux.png
  color: "#0f94d2"
{% endlinks %}

2. 准备好网络，建议使用网线或手机 USB 共享网络

## 基础安装
1. 连接网络后，同步系统时间
```bash
timedatectl
```

2. 使用`cfdisk`分区
```bash
cfdisk
```
分区示例：
| 挂载点 | 分区 | 分区类型 | 大小 |
| :-: | :-: | :-: | :-: |
| `/mnt/boot` | `/dev/sda5` | EFI 系统分区 | 1G |
| `[SWAP]` | `/dev/sda6` | Linux swap (交换空间) | 16G（依内存而定） |
| `/mnt` | `/dev/sda7` | Linux x86-64 根目录 (/) | 剩余空间 |

3. 格式化分区（以下参数替换为上一步中的挂载点）
格式化根分区：
```bash
mkfs.ext4 /dev/sda7（根分区）
```
格式化交换分区（如有）：
```bash
mkswap /dev/sda6（交换空间分区）
```
格式化系统分区：
```bash
mkfs.fat -F 32 /dev/sda5（EFI 系统分区）
```

4. 挂载分区
挂载根分区：
```bash
mount /dev/sda7（根分区） /mnt
```
挂载 EFI 系统分区：
```bash
mount --mkdir /dev/sda5（EFI系统分区） /mnt/boot
```
启用交换分区（如有）：
```bash
swapon /dev/sda6（交换空间分区）
```

5. 安装软件包
intel 芯片选择`intel-ucode`，AMD 芯片选择`amd-ucode`
```bash
pacstrap -K /mnt base linux linux-firmware intel-ucode base-devel networkmanager vim sudo zsh zsh-completions
```

6. 生成 fstab 文件
```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

7. chroot 到新安装的系统
```bash
arch-chroot /mnt
```

8. 设置时区
```bash
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
hwclock --systohc
```

9. 区域和本地化设置
先设置为英文，在安装的过程中更容易判断和处理问题：
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
生成`locale`：
```bash
locale-gen
```
在`/etc/locale.conf`中设定`LANG`变量：
```bash
echo 'LANG=en_US.UTF-8' > /etc/locale.conf
```

10. 设置主机名
```bash
echo 'myhostname（主机名）' > /etc/hostname
```

11. 设置 root 密码
```bash
passwd
```

12. 安装引导程序
```bash
pacman -S grub efibootmgr os-prober
```
```bash
mount /dev/sda5 /boot
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
```
使用 vim 编辑`/etc/default/grub`文件：
```bash
vim /etc/default/grub
```
去掉`GRUB_DISABLE_OS_PROBER=false`前的注释或添加该语句

生成配置文件：
```bash
os-prober
grub-mkconfig -o /boot/grub/grub.cfg
```

13. 完成安装
```bash
exit
umount -R /mnt
reboot
```

## 后续安装步骤
1. 配置 root 账户的默认编辑器
上述步骤重启后，移除安装介质，使用 root 账号登录，并配置 root 账户的默认编辑器：
```bash
vim ~/.bash_profile
```
之后插入：
```bash
export EDITOR='vim'
```

2. 创建非 root 用户
```bash
useradd -m -G wheel -s /bin/bash myusername
passwd myusername
```

3. 编辑`sudoers`文件
```bash
EDITOR=vim visudo
```
这两行选择一行取消注释（后者相比前者免去了每次输密码的麻烦）
```bash
# %wheel ALL=(ALL:ALL) ALL
# %wheel ALL=(ALL:ALL) NOPASSWD: ALL
```

4. 连接网络
```bash
systemctl enable NetworkManager
systemctl start NetworkManager
```

5. 开启`Multilib`仓库和`archlinuxcn`仓库
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

6. 安装 KDE Plasma 桌面环境
```bash
pacman -S plasma-meta konsole dolphin
```

7. 进入图形化登录界面
```bash
systemctl enable sddm
systemctl start sddm
```

8. 安装中文字体，设置系统为中文
```bash
sudo pacman -S wqy-zenhei noto-fonts noto-fonts-cjk noto-fonts-emoji noto-fonts-extra
```
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/Arch.lang.png#pic_center)
注销或重启后生效

9. 后续步骤
后续需考虑安装 yay 包管理器、中文输入法、浏览器、显卡驱动等，欢迎参考[系列文章](/post/arch-linuxxin-xi-tong-kai-huang)
