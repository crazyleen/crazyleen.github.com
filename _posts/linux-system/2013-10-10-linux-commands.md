---
layout: post
title: "linux常用命令备忘录"
description: "linux 常用命令备忘"
keywords: "linux, command"
category: Linux
tags: [linux]
---
{% include JB/setup %}


# linux常用命令备忘录

## grep 用法

	-R, -r, --recursive
	-L, --files-without-match  print only names of FILEs containing no match
	-l, --files-with-matches  print only names of FILEs containing matches

打印有某字符串的文件名

语法grep [string] -rl [dir]

	heavey@heavey-ThinkPad-T420:~$ grep linux -rl .
	./index.html~
	./.git/index
	./.git/logs/refs/heads/master
	./.git/logs/HEAD
	./index.html
	./_site/linux/2013/10/10/xwindow.html
	

## 批量替换文本字符串

### sed批量替换

	sed -i "s/oldstring/newstring/g" `grep oldstring -rl yourdir`

例如：替换/home下所有文件中的www.bcak.com.cn为bcak.com.cn

	sed -i "s/www.bcak.com.cn/bcak.com.cn/g" `grep www.bcak.com.cn -rl /home`


### perl批量替换

	perl -pi -e 's|ABCD|Linux|g' `find ./ -type f`

将调用perl执行一条替换命令，把find命令找到的所有文件内容中的ABCD替换为Linux

	find ./ -type f

此命令是显示当前目录下所有的文件, 's|ABCD|Linux|g'是perl要执行的脚本，即把所有ABCD替换为Linux
如果不写最后的那个g，'s|ABCD|Linux'将只替换每一行开头的ABCD 


## 递归删除文件\文件夹
 
### 删除文件夹

	find . -name "*.svn" -type d -print -exec rm -rf {} \; 
 
### 删除文件

	find  .  -name  '*.exe'  -type  f  -print  -exec  rm  -rf  {} \;

1. "."表示从当前目录开始递归查找。
2. “ -name "svn" "根据名称来查找。 
3. " -type d "查找的类型为目录 
4. " -type f "查找的类型为文件
5. "-print" 输出查找的文件目录名 
6. 最主要的是是-exec了，-exec选项后边跟着一个所要执行的命令，表示将find出来的文件或目录执行该命令。exec选项后面跟随着所要执行的命令或脚本，然后是一对儿{}，一个空格和一个\，最后是一个分号。 
 

