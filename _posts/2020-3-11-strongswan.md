---
layout: post
title: strongswan的安装和使用-Host-Host场景
categories: Network 
description: strongswan 的安装和使用-搭建Host-Host场景
keywords: network, openssl, strongswan, ipsec, vpn
---
strongSwan是一个Linux平台下或者基于UNIX的操作系统下，支持IKEv1/IKEv2密钥的开源的基于IPsec的VPN解决方案。

* [编译安装](#编译安装)
* [场景搭建](#场景搭建)
    * [Swanctl](#Swanctl)
    * [IPSec](#IPSec)
* [调用测试](#调用测试)
    * [命令行调用](#命令行调用)
    * [系统调用](#系统调用)
* [问题](#问题)
 

## 编译安装
下载并解压strongswan-5.8.2
> wget http://download.strongswan.org/strongswan-5.8.2.tar.bz2  
> tar xjvf strongswan-5.8.2.tar.bz2  
> cd strongswan-5.8.2  

根据自己的应用场景配置strongswan安装程序，本文档建立基于Openssl + QAT的Ipsec，所以开启openssl支持
> ./configure \-\-prefix=/usr -\-sysconfdir=/etc -\-enable-test-vectors -\-disable-gmp -\-enable-openssl  
> > 其他配置详情可以通过./configure -h浏览  
>
> make  
> sudo make install  

注意，安装前请先安装好Openssl环境，QAT相关配置是可选的，具体步骤可以看[Openssl + QAT Engine 在VF上的安装和使用](https://leyao-daily.github.io/2020/03/12/openssl-qat/)

如果使用其他配置，请根据编译提示安装所需的软件包即可。

## 场景搭建
本说明中采用最简单的场景进行搭建，建立Host与Host对接的场景。
![host-to-host 场景](https://raw.githubusercontent.com/leyao-daily/leyao-daily.github.io/master/images/posts/strongswan/h2h.png)

采用Strongswan搭建IPSec可以通过两种方式，旧版的IPSec工具和新版Swanctl工具，两种搭建方法都是基于Strongswan的，但配置过程完全不同。
###IpSec

###Swanctl
