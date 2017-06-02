# 如何配置nginx location?

默认的根目录为：
```
/usr/local/nginx/html
```
原始状态为：
```
location / {
    root   html;
    index  index.php index.html index.htm;
}
```
要改成某个指定路径比如说：/home/www：
```
location / {
    root   /home/www;
    index  index.php index.html index.htm;
}
```
有可能会遇到403的错误，应该是权限不够造成的。不过很大可能是对应的目录中没有index.html文件。
