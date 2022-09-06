---
title: 二叉树
date: 2022-09-06 09:25:00
author: XueYisheng
img: https://cdn.staticaly.com/gh/xys176/image-hosting@master/二叉树博客封面.6vbix11d1qs0.webp
top: true
hide: false
cover: true
coverImg: https://cdn.staticaly.com/gh/xys176/image-hosting@master/二叉树博客封面.6vbix11d1qs0.webp
password: 8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
toc: false
mathjax: false
summary: 数据结构学习二叉树部分
categories: 数据结构
tags:
  - Markdown
  - 二叉树
---
# 二叉树

## 二叉树链式结构的实现
### 定义二叉树
```C++
typedef char BTDataType;

typedef struct BinaryTreeNode
{
        BTDataType data;
        struct BinaryTreeNode* _left;
        struct BinaryTreeNode* _right;
}BTNode;

```

