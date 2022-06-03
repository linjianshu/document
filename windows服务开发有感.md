---
title: "windows服务开发备忘"
date: 1999-10-01T09:17:59+08:00
draft: false
categories:
    -项目相关
tags:
    - windows服务
---

#### windows服务开发备忘

先开个窗体来调试试试看

再新增一个service服务进来

修改默认服务名 

添加安装程序 修改为本地

![image-20210928105412125](windows%E6%9C%8D%E5%8A%A1%E5%BC%80%E5%8F%91%E6%9C%89%E6%84%9F.assets/image-20210928105412125.png)

记得引入日志 并将config文件复制到输出目录

有时候install.bat命令不行可能是系统没有权限

跑服务的时候记得再program里改成服务,别泡成窗体应用了

服务的onstart里需要写的是异步方法或者新开一个线程,否则会出现无法服务进程无法连接到服务控制器上的错误

![image-20210928105853916](windows%E6%9C%8D%E5%8A%A1%E5%BC%80%E5%8F%91%E6%9C%89%E6%84%9F.assets/image-20210928105853916.png)



![image-20210928105911601](windows%E6%9C%8D%E5%8A%A1%E5%BC%80%E5%8F%91%E6%9C%89%E6%84%9F.assets/image-20210928105911601.png)

接口服务嘛,最好尝试ping一下服务器,服务器畅通才能工作

另外最好对间隔时间做到可配置







