---
layout: post
title: hexo安装
date: 2023-06-29 09:51:27
tags: 
    - blog
categories:
    - [computer]
---

## 安装Git

> 安装Git

```shell
apt-get -y install git
```

> 配置Git
<!-- more -->
```shell
git config global user.name="testname"
git config global user.email="test@email.com"
```

## 安装Node.js

> 检测npm和node是否安装

```shell
npm -v
node -v
```

> 升级npm版本

```shell
npm install npm -g
```

> 设置npm淘宝镜像源，查看npm镜像源

```shell
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

```shell
npm install -g cnpm --registry=https://registry.npm.taobao.org   
```

> 查看全局安装的包

```shell
npm -g list
```

## 安装Hexo

```shell
npm install -g hexo-cli
# 局部安装hexo
npm install hexo
#linux
echo 'PATH="$PATH:./node_modules/.bin"' >> ~/.profile
```

## 安装Hexo主题

```shell
git clone https://github.com/theme-next/hexo-theme-next /hexo/themes/next
```

## 配置Hexo

```shell
# 修改_config.xml
# 主题
theme: next
# github部署
deploy:
  type: git
  repo: git@github.com:github名字/仓库名字
  branch: master
```
