---
title: Transformer模型
date: 2022-09-07 09:51:00
author: XueYisheng
img: https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(6).15298dmharts.webp
top: false
hide: false
cover: true
coverImg: https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(6).15298dmharts.webp
password: 8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
toc: false
mathjax: false
summary: Attention is all you need，提出了解决sequence to sequence问题的transformer模型，该文章使用全Attention的结构代替了LSTM，抛弃了之前传统的encoder-decoder模型必须结合CNN或者RNN的固有模式。
categories: 人工智能
tags:
  - 神经网络
---
## 输入部分
### 1. Embedding
输入可以按字切分，对于翻译而言，可以把字切分成字向量。 
### 2. 位置嵌入
RNN在处理翻译时，是一个一个输入，前一个处理结束后才进行下一个的处理，具备先后时序关系。而RTN是一起处理的，这就导致RTN处理前需要位置编码，告知处理或翻译中字的先后关系。举个例子，若没有位置编码，无法保证在“我爱你”翻译过程中，“我”在“你”的前面。
- 位置编码公式如下：
![公式](https://cdn.staticaly.com/gh/xys176/image-hosting@master/image.1nr5qo7msdb4.webp) 
- 2i即偶数位，2i+1即奇数位。
![示例图](https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(1).2705d9v11cu8.webp)
## 注意力机制
注意力机制Attention就是权重。
### 1. Encoder-Decoder模型
Encoder-Decoder模型就是RNN模型的变体。把整体对一句话编码，再进行机器翻译，这种无论输入多长，一起翻译的模型，导致翻译精度下降。
![RNN模型](https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(2).73yo6kne9mk0.webp)
### 2. Attention模型
Attention机制通过每个时间输入不同的C，来解决眉毛胡子一把抓的问题。其中α表明了在t时刻所有输入的权重。当前时刻以C1的视角往下看，就是每个输入不同输入的注意力（Attention分布）。经过神经网络数据训练，就可以得到最好的Attention权重矩阵。
![Attention模型](https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(3).4r8uil0s2ro0.webp)
### 3. Self-Attention
因为在Attention机制中已经是完成对所有的输入全局评判，因此对于输入顺序已经不重要。比如在一句话的翻译中，Attention机制会计算每个单词与其他单词之间的关联。利用这些权重加权表示，再放到神经网络中，就很好的得到了上下文的信息。
![Self-Attention](https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(4).41ueuk04f3q0.webp)
<br>把每个信息之间的联系多处理几次，得到的权重再次进行处理。得到的就是Self-Attention机制。   
![多重联系](https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(5).1hjqt24186m8.webp)
<br>总结下来，Attention机制有三大优点。
1. 参数更少。
2. 速度更快。
3. 效果更好。想·

核心思想就是通过加权求和，本质就是在不同的上下文中，专注不同的信息，因此无论是NLP，图像还是搜索，预测。使用Attention都有好的处理结果。

![应用图](https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(6).15298dmharts.webp)

## 解码编码 



___

