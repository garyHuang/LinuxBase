# 学会查询帮助文档—man


这个man 通常是用来看一个命令的帮助文档的。格式为 ” man 命令 ” 例如输入命令：
```
man ls
```
则会显示如下结果：
```
LS(1)                            User Commands                           LS(1)

NAME
    ls - list directory contents

SYNOPSIS
    ls [OPTION]... [FILE]...

DESCRIPTION
    List  information  about  the FILEs (the current directory by default).
    Sort entries alphabetically if none of -cftuvSUX nor --sort.

    Mandatory arguments to long options are  mandatory  for  short  options
    too.

    -a, --all
           do not ignore entries starting with .

    -A, --almost-all
           do not list implied . and ..

    --author
           with -l, print the author of each file
```
这样可以查看 “ls” 这个命令的帮助文档，进入后按 ‘q’ 键退出。 