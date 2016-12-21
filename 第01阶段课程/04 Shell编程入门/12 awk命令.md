# awk 命令

## 1、简介
AWK是一个优良的文本处理工具，Linux及Unix环境中现有的功能最强大的数据处理引擎之一。这种编程及数据操作语言（其名称得自于它的创始人阿尔佛雷德·艾侯、彼得·温伯格和布莱恩·柯林汉姓氏的首个字母）的最大功能取决于一个人所拥有的知识。awk经过改进生成的新的版本nawk,gawk，现在默认linux系统下日常使用的是gawk，用命令可以查看正在应用的awk的来源（ls -l /bin/awk ）

## 2、使用
```
awk -F ':' 'OFS="#" {print $1 , $4}' 1.txt
   -F 指定分隔符
   OFS 指定输入的链接符号,默认是空格
   {print $1,$4} 指定打印第1段和第4段
 awk -F ':' ' $1~/r*o/ {print $1} ' 1.txt
     $1~/ro/ 表示第一段字符串中有ro的，支持正则表达式
 awk -F ':' ' $3>1000 {print $1} ' 1.txt
   表示第三段大于1000的过滤出来
 awk -F ':' '$3<$4 {print $1} ' 1.tx
  表示第三段小于第四段的过滤出来
 awk -F ':' '$1=="root"' 1.txt
  获取第一段登录root字符串的行 
 awk -F ':' '$7!~/nolog/' 1.txt
  第7段不包含nolog的行
 awk -F ':' 'OFS=":" { if (NR==10) print $1 , $7}' 1.txt
  打印第10行的第一段和第七段
 awk -F ':' 'OFS=":" {print NF}' 1.txt 
   打印行数组拆分的个数 
 awk -F ':' 'OFS=":" {print NR , $NF}' 1.txt 
   NR 表示行数,NF表示数组拆分个数，$NF标识打印最后一个段的值
 awk -F ':' 'OFS=":" {if ($3>$4) $7=$3+$4 ; print $0}' 1.txt  
  判断，当第三段大于第四段的时候，将第七段的值设置第三段加第四段
 awk -F ':' '{(sum=sum+$3)};END {print sum}' 1.txt 
     循环求和，END表示循环结束，打印结果sum
 awk 'ORS=" "{print}' 1.txt 
   其中ORS指定 打印结果的换行符
Shell数组
array=(`cat /etc/issue | awk '{if(NR==1){print $1 , $2}}'`)
echo "${array[0]}"  "${array[1]}"
# 统计Ip访问次数
awk '{a[$1]++}END{for (i in a)print a[i],i}' bak.log
```