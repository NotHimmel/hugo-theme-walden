+++
title = "Linux Virtual Machine"
date = 2025-04-03T13:46:50+08:00
draft = false
categories = "linux"
tags = ["handbook"]
slug = "virtualmachine"
[params]
    author = "NotHimmel"
+++

<!--more-->
## 选择虚拟机镜像安装  
按部就班安装即可。  

## 网络配置  
1. 查看本机网络配置，后面要用  
进入cmd，输入ipconfig，记录一下：  
   IPv4 地址 . . . . . . . . . . . . : 192.168.31.120
   子网掩码  . . . . . . . . . . . . : 255.255.255.0
   默认网关. . . . . . . . . . . . . : 192.168.31.254
2. 配置虚拟机网络  
   打开虚拟机，选择虚拟机设置，选择网络适配器，选择NAT8模式，点击确定，保存设置。
   菜单栏-编辑-虚拟网络编辑器，vmnet8，关闭DHCP服务，更改设置，
   子网地址前三位同本机的子网地址，此处例为192.168.31.0，子网掩码255.255.255.0，  
   net8的NAT设置网关IP同本机默认网关：192.168.31.254。  
3. 开机，设置静态IP
```bash
# CentOS
sudo vim /etc/sysconfig/network-scripts/ifcfg-ens3*
IPADDR=192.168.219.130（最后一位看自己情况）
GATEWAY=192.168.31.254（同本机网关）
NETMASK=255.255.255.0
DNS1=114.114.114.114
DNS2=8.8.8.8
BOOTPROTO=static
ONBOOT=yes
## 保存后重启网络,DNS会自动更新到/etc/resolv.conf
service network restart
## 防火墙
firewall-cmd --state
systemctl stop firewalld.service
systemctl disable firewalld.service
```

```bash
# Ubuntu 我好像没改就直接好使了，下面的没试
sudo vim /etc/network/interfaces
ifcae eth0 inet static
address 192.168.31.110
netmask 255.255.255.0
gateway 192.168.31.254
# DNS
sudo vi /etc/resolv.conf  
nameserver 114.114.114.114
nameserver 8.8.8.8 

# 重启网络
sudo /etc/init.d/networking restart
```