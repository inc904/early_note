git remote -v 查看所有远程仓库

git status 查看当前库的状态,查看修改了什么内容

git branch 查看当前分支情况

git checkout ss 切换到 ss 分支

git checkout -b xx 创建并切换到 xx 分支

git merge ss 切换到 master 分支后，执行该命令，意为，将 ss 分支上的暂存的内容合并到 master 分支

git push 推送到云端库

git push -u origin ss // ss 分支首次推送内容到云端 origin

## git 基本配置

```shell
git config --list ## 查看已经配置的参数

## 配置 提交代码时候的用户名和邮箱
git config --global user.name 'ytf'
git config --global user.email 'ytf@aliyun.com'
```

## 创建 git 仓库

```shell
## 初始化当前目录
git init
## 连接远程库
git remote add 'origin' http://something.git
## 查看文件夹关联库的信息
git remove -v
## 删除库
git remote rm '库名'
```

## 获取 git 仓库

`git clone https://something.git`

## 提交更新

1. 先执行更新文件
   `git pull origin master`
2. 添加要上传的文件到暂存区
   `git add [willUpdatedFileName]`
3. 添加提交信息
   `git commit -m 'some description'`
4. 最后执行推送更新到远程库
   `git push origin master`
