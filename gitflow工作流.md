# 首先从远端仓库拉下git仓库：
```
git clone url
```
# 然后查看远端所有分支：
```
git branch -a
```
# 找到需要开发的版本分支之后将其拉取到本地：
```
git checkout -b branchName origin/branchname
```
# 在版本分支上开新的功能分支：
```
git checkout -b branchName //0.9.6(版本分支名可有可无，只要当前HEAD分支是版本分支即可)
```
# 新的功能分支上完成对应功能的开发后提交
```
git add -a
git commit -m 'add some feature'
git push
```
# 等待大佬合并功能后删除该分支并进行下次功能的开发
```
git branch -d
```
