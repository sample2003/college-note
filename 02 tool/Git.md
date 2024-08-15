
# 一、安装与配置

## 1. 下载安装

[git官网下载地址](https://git-scm.com/)

## 2. 配置

![[屏幕截图 2023-09-11 102607.png]]


## 3. 配置用户名

git config --global user.name "qitong chen"

## 4. 配置邮箱

git config --global user.email 3072641494@qq.com

## 5. 保存用户信息

git config --global credential.helper store

## 6. 查看用户信息

git config --global --list

--------------用户信息--------------

filter.lfs.clean=git-lfs clean -- %f
filter.lfs.smudge=git-lfs smudge -- %f
filter.lfs.process=git-lfs filter-process
filter.lfs.required=true
user.name=qitong chen
user.email=3072641494@qq.com
credential.helper=store

# 二、创建仓库

## 1. 本地创建

```powershell
git init repo
```

## 2. 远程克隆创建

```powershell
git clone "https://github.com"
```

# 三、工作方式

![[屏幕截图 2023-09-11 104227.png]]

![[屏幕截图 2023-09-11 100325.png]]

# 四、添加和提交文件

## 1. 添加文件

```powershell
echo "first note" > file1.txt

cat file1.txt
```

## 2. 将文件提交到暂存区

```powershell
# 添加一个文件
git add file1.txt

# 添加一类文件
git add *.txt

# 添加当前目录所有文件
git add .
```

## 3. 将文件从暂存区取回工作区

```powershell
git rm --cache file
```

## 4. 查看文件状态

```powershell
git status
```


## 5. 将文件提交到仓库

```powershell
git commit -m "第一次提交"
```

若缺少-m参数，则进入vim编辑器填写提交

![[Pasted image 20230911105108.png]]

## 6. 查看提交记录

```powershell
# 查看详细提交记录
git log

# 查看简单的提交记录
git log --oneline
```

# 五、版本回退

![[屏幕截图 2023-09-11 105827.png]]

## 1. 将提交内容回退到工作区和暂存区

```powershell
git reset --soft 版本号
```

## 2. 将提交内容回退

```powershell
git reset --hard 版本号
```

## 3. 将提交内容回退到工作区（默认）

```powershell
git reset --mixed 版本号
```

## 4. 回退到上一个版本

```powershell
git reset --soft ^HEAD
```

# 六、版本比较

## 1. 比较工作区和暂存区内容（默认）

```powershell
# 默认比较的是工作区和暂存区的内容
git diff
```

## 2. 比较工作区和本地仓库内容

```powershell
# 比较的是工作区和本地仓库的内容
git diff HEAD
```

## 3. 比较暂存区和本地仓库内容

```powershell
# 比较的是暂存区和本地仓库的内容
git diff --cached
```

## 4. 比较两个版本间内容

```powershell
# 比较两个版本间内容
git diff 提交id1 提交id2
```

## 5. 比较当前版本与版本间内容

HEAD表示当前分支的最新提交

### 01 比较当前版本与上一版本间内容

git diff HEAD~ HEAD
git diff HEAD^ HEAD

### 02 比较当前版本与上上一个版本间内容

git diff HEAD~2 HEAD

### 03 只比较当前版本与上上一个版本的file.txt内容

git diff HEAD~2 HEAD file.txt


## 6. 比较两个分支间内容

```powershell
# 比较两个分支间内容
git diff 分支名1 分支名2
```

## 7. 

![[屏幕截图 2023-09-14 085613.png]]

# 七、文件删除

## 1. （先）删除工作区文件

```powershell
rm file.txt
```

## 2. （再）删除暂存区文件

```powershell
git add file.txt
```

## 3. （先）删除工作区和暂存区文件

```powershell
git rm file.txt
```

## 4. （再）删除版本库文件

```powershell
git commit -m "delete file.txt"
```

# 八、.gitignore

![[屏幕截图 2023-09-14 151950.png]]

## 1. 前提 

添加到.gitignore的文件不能是已经被添加到版本库中的文件

## 2. 将文件添加到忽视文件中

```powershell
echo song.log > .gitignore
```

## 3. 将某一类文件添加到忽视文件中

```powershell
vi .gitignore

*.log
```

## 4. 将文件夹添加到忽视文件中

空文件夹也不会被添加到版本控制中

```powershell
vi .gitignore

*.log

file/
```

## 5. 匹配规则

![[屏幕截图 2023-09-14 155842.png]]

![[屏幕截图 2023-09-14 160025.png]]

![[屏幕截图 2023-09-14 160009.png]]

# 九、SSH

[11.SSH配置和克隆仓库_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1HM411377j/?p=11&spm_id_from=pageDriver&vd_source=e6e89b6acd5f6d51170394e516005d2a)

# 十、关联仓库

git pull 远程仓库名 main分支