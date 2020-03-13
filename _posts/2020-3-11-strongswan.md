---
layout: post
title: Openssl + QAT Engine 在VF上的安装和使用
categories: Network
description: strongswan 的安装和使用
keywords: sriov, qat, openssl, pf/vf, crypto
---
wget http://download.strongswan.org/strongswan-5.8.2.tar.bz2

tar xjvf strongswan-5.8.2.tar.bz2; 

cd strongswan-5.8.2

./configure --prefix=/usr --sysconfdir=/etc --<your-options>
#./configure --prefix=/usr --sysconfdir=/etc --enable-test-vectors --disable-af-alg --disable-gmp --enable-openssl
make
sudo make install

apt-get install -y pciutils-dev g++ pkg-config libssl-dev


SLL->SHIM
./configure --enable-icp-sriov=guest
