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
summary: 树是一种非线性的数据结构，它是由n（n>=0）个有限结点组成一个具有层次关系的集合。把它叫做树是因为它看起来像一棵倒挂的树，也就是说它是根朝上，而叶朝下的。
categories: 数据结构
tags:
  - 二叉树
---
# 二叉树

## 二叉树链式结构的实现
### 1.定义二叉树
（二叉树节点与节点存储的数据类型）
```
typedef char BTDataType;

typedef struct BinaryTreeNode
{
        BTDataType data;
        struct BinaryTreeNode* _left;
        struct BinaryTreeNode* _right;
}BTNode;

```
创建一个存储字符数据类型的二叉树。可以直接在typedef修改二叉树中存储的数据类型，便于后期修改。
### 2. 创建（新建）节点 

```
BTNode* BuyNode(BTDataType x)
{
        BTNode* node = (BTNode*)malloc(sizeof(BTNode));
        assert(node);
        node->data = x;
        node->_left = NULL;
        node->_right = NULL;
        return node;
}
```
默认设置左右孩子为空。   
使用assert检测node节点创建是否成功。若有错，系统会有提示，而不是直接崩溃。例如使用整数除以0，assert函数就会报错。
### 3. 创建（新建）二叉树 
```
BTNode* CreatBinaryTree()
{
        BTNode* node1 = BuyNode('1');
        BTNode* node2 = BuyNode('2');
        BTNode* node3 = BuyNode('3');
        BTNode* node4 = BuyNode('4');
        BTNode* node5 = BuyNode('5');
        BTNode* node6 = BuyNode('6');

        node1->_left = node2;
        node1->_right = node3;
        node2->_left = node4;
        node2->_right = node5;
        node3->_right = node6;

        return node1;
}
```
创建如图所示的二叉树模型。
<div align=center>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(25).1wkpets31ubk.webp"  width="45%"/>
</div>  

### 4. 遍历二叉树 
遍历二叉树，就是对二叉树的每个节点访问一次。并且需要满足某种特定的规则。主要分为前序，中序，后续遍历。   
因此对于上图所表示的二叉树有以下遍历结果：   
| Name |  score |
| - |  -: |
| 前序遍历 |  1 2 4 # # 5 # # 3 # 6 # # |
| 中序遍历 |  # 4 # 2 # 5 # 1 # 3 # 6 # |
| 后序遍历 |  # # 4 # # 5 2 # # # 6 3 1 |
#### 4.1 前序遍历 
前序遍历(Preorder Traversal 亦称先序遍历)——访问根结点的操作发生在遍历其左右子树之前。
<div align=center>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(26).2n6gqyw62pc0.webp"  width="45%"/>
</div> 

- 前序遍历，根，左子根，右子根。先1，后1的左孩子2,2的左孩子4,4的左孩子空，4的右孩子空，2的右孩子5,5的左右孩子均为空，1的右孩子3,3的左孩子空，3的右孩子6,6的左右孩子均为空。      

```
void BinaryTreePrevOrder(BTNode* root)
{
        if (root == NULL)
        {
                printf("# ");
                return;
        }
        printf("%c ",root->data);
        BinaryTreePrevOrder(root->_left);
        BinaryTreePrevOrder(root->_right);
}
```
<div align=center>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(29).1dsr0n5pyfvk.webp"  width="100%"/>
</div> 

#### 4.2 中序遍历 
- 中序遍历(Inorder Traversal)——访问根结点的操作发生在遍历其左右子树之间。     

中序遍历，左子根，根，右子根。先向左遍历找到，最左子根4的左孩子为空，再根4，4的右孩子为空，再根2，再2的右孩子5，再5的左孩子为空，在根5，再5的右孩子为空，再根1，再1的右子树根3，但3有左孩子，先访问3的左孩子空，再根3，再3的右子树根6，但6有左孩子，再6的左孩子为空，再根6，再6的右孩子为空。

<div align=center>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(27).15zc94ev9a74.webp"  width="45%"/>
</div>

```
void BinaryTreeInOrder(BTNode* root)
{
        if (root == NULL)
        {
                printf("# ");
                return;
        }
        BinaryTreeInOrder(root->_left);
        printf("%c ", root->data);
        BinaryTreeInOrder(root->_right);
}
```
<div align=center>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(30).6emaycebxhk0.webp"  width="100%"/>
</div> 

#### 4.3 后序遍历 
- 后序遍历(Postorder Traversal)——访问根结点的操作发生在遍历其左右子树之后。 

后序遍历，左子根，右子根，根。1的最左为4，先4的左孩子为空，再4的右孩子为空，再根4，再回溯到2,到2的右子树5，再访问5的左右孩子均为空。再回溯访问2，再回溯到1,1的右子树3,再访问3的左孩子为空，再回溯到2，2的右子树6，再访问6的左右孩子为空。再回溯访问6，再回溯访问到1。
<div align=center>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(28).7769nyaj1d00.webp"  width="45%"/>
</div>

```
void BinaryTreePostOrder(BTNode* root)
{
        if (root == NULL)
        {
                printf("# ");
                return;
        }
        BinaryTreePostOrder(root->_left);
        BinaryTreePostOrder(root->_right);
        printf("%c ", root->data);
}
```
<div align=center>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(31).2lztw4cs8xs0.webp"  width="100%"/>
</div> 
三个运行结果和初期预测的执行结果相同。

### 5. 二叉树的简单统计

#### 5.1 二叉树节点个数
```
// 二叉树节点个数
int BinaryTreeSize(BTNode* root)
{
        if (root == NULL)
        {
                return 0;
        }
        return BinaryTreeSize(root->_left) + BinaryTreeSize(root->_right) + 1;
}
```

#### 5.2 二叉树叶节点个数
一个特别需要注意的点：<font color=red>在二叉树的递归，进入循环的第一步一定要先判断节点是否为空</font>。对于下面的代码而言，若是先判断左右孩子是否为空再判断节点为空，程序就会崩溃。因为会出现当程序访问了空节点时还要判断该空节点的左右孩子是否为空。

```
int BinaryTreeLeafSize(BTNode* root)
{
        if (root == NULL)
                return 0;
        if (root->_left == NULL && root->_right == NULL)
        {
                return 1;
        }
        return BinaryTreeLeafSize(root->_left) + BinaryTreeLeafSize(root->_right);
}
```
<div align=center>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(33).5z4b45ssy280.webp"  width="100%"/>
</div>

#### 5.3 二叉树查找值为x的节点
```
BTNode* BinaryTreeFind(BTNode* root, BTDataType x)
{
        if (root == NULL)
        {
                return NULL;
        }
        if (x == root->data)
        {
                printf("已找到数值为%c的节点", x);
                return root;
        }
        BTNode* leftRet = BinaryTreeFind(root->_left, x);
        if (leftRet)
        {
                return leftRet;
        }
        BTNode* rightRet = BinaryTreeFind(root->_right, x);
        if (rightRet)
        {
                return rightRet;
        }
        return NULL;
}
```
<div align=center>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(34).513bg8t4lwg0.webp"  width="100%"/>
</div>
在二叉树中，对左右孩子的判断要紧接着递归结束就判断。若等左右递归完一起判断，有较大可能出错。

一个错误代码，下面的代码，只要是查找的数在左子树就能正确找到，右子树也会找到，但是会返回NULL。函数最后结束值不同。
```
BTNode* BinaryTreeFind(BTNode* root, BTDataType x)
{
        if (root == NULL)
        {
                return NULL;
        }
        if (x == root->data)
        {
                printf("已找到数值为%c的节点", x);
                return root;
        }
        BinaryTreeFind(root->_left, x);
        BinaryTreeFind(root->_right, x);
}
```
#### 5.4 二叉树第K层节点个数
```
int BinaryTreeLevelKSize(BTNode* root, int k)
{
        if (root == NULL)
        {
                return 0;
        }
        if (k == 1 )
        {
                return 1;
        }
        return BinaryTreeLevelKSize(root->_left, k - 1) + BinaryTreeLevelKSize(root->_right, k - 1);
}
```
<div align=center>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(35).76xstjqy2s80.webp"  width="90%"/>
</div>