# git 使用

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->
<!-- code_chunk_output -->

* [git 使用](#git-使用)
	* [账户与登录配置](#账户与登录配置)
		* [配置用户名](#配置用户名)
		* [创建SSH Key](#创建ssh-key)
	* [版本库操作](#版本库操作)
		* [创建版本库](#创建版本库)
		* [添加文件到Git仓库](#添加文件到git仓库)
		* [查看仓库当前状态与文件差异](#查看仓库当前状态与文件差异)
		* [版本回退](#版本回退)
		* [撤销修改](#撤销修改)
		* [添加远程仓库](#添加远程仓库)
		* [推送数据到远程仓库](#推送数据到远程仓库)
		* [从远程仓库克隆](#从远程仓库克隆)
		* [查看远程库信息](#查看远程库信息)
	* [分支管理](#分支管理)
		* [创建分支](#创建分支)
		* [查看分支](#查看分支)
		* [合并分支](#合并分支)
		* [查看分支合并视图](#查看分支合并视图)
		* [删除分支](#删除分支)
		* [变基](#变基)
	* [标签](#标签)
		* [打标签](#打标签)
		* [查看标签](#查看标签)
		* [推送标签](#推送标签)
		* [删除标签](#删除标签)

<!-- /code_chunk_output -->

## 账户与登录配置
### 配置用户名
```bash
git config --global user.name "Your name"
git config --global user.email "email@example.com"
```
### 创建SSH Key
``` bash
ssh-keygen -t rsa -C "youremail@example.com"
```

## 版本库操作
### 创建版本库
- `git init`
```bash
mkdir learngit
cd learngit
## 当前目录下会多一个.git的目录
git init
```
### 添加文件到Git仓库

- `git add <file>`
- `git commit -m <message>`

新建一个readme.md,file.txt

```bash
## add 可以添加多个文件
## . 表示添加所有
git add readme.txt  file.txt
git commit -m "wrote a readme file"
```
### 查看仓库当前状态与文件差异
- `git status`
- `git diff <file>`
- `git diff HEAD -- readme.txt` 工作区和版本库文件的区别

```bash
git status
git diff file.txt
```

### 版本回退
- `git log` 查看提交历史
  - `git log --pretty=oneline`
- `git relog` 查看命令历史
- `git reset --hard HEAD^` 指针回退
- `git reset --hard 1094a` id回退


> 在Git中，用`HEAD`表示当前版本，也就是最新的提交1094adb...（注意我的提交ID和你的肯定不一样），上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个^比较容易数不过来，所以写成`HEAD~100`。


```bash
git log
```
### 撤销修改
- 当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令 `git checkout -- file`
- 当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD <file>`，就回到了场景1，第二步按场景1操作。
- 已经提交了不合适的修改到版本库时，想要撤销本次提交，参考`版本回退`一节，不过前提是没有推送到远程库。

> git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

### 添加远程仓库
```bash
git remote add origin git@github.com:xxx/xxx.git
```

### 推送数据到远程仓库
```bash
git push -u origin master
```
> 我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来

### 从远程仓库克隆
```bash
git clone git@github.com:xxx/xxx.git
```
### 查看远程库信息
```
git remote -v
```
## 分支管理
### 创建分支
```bash
git checkout -b dev
## 与远程关联
git checkout -b dev origin/dev
```
等价于
```bash
git branch dev
git checkout dev
## 与远程关联
git branch --set-upstream-to=origin/dev dev
git branch --set-upstream branch-name origin/branch-name
```
### 查看分支
```bash
git branch
```
### 合并分支
```bash
git merge dev
## 不启用fast forward
git merge --no-ff -m "merge with no-ff" dev
```

### 查看分支合并视图
```bash
git log --graph
git log --graph --pretty=oneline --abbrev-commit
```
### 删除分支
```bash
git branch -d dev
```
> 如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除

### 变基
```bash
git rebase
```
- rebase操作可以把本地未push的分叉提交历史整理成直线；
- rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

## 标签
### 打标签
```bash
git tag v1.0
it tag v0.9 f52c633
## 创建带有说明的标签，用-a指定标签名，-m指定说明文字：
git tag -a v0.1 -m "version 0.1 released" 1094adb
```


### 查看标签
> 标签不是按时间顺序列出，而是按字母排序的。可以用`git show <tagname>`查看标签信息
```bash
git tag
git show v0.9
```
### 推送标签
```bash
git push origin v1.0
## 全推
git push origin --tags
```
### 删除标签
```bash
git tag -d v0.1
## 远程删除标签
git push origin :refs/tags/v0.9
```
