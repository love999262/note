最近打算把记录搬到HEXO上,不过工作比较繁忙,等稳定下来之后就开始动手折腾,顺便在这里记录从零开始折腾HEXO.

### 起步
[hexo](https://github.com/hexojs/hexo)
其实上面已经说的很清楚了:
```
$ npm install hexo-cli -g
```

用上面的命令安装HEXO到全局,然后在CLI里就有了hexo命令:

新建一个文件夹进入根目录
```
$ hexo init
```
这里就初始化好了一个hexo 仓库

用hexo s命令启动本地服务器,一般在4000端口可以看到
```
$ hexo server
//localhost://4000
```


用new命令可以新建一个文件
```
$ hexo new "Hello Hexo"
```
不过一般不用这样我可以直接将写好的markdown文件复制到source/_posts目录下

下面说说怎么更换主题:

首先去github上找到想要的主题,直接下载解压到一个文件夹里,然后改名,放到themes目录中,然后进人_config.yml文件更改对应的字段:
```
theme: theme_name
```
重启服务器就可以了

下面说说怎么生成静态文件:
这个命令可以生成静态文件
```
$ hexo generate
```
如何部署?
在github上建立以用户名+.github.io格式的仓库
然后我们复制git链接进入_config.yml文件
```
deploy:
    type: git
    repository: https://github.com/love999262/love999262.github.io.git
    branch: master

```
键入:
```
hexo deploy
```
注意上面的命令在高版本的hexo中可能会报错
```

$ npm install hexo-deployer-git --save
```
可以输入上面的命令再键入一次
个人小结:
hexo对于有NODE和GIT基础的人来说部署起来其实是很容易的,对与对编程整个都很陌生的人来说就比较麻烦,主要是很多概念不懂,个人觉得其实这东西看起来好看,可能有的主题并不是那么的实用,因为并没有一个简约的目录,所以写技术博客还是要找个带目录的主题
- [blog](https://love999262.github.io/) 
