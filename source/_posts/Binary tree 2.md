---
title: 二叉树(LeetCode练习题)
date: 2022-09-11 22:02:00
author: XueYisheng
img: https://cdn.staticaly.com/gh/xys176/image-hosting@master/QQ截图20220911222430.6nfcwg9lnmk0.webp
top: false
hide: false
cover: true
coverImg: https://cdn.staticaly.com/gh/xys176/image-hosting@master/QQ截图20220911222430.6nfcwg9lnmk0.webp
password: 8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
toc: false
mathjax: false
summary: 树是一种非线性的数据结构，它是由n（n>=0）个有限结点组成一个具有层次关系的集合。把它叫做树是因为它看起来像一棵倒挂的树，也就是说它是根朝上，而叶朝下的。
categories: 数据结构
tags:
  - 二叉树
  - LeetCode
---
# 二叉树LeetCode联系（C语言）

## 965. 单值二叉树
https://leetcode.cn/problems/univalued-binary-tree/
```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

bool isUnivalTree(struct TreeNode* root){
    if(root == NULL)
    {
        return true;
    }
    if(root->left && root->left->val != root->val)
    return false;
    if(root->right && root->right->val != root->val)
    return false;
    return isUnivalTree(root->left)&&isUnivalTree(root->right);
}

```
- 二叉树中的判断，以判错作为返回条件更清晰。当root==NULL时返回真。
- 返回值中可以同时进行判断&&。
---

## 100. 相同的树
https://leetcode.cn/problems/same-tree/

```
bool isSameTree(struct TreeNode* p, struct TreeNode* q){
    if(p == NULL && q == NULL)
    {
        return true;
    }else if(p == NULL && q != NULL)
    {
        return false;
    }else if(p != NULL && q == NULL)
    {
        return false;
    }else if(p->val != q->val)
    {
        return false;
    }
    if(!isSameTree(p->left,q->left)) 
    {
        return false;
    }
    if(!isSameTree(p->right,q->right))
    {
        return false;
    }
    return true;
}
```
- 清楚判错的所有条件，不要漏掉情况
---
## 101. 对称二叉树 
https://leetcode.cn/problems/symmetric-tree/
```
bool isCompare(struct TreeNode* p,struct TreeNode* q)
{
    if(p == NULL && q == NULL)
    {
        return true;
    }else if(p != NULL && q == NULL)
    {
        return false;
    }else if((p == NULL && q != NULL))
    {
        return false;
    }else if(p->left!=NULL && q->right!=NULL && p->left && p->left->val != q->right->val)
    {
        return false;
    }else if(p->left == NULL && q->right != NULL)
    {
        return false;
    }else if(p->right == NULL && q->left != NULL)
    {
        return false;
    }else if(p->left != NULL && q->right == NULL)
    {
        return false;
    }else if(p->right != NULL && q->left == NULL)
    {
        return false;
    }
    return isCompare(p->left,q->right) && isCompare(p->right,q->left);
}

bool isSymmetric(struct TreeNode* root){
    if(root == NULL)
    {
        return true;
    }
    return isCompare(root,root);
}
```

## 104. 二叉树的最大深度
https://leetcode.cn/problems/maximum-depth-of-binary-tree/

```
int maxDepth(struct TreeNode* root){
    if(root == NULL)
        return 0;
    int leftD = maxDepth(root->left);
    int rightD = maxDepth(root->right);
    return leftD > rightD ? leftD+1 : rightD+1;
}
```
## 572. 另一棵树的子树
https://leetcode.cn/problems/subtree-of-another-tree/
```
bool Compare(struct TreeNode* root, struct TreeNode* subRoot)
{
    if(root == NULL && subRoot == NULL)
    {
        return true;
    }
    if(root == NULL && subRoot !=NULL)
    {
        return false;
    }
    if(root != NULL && subRoot == NULL)
    {
        return false;
    }
    if(root != NULL && subRoot != NULL && root->val != subRoot->val)
    {
        return false;
    }
    return Compare(root->left,subRoot->left) && Compare(root->right,subRoot->right);
}

bool SubtreeCompare(struct TreeNode* root, struct TreeNode* subRoot)
{
    if(root == NULL)
    {
        return false;
    }
    if(root->val == subRoot->val)
    {
        bool temp = Compare(root,subRoot);
        if(temp == true)
        return temp;
    }
    return SubtreeCompare(root->left,subRoot) || SubtreeCompare(root->right,subRoot);
}

bool isSubtree(struct TreeNode* root, struct TreeNode* subRoot){
    if(subRoot == NULL)
        return true;
    //if(subRoot->val != root->val)
    //    return false;
    if(root == NULL && subRoot != NULL)
    {
        return false;
    }
    return SubtreeCompare(root, subRoot);
}
```

## 144. 二叉树的前序遍历
https://leetcode.cn/problems/binary-tree-preorder-traversal/
```
//前序遍历
void PreOrder(struct TreeNode* root, int *array, int* pi)
{
    if(root == NULL)
    {
        return;
    }
    array[(*pi)++] = root->val;
    PreOrder(root->left,array,pi);
    PreOrder(root->right,array,pi);
}

 //得到数组的长度
 int getLong(struct TreeNode* root)
 {
     if(root == NULL)
     {
         return 0;
     }
     return getLong(root->left)+getLong(root->right) + 1;
 }

int* preorderTraversal(struct TreeNode* root, int* returnSize){
    *returnSize = getLong(root);
    int *array = (int*)malloc(*returnSize * sizeof(int));
    int i = 0;
    PreOrder(root,array,&i);
    return array;
}
```
- 这种在遍历的递归中有数组存在的，对数组的下标值访问，必须以指针地址的方式访问。才能保证每次都是在原来的基础上加一，如果不用指针，就会发生修改局部变量i，而没有修改上层中的i值。发生访问错误。
## 94. 二叉树的中序遍历 
https://leetcode.cn/problems/binary-tree-inorder-traversal/
```
//中序遍历
void InOrder(struct TreeNode* root,int* array,int* pi)
{
    if(root == NULL)
    {
        return;
    }
    InOrder(root->left,array,pi);
    array[(*pi)++] = root->val;
    InOrder(root->right,array,pi);
}

 //得到节点个数
 int getLong(struct TreeNode* root)
 {
     if(root == NULL)
     {
         return 0;
     }
     return getLong(root->left)+getLong(root->right)+1;
 }

int* inorderTraversal(struct TreeNode* root, int* returnSize){
    *returnSize = getLong(root);
    int* array = (int*)malloc(sizeof(int) * *returnSize);
    int i = 0;
    InOrder(root,array,&i);
    return array;
}
```

## 145. 二叉树的后序遍历
https://leetcode.cn/problems/binary-tree-postorder-traversal/

```
//后序遍历
void PostOrder(struct TreeNode* root,int* array,int* pi)
{
    if(root == NULL)
    {
        return ;
    }
    PostOrder(root->left,array,pi);
    PostOrder(root->right,array,pi);
    array[(*pi)++] = root->val;
}

//得到节点个数
int getLong(struct TreeNode* root)
{
    if(root == NULL)
    {
        return 0;
    }

    return getLong(root->left) + getLong(root->right) + 1;
}

int* postorderTraversal(struct TreeNode* root, int* returnSize){
    *returnSize = getLong(root);
    int* array = (int*)malloc(sizeof(int) * *returnSize);
    int i = 0;
    PostOrder(root,array,&i);
    return array;
}
```
