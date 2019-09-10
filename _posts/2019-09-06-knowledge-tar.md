---
layout: post
title:  "服务器上传/下载文件"
date:   2019-09-06
categories: 知识点
tags: 知识点
---

* content
{:toc}
`Linux`服务器上文件或文件夹下载



**打包**：`tar -zcvf 新文件 源文件或文件夹`

```
-- 单文件打包
$ tar -zcvf index.tar.gz index.html		

-- 多文件打包
$ tar -zcvf index.tar.gz index.html css/ js/ image/
```

**解压**：`tar -zxcf 新文件 源文件或文件夹`

```
-- 解压到当前目录下
$ tar -zxvf index.tar.gz

-- 解压到指定目录
$tar -zxvf index.tar.gz /home/www
```

注：`c`指的是`create`创建，`x`指的是`extract`提炼。



**使用`xshell`工具 进行上传/下载**

安装`lrzsz`：`yum install lrzsz`

`rz target`：会将`windows`文件上传到`linux`服务器

`sz filename`：将文件下载到`windows`本地


