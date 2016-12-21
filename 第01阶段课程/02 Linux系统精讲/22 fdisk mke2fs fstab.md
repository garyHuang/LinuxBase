#  fdisk mke2fs fstab

## 

## 1、查看磁盘列表
```
fdisk -l
```
## 2、格式化分区
```
fdisk /dev/sdb
```
提示输入m查看帮助,输入m
```
Command action
   a   toggle a bootable flag
   b   edit bsd disklabel
   c   toggle the dos compatibility flag
   d   delete a partition(删除分区)
   l   list known partition types(列出知道类型的分区)
   m   print this menu(打印菜单)
   n   add a new partition(新增一个分区)
   o   create a new empty DOS partition table
   p   print the partition table(打印分区表)
   q   quit without saving changes(退出不保存)
   s   create a new empty Sun disklabel(创建一个新的Sun标识)
   t   change a partition's system id(改变磁盘分区id)
   u   change display/entry units
   v   verify the partition table
   w   write table to disk and exit (保存并且退出)
   x   extra functionality (experts only)
```
这时可以输入n创建一个新的分区，然后，输入p创建主分区,然后选择磁盘大小的区间。如果需要多个分区，可重复此操作。
退出的时候输入w，不要输入q，否则分区将不能保存
## 3、磁盘格式化
```
mke2fs -t ext4 /dev/sdb1
```
### 磁盘附加
```
mount /dev/sdb1 /export/
```
### 磁盘开机启动挂载
```
# 首先查看磁盘 uuid，
blkid
# 修改文件 /etc/fstab
UUID="c5aa6f5c-2081-49b0-ae76-2934df224f88" /export ext4   defaults   0 0
# 第一段 磁盘uuid
# 第二段 磁盘挂载的目录
# 第三段 磁盘格式类型
# 第四段 磁盘挂载格式，默认就好
# 第五段 磁盘释放备份，1为备份，0为不备份
# 第六段 磁盘开机是否需要检查
```