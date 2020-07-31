---
layout: post
title: Rust语言特性总结
categories: Language 
description: Rust语言特性总结
keywords: rust, program language, features, web-assembly 
---
本文对Rust语言特性进行了简单的介绍和总结。

* [零成本的抽象](#零开销的抽象)
* [调用测试](#调用测试)
    * [系统调用](#系统调用)
* [问题](#问题)
 

## 零成本抽象
零成本抽象的定义来自C++，C++创始人Bjarne Stroustrup定义：
> What you don’t use, you don’t pay for. And further: What you do use, you couldn’t hand code any better.

零成本抽象定义：
> 1. 没有整体开销：零成本抽象不应该对不使用它的程序的性能表现产生负面影响。

