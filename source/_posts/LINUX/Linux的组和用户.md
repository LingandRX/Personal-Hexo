---
layout: post
title: Linux的组和用户
date: 2023-06-29 10:41:41
tags:
    - Linux
categories:
    - [LINUX]
---

> 查看用户组和用户

```shell
cat /etc/group
cat /etc/passwd
```

> 删除用户组和用户

```shell
# 删除用户组
groupdel 用户组
# 删除用户，不删除用户数据
userdel 用户
# 删除用户，删除用户数据
userdel -r 用户
```
