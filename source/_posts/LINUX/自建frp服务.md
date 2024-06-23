---
title: 自建frp服务
date: 2024-06-23 20:47:41
tags:
    - Linux
    - frp
categories:
    - [LINUX]
---


## 序言
[Frp链接](https://github.com/fatedier/frp)
[Frp中文文档](https://gofrp.org/zh-cn/docs/)
1. 安装
2. 配置
## 安装
### 解压Frp工具包
```bash
# 下载链接:https://github.com/fatedier/frp/releases
wget https://github.com/fatedier/frp/releases/download/v0.58.1/frp_0.58.1_linux_amd64.tar.gz
# 解压
tar -zxvf frp_0.58.1_linux_amd64.tar.gz /usr/local/frp

# 使用 yum 安装 systemd（CentOS/RHEL）
yum install systemd

# 使用 apt 安装 systemd（Debian/Ubuntu）
apt install systemd
```
### 创建frps.service服务
```bash
# 创建service文件,用于管理frps服务
sudo vim /etc/systemd/system/frps.service
```
`frps.service`:
```ini
[Unit]
# 服务名称，可自定义
Description = frp server
After = network.target syslog.target
Wants = network.target

[Service]
Type = simple
# 启动frps的命令，需修改为您的frps的安装路径
ExecStart = /usr/local/frp/frps -c /usr/local/frp/frps.toml

[Install]
WantedBy = multi-user.target
```

```bash
# 启动frp
sudo systemctl start frps
# 停止frp
sudo systemctl stop frps
# 重启frp
sudo systemctl restart frps
# 查看frp状态
sudo systemctl status frps
# 开启自启动
sudo systemctl enable frps
```

## 配置

### 通过自定义域名访问内网的 Web 服务
`frps.toml`
```toml
bindPort = 7000
vhostHTTPPort = 8080
```
`frpc.toml`
```toml
serverAddr = "x.x.x.x"
serverPort = 7000

[[proxies]]
name = "web"
type = "http"
localPort = 80
customDomains = ["www.yourdomain.com"]

[[proxies]]
name = "web2"
type = "http"
localPort = 8080
customDomains = ["yourIp"]
```
