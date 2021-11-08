---
layout: post
title:  ubuntu sudo免密
categories: [ubuntu]
tags: [ubuntu, sudo]
---

sudo 每次输入密码比较麻烦，可以通过下面方法使sudo免密
#### 修改方法
```
sudo visudo
在文件末尾添加(Your_UserName替换为你的用户名)：
UserName ALL=(ALL) NOPASSWD: ALL
```