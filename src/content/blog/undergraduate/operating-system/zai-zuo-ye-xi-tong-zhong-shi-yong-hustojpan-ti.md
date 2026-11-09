---
title: 在作业系统中使用HustOJ判题
link: zai-zuo-ye-xi-tong-zhong-shi-yong-hustojpan-ti
date: 2023-04-06 05:05:16
categories:
  - - 本科作业
    - 操作系统
cover: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/HUSTOJ.cover.png
tags:
  - SpringBoot
  - MySQL
---

# 安装 HustOJ
1. 建议使用 Ubuntu 等官方支持系统，使用自动安装脚本安装，不建议使用 Docker
2. 安装完成后打开`127.0.0.1`即可看到图形化界面
3. 数据库运行在 3306 端口，用户名密码在安装完成后终端里显示，注意保存

# 判题结果对照表
判题结果保存在`jol`数据库中`solution`表的`result`列
`result=4`表示通过，`result<4`表示完成判题
| result | 英文 | 中文 |
| :-: | :-: | :-: |
| 0 | Pending | 等待中 |
| 1 | Pending_Rejudging | 等待重判 |
| 2 | Compiling | 编译中 |
| 3 | Running_Judging | 判题中 |
| 4 | Accepted | 结果正确 |
| 5 | Presentation_Error | 格式错误 |
| 6 | Wrong_Answer | 答案错误 |
| 7 | Time_Limit_Exceed | 时间超限 |
| 8 | Memory_Limit_Exceed | 内存超限 |
| 9 | Output_Limit_Exceed | 输出超限 |
| 10 | Runtime_Error | 运行时错误 |
| 11 | Compile_Error | 编译错误 |
| 12 | Compile_OK | 编译通过 |
| 13 | TEST_RUN |  |
| 14 | MANUAL_CONFIRMATION |  |
| 15 | SUBMITTING | 提交中 |
| 16 | REMOTE_PENDING | 远程等待中 |
| 17 | REMOTE_JUDGING | 远程判题中 |
