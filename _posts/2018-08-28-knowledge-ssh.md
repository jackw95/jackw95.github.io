---
layout: post
title:  "SSH"
date:   2019-08-23
categories: 知识点
tags: web
excerpt: 安全的外壳协议
---

* content
{:toc}

####`SSH`协议
`Secure Shell`的缩写，安全的外壳协议。是为建立在应用层基础上的安全协议，专为远程登录会话和其他网络服务提供安全性的协议。
提供两种级别的安全验证：
- 基于口令的安全验证：账号和密码形式
- 基于密钥的安全验证：公钥和私钥形式（公钥存储在访问的服务器上）

创建`SSH`密钥：`ssh keygen -t rsa -C "email"`
然后在`~/.ssh`目录下：
`id_rsa`：存储私钥的文件
`id_rsa.pub`：存储公钥的问天