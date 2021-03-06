# PyTorch-Bert-BiLSTM-ATT-LJP
PyTorch Bert BiLSTM ATT LJP

# 观点

- 使用的是 huggingface/pytorch-pretrained-BERT 的pytorch版本，Bert中文开源模型也是采用的huggingface转换过的。

- 目前训练好的中文bert模型是基于字的，没有基于词的，训练语料不明确，分词方法是在每个汉字前后加载空格。

- 法律文本属于长文本，这对使用bert有很大的限制，bert模型对最大长度的限制为512，还是加上[CLS] [SEP]两个字符，对法律文本来说，这个长度不切实际。伴随长度的增加，显存等也不足够，只能减小batch，切割长句子，再进行还原。

- 法律文本数据量很大，利用bert模型抽取字的表示的话需要近10G甚至上百G的存储空间，这对内存，存储空间，效率等都是考验。

- 我目前尝试了两种bert作为预训练的做法。

- 第一种是抽取句子表示，bert模型虽然是基于字的，但是在获取字的表示之后可能采用pooling的方式获取句子的表示，这样的简单测试得到的bert特征文件并不是很大，差不多几百兆，然后把抽取出来的特征与BiLSTM之后pooling之后的结果拼接在一起，性能堪忧。

- 第二种就是获取bert原始的字的表示，虽然在我写的脚本速度上面做了优化，但是抽取出来的特征文件上百G，对内存是极大的考验。对于硬件的限制，只能把bert模型嵌入到代码中，即用即抽取bert字的表示，速度很慢，显存占用也不小。通过抽取字的表示，然后过BiLSTM和pooling，与原来BiLSTM基于词的baseline模型拼接，目前来看，速度巨慢，性能也不是很好。

- 还在尝试中，有很多的问题假设。
	- 中文bert模型的训练语料是什么
	- 基于字的bert模型是不是有某些限制
	- 能不能训练法律领域的bert模型
	- 对bert模型进行fine-tune会不会有更好的效果。


