# 词向量 - FastText

---

fastText是一款文本分类与向量化工具，是一个轻量级库，允许用户据学习文本表示和文本分类器，可在标准通用硬件上运行，之后可以缩小模型大小，部署在适合的移动设备。

fastText最惊艳的地方在于，和最前沿深度神经网络模型相比，它在分类精度等指标毫不逊色的情况下， 把训练和推断速度降低了几个数量级。

fastText能够做到效果好，速度快，主要依靠两个秘密武器：

- 一是利用了词内的n-gram信息(subword n-gram information)，
- 二是用到了层次化Softmax回归(Hierarchical Softmax)的训练trick。

### Subword n-gram Information(词内n-gram信息)

之前的文本向量化工作都是以词汇表中的独立单词作为基本单元进行训练学习的，会有如下问题

- 低频词、罕见词，由于在语料中本身出现的次数就少，得不到足够的训练，效果不佳；
- 未登录词，如果出现了一些在词典中都没有出现过的词，或者带有某些拼写错误的词，传统模型更加无能为力。

fastText引入了**subword n-gram**的概念来解决词形变化**(morphology)**的问题。直观上，它将一个单词打散到字符级别，并且利用字符级别的n-gram信息来捕捉字符间的顺序关系，希望能够以此丰富单词内部更细微的语义。

在训练过程中，每个n-gram都会对应一个向量，而原来完整单词的词向量就由它对应的所有n-gram的向量求和得到。所有的单词向量以及字符级别的n-gram向量会同时相加求平均作为模型的输入。

从实验效果来看，subword n-gram信息的加入，不但解决了低频词未登录词的表达的问题，而且对于最终任务精度一般会有几个百分点的提升。唯一的问题就是由于需要估计的参数多，模型可能会比较膨胀。不过，Facebook也提供了几点压缩模型的建议：

- 采用hash-trick。由于n-gram原始的空间太大，可以用某种hash函数将其映射到固定大小的buckets中去，从而实现内存可控；
-  采用quantize命令，对生成的模型进行参数量化和压缩；
-  减小最终向量的维度。

### Hierarchical Softmax(层次Softmax)

层次化的Softmax的思想实质上是将一个全局多分类的问题，转化成为了若干个二元分类问题，从而将计算复杂度从O(V)降到O(logV)。

每个二元分类问题，由一个基本的逻辑回归单元来实现。如下图所示，从根结点开始，每个中间结点（标记成灰色）都是一个逻辑回归单元，根据它的输出来选择下一步是向左走还是向右走。下图示例中实际上走了一条“左-左-右”的路线，从而找到单词w₂。而最终输出单词w₂的概率，等于中间若干逻辑回归单元输出概率的连乘积。![img](https://image.jiqizhixin.com/uploads/editor/74faf283-7abb-4a5b-851d-a27502d031cc/%E9%BB%844.png)