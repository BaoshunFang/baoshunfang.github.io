---
layout: post
title:  ubuntu安装并启动ssh server
categories: [ubuntu]
tags: [ubuntu, ssh]
---

刚安装的ubuntu系统只带了ssh client，没有ssh server，需要手动安装
#### 查看当前系统是否安装了ssh-server
`dkpg -l | grep ssh`
示例机器已经安装了ssh-server，如果没有安装会只有client
![SSH](/img/posts/grep_ssh.png "grep ssh")
#### 安装openssh-server
`sudo apt-get install openssh-server`
#### 确认ssh-server服务已开启
如图：sshd 表示服务已开启
![SSHD](/img/posts/sshd_service.png "sshd service")
