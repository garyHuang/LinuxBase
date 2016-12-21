# tr 和 split

## 1、简介
tr 替换字符串命令
split 拆分文件命令

## 2、tr 使用
```
 ls *.txt | tr 'a-z' 'A-Z'
 #将当前目录所有txt文件名的小写字母转换成为大写字母
 echo 'abcdefghijkmnlopqrstuvwxyz' | tr 'abcd' 'ABCD'
 #将字符串abcd替换成为ABCD，tr后面的字符串是一一对应的数
```
## 3、split使用
```
split -b 100 1.txt new_
# 将文件以100b的大小进行拆分，拆分的文件以new_开头，默认以x开头
# -l 制定文件按照行数进行拆分
```

## 3、perl 替换文件内容
```
perl -p -i -e "s/aming/AMING/g" *.txt
```