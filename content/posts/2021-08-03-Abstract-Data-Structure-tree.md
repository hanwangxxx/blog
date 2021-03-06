---
title: 抽象数据结构-树
description: 常用的抽象数据类型（ADT） 树的介绍
tags:
  - 数据结构
  - 树
  - 二叉树
image: "https://tva1.sinaimg.cn/large/007S8ZIlly1gfjv3xmkknj30jb0cymxw.jpg"
slug: "/abstract-data-structure-tree/"
noComments: false
---


数据结构我们可以从逻辑上分为线性结构和非线性结构。

线性结构有数组，队列，栈，链表等， 
非线性结构有树，图等。

需要注意的是，线性和非线性不代表存储结构是线性的还是非线性的，这两者没有任何关系，它只是一种逻辑上的划分。比如我们可以用数组去存储二叉树。一般而言，有前驱和后继的就是线性数据结构。比如数组和链表。

队列是一种受限的序列。受限在哪呢？受限就受限在它只能够操作队尾和队首，并且只能只能在队尾添加元素，在队首删除元素。而数组就没有这个限制。在计算机科学中，一个 队列 (queue) 是一种特殊类型的抽象数据类型或集合，集合中的实体按顺序保存。

队列基本操作有两种：
向队列的后端位置添加实体，称为入队
从队列的前端位置移除实体，称为出队。
队列中元素先进先出 FIFO (first in, first out) 的示意：

![queue](https://tva1.sinaimg.cn/large/007S8ZIlly1gfjv3xmkknj30jb0cymxw.jpg)