---
title: 引导程序
link: yin-dao-cheng-xu
date: 2022-03-03 19:46:48
categories:
  - - 本科作业
    - 操作系统
cover: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E5%BC%95%E5%AF%BC%E7%A8%8B%E5%BA%8F.3.png
tags:
  - 操作系统
  - 引导程序
  - 汇编
---

# 实验目的
1. 对主引导记录进行理解。
2. 明白操作系统生成的过程。
3. 在 U 盘上实现一个可运行的引导程序。
# 实验内容
1. 用汇编语言编写一小段程序，如在屏幕上输出一个字符。（调用中断）
2. 利用命令或 winhex 等工具将编译好的二进制程序写入 U 盘的主引导记录
3. 开机，选择 U 盘启动，观察实验效果。
4. 进一步地，丰富前述程序的功能，如增加键盘中断，可以对键盘上的动作进行响应（如敲入某字符 X，屏幕能回显即可）。
5. 再次写入引导扇区，观察实验效果
:::info
预备知识：主引导记录、操作系统的生成和初启、汇编
:::
# 程序功能及设计思路
## 在屏幕上显示字符
使用 es（附加段寄存器）寄存器来存储和显示字符。首先，通过 es 寄存器指向显存地址：
```al
mov ax,0xb800
mov es,ax
```
由于字符和颜色是交替存储的，先指定字符：
```al
mov byte [es:0x00],'H'
mov byte [es:0x02],'e'
mov byte [es:0x04],'l'
mov byte [es:0x06],'l'
mov byte [es:0x08],'o'
mov byte [es:0x0a],','
mov byte [es:0x0c],"u"
mov byte [es:0x0e],'b'
mov byte [es:0x10],'u'
mov byte [es:0x12],'n'
mov byte [es:0x14],'t'
mov byte [es:0x16],'u'
mov byte [es:0x18],'!'
```
## 键盘输入字符回显
累加器 eax 从地址`0x01`开始，ecx 控制循环次数。每设置一个颜色后，累加器 eax 增加 2，设置下一地址的颜色。
```al
    mov eax, 0x01
    mov ecx, 0x19
color:
    mov byte [es:eax],0x0a
    add eax,2
    mov byte [es:eax],0x0b
    add eax,2
    mov byte [es:eax],0x0c
    add eax,2
    mov byte [es:eax],0x0d
    add eax,2
    mov byte [es:eax],0x0e
    add eax,2
    mov byte [es:eax],0x09
    add eax,2
    mov byte [es:eax],0x0f
    add eax,2
    loop color
```
## 键盘输入字符回显
通过`int 16h`即键盘中断，可以将键盘输入的字符放入寄存器 AL 中，再通过`int 10h`中断则可以将 AL 中的内容回显在屏幕上。
```al
start:
    mov ah, 0h
    int 16h
    mov ah, 0eh
    int 10h
    jmp start
```
## 总结：完整代码
完整的代码如下：
```al
    org 7c00h
    mov ax,0xb800
    mov es,ax
    mov byte [es:0x00],'H'
    mov byte [es:0x02],'e'
    mov byte [es:0x04],'l'
    mov byte [es:0x06],'l'
    mov byte [es:0x08],'o'
    mov byte [es:0x0a],','
    mov byte [es:0x0c],"u"
    mov byte [es:0x0e],'b'
    mov byte [es:0x10],'u'
    mov byte [es:0x12],'n'
    mov byte [es:0x14],'t'
    mov byte [es:0x16],'u'
    mov byte [es:0x18],'!'
    mov eax, 0x01
    mov ecx, 0x19
color:
    mov byte [es:eax],0x0a
    add eax,2
    mov byte [es:eax],0x0b
    add eax,2
    mov byte [es:eax],0x0c
    add eax,2
    mov byte [es:eax],0x0d
    add eax,2
    mov byte [es:eax],0x0e
    add eax,2
    mov byte [es:eax],0x09
    add eax,2
    mov byte [es:eax],0x0f
    add eax,2
    loop color
    jmp start
start:
    mov ah, 0h
    int 16h
    mov ah, 0eh
    int 10h
    jmp start
times 510-($-$$) db 0
    db 0x55,0xaa
```
# 程序运行情况
## 软盘映像启动
用 NASM 将汇编程序制作成`img映像文件`，并用虚拟机打开：
![内置字符，彩色](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E5%BC%95%E5%AF%BC%E7%A8%8B%E5%BA%8F.1.png#pic_center "内置字符，彩色")
开机，就可以看到程序中设置好的“Hello,ubuntu!”内容，字体的颜色是循环的彩色。
![回显字符，同样彩色](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E5%BC%95%E5%AF%BC%E7%A8%8B%E5%BA%8F.2.png#pic_center "回显字符，同样彩色")
在键盘上输入字符，每输入一个字符就会得到即时的屏幕回显，并且回显的字符也是彩色。
## U 盘启动
用 NASM 将汇编程序制作成二进制的`bin文件`，再用 WinHex 写入到 U 盘中的前`512`个字节。
![WinHex写入U盘](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E5%BC%95%E5%AF%BC%E7%A8%8B%E5%BA%8F.3.png#pic_center "WinHex写入U盘")
:::warning
UEFI 似乎是不能启动的，在 BIOS 中改用传统启动
:::
:::info
U 盘启动和虚拟机中的效果基本一致，就不再展示啦
:::