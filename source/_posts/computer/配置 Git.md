---
layout: post
title: 配置 Git
date: 2023-05-31 07:51:51
tags:
    - Git
    - Linux
    - Windows
categories:
    - Computer
---
## 配置用户信息

```bash
git config --global user.name 'username'
git config --global user.email 'youremail@email.com'
```
<!-- more -->
## 生成 id_rsa 和 id_rsa.pub 

```bash
ssh-keygen -t rsa

# 存储密钥路径
.ssh/
├── authorized_keys
├── id_rsa
├── id_rsa.pub
└── known_hosts

authorized_keys: 免密登录/密钥登录
id_rsa: 密钥
id_rsa.pub: 公开密钥
known_hosts: 记录登录机器信息
```

## 配置Github

1. 在github设置界面打开`SSH and GPG keys`页面
2. 点击`new SSH keys`
3. 填写Title,任意名称
4. `Key type`默认即可
5. 将`id_rsa.pub`中的内容至`Key`内容框中

## 测试 Github 是否连通

```bash
ssh -t git@github.com
```

## 配置免密登录

```bash
scp -P 22 ~/.ssh/id_rsa.pub root@ipAddr:~/home/your
cat ~/home/your/id_rsa.pub > ~/ssh/authorized_keys
ssh root@ipAddr
```