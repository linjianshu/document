#### hugo学习文档

1.应该要配置一下环境变量(如果使用hugo extend的话)

![image-20210927201218400](hugo%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210927201218400.png)

2.然后打开一个任意位置的文件夹 cmd命令

```bash
D:\Softwares\hugo_extended_0.53_Windows-64bit>hugo new site ./ -f=yaml --force
```

3.初始化git

在文件夹里右键git bash

```bash
Administrator@yourtreedad MINGW64 /d/Softwares/hugo_extended_0.53_Windows-64bit/ljsDemo
$ git init
Initialized empty Git repository in D:/Softwares/hugo_extended_0.53_Windows-64b
it/ljsDemo/.git/

Administrator@yourtreedad MINGW64 /d/Softwares/hugo_extended_0.53_Windows-64bit/ljsDemo (master)
$ git submodule add https://github.com/hugo-toha/toha.git themes/toha
Cloning into 'D:/Softwares/hugo_extended_0.53_Windows-64bit/ljsDemo/themes/toha
'...
remote: Enumerating objects: 3647, done.
remote: Counting objects: 100% (1372/1372), done.
remote: Compressing objects: 100% (666/666), done.
remote: Total 3647 (delta 814), reused 1187 (delta 701), pack-reused 2275
Receiving objects: 100% (3647/3647), 31.82 MiB | 2.42 MiB/s, done.
Resolving deltas: 100% (2082/2082), done.
starting fsmonitor-daemon in 'D:/Softwares/hugo_extended_0.53_Windows-64bit/ljs
Demo/themes/toha'
warning: LF will be replaced by CRLF in .gitmodules.
The file will have its original line endings in your working directory
```

4.选择一个漂亮的主题

https://toha-guides.netlify.app/posts/getting-started/prepare-site/

5.尝试运行在本地跑一遍

```bash
D:\Softwares\hugo_extended_0.53_Windows-64bit\mysite>hugo server -t toha -w
Start building sites …
hugo v0.87.0-B0C541E4+extended windows/amd64 BuildDate=2021-08-03T10:57:28Z VendorInfo=gohugoio

                   | EN
-------------------+------
  Pages            |  37
  Paginator pages  |   1
  Non-page files   |   0
  Static files     | 293
  Processed images |  22
  Aliases          |   4
  Sitemaps         |   1
  Cleaned          |   0

Built in 2157 ms
...
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop

```

