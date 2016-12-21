# rpm 工具

## 说明
 是RPM Package Manager（RPM软件包管理器）的缩写，这一文件格式名称虽然打上了RedHat的标志，但是其原始设计理念是开放式的，现在包括OpenLinux、S.u.S.E.以及Turbo Linux等Linux的分发版本都有采用，可以算是公认的行业标准了。


## 1、安装rpm包
```
# vh 显示安装进度
rpm -ivh json-c-0.11-12.el6.x86_64.rpm
```

## 2、查找是否安装了某个软件
```
rpm -qa | grep json-c 
```

## 3、卸载软件
```
rpm -e json-c 

#加nodeps为强制删除
rpm -e --nodeps json-c
```