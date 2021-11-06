# Tricks - 文本分类

---



- 数据预处理vocab的选取(前N个高频词或者过滤掉出现次数小于3的词等等)
- 词向量的选择，可以使用与训练好的词向量如谷歌，Facebook开源出来的，当训练集比较大的时候也可以进行微调或者随机初始化与训练同时进行，训练集较小就无需微调。
- 结合要使用的模型，可以把数据处理成char，word或者都用
- 有时将**词性标注信息**也加入到训练数据会受到比较好的效果
- 关于PAD(不同长度序列补全)，取均值或者一个稍微比较大的数，别取最大值那种。
- 神经网络结构上加上dropout和BN可能会好点，RNN based model(LSTM,GRU等，使用**双向结构**)，embedding后使用dropout。
- 显然问题fasttext,简单问题CNN，复杂问题RNN，终极问题bert。
- ensemble
- 文本做数据增强(EDA，同义词替换),对文本进行随机的shuffle和drop等操作增加数据量。

### 深度学习中的一些trick(主要针对论文和比赛)

- embedding是否参与训练（实际中基本对半）
- BN和Dropout，以及他们的相对位置。
- meta-feature的使用，比如词性，情感，还有各种语言学特征和元信息等等
- 用CNN的话，用空洞版本(空洞卷积),窗口搞大，基本稳定超过3,4,5的conv1D
- 数据增强，drop。shuffle。replace。近义词，扩充，截取。
- 循环学习率(base max step调好能巨大加速收敛速度)
- char/subword level的使用
- 词元化，词干化
- 不均衡下的采样，梯度收缩，focal loss
- 伪标签，半监督
- 去停用词，标点保留还是去掉
- 过拟合后冻层finetune
- 长短文本有其适应的模型
- 多embedding concat,mean，
- vocab的数量，是否统一替换或者过滤低频词。
- 网络增加冗余的激活然后concat。
- **Maxlen覆盖百分之99就可以，不需要最大**，换随机种子(玄学)















## Reference

[文本分类有哪些论文中很少提及却对性能有重要影响的tricks？](<https://mp.weixin.qq.com/s?__biz=MzIwNzc2NTk0NQ==&mid=2247485033&idx=1&sn=1f43019d702607d7dfc47ddfc7f84090&chksm=970c2ebfa07ba7a948965596237d2d6cce3447c71233dc74f0c17de7a38e198b9c2092793ded&scene=21#wechat_redirect>)

