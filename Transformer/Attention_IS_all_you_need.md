# Attention is all you need
## Paper Reading

### 1. 标题+作者
<img src="./picture/transformer_1.png" width="400px" alt="Transformer Model Architecture - Part 1"/>
<img src="./picture/transformer_2.png" width="400px" alt="Transformer Model Architecture - Part 2"/>

- **Ashish Vaswani**
- **Noam Shazeer**
- **Niki Parmar**
- **Jakob Uszkoreit**
- **Llion Jones**
- **Aidan N. Gomez**
- **Łukasz Kaiser**
- **Illia Polosukhin**

> *注意：8位作者按照贡献大小随机排序，不存在"第一作者"的概念。*

### 2. 摘要
<img src="./picture/transformer_3.png" width="400px" alt="Abstract"/>

- 名字是transformer，还好这个名字出名了，不然大家搜出来都是变形金刚。然后Alexnet其实论文是没有名字的，但是由于太出名了，大家把第一作者的名字拿出来叫Alex.
这个论文就是只使用了attention mechanisms，去掉了Recurrence 和卷积。
- 主要是用于机器翻译上，所以下面都是关于机器翻译的内容。BLEU是专门用于评估机器翻译的指标。

### 3. 结论
<img src="./picture/transformer_4.png" width="400px" alt="Conclusion"/>

*作者提出了一个基于纯粹注意力机制的模型，摒弃了RNN和卷积网络的需求。*

### 4. 导言
<img src="./picture/transformer_5.png" width="400px" alt="Introduction"/>

- 第一段：机器学习的相关研究，有LSTM，GRU，他们都使用了encoder-decoder的结构。


- 第二段：是讲了RNN的缺点，RNN主要有两个缺点。
1.会丢失前面的信息，没有长期依赖。
2.计算得要前面计算好了作为输入，所以很慢，不能并行
虽然目前有很多论文有改善，比如中间层变的很大，但是占用的内存也会更多。

- 第三段就是引入了attention机构，去掉了Rnn和卷积。

### 5. 相关工作


- 第一段：
卷积比较难对比较远的地方进行建模，卷积每次都是看一个比较小的窗口，比如3x3。如果两个像素隔得比较远的话，就需要用很多卷积，一层一层的上去，最后把隔的远的像素融合起来。如果使用transformer的注意力机制的话，每次可以看到所有的像素。一层就能把所有的序列看到。卷积比较好的地方是可以做多个输出通道，一个输出通道可以去识别不一样的模式。所以他也想要这样的输出效果，而提出了multi-head attention来模拟卷积审神经网络多输出通道的一个效果

- 第二段：自主意机制，这个也不是作者提出来的，以前就有了。

### 6. 模型
<img src="./picture/transformer_7.png" width="400px" alt="Model Overview"/>

- 第一段：
现在翻译比较好的模型都是一个encoder-decoder的结构。然后它解释了什么是一个编码器解码器。
x表示你的词语，z表示x这个词语的向量表示，这就是你的编码器的输出，将原始的输入变成机器学习可以理解的一个向量。
对解码器来讲，我会拿到编码器的输出，然后会生成一个长为m的序列y，n和m不一样，因为翻译的输出有可能不相等。他和编码器的最大的不一样的地方，他的词是一个词一个词的生成的，因为对于编码器来讲，很有可能一次性看完所有的句子。比如做翻译的时候，把所有的英语句子给你，解码的时候只能一个一个生成，这个东西叫auto-regressive.输入又是你的输出。过去的输出，又是你的输入。

<img src="./picture/transformer_7.png" width="400px" alt="Transformer Model"/>
*Transformer模型结构图解*

- 这个图基本上就是transformer的图，但是这个图直接看应该看不懂，很难。


如果是中文翻英文的话，inputs就是中文的句子，解码器在做预测的时候是没有输入的，output一个一个往后移。

Nx就是核心的block，也是一个transformer block。具体进去看的话有一个multi-head attentation,再加上一个MLP，中间有一些残差连接。
encoder的输出也就输入到了decoder，在中间，这个很有意思。
多了一个masked multi-head attention.

首先他介绍了encoder。
完全一样的层，有6个，每个layer里面都有一个子层，
simple就是一个MLP, 每个子层都用了残差连接。最后在使用了一个layernorm。因为残差连接的输入和输出必须是同样的大小，如果不一样就要投影，为了简单起见，每一个层的输出的维度变成512。这和CNN不一样，维度减少，channel往上拉。这个模型也是比较简单的。调参数也是比较简单的，也就N和维度可以调整的。gpt和bert也就这两个可以调整。能够花几句话讲清楚是不错的。

- 为什么不使用batch norm

<img src="./picture/transformer_8.png" width="400px" alt="Layer vs. Batch Normalization"/>
- 算均值和方差上面。
batchnorm是对全局来算。
Layer norm是在每个feature上进行算。所以波动没有那么大。

后来有人来解释是由于梯度。

### 7. 实验
*内容待补充*

### 8. 评论
*内容待补充*

---

