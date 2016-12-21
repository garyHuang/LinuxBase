# passwd 修改用户密码

## passwd 用户名 修改指定用户密码
```
passwd gary
```
## 安装生成随机密码的插件
```
yum install -y expect
```
## 生成一个12位的随机密码
```
mkpasswd -l 12 
```
## 密码不要有特殊字符
```
mkpasswd -l 12 -s 0
```
## 密码内要求有N个数字
```
mkpasswd -l 12 -s 0 -d 4 
```
## 指定大写字母个数
```
mkpasswd -C 3 -l 12
```
## 指定小写字母个数
```
mkpasswd -C 3 -l 12
```
## shell 一键设置密码
```
echo "密码" | passwd --stdin 用户名
```
