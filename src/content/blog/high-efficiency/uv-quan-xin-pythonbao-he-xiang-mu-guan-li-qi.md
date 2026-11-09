---
title: uv（全新Python包和项目管理器）
link: uv-quan-xin-pythonbao-he-xiang-mu-guan-li-qi
date: 2025-08-26 14:39:25
categories:
  - - 高效工具
cover: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/uv.cover.png
tags:
  - 高效工具
  - uv
  - Python
---

uv 官方[docs](https://docs.astral.sh/uv)：
{% links %}
- site: uv 官方 docs
url: https://docs.astral.sh/uv
desc: 点击查看 uv 官方文档
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icons/uv.png
  color: "#26102f"
  {% endlinks %}

# 在项目里使用（pyproject.toml 工作流）
## 初始化项目
```bash
mkdir hello-uv && cd hello-uv
uv init
```
这会生成一个最小的`pyproject.toml`并准备好项目结构，也可以在已有项目目录里执行`uv init`来补齐配置。该命令将生成以下文件：
```plain
├── .gitignore
├── .python-version
├── README.md
├── main.py
└── pyproject.toml
```
## 创建虚拟环境
若省去该步骤，uv 也会在安装依赖时自动创建虚拟环境
```bash
# 在项目目录创建虚拟环境（.venv）
uv venv
# 指定Python版本创建虚拟环境
uv venv --python 3.12
```
## 添加依赖
```bash
uv add <package_name>
# 安装指定版本Python包
uv add '<package_name>==2.31.0'
```
`uv add`会更新`pyproject.toml`并写入锁文件`uv.lock`，保证可复现安装
## 导入 requirements.txt
```bash
uv add -r requirements.txt
```
## 删除依赖
```bash
uv remove <package_name>
```
## 升级包
```bash
uv lock --upgrade-package requests
```
该`--upgrade-package`标志将尝试将指定的包更新到最新的兼容版本，同时保持锁文件的其余部分完好无损
## 使用代理安装依赖
需要注意，该方法的临时环境变量只对当前终端有效
```bash
export HTTPS_PROXY=<proxy>
uv add <package_name>
```
