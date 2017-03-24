最近重装了系统，git的初始环境配置又得从网上找，挺麻烦的，干脆记一下以免以后再次遇到这种情况。
首先去git官网下载git后安装git bash，这一步没啥说的。
然后打开git bash 输入
```
    $ git config --global user.name "Sun Yuguang"
    $ git config --global user.email "sun87959012@hotmail.com"
```
这两步是设置用户名和邮箱，没啥用。
```
	$ ssh-keygen -t rsa -C "sun87959012@hotmail.com"
```
输入后连续回车
这一步是生成SSH密钥，有用。
```
	$ cd ~/.ssh
	$ ll
```
查看是否存在目录
最后得到了两个文件：id_rsa和id_rsa.pub
```
将id_rsa.pub文件里的内容拷贝出来
clip < ~/.ssh/id_rsa.pub
```
粘贴到github网站上就可以了

测试：
```
ssh git@github.com
```
--------------------------------
```
git config --global credential.helper store
```
git push免密码的命令

-----
git 查看所有远端分支：
```
git branch -a
```
git获取远端分支:
```
git fetch origin branchname / git checkout -b branchname origin/branchname
```

git 删除本地分支:
```
git branch -d/D(force)
```
git 查看版本信息
```
git log
```
git 比较差异
```
git diff masterA masterB
```
git 丢弃所有未提交
```
git stash
```
git 回退到上个版本
```
git reset --hard HEAD^ 
```
git 回退到某个特定版本
```
git reset --hard commitNum
```
git 更新分支信息
```
git fetch origin --prune / git fetch
```
git 查看所有分支信息
```
git branch -a
```
git 删除远程分支
```
git branch -r -d origin/branch-name  /  git push origin :branch-name
```
git reset
版本回退
```
git reset --hard 版本号
```
绿字变红字(撤销add)
```
git reset HEAD fileName
```
红字变无 (撤销没add修改)
```
git checkout -- fileName / stash
```
git 强制推送到远端分支
```
git push -f origin branchname
```
git 重命名本地分支
```
git branch -m oldbranchname newbranchname
```
git push设置默认分支为当前分支（不用每次都输分支名）
```
git config --global push.default "current"
```
git 修改提交的注释
```
git commit --amend
```

git 设置缓存大小
```
git config --global http.postBuffer 524288000
```

git 去除ADD提醒
```

git config core.autocrlf false

```
git 以提交新版本的方式回退到制定的版本
```
$ git revert HEAD/commit
```
