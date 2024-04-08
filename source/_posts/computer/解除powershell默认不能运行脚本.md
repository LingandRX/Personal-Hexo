---
layout: post
title: 解除powershell默认不能运行脚本
date: 2023-06-14 19:41:46
tags:
    - powershell
categories:
    - [computer]
---


## PowerShell不能运行脚本

因为PowerSehll默认禁止运行脚本的
具体可以参考微软的说明[https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.3]

## 解除powershell默认不能运行脚本

在PowerShell管理员模式输入

```shell
 set-ExecutionPolicy RemoteSigned
```
