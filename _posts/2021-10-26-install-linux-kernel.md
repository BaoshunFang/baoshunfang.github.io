---
layout: post
title:  编译安装及卸载Linux内核
categories: [kernel]
tags: [linux, kernel]
---

#### 内核下载地址
[官方源](https://kernel.org)
[国内镜像](https://kernel.source.codeaurora.cn/pub/scm/linux/kernel/git/torvalds/linux.git/)
#### 环境配置
`sudo apt update && sudo apt upgrade  `
`sudo apt-get install git fakeroot build-essential ncurses-dev xz-utils libssl-dev bc flex libelf-dev bison`
#### 配置内核
拷贝当前内核的配置文件：  
`cp /boot/config-$(uname -r) .config`
用menuconfig做必要的更改：  
`make menuconfig`
#### 编译和安装
编译  
`make -j16`  
安装模块  
`sudo make modules_install`  
安装内核  
`sudo make install`
#### 启动内核作为引导
`sudo update-initramfs -c -k 5.13.0  #使用正确的版本号` 
更新grub
`sudo update-grub`

#### 卸载官方释放版本
获取所有安装的内核版本
`dpkg --get-selections | grep linux`
选择要卸载的版本，卸载下列安装包
```
sudo apt remove linux-image-<版本>-generic
sudo apt remove linux-headers-<版本>
sudo apt remove linux-headers-<版本>-generic
sudo apt remove linux-modules-<版本>-generic
```
#### 卸载源码安装版本
```
sudo rm -rf /boot/vmlinuz-<版本>
baoshun@baoshun-ubuntu:~$ sudo rm -rf /boot/initrd.img-<版本>
baoshun@baoshun-ubuntu:~$ sudo rm -rf /boot/System.map-5.15.0+*
baoshun@baoshun-ubuntu:~$ sudo rm -rf /boot/config-<版本>
baoshun@baoshun-ubuntu:~$ sudo rm -rf /lib/modules/<版本>/
```
内核卸载后，记得更新grub
`sudo update-grub`