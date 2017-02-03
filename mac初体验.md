首先是外接win键盘之后需要改键,点击系统偏好设置之后点击键盘修饰键command <=> win,Option <=> alt,control <=> ctrl.
下面记录几个开发中常用的快捷键:
在谷歌浏览器中打开调试工具:command + alt + i;
qq截图:ctrl + command + a;
刷新:command + r;
------
1. mac下搭建nginx服务器：在终端输入：

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
下载homebrew包管理工具
2. 先clone nginx项目到本地：
```
brew tap homebrew/nginx
```
3. 执行安装：
```
brew install nginx-full --with-rtmp-module
```
4. 通过操作以上步骤nginx和rtmp模块就安装好了，下面开始来配置nginx的rtmp模块
首先来看看我们的nginx安装在哪里了:
执行：
```
brew info nginx-full
```

```
Docroot is: /usr/local/var/www

The default port has been set in /usr/local/etc/nginx/nginx.conf to 8080 so that
nginx can run without sudo.

nginx will load all files in /usr/local/etc/nginx/servers/.

- Tips -
Run port 80:
 $ sudo chown root:wheel /usr/local/Cellar/nginx-full/1.10.0/bin/nginx
 $ sudo chmod u+s /usr/local/Cellar/nginx-full/1.10.0/bin/nginx
Reload config:
 $ nginx -s reload     #重新加载配置文件
Reopen Logfile:
 $ nginx -s reopen   #再次打开日志文件
Stop process:
 $ nginx -s stop           #停止服务器
Waiting on exit process
 $ nginx -s quit           #退出服务器
```

从上面可以看出

nginx安装所在位置
```
/usr/local/Cellar/nginx-full/
```
nginx配置文件所在位置
```
/usr/local/etc/nginx/nginx.conf
```
nginx服务器根目录所在位置
```
/usr/local/var/www
```
执行命令 
```
nginx
```
，测试下是否能成功启动nginx服务
```
/usr/local/Cellar/nginx-full/1.10.0/bin/nginx
```
在浏览器地址栏输入：http://localhost:8080 如果出现
Welcome to nginx!
代表nginx安装成功了!

修改nginx.conf这个配置文件，配置rtmp
用Xcode打开nginx.conf, 找到

```
/usr/local/etc/nginx/nginx.conf
```

文件,拖入到Dock中的Xcode,就可以打开.

```
http {
    ……
}
#在http节点下面(也就是文件的尾部)加上rtmp配置：
rtmp {
    server {
        listen 1935;
        application gzhm {
            live on;
            record off;
        }
    }
}
```

说明:
rtmp是协议名称
server 说明内部中是服务器相关配置
listen 监听的端口号, rtmp协议的默认端口号是1935
application 访问的应用路径是 gzhm
live on; 开启实时
record off; 不记录数据

5. 保存文件后，重新加载nginx的配置文件:nginx -s reload

brew安装ffmpeg
```
brew install ffmpeg
```

brew安装ffmpeg（带X265）
```
brew reinstall ffmpeg --with-x265
```
