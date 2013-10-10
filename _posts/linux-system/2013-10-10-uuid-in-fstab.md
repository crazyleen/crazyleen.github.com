---
layout: post
title: "用UUID在Fstab中挂载分区"
description: "用UUID在fstab中挂载分区"
keywords: "UUID, fstab"
category: Linux
tags: [ubuntu]
---
{% include JB/setup %}

# 用UUID在fstab中挂载分区

Linux 在启动的时候通过 fstab 中的信息挂载各个分区，一个典型的分区条目就像这样：
 
	/dev/sdb5 /mnt/usb vfat utf8,umask=0 0 0
 
/dev/sda4 为需要挂载的分区，sda4 是 Linux 检测硬盘时按顺序给分区的命名，一般来讲，这个名称并不会变化，但是如果你有多块硬盘，硬盘在电脑中的顺序变化的时候，相同的名称可能代表着不同的硬盘分区，如果你是从 USB 设备启动，与其他 USB 设备的插入顺序也会导致分区识别的困难。
 
这个时候 UUID 就派上用场了，UUID 全称是 Universally Unique Identifier，也就是说，每个分区有一个唯一的 UUID 值，这样就不会发生分区识别混乱的问题了。
 
在 fstab 中用 UUID 挂载分区，看起来向这样：
 
	UUID=1234-5678 /mnt/usb vfat utf8,umask=0 0 0
 
在 UUID= 后面填入分区相应的 UUID 值，就可以正确挂载分区了。
 
获取分区的UUID有 3 种方法：
 
1. 通过浏览 /dev/disk/by-uuid/ 下的设备文件信息。
 
	# ls -l /dev/disk/by-uuid/
	------
	lrwxrwxrwx 1 root root 10 10-13 09:14 0909-090B -> ../../sdb5
	lrwxrwxrwx 1 root root 10 10-13 09:13 7c627a81-7a6b-4806-987b-b5a8a0a93645 -> ../../sda4
	.....
 
2. 通过 vol_id 命令。
 
	# vol_id /dev/sdb5
	ID_FS_USAGE=filesystem
	ID_FS_TYPE=vfat
	ID_FS_VERSION=FAT32
	ID_FS_UUID=0909-090B
	ID_FS_UUID_ENC=0909-090B
	ID_FS_LABEL=SWAP
	ID_FS_LABEL_ENC=SWAP
	ID_FS_LABEL_SAFE=SWAP
 
3. 通过 blkid 命令
 
	# blkid /dev/sdb5
	/dev/sdb5: LABEL="SWAP" UUID="0909-090B" TYPE="vfat"
 
通过这三种方法都可以获得分区的 UUID，UUID 依据分区不同，长度和格式都不相同
