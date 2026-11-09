---
title: 磁盘管理
link: ci-pan-guan-li
date: 2022-02-24 09:29:00
categories:
  - - 本科作业
    - 操作系统
cover: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E7%A3%81%E7%9B%98%E7%AE%A1%E7%90%86.1.png
tags:
  - 操作系统
  - C++
  - QT
---

:::info
程序在 Linux 平台上编写，`Qt(C++)`实现可视化。题目很简单，本项目的特色在于可视化界面。
:::

{% links %}
- site: 磁盘管理
  url: https://github.com/BattleforAzeroth/DiskManagement
desc: github 仓库
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icons/GitHub.png
  color: "#24292f"
{% endlinks %}
# 实验目的
1. 对磁盘调度的相关知识作进一步的了解，明确磁盘调度的原理。
2. 加深理解磁盘调度的主要任务。
3. 通过编程，掌握磁盘调度的主要算法。
# 实验内容
1. 对于如下给定的一组磁盘访问进行调度：
| 请求服务到达 | A   | B   | C   | D   | E   | F   | G   | H   | I   | J   | K   | L   | M   | N   |
| :----------: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| 访问的磁道号 | 30 | 50 | 100 | 180 | 20 | 90 | 150 | 70 | 80 | 10 | 160 | 120 | 40 | 110 |
2. 要求分别采用先来先服务、最短寻道优先以及电梯调度算法进行调度。
3. 要求给出每种算法中磁盘访问的顺序，计算出平均移动道数。
4. 假定当前读写头在 90 号，电梯调度算法向磁道号增加的方向移动。
# 界面 UI
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E7%A3%81%E7%9B%98%E7%AE%A1%E7%90%86.1.png#pic_center)
# 数据说明
通过`data.txt`文件读入数据。
第一行：磁头当前位置，磁头方向；
第 2～n 行：请求服务名称，访问的磁道号。