# grep 命令

## 1、简介
grep （缩写来自Globally search a Regular Expression and Print）是一种强大的文本搜索工具，它能使用正则表达式搜索文本，并把匹配的行打印出来。Unix的grep家族包括grep、egrep和fgrep。

## 2、使用
```
grep -c root -A 2 -B 2 /etc/passw
 -c 统计出现了root字符串的行数
 -n 显示匹配的行索引
 -A 显示匹配数据的下面两行
 -B 显示匹配数据的上面两行
 -C 显示匹配数据的上下各两行
 -r 匹配文件内容，显示文件名
 grep -E 命令 和 egrep 命令使用方式一样
```