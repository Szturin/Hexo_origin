---
title: '【Git学习】[1]入门命令'
top: false
cover: 
toc: true
mathjax: false
password:
  - 编程
  - Git
  - github
tags: Git
categories:
  - - 学习笔记
    - Git
  - - C/C++
abbrlink: 8948
date: 2024-02-23 23:42:30
author:
img:
coverImg:
summary:
---

# 一、本地项目托管到github仓库的快捷命令

## 1. Git仓库的创建和文件提交：

```bash
git clone <url> [directory] //克隆仓库
git init//创建初始化仓库
```

## 2. 将文件添加到缓存 :

```bash
git add . //将当前文件目录下所有文件移入暂存区`` 
```
## 3. 将缓存区内容添加到仓库中：

```bash
git commit -m "第一次版本提交" //在后面加-m选项，以在命令行中提供提交注释
git commit -am "第一次版本提交"//跳过add这一步，可以直接使用 -a选项
```

## 4. Git连接到远程仓库（github）

```bash
git remote add [alias] [url]//参数[alias]为别名， [url]为远程仓库的地址
```

## 5. 本地内容推送到远程仓库

```python
git push -u origin main
```

# # 常见问题

## 1. ``git push -u origin main`` 报错：

![image-20240830004335755](【Git学习】-1-入门命令/image-20240830004335755.png)

>**解决方案：**
>
>要解决这个问题，你需要先将远程仓库的更改合并到你的本地分支中，然后再进行推送。你可以按照以下步骤操作：
>
>1. **执行 `git pull`**
>     在你的本地仓库中执行以下命令来获取并合并远程仓库的更改：
>
>   ```
>   git pull origin main
>   ```
>
>   这将从远程的 `main` 分支拉取最新的提交，并尝试将这些更改合并到你本地的 `main` 分支中。
>
>2. **解决冲突（如果有的话）**
>     如果 Git 在合并过程中遇到冲突，它会提示你有冲突需要手动解决。你需要打开冲突的文件，手动编辑解决冲突，然后使用 `git add` 命令将解决冲突后的文件标记为已解决。
>
>3. **提交合并（如果有冲突）**
>     解决冲突后，你需要提交这些更改：
>
>   ```
>   git commit
>   ```
>
>   如果没有冲突，Git 会自动完成合并。
>
>4. **重新推送到远程仓库**
>     一旦你已经合并了远程的更改，你可以再次尝试推送到远程仓库：
>
>   ```
>   git push origin main
>   ```
>
>按照上述步骤操作，你应该能够成功地将本地更改推送到远程仓库。如果你对合并操作不太熟悉，可以提前备份你的代码库以防万一

# # 更新日志

> date:2024.1.10
>
> 优化blog内容

>  date:2024.2.18
>
> 优化blog内容

> date:2024.8.30
>
> 优化blog内容