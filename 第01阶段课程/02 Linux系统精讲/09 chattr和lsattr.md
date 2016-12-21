# chattr 和 lsattr

## chattr
只有超级权限的用户才具有使用该命令的权限，这项指令可改变存放在ext2、ext3、ext4、xfs、ubifs、reiserfs、jfs等文件系统上的文件或目录属性。
######　语法
```
chattr [ -RV ] [ -v version ] [ mode ] files...
```
###### mode说明
最关键的是mode部分，mode 是又+-=组成 ASacDdIijsTtu 这些字符的，这部分是用来控制文件属性的。
> a：即append，设定该参数后，只能向文件中添加数据，而不能删除，多用于服务器日志文 件安全，只有root才能设定这个属性。
> i：设定文件不能被删除、改名、设定链接关系，同时不能写入或新增内容。i参数对于文件 系统的安全设置有很大帮助。

```
# 文件不能删除，修改名称，移动
chattr +i 1.txt
# 文件只能使用append方式进行追加
chattr +a 1.txt 
```


## lsattr 
改命令 为查看文件隐藏属性的权限命令. 
```
# 查看当前文件夹的文件属性
lsattr
# 查看某个文件属性
lsattr 1.txt 
# 查看文件夹本身的属性
lsattr -d /root
```