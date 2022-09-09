---
title: 二叉树
date: 2022-09-06 09:25:00
author: XueYisheng
img: https://cdn.staticaly.com/gh/xys176/image-hosting@master/QQ截图20220906223724.r3hz1ff4g2o.webp
top: true
hide: false
cover: true
coverImg: https://cdn.staticaly.com/gh/xys176/image-hosting@master/QQ截图20220906223724.r3hz1ff4g2o.webp
password: 8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
toc: false
mathjax: false
summary: 数据结构学习二叉树部分.树是一种非线性的数据结构，它是由n（n>=0）个有限结点组成一个具有层次关系的集合。把它叫做树是因
为它看起来像一棵倒挂的树，也就是说它是根朝上，而叶朝下的。
categories: 数据结构
tags:
  - Markdown
  - 二叉树
---
# 二叉树

## 二叉树链式结构的实现
### 定义二叉树
```
typedef char BTDataType;

typedef struct BinaryTreeNode
{
        BTDataType data;
        struct BinaryTreeNode* _left;
        struct BinaryTreeNode* _right;
}BTNode;

```

