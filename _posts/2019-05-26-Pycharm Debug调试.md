---
layout:     post
title:      Pycharm Debug使用
subtitle:   Pycharm Debug 断点入门
date:       2019-05-26
author:     Threekb
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - python
    - pycharm
    - Debug
---

# Pycharm断点调试

**断点是在开发或者审计过程中最常用的一个功能，这篇文章不做审计的详细解释，只单纯介绍debug功能的简单使用。**



### 第一步：

* 设置参数，如果没有可以不设置

​       依次打开 Run -> Edit Configurations

![](https://threekb-1259310634.cos.ap-beijing.myqcloud.com/blog/1558851261(1).jpg)

* 设置Script path为调试的.py路径
* 设置parameters为参数，没有可以不写

![](https://threekb-1259310634.cos.ap-beijing.myqcloud.com/blog/1558851300(1).jpg)

### 第二步：

* 在程序的入口或者要测试的功能代码处打上断点，在行号处单机即可
* 接下来点击右上角小虫子的按钮，开始进行调试

![](https://threekb-1259310634.cos.ap-beijing.myqcloud.com/blog/1558851361(1).jpg)

### 第三步

* 已经开始调试后我们可以看到在debug窗口处有几个功能按钮，从左到右依次为：
  * Step over （F8）  单步运行，运行接下来的一条代码
  * Step into  （F7）  配合F8运行，进入函数每部，碰到想要查看具体运行过程的函数可以在F8到这个位置之后 F7进入函数内部查看
  * Step into mycode  （alt+shift+F7） F7和F8的结合，遇到函数会进入函数内部，否则只会F7单步运行
  * Force step Into （shift + F8）进入函数内部后调试完，使用这个跳出
  * Resume program (F9)  直接跳到下一个断点
  * Run to cursor （alt + F9） 运行光标位置的代码

![](https://threekb-1259310634.cos.ap-beijing.myqcloud.com/blog/1558851412(1).jpg)



**其实也就几个功能点，怎么用完全看情况，需求而言！**
