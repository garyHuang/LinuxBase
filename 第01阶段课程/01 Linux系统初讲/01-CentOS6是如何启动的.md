# CentOS6是如何启动的
 Linux的启动其实和windows的启动过程很类似，不过windows我们是无法看到启动信息的，而Linux启动时我们会看到许多启动信息，例如某个服务是否启动。Linux系统的启动过程大体上可分为五部分：内核的引导、运行init、系统初始化、建立终端、用户登录系统。
 
## 1、内核引导
当计算机打开电源后，检查BIOS，按照BIOS中设置的启动设备（通常是硬盘）来启动。紧接着由启动设备上的grub程序开始引导Linux，当引导程序成功完成引导任务后，Linux从它们手中接管了CPU的控制权，然后CPU就开始执行Linux的核心映象代码，开始了Linux启动过程。也就是所谓的内核引导开始了，在内核引导过程中其实是很复杂的，我们就当它是一个黑匣子，反正是Linux内核做了一系列工作，最后内核调用加载了init程序，至此内核引导的工作就完成了。交给了下一个主角init.

## 2.运行init
init进程是操作系统全部进程的起点，可以把他比作是所有进程的启动源头，没有这个进程，系统中的进程无法启动.init 最主要的功能就是准备软件执行的环境，包括系统的主机名，网络设置，编码，文件系统格式等其他服务器的启动等。而所有的通知都会通过init的配置文件/etc/inittab来规划,而inittab内还有一个重要的启动级别，启动级别不同Linux的使用环境就不同,我们来看看这个文件可以支持的级别
```
# 0 - halt 关机
# 1 - 单用户模式
# 2 - 多用户模式，和3启动级别不同是没有有NFS
# 3 - 多用户模式
# 4 - 系统未使用，保留
# 5 - X11控制台，登陆后进入图形GUI模式
# 6 - 系统正常重启
id:3:initdefault:
```
## 3、系统初始化
系统初始化，就是去执行/etc/init/下的各个配置文件。inittab配置文件中有这么一行 “System initialization is started by /etc/init/rcS.conf” 也就是说系统初始化会先执行/etc/init/rcS.conf 而该配置文件中又有一行 “exec /etc/rc.d/rc.sysinit” 所以，重心又转移到了这个rc.sysinit文件上，它会做如下工作：激活交换分区，检查磁盘，加载硬件模块以及其它一些需要优先执行任务。当rc.sysinit程序执行完毕后，将返回init继续下一步，又到了/etc/init/rc.conf, 在这个配置文件里，最关键的一行为 “exec /etc/rc.d/rc $RUNLEVEL” 而$RUNLEVEL是在/etc/inittab中定义的(最下面的那一行)，以阿铭的/etc/inittab为例，表示$RUNLEVE=3, 所以此时会执行 “/etc/rc.d/rc 3” 此时实际上是把/etc/rc.d/rc3.d/ 下的脚本都给执行了，随后/etc/rc.d/rc.local也会被执行，通常我们会把开机启动执行的命令放到这个脚本下。服务执行完，系统初始化也就完成了。接下来该建立终端了。

## 4、建立终端
建立终端是由配置文件/etc/init/tty.conf, /etc/init/serial.conf和/etc/sysconfig/init等配置文件来完成的。在2、3、4、5的运行级别中都将以respawn方式运行mingetty程序，mingetty程序能打开终端、设置模式。同时它会显示一个文本登录界面，这个界面就是我们经常看到的登录界面，在这个登录界面中会提示用户输入用户名，而用户输入的用户将作为参数传给login程序来验证用户身份

## 5、用户登陆系统
对于运行级别为5的图形方式用户来说，他们的登录是通过一个图形化的登录界面。登录成功后可以直接进入KDE、Gnome等窗口管理器。而本文主要讲的还是文本方式登录的情况：当我们看到mingetty的登录界面时，我们就可以输入用户名和密码来登录系统了。
Linux的账号验证程序是login，login会接收mingetty传来的用户名作为用户名参数。然后login会对用户名进行分析：如果用户名不是root，且存在 “/etc/nologin” 文件，login将输出nologin文件的内容，然后退出。这通常用来系统维护时防止非root用户登录。只有 “/etc/securetty” 中登记了的终端才允许root用户登录，如果不存在这个文件，则root可以在任何终端上登录。”/etc/usertty” 文件用于对用户作出附加访问限制，如果不存在这个文件，则没有其他限制。
在分析完用户名后，login将搜索 “/etc/passwd” 以及 “/etc/shadow” 来验证密码以及设置账户的其它信息，比如：主目录是什么、使用何种shell。如果没有指定主目录，将默认为根目录；如果没有指定shell，将默认为 “/bin/bash”。
login程序成功后，会向对应的终端在输出最近一次登录的信息(在 “/var/log/lastlog” 中有记录)，并检查用户是否有新邮件(在 “/usr/spool/mail/” 的对应用户名目录下)。然后开始设置各种环境变量：对于bash来说，系统首先寻找 “/etc/profile” 脚本文件，并执行它；然后如果用户的主目录中存在 .bash_profile 文件，就执行它，在这些文件中又可能调用了其它配置文件，所有的配置文件执行后后，各种环境变量也设好了，这时会出现大家熟悉的命令行提示符，到此整个启动过程就结束了。


