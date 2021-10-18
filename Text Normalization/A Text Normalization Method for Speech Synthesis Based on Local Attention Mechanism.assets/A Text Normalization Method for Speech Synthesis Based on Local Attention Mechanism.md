# A Text Normalization Method for Speech Synthesis Based on Local Attention Mechanism

## 论文摘要：

文章主要提出了一种基于RNN和local attention机制的神经网络来解决语音生成当中的文本正则化的问题。**自回归网络的使用可以帮助模型参考文本的上下文信息，Local Attention机制可以帮助缩小模型的规模，且在文本正则化的场景中，判定一段特定文本属于哪一类的正则标准，的确不需要全局的取观察上下文，往往需要根据距离较近的上下文来做判断**。文章主要对比了使用Local Attention、 Attention以及不用Attention三种情况下的模型效果。



## 模型结构

传统的Seq2Seq模型，Encoder部分使用双向GNU，Decoder使用单向GNU，中间加Local Attention模型。**输入是序列编码，输出是对应的正则化后的结果。**不清楚这样做效果是否真的好，感觉可以借鉴这篇文章中的local attention的机制。

![截屏2021-10-12 下午4.28.19](A Text Normalization Method for Speech Synthesis Based on Local Attention Mechanism.assets/截屏2021-10-12 下午4.28.19.png)

### 总结

Decoder用的是Teacher Forcing，这个机制感觉在做生成模型时会出现难以训练的问题，可能出现预测时超长的问题。感觉不能直接用生成模型去做，应该将文本正则化的问题归类为分类模型，将不同的正则化规则分为有歧义的和没有歧义的两类，没有歧义的可以直接进行转化，有歧义的部分扔进模型做判断。最后根据判断结果，检查该部分是否符合该规则，比如说监测到“2020年”，模型输出认为应该逐字转换，首先判断2020是否符合逐字转换的条件（d+），最后再做转换。



