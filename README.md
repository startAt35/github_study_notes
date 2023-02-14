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

### git基本操作

- clone已有仓库

```
git clone git@github.com:startAt35/github_study_notes.git
```

- 编写代码后查看状态

```
git status
```

- 将修改的文件添加到暂存(以readme.md为例)

```
git add README.md
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

