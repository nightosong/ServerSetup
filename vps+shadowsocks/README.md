[TOC]
# Vultr + VPS + Shadowsocks

## 购买

网址：https://www.vultr.com

* 1.选择Location
* 2.选择系统（Centos7-64bit）
* 3.选择配置
* 4.额外选项(Enabel IPv6, Enable Private Networking)

（后续补图）

## 服务器

### 下载Xshell

### 配置shadowsocks

* 1.准备工作

```
# 安装vim命令
yum -y install vim

# 安装wget命令
yum -y install wget

# 安装netstat命令
yum -y install net-tools

# 安装firewall命令
yum -y install firewalld
```

* 2.安装shadowsocks

```
wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh
chmod +x shadowsocks.sh
./shadowsocks.sh 2>&1 | tee shadowsocks.log
```

* 3.设置配置文件
  * 单端口  
  ```
  {
     "server":"0.0.0.0",
     "server_port":8080,
     "local_address":"127.0.0.1",
     "local_port":1080,
     "timeout":300,
     "method":"aes-256-cfb",
     "fast_open":false
  }
  ```
  * 多端口  
  ```
  {
    "server":"0.0.0.0",
    "local_address":"127.0.0.1",
    "local_port":1080,
    "port_password":{
        "8080":"a040225",
        "8081":"a040225",
        "8082":"a040225",
        "8083":"a040225"
    },
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open":false
  }
  ```

* 4.设置防火墙

防火墙操作
```
# 开启服务
systemctl start firewalld.service

# 关闭服务
systemctl stop firewalld.service

# 设置开机启动
systemctl enable firewalld.service

# 关闭开机启动
systemctl disable firewalld.service

# 查看状态
systemctl status firewalld
```

查看防火墙状态
```
firewall-cmd --state
```
查看已开启端口
```
firewall-cmd --list-ports
```
开启端口
```
firewall-cmd --zone=public --add-port=8080/tcp --permanent
```
重启防火墙
```
firewall-cmd --reload
```
**操作步骤**
  1. 查看已开放端口
  2.开启未开放端口
  3.重启防火墙
  
### 操作shadowsocks

```
# 开启服务
/etc/init.d/shadowsocks start

# 停止服务
/etc/init.d/shadowsocks stop

# 重启服务
/etc/init.d/shadowsocks restart

# 查看状态
/etc/init.d/shadowsocks status
```
  
## 客户端

### 下载shadowsocks  

**windows**: https://github.com/shadowsocks/shadowsocks-windows/releases  
**android**: https://github.com/shadowsocks/shadowsocks-android/releases  
**mac**: https://github.com/shadowsocks/ShadowsocksX-NG/releases  

### 配置shadowsocks

### 设置ipv4与ipv6

