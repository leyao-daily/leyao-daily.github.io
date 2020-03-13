---
layout: post
title: Openssl + QAT Engine 在VF上的安装和使用
categories: Crypto
description: Openssl + QAT Engine 在VF上的安装和使用
keywords: sriov, qat, openssl, pf/vf, crypto
---
本文档的目的在于提供一个具体而有效的Openssl + QAT Engine的搭建指南，区别于传统的搭建环境，我是在基于libvirt启动的虚拟机中，对利用SRIOV技术而挂载进入VM的QAT VF进行驱动加载和配置，完成Openssl Crypto Library对QAT的有效利用。

* [背景](#背景)
    * [搭建环境](#搭建环境)
    * [系统配置](#系统配置)
* [安装使用](#安装使用)
    * [基本环境](#基本环境)
    * [QAT驱动安装](#QAT驱动安装)
    * [Openssl安装](#Openssl安装)
    * [QAT Engine安装](#QAT Engine安装)
    * [QAT VF配置](#QAT VF配置)
* [调用测试](#调用测试)
    * [命令行调用](#命令行调用)
    * [系统调用](#系统调用)
* [问题](#问题)

## 背景
### 搭建需求
使用QAT，要求主机或者Sever有QAT加速卡，本文档中搭建所用的服务器有三个QAT卡
> root@ubuntu:~# lspci -d:37c8
> > 0000:3d:00.0 Co-processor: Intel Corporation C62x Chipset QuickAssist Technology (rev 04)  
> > 0000:3f:00.0 Co-processor: Intel Corporation C62x Chipset QuickAssist Technology (rev 04)  
> > 0000:da:00.0 Co-processor: Intel Corporation C62x Chipset QuickAssist Technology (rev 04)  

### 系统配置
> cpu
> > CPU(s):              72  
> > Model name:          Intel(R) Xeon(R) Gold 6139 CPU @ 2.30GHz  

> memory
> > Mem:           251G 

> OS
> > Ubuntu-18.04-server  
> > Linux ubuntu 4.15.0-55-generic #60-Ubuntu SMP Tue Jul 2 18:22:20 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux  

注意：本文档接下来的步骤都是在Host中启动的libvirt虚拟机中进行的操作。

## 安装使用
### 基本环境
请在root权限下进行本文档的步骤
> sudo -i

安装后续安装所需的库，挂载依赖驱动
> apt update  
> apt-get install -y gcc make libpci-dev g++ pkg-config libssl-dev autoconf libtool libnuma-dev  
> modprobe uio  

检查QAT VF被正确分配
> lspci -d:37c9
> > 00:04.0 Co-processor: Intel Corporation Device 37c9 (rev 04)  

### QAT驱动安装
从01.org下载对应机器中QAT卡的驱动 [指南和驱动](https://01.org/intel-quickassist-technology)
> cd  
> wget https://01.org/sites/default/files/downloads//qat1.7.l.4.8.0-00005.tar.gz  

创建工作目录并解压驱动包
> mkdir QAT  
> mv qat1.7.l.4.8.0-00005.tar.gz ./QAT  
> cd QAT && tar zxvf qat1.7.l.4.8.0-00005.tar.gz  

配置QAT并编译安装，对于QAT VF来说，驱动安装需要配置guest sriov mode
> ./configure --enable-icp-sriov=guest  
> make  
> make install  

（Optional）安装sample应用
> make samples-install

确认QAT驱动安装并加载
> lsmod | grep qat
> > qat_c62xvf             16384  0  
> >
> > intel_qat             196608  2 usdm_drv,qat_c62xvf  
> >
> > uio                    20480  1 intel_qat  
>
> #还可以通过sample应用进行QAT测试  
> cpa_sample_code  

### Openssl安装
下载安装包并解压
> cd  
> wget https://github.com/openssl/openssl/archive/OpenSSL_1_1_1a.tar.gz --no-check-certificate  
> tar zxvf OpenSSL_1_1_1a.tar.gz  
> cd openssl-OpenSSL_1_1_1a  

配置并安装Openssl
> ./config --prefix=/usr/local/ssl  
> make depend  
> make  
> make install  

配置Openssl Engine环境
> echo export OPENSSL_ENGINES=/usr/local/ssl/lib/engines-1.1 >> /root/.bashrc


### QAT Engine安装 
下载安装包并解压
> cd  
> wget https://github.com/intel/QAT_Engine/archive/v0.5.43.tar.gz --no-check-certificate  
> tar zxvf v0.5.43.tar.gz  
> cd QAT_Engine-0.5.43  

配置并安装QAT Engine
> ./autogen.sh  
> ./configure --with-qat_dir=/root/QAT --with-openssl_install_dir=/usr/local/ssl  
> make  
> make install  

### QAT VF配置
本文档所搭建环境中QAT使用C6xx系列驱动，而且是对VF的编译，于是编译完成后会在/etc下看到VF配置文件
> ls /etc | grep c6xx
> > c6xxvf_dev0.conf

这里要注意，因为要通过Openssl使用QAT Engine，所以对QAT的配置需要更改section name并重启qat_service
> sed -i 's/\[SSL\]/\[SHIM\]/g' /etc/c6xxvf_dev0.conf  
> service qat_service restart  

Openssl打印QAT引擎信息
> openssl engine -t -c -vvvv qat
> > (qat) Reference implementation of QAT crypto engine  
> > [RSA, DSA, DH, AES-128-CBC-HMAC-SHA1, AES-128-CBC-HMAC-SHA256, AES-256-CBC-HMAC-SHA1, AES-256-CBC-HMAC-SHA256, TLS1-PRF, HKDF]  
> >     [ available ]  
> >     ...  

## 调用测试
### 命令行调用
Openssl通过命令行显示的调用QAT Engine来使用QAT卡十分简单，只需要在命令中加入-engine qat
纯Openssl同步测速rsa2048
> openssl speed -elapsed rsa2048

|     |   sign   |  verify  |  sign/s  | verify/s |
| :-: | :-: | :-: | :-: | :-: |
|rsa 2048 bits | 0.000612s | 0.000018s |   1633.5 | 57114.6 | 

使用QAT卡同步测速res2048
> openssl speed -engine qat -elapsed rsa2048

|     |   sign   |  verify  |  sign/s  | verify/s |
| :-: | :-: | :-: | :-: | :-: |
| rsa 2048 bits | 0.000472s | 0.000069s | 2118.5 | 14549.3 | 

纯Openssl异步测速rsa2048
> openssl speed -elapsed -async_jobs 36 rsa2048

|     |   sign   |  verify  |  sign/s  | verify/s |
| :-: | :-: | :-: | :-: | :-: |
| rsa 2048 bits | 0.000614s | 0.000018s | 1627.6 | 56026.5 |

使用QAT卡异步测速res2048
> openssl speed -engine qat -elapsed -async_jobs 36 rsa2048 

|     |   sign   |  verify  |  sign/s  | verify/s |
| :-: | :-: | :-: | :-: | :-: |
| rsa 2048 bits | 0.000034s | 0.000009s | 29235.7 | 109564.0 | 

其中rsa2048是测试的算法，还可以替换测试其他如ecdhp256、ecdsap256等等

### 系统调用
通过修改openssl的config文件，我们可以默认调用QAT Engine来进行加解密等操作
> vim /etc/ssl/openssl.cnf

需要在文件最开始声明初始化内容，写入
> openssl_conf = openssl_init

在这里声明了section：openssl_init，在openssl.cnf中紧挨着第一个section前写入
> [ openssl_init ]  
> engines = engine_section  

engines字段是OpenSSL识别为配置模块的关键字。该字段是包含要加载的引擎列表的部分名称。因此，对于英特尔®QAT OpenSSL *引擎，这里之后要写入:
> [ engine_section ]  
> qat = qat_section  

然后配置QAT Engine相关的信息
> [ qat_section ]  
> engine_id = qat  
> dynamic_path = /usr/local/ssl/lib/engines-1.1/qat.so  
> default_algorithms = ALL  

这样，在之后对openssl的调用中，都会默认使用QAT进行加速。
> openssl speed -elapsed -async_jobs 36 rsa2048

|     |   sign   |  verify  |  sign/s  | verify/s | 
| :-: | :-: | :-: | :-: | :-: |
| rsa 2048 bits | 0.000034s | 0.000008s |  29359.8 | 119933.0 | 

以上就是在拥有QAT VF的VM中搭建Openssl + QAT Engine的全过程了。

## 问题
> configdata.pm not present in the @INC path
> > export PERL5LIB=$PERL5LIB:/root/openssl-OpenSSL_1_1_1a
