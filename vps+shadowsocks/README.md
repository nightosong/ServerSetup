[TOC]
# Vultr + VPS + Shadowsocks

## 购买

网址：https://www.vultr.com

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

