---
layout: post
title: "在linux递归删除某个文件\文件夹(svn)的命令"
description: "在linux递归删除某个文件\文件夹(svn)的命令"
keywords: "linux, find"
category: Linux
tags: [ubuntu]
---
{% include JB/setup %}

### 在linux递归删除某个文件\文件夹(svn)的命令： 
 
#### 删除文件夹

	find . -name "*.svn" -type d -print -exec rm -rf {} \; 
 
#### 删除文件

	find  .  -name  '*.exe'  -type  f  -print  -exec  rm  -rf  {} \;

1."."表示从当前目录开始递归查找。 
2.“ -name "svn" "根据名称来查找。 
3." -type d "查找的类型为目录 
4." -type f "查找的类型为文件
5."-print" 输出查找的文件目录名 
6.最主要的是是-exec了，-exec选项后边跟着一个所要执行的命令，表示将find出来的文件或目录执行该命令。exec选项后面跟随着所要执行的命令或脚本，然后是一对儿{}，一个空格和一个\，最后是一个分号。 
 

