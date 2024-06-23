---
layout: post
title: 安装 Hexo
date: 2023-06-29 09:51:27
tags:
    - Hexo
    - Node
categories:
    - Computer
---

## 安装和配置Git

[Git下载链接](https://git-scm.com/downloads)
```bash
# 安装Git
apt-get -y install git

# 配置Git
git config global user.name="testname"
git config global user.email="test@email.com"
```

## 安装NVM和Node

[nvm文档](https://github.com/nvm-sh/nvm)
[nvm-windows 下载链接](https://github.com/coreybutler/nvm-windows/releases)
```bash
# 安装Node.js
# 检测npm和node是否安装
nvm -v

# nvm 已安装列表
nvm list
# nvm 远程可安装列表
nvm list available
# nvm 卸载指定版本
nvm uninstall [version]
# nvm 使用指定版本
nvm use [version]

# 安装顺序
nvm list available
nvm install [version]
nvm list
nvm use [version]
node -v
```

```bash
npm install npm -g
```

### 设置Nvm和Node镜像源

```bash
# 配置当前安装包的镜像源
npm install -g <安装包名> --registry=https://registry.npm.taobao.org
# 本次安装为当前配置的镜像源
npm install --registry=https://registry.npm.taobao.org   
# 查看当前镜像源
npm config get registry
# 修改~/.npmrc，加入以下内容
npm config set registry https://registry.npm.taobao.org   
registry = https://registry.npm.taobao.org   
```

> 使用cnpm更换npm

```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org   
```

> 查看全局安装的包

```bash
npm -g list
```

## 安装和配置Hexo

```bash
# 全局安装 hexo
npm install -g hexo-cli
# 局部安装 hexo
npm install hexo
# 安装 Hexo 主题
git clone https://github.com/theme-next/hexo-theme-next /hexo/themes/next
```

```bash
# 修改_config.xml
# 主题
theme: next
# github部署
deploy:
  type: git
  repo: git@github.com:github名字/仓库名字
  branch: master
```
