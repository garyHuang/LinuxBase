#  exec 和 xargs

## 1、简介
xargs是一条Unix和类Unix操作系统的常用命令。它的作用是将参数列表转换成小块分段传递给其他命令，以避免参数列表过长的问题

## 2、使用区别
```
find . -name 'core' -type f -exec rm {} \; 

find . -name 'core' -f type | xargs -i rm {} 

find . -name 'core' -f type | xargs rm
```