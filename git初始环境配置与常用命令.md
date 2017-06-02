# 最近重装了系统，git的初始环境配置又得从网上找，挺麻烦的，干脆记一下以免以后再次遇到这种情况。

- 首先去git官网下载git后安装git bash，这一步没啥说的。

然后打开git bash 输入

```
$ git config --global user.name "Sun Yuguang"
$ git config --global user.email "sun87959012@hotmail.com"
```

- 这两步是设置用户名和邮箱，没啥用。

```
$ ssh-keygen -t rsa -C "sun87959012@hotmail.com"
```

- 输入后连续回车,这一步是生成SSH密钥，有用。

```
$ cd ~/.ssh
$ ll
```

- 查看是否存在目录,最后得到了两个文件：`id_rsa`和`id_rsa.pub`

- 将id_rsa.pub文件里的内容拷贝出来

```
$ clip < ~/.ssh/id_rsa.pub
```

- 粘贴到github网站上就可以了

- 测试：

```
$ ssh git@github.com
```
--------------------------------
```
$ git config --global credential.helper store
```

- git push免密码的命令

-----

- git 查看所有远端分支：
```
$ git branch -a
```
- git获取远端分支:

```
$ git fetch origin branchname / git checkout -b branchname origin/branchname
```

- git 删除本地分支:
```
$ git branch -d/D(force)
```
- git 查看版本信息
```
$ git log
```
- git 比较差异
```
$ git diff masterA masterB
```
- git 丢弃所有未提交
```
$ git stash
```
- git 恢复最近一次的stash

```
$ git stash pop
```

- git 回退到上个版本
```
$ git reset --hard HEAD^ 
```
- git 回退到某个特定版本
```
$ git reset --hard commitNum
```
- git 更新分支信息
```
$ git fetch origin --prune / git fetch
```
- git 查看所有分支信息
```
$ git branch -a
```
- git 删除远程分支
```
$ git branch -r -d origin/branch-name  /  git push origin :branch-name
```
- git 回退到具体的版本
```
$ git reset --hard 版本号
```
- 绿字变红字(撤销add)
```
$ git reset HEAD fileName
```
- 红字变无 (撤销没add修改)
```
$ git checkout -- fileName / stash
```
- git 强制推送到远端分支
```
$ git push -f origin branchname
```
- git 重命名本地分支
```
$ git branch -m oldbranchname newbranchname
```
- git push设置默认分支为当前分支（不用每次都输分支名）
```
$ git config --global push.default "current"
```
- git 修改提交的注释
```
$ git commit --amend
```

- git 设置缓存大小
```
$ git config --global http.postBuffer 524288000
```

-  git 去除ADD提醒
```
$ git config core.autocrlf false
```
- git 以提交新版本的方式回退到制定的版本
```
$ git revert HEAD/commit
```

- git 查看每一行代码最后一次提交的信息

```
$ git blame filename
```
- git查看某个文件的详细提交记录 
```
$ git log -p filename
```
- git撤销回滚
- 方法有多种,这里提一种
1. 查看log:

```
git log/git log -g
```

2. 找到对应的版本的log,复制版本号后检出新分支:

```
git branch recover-branch def9ca / git checkout -b recover-branch dfeas12
```

- git将已存在的本地分支推送到远端仓库

```
$ git init
$ git add README.md
$ git commit -m "first commit"
$ git remote add origin https://github.com/love999262/moe.git
$ git push -u origin master
```

- gitflow工作流

- 首先从远端仓库拉下git仓库：

```
$ git clone url
```

- 然后查看远端所有分支：

```
$ git branch -a
```

- 找到需要开发的版本分支之后将其拉取到本地：

```
$ git checkout -b branchName origin/branchname
```

- 在版本分支上开新的功能分支：

```
$ git checkout -b branchName //0.9.6(版本分支名可有可无，只要当前HEAD分支是版本分支即可)
```

- 新的功能分支上完成对应功能的开发后提交

```
$ git add -a
$ git commit -m 'add some feature'
$ git push
```

- 等待大佬合并功能后删除该分支并进行下次功能的开发

```
$ git branch -d
```

- git submodule拉取远端分支:进入对应的目录下

```
$ git submodule update --init
```
