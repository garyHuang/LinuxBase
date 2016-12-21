# crontab 定时任务

## 1、简介
crontab命令常见于Unix和类Unix的操作系统之中，用于设置周期性被执行的指令。该命令从标准输入设备读取指令，并将其存放于“crontab”文件中，以供之后读取和执行。该词来源于希腊语 chronos(χρνο)，原意是时间。常，crontab储存的指令被守护进程激活， crond常常在后台运行，每一分钟检查是否有预定的作业需要执行。这类作业一般称为cron jobs。



## 2、安装
```
yum install -y crontabs
```
## 3、使用
必需保证crond服务器是启动状态,用ps检查crond是否启动
```
ps aux | grep crond
```

## 3、新增一个任务
```
# 打开定时任务编辑文件
crontab -e 
#新增下列内ring，标识每3分钟同步一次日期
*/3 * * * * /usr/sbin/ntpdate time.pool.aliyun.com 1> /dev/null 2>&1
# 如果不能用vim编辑，导入变量
export EDITOR=vim
```
## 4、查看当用用户的定时任务
```
crontab -l
```