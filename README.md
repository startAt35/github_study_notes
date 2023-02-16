# github_study_notes
github学习笔记

## 前期准备

### ssh登录

- 设置ssh key

```
ssh-key -t rsa -C "my_email@xxx.com"
```

将生成的id_rsa.pub文件内容添加到GitHub的ssh key中

- 验证ssh设置成功

```
ssh -T git@github.com

# 如下结果即为成功
Hi startAt35! You've successfully authenticated, but GitHub does not provide shell access.
```

### 创建仓库

在github页面中点击加号-new repository，创建新的仓库

### 中文乱码解决方法

```
git config --global core.quotepath false
```

## 查看配置文件

- 设置提交时显示的用户名

```
git config --global user.name "NAME"
```

- 设置提交时显示的email

```
git config --global user.email "EMAIL"
```

- git命令输出着色，便于阅读

```
git config --global color.ui auto
```

- 显示本地仓库的配置

```
git config --list
# 或者
git config -l
```

- 删除全局设置

```
git config --global --unset <entry-name>
```

## git基本操作

- clone已有仓库

```
git clone git@github.com:startAt35/github_study_notes.git
git clone GIT_URL 指定目录 # clone到指定目录
git clone GIT_URL -b <分支名称> 指定目录 # clone到指定目录，并指定分支
git clone --depth=1 URL # clone最新的一次提交
```

- 编写代码后查看状态

```
git status
```

- 将修改的文件添加到暂存(以readme.md为例)

```
git add README.md
git add . # 暂存所有更改
git add -A # 暂存所有更改
```

- 保存仓库的历史记录

```
git commit -m "some messages"
```

git commit命令将当前暂存区中的文件实际保存到仓库的历史记录中，通过这些记录，我们 就可以在工作树中恢复文件。

-m参数后的"some messages"是对本次提交内容的描述

- 本地文件推送到github

```
git push
```

> git add 和git commit 都是对本地文件进行操作，git push则是将本地文件推送到github上

- 查看提交日志

```
git log
git log dir_name # 只显示该目录下的日志
git log README.md # 只显示该文件相关的日志
git log -p # 显示文件的改动
git log -p README.md 
```

- 查看更改前后差别

```
git diff # 查看当前工作树与暂存区的差别
git diff HEAD # 查看工作树与最新提交的差别
git diff <commit-id> <commit-id> # 查看本地仓库中任意2个commit之间的文件变动
```

## 分支的操作

在进行多个并行作业时，会用到分支。在并行开发的过程中，往往同时存在多个最新代码状态。例如，从master分支创建feature-a分支和fix-b分支

- 列出本地分支

```
git branch # 带*表示当前所在的分支
git branch -av # 列出所有分支，包括本地和远程
```

- 创建一个新分支feature-a，并切换到该分支

```
git checkout -b feature-a
```

- 连续执行以下2条命令，也可以达到上一条命令的效果

```
git branch fix-b # 创建新分支，但是当前分支不变
git checkout fix-b # 切换到b分支
```

git add之前要查看当前分支，以防提交到错误的分支上

- 切换到main分支

```
git checkout main
```

- 删除分支

```
git branch -d fix-b
```

- 合并分支（分支a合并到b）

```
git checkout fix-b # 先切换到分支b
git merge feature-a # 再将分支a合并到分支b
```

- 重命名分支

```
git branch -m <new>
git branch -m <old> <new>
```

- 删除远程分支

```
git push origin --delete <old> # 方法1
git push origin :oldBranchName # 方法2
```



## 更改提交

- 将所有内容恢复到最后一次提交

```
git reset --hard
```

- 将所有内容恢复到某时间点状态，只需要提供时间点的哈希值（版本号）即可

```
git log # 查询commit的hash
git reset --hard 89be2471d44286ffd8b93f8ed1a57bcc89388434
```

- 取消暂存，保留文件更改

```
git reset [file]
```



## 推送至远程仓库

- 设置本地仓库的远程仓库

```
git remote add origin git@github.com:startAt35/xxxx.git # 将远程仓库xxxx标识为origin
```

- 推送至远程仓库

```
git push
# 使用-u参数可以在推送的同时，将origin仓库的master分支设置为本地仓库当前分支的上游
# 添加这个参数后，将来运行git pull命令从远程仓库获取内容时，本地仓库的这个分支可以直接从origin的master分支获取内容
git push -u origin master 
```

- 推送到master以外的分支

```
git checkout -b feature-d
giit push -u origin feature-d
```

- 获取远程仓库的名称

```
git remote
git remote -v # 除了名称，还会获取url
```

