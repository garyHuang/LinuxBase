# iptables

## 1、简介
iptables 是与最新的 3.5 版本 Linux 内核集成的 IP 信息包过滤系统。如果 Linux 系统连接到因特网或 LAN、服务器或连接 LAN 和因特网的代理服务器， 则该系统有利于在 Linux 系统上更好地控制 IP 信息包过滤和防火墙配置。
防火墙在做信息包过滤决定时，有一套遵循和组成的规则，这些规则存储在专用的信 息包过滤表中，而这些表集成在 Linux 内核中。在信息包过滤表中，规则被分组放在我们所谓的链（chain）中。而netfilter/iptables IP 信息包过滤系统是一款功能强大的工具，可用于添加、编辑和移除规则。
虽然 netfilter/iptables IP 信息包过滤系统被称为单个实体，但它实际上由两个组件netfilter 和 iptables 组成。
netfilter 组件也称为内核空间（kernelspace），是内核的一部分，由一些信息包过滤表组成，这些表包含内核用来控制信息包过滤处理的规则集。
iptables 组件是一种工具，也称为用户空间（userspace），它使插入、修改和除去信息包过滤表中的规则变得容易。除非您正在使用 Red Hat Linux 7.1 或更高版本，否则需要下载该工具并安装使用它。[1] 

## 2、使用
Centos 7 安装 iptables
```
yum install iptables-services
```
使用命令
```
iptables -t filter -I INPUT -p tcp --dport 80 -s 192.168.31.138 -j REJECT
#-t 指定表，有三张表 filter,nat,mangle 默认是 filter表
#-I 为插入，新增加的规则会在规则列表的最上面出现
#-A 为增加，新增加规则会在规则列表的最下面出现
#-p 指定协议
#--dport 80 指定端口,没有必需有-p 指定协议
#-s 指定来源ip地址
#-j 指定规则，ACCEPT 允许，REJECT 拒绝 , DROP 允许，不记录任何操作
#iptable -F 清空防火墙规则
#iptables-restore < 1.ipt #恢复防火墙规则
#iptable-save > 1.ipt #保存防火墙规则到1.ipt文件中
#filter表 主要用来限制进入本机的包和出去的包
#nat表 主要用于网络地址转换，比如家用的小路由器就是用nat表实现的
#mangle表 主要用来给包打标记

iptables -L
# 查看当前防火墙的规则
```