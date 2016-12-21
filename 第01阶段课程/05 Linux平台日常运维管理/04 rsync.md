# rsync

## 1、简介
rsync是类unix系统下的数据镜像备份工具——remote sync。一款快速增量备份工具 Remote Sync，远程同步 支持本地复制，或者与其他SSH、rsync主机同步。

## 2、安装
```
yum install -y rsync
```

## 3、同步目录
```
# 同步两个目录
rsync -avLuPz --exclude="*.xml" --delete tomcat8/ tomcat001/
#-a 拷贝
#v 显示拷贝的文件
#P 显示拷贝文件进度
#z 压缩拷贝
#L 拷贝 软件链接的目标文件
#u 如果目标文件比源文件还新，那么则忽略该文件
#--exclude 匹配这个规则的文件例外不拷贝
#--delete 让两个目录下的文件保持一直，tomcat8下删除的文件 在 tomcat001 下也删除
 
# 同步远程目录和本地目录
rsync -avLuPz /opt/tomcat8/ 192.168.31.213:/opt/tomcat
```

## 4、rsync 服务
新增配置文件 /etc/rsync.conf， rsync服务默认读取这个配置文件
```
port=8730
#日志文件
log file=/var/log/rsync.log
#进程pid存储文件
pid file=/var/run/rsync.pid
[hf]
path=/opt/
user chroot=true
max connection=4
read only=no
list=yes
uid=root
gid=root
auth users=root
secrets file=/etc/rs.pwd
hosts allow=192.168.1.30


# port 端口，默认端口是 8730
# log file 日志文件
# pid file pid保存的目录
# [hf] 模块名称,拉去文件的时候需要指明
# path rsync同步的路径
# user chroot 使用目录权限
# max connection 最大连接数
# read only 是否只读
# list 是否允许把模块的名字列出来
# uid 用哪个用户的身份推送用户
# gid 推送的组
# auth users 验证rsync的用户名
# secrets file 验证密码文件
# hosts allow 允许的hosts
# secrets file 密码文件格式：用户名是 auth users 指定的账户名，密码文件必须是600，或者是400
 root:123aaa

```
启动服务
```
rsync --dameon
```
客户端拉文件
```
rsync -avzPL --port 8730 root@192.168.1.25::hf/ /opt/

# --port 指定端口号
# root rsync配置的账号 auth users 的账户名
# hf 模块名称
# hf/ 从hf模块的根目录拷贝
# /opt/ 拷贝到 这个目录


rsync -avzPL --port 8730 --password-file=/etc/rs.pwd root@192.168.1.25::hf/ /opt/
# /etc/rs.pwd #该文件里面只写密码，并且权限要设置为400
```
