---
title: 长短期记忆网络（LSTM）
date: 2022-09-06 09:25:00
author: XueYisheng
img: https://cdn.staticaly.com/gh/xys176/image-hosting@master/image.5bgoyw79ji80.webp
top: true
hide: false
cover: true
coverImg: https://cdn.staticaly.com/gh/xys176/image-hosting@master/image.5bgoyw79ji80.webp
password: 8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
toc: false
mathjax: false
summary: 长短期记忆网络（LSTM，Long Short-Term Memory）是一种时间循环神经网络，是为了解决一般的RNN（循环神经网络）存在的长期依赖问题而专门设计出来的，所有的RNN都具有一种重复神经网络模块的链式形式。
categories: 人工智能
tags:
  - Markdown
  - 神经网络
---
# 长短期记忆-LSTM


## 简介
时间的长短期预测，包括股票预测，气象预测语音识别等。这个时候传统的循环神经网络RNN就捉襟见肘。它虽然建立了不同时刻隐藏层之间的关系。实现了记忆的效果，但只是基于前一时刻。
- RNN是一种短时记忆。
- RNN是想把所有的信息都记住，无论是有用还是没用的信息。不具备筛选的功能。
<div align=center>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(7).cmtksvb31gg.webp"  width="50%"/>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(8).ju9vfra8u80.webp" width="50%"/> 
</div>  

## RNN传统循环神经网络模型  
左边红球是不同时间的输入x,中间蓝色是隐藏状态s，右边绿球是网络输出y。在LSTM中增加新的时间线（粉色），同时增加与隐藏状态的联系。
因此，相比较RNN，在STLM中，计算当前时刻t的隐藏状态时，就需要输入x(t)，前一时刻s（t-1)，还需要包含当前时刻的信息c(t)。这就是相当于一个日记本（记忆细胞），记录当前时刻的信息。
<div align=center>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(9).6kiyvgziryo.webp"  width="50%"/>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(10).2g03g19mq0w0.webp" width="50%"/> 
</div> 
对右上图转换，s(t)与c(t)之间的联系关系被拆分成如下的f1,f2,与c(t)指向s(t)线，一共三条联系线。 <br>  

- f1被称作遗忘门，起到删除功能。它根据昨天记忆s(t-1)和今天输入x(t)，决定来修改删除之前记录c(t-1)。数学表示如下图。其中sigmoid函数取值0到1之间，矩阵元素向乘，会抹掉为0的项，相当于选择性遗忘部分信息。<br>
- f2被称作选择门，其增加选择功能。其中sigmoid函数对信息进行选择，tanh函数取值-1到1之间，起到对数据整理加归纳.<br>
- 因此，得到c（t）=f1*c(t-1)+f2。这个得到的c(t)不仅会继续向下传递，同时还会来更新当前短期记忆s(t)，即第三条关联线。
<div align=center>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(11).5z5rn8f9ejs.webp"  width="30%"/>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(13).cb3raezz27k.webp" width="30%"/> 
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(12).65waw4lqhec0.webp" width="30%"/> 
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(16).2yk69gynmxa0.webp" width="40%"/> 
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(14).41bi9k8jv2g0.webp" width="40%"/> 
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(17).6ejn8w2i9yk0.webp" width="40%"/> 
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(18).678cphnkm7s0.webp" width="40%"/> 
</div>
经过以上操作，就可得到输出y（t）,同时保持并得到短期记忆链s与长期记忆链c。并且相互更新。  

## 传统LSTM向前传播过程
详细讲解LSTM中具体的细节实现。LSTM的详细传递模型图。
每一个绿色矩形中，都被成为一个记忆细胞。
<div align=center>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image.5bgoyw79ji80.webp" width="80%"/> 
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(19).1gehkqruadi8.webp" width="30%"/>   
</div>

- σ就是sigmoid函数,也被称作门，取值在0到1之间。
- 下图中的g(t)就是c(t)。
- 得到c(t)之后，h(t)由c(t)向下经过tanh函数门，再与o(t)想乘。o(t)与f(t)相同，都是遗忘门。
- h(t)即使当前输出状态（紫色的可直接输出），也是长时记忆链的当前状态。并持续向下传播。
- y(t)就是输出，对应需要的格式。可灵活多变。
<div align=center>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(20).2hkik6yigly0.webp" width="80%"/>   
</div>

## LSTM的变体
### 1. 长时记忆影响
增加前一时刻长时记忆的影响，在遗忘门之前得到前一时刻的长期记忆c(t)。
<div align=center>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(21).2dkydrfawlxc.webp" width="80%"/>   
</div>

### 2. 耦合遗忘门和输入门
这种情况下，只有遗忘了旧的信息，才会添加新的信息。“1”减去矩阵中所要遗忘的，矩阵为1的项，减完后为0，进入更新门，此时需要遗忘部分为0，矩阵想乘时，就会丢弃掉这部分数据。（1-f(t))代表更新的结果，再加遗忘门数据。得到长时记忆输出C(T)。
<div align=center>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(22).70n8gfo01ww0.webp" width="80%"/>   
</div>

### 3. 组合为更新门且合并长时记忆
整合长时和短期记忆，全部都需要依赖前一时刻的短期记忆。
<div align=center>
<img  src="https://cdn.staticaly.com/gh/xys176/image-hosting@master/image-(24).6n994o3w2qk0.webp" width="80%"/>   
</div>

---
参考：   
https://www.bilibili.com/video/BV1qM4y1M7Nv?spm_id_from=333.337.search-card.all.click   
https://www.bilibili.com/video/BV1Z34y1k7mc?spm_id_from=333.337.search-card.all.click   
http://colah.github.io/posts/2015-08-Understanding-LSTMs/


___

