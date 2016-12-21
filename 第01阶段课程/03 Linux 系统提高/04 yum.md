# yum 

## 说明

Yum（全称为 Yellow dog Updater, Modified）是一个在Fedora和RedHat以及CentOS中的Shell前端软件包管理器。基于RPM包管理，能够从指定的服务器自动下载RPM包并且安装，可以自动处理依赖性关系，并且一次安装所有依赖的软件包，无须繁琐地一次次下载、安装。

## 1、配置国内yum源镜像
> 搜狐yum源 http://mirrors.sohu.com/
> 阿里云yum源 http://mirrors.aliyun.com/

下载适合自己系统的yum源文件,我测试的是Centos6，下载这个
```
http://mirrors.aliyun.com/repo/Centos-6.repo
```
下载阿里云扩展yum源
```
http://mirrors.aliyun.com/repo/epel-6.repo
```
删除本地 /etc/yum.repos.d 下所有文件，将上面两个文件，上传到该目录，然后执行命令，需要一定的时间执行创建缓存
```
yum clean all

yum makecache fast
```

## 2、yum安装软件
```
yum install -y vim-enhanced
```
## 2、yum 搜索需要安装的软件名
```
yum list | grep vim

yum search vim
```
## yum 卸载软件
```
yum remove -y vim-enhanced
```

## 3、yum下载rpm包
首先安装插件 yum-plugin-downloadonly
```
yum install -y yum-plugin-downloadonly
# 如果安装失败就安装下面工具
yum install -y yum-utils
```
下载的包，必需是未安装的包
```
yum install -y --downloadonly --downloaddir=./ vim-enhanced
```

