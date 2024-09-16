---
title: 【Git学习】[4]远程仓库
top: false
toc: true
mathjax: false
date: 2024-09-16 13:32:01
author:
img:
coverImg:
cover:
password:
summary:
tags:
categories:
---

## 重命名远程仓库

```
git remote rename origin github
```

![image-20240916133628463](【Git学习】-4-远程仓库/image-20240916133628463.png)

# #问题

## 一、Hexo推送源文件，安全性报错

![image-20240916135838561](【Git学习】-4-远程仓库/image-20240916135838561.png)

解决方案：转到log中指向的链接，选择use for test,

![image-20240916135827657](【Git学习】-4-远程仓库/image-20240916135827657.png)

可以看到，修改后，再次push，成功提交到github。

![image-20240916140029571](【Git学习】-4-远程仓库/image-20240916140029571.png)
