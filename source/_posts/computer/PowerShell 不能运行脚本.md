---
layout: post
title: PowerShell 不能运行脚本
date: 2023-06-14 19:41:46
tags:
    - PowerShell
    - Windows
categories:
    - Computer
---

## 解除powershell默认不能运行脚本

[PowerSehll默认禁止运行脚本](https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.3)

> 在管理员模式 PowerShell 输入

```bash
set-ExecutionPolicy RemoteSigned
```
