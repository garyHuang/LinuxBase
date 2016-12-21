# usermod修改用户属性

## usermod修改用户
```
# 修改用户组
usermod -g comm gary 
# 修改用户 脚本
usermod -s /sbin/nologin gary
# 修改用户id
usermod -u 1001 gary
# 修改家目录
usermod -M /home/gary123 gary
```
