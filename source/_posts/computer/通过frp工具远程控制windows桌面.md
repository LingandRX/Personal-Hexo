---
title: 通过frp工具远程控制windows桌面
date: 2023-04-29 17:20:54
sticky: false
tags: 
    - frp 
    - windows
    - Linux
categories:
    - [computer]
---

## frp是什么？

frp 是一个专注于内网穿透的高性能的反向代理应用，支持 TCP、UDP、HTTP、HTTPS 等多种协议。可以将内网服务以安全、便捷的方式通过具有公网 IP 节点的中转暴露到公网。

## 如何通过frp远程控制windows？

> 需要的环境如下：
>
> 一台具有公网ip的云服务器——服务端
>
> 一台搭载windows系统的机器——客户端
>
> 一台测试机——手机、平板、电脑
<!-- more -->
## 服务端配置

## 下载工具

```shell
# 下载frp工具压缩包
wget https://github.com/fatedier/frp/releases/download/v0.48.0/frp_0.48.0_linux_amd64.tar.gz
# 解压
tar -zxvf frp_0.48.0_linux_amd64.tar.gz
# 重命名文件夹
mv frp_0.48.0_linux_amd64 frp
# 移动文件夹至/usr/local/
mv frp /usr/local/
# 进入frp文件夹
cd /usr/local/frp/
```

```shell
# frp的目录结构如下所示
.
├── frpc
├── frpc_full.ini
├── frpc.ini
├── frps
├── frps_full.ini
├── frps.ini
└── LICENSE
```

## 修改frp配置

```shell
# 修改frps.ini文件
vim frps.ini
```

* frps.ini文件

```shell
[common]
# 监听服务器本地的端口
bind_port = 7000
# 日志文件存放位置
log_file = /var/log/frps.log
# 用于客户端和服务端连接的口令
token = 123456
# 以下是web端控制台
dashboard_user = admin ;控制台的用户名
dashboard_pwd = password ;控制台的密码
dashboard_port = 7500 ;控制台的端口
```

## 启动frps服务测试

```shell
# 临时启动
./frps -c frps.ini
# 后台运行
nohup ./frps -c frps.ini & > frp.log

# 通过公网ip地址:7500 查看Web端控制台是否启动成功

# 停止nohup后台运行
# 查看frps进程号PID
ps -def | grep frp
# 杀死进程
kill -9 进程号PID
```

## 注册为systemctl服务

```shell
# 创建systemctl配置文件
vim frps.service
```

```shell
[Unit]
Description = frp server
After = network.target syslog.target
Wants = network.target

[Service]
Type = simple
# frp文件地址，由于frps.ini的日志使用了相对地址，所以WorkingDirectory要指定frp目录
WorkingDirectory=/usr/local/frp
ExecStart = /usr/local/frp/frps -c /usr/local/frp/frps.ini

[Install]
WantedBy = multi-user.target
```

将`frps.service`复制到`/etc/systemd/system`目录下

```shell
cp frps.service /etc/systemd/system
```

启动systemctl的frps服务

```shell
# 设置开机自启
systemctl enable frps
# 启动frps服务
systemctl start frps
# 查看运行状态
systemctl status frps
```

通过查看端口，查看服务是否启动

```shell
netstat -lntup | grep 7000

# 看到如下里面，服务即启动成功
tcp6       0      0 :::7000                 :::*                    LISTEN      2137/frps
```

## 客户端配置

### 下载frp工具

```powershell
# 下载frp
https://github.com/fatedier/frp/releases/download/v0.48.0/frp_0.48.0_linux_amd64.tar.gz
```

* 解压后目录结构如图所示

![image-20230429203637429](http://img.lingandrx.space/image-20230429203637429.png)

## 修改frpc配置

修改`frpc.ini`文件

```shell
[common]
# 服务器公网ip
server_addr = 127.0.0.1
# 服务器开启的端口
server_port = 7000
# 用于客户端和服务端连接的口令
token = 123456

[3389]
type = tcp
local_ip = 127.0.0.1
# windows远程控制端口
local_port = 3389
# 远程访问端口
remote_port = 3214
```

## 启动frpc

### 方法一

```shell
# 在cmd命令行模式下进行
cd */frp_0.47.0_windows_amd64
frpc -c frpc.ini
```

### 方法二

创建`run.bat`文件,并修改`run.bat`内容

```shell
@echo off
if "%1" == "h" goto begin
mshta vbscript:createobject("wscript.shell").run("""%~nx0"" h",0)(window.close)&&exit
:begin
REM
cd frp所在路径
frpc -c frpc.ini
exit
```

```shell
win+r快捷键打开运行，输入shell:starup，打开启动文件夹
```

将`run.bat`的快捷方式放入该文件夹内，即可开机自启，重启电脑生效。

## 远程连接Windows

通过Windows远程连接访问客户端

```shell
# 访问地址公网ip+客户端配置的远程端口
公网ip:3214
# 客户端用户名
user
# 客户端密码
123456
```
