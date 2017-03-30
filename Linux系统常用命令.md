记录一下吧,前前后后玩类Unix系统也有一年左右了,说不上有什么心得,常用的命令还是要知道含义的,cd ls pwd这些最常用的以及top ps -ef netstat这些次一级的都会记录的,实在是没用到的就不记了毕竟我又不是Linux运维.另外要记得Linux版本差异与命令差异,所记录的大多数都是通用的.
- 移动到指定的目录
```
$ cd ${dir}
```

- 查看当前所在目录

```
$ pwd
```

- 查看当前目录下的子文件

```
ls
```

- 查看当前目录下所有子文件以及详细信息

```
ls -al
```
这里说下详细信息的含义吧:

```
drwxr-xr-x   17 curuser  staff      578  3 30 10:21 .git
```
drwxr-xr-x: 
d:
这里的d代表文件类型dir目录类型,如果是l就是链接文件-是普通文件p是管道
rwx:
代表权限,r->read,w->write,x->execute,可以看到这里有三组rwx如果对应的顺位上有对应的字母则代表有相应的权限否则就是没有,第一组是该文件所有者的权限,第二组代表同组用户的权限,最后一组是其他用户权限,权限可以用sudo chmod 777 filename的更改对应的权限.

sudo chmod 777:
更改文件的权限 7最大代表有rwx所有的权限第一个7是文件所有者第二个代表同组,第三个是其他用户,1代表读的权限,2代表写的权限,4代表执行的权限,可以随意加减和用单个值来确定要赋予什么权限.

第二列17代表硬链接数,暂时没怎么接触过,不多说.
第三列curuser代表文件所属用户第四列代表所属用户组
第五列代表文件大小最后就是修改时间和文件名

- 永久保存环境变量
```
vim ~/.bash_profile
```
在这里写对应的关系

```
desk='/Users/bi/Desktop'
html='/Users/bli/Desktop/html'
download='/Users/bi/Downloads'
publish='/Users/bi/Desktop/html/player/js/'
player='/Users/bi/Desktop/html/bplayer'
```
这样保存之后就可以cd $desk这样一键cd到桌面了,也有其他的玩法.

- 移动文件/给文件改名

```
mv filename dirname / mv filename NewFilename
```
- 删除文件

```
rm filename
```
对于一些非空的目录文件这样做是没用的需要用到一些禁术:

```
sudo rm -rf dir
```

关于这个命令的传说就不多说了,用之前请知道你自己在做什么- -

- 新建文件夹
```
mkdir dirname
```

- 新建文件

```
touch filename
```

- 查看当前进程

```
top
```
这里可以加一些比如说-a的参数来对其进行排序.

- 查看网络情况

```
netstat
```

- 查看当前的内网IP地址

```
ifconfig |grep inet
```

- 强制杀死进程: 用top或者lsof等命令查询PID后
```
kill -9 PID
```

- 显示所有进程

```
ps -ef
```
一般这个命令通过|grep筛选出想找的进程或者服务
