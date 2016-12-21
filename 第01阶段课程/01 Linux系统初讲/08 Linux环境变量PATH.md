# Linux环境变量PATH

在讲环境变量之前阿铭先介绍一个命令 which, 它用来查找某个命令的绝对路径。
```
[root@local01 ~]$ which rmdir
/usr/bin/rmdir
[root@local01 ~]$ which rm
alias rm='rm -i'
	/usr/bin/rm
[root@local01 ~]$ which ls
alias ls='ls --color=auto'
	/usr/bin/ls
```
‘rm’ 和 ‘ls’ 是两个特殊的命令，使用 alias 命令做了别名。我们用的 ‘rm’ 实际上是 ‘rm -i’ 加上 ‘-i’ 选项后，删除文件或者命令时都会问一下是否确定要删除，这样做比较安全。 ‘alias’ 可以设置命令的别名也可以设置文件的别名，‘which’ 这个命令平时只用来查询某个命令的绝对路径，不常使用。
上边提到了alias，也提到了绝对路径的/bin/rm ，然后你意识到没有，为什么我们输入很多命令时是直接打出了命令，而没有去使用这些命令的绝对路径？这是因为环境变量PATH在起作用了。请输入 echo $PATH，这里的echo其实就是打印的意思，而PATH前面的$表示后面接的是变量。
```
[root@localhost ~]# echo $PATH
/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin
```
因为/bin 在PATH的设定中，所以自然就可以找到ls了。如果你将 ls 移动到 /root 底下的话，然后你自己本身也在 /root 底下，但是当你执行 ls 的时候，他就是不理你？怎么办？这是因为 PATH 没有 /root 这个目录，而你又将 ls 移动到 /root 底下了，自然系统就找不到可执行文件了，因此就会告诉你 ‘command not found!’

```
[root@localhost ~]# mv /bin/ls /root/
[root@localhost ~]# ls
-bash: /bin/ls: 没有那个文件或目录 
```
那么该怎么克服这种问题呢？有两个方法，一种方法是直接将 /root 的路径加入 $PATH 当中！如何增加？可以使用命令 PATH=$PATH:/root:
```
[root@localhost ~]# PATH=$PATH:/root
[root@localhost ~]# echo $PATH
/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin:/root
[root@localhost ~]# ls
anaconda-ks.cfg  install.log  install.log.syslog  ls
```
另一种方法就是使用绝对路径：
```
[root@localhost ~]# /root/ls
anaconda-ks.cfg  install.log  install.log.syslog  ls
```

