# 命名实体识别是什么

**命名实体识别（Named Entity Recoginition, NER）**旨在将一串文本中的实体识别出来，并标注出它所指代的类型，比如人名、地名等等。具体地，根据MUC会议规定，命名实体识别任务包括三个子任务：

- 实体名：人名、地名、机构名等
- 时间表达式：日期、时间、持续时间等
- 数字表达式：百分比、度量衡、钱、基数等

我们来看这句话，**百度于2021年3月23日正式回香港上市**，这句话中"百度"是个机构名，"香港"是个地名，"2021年3月23日"是个日期，命名实体识别任务能够通过建模的方式来帮助我们自动地发现这些实体。

命名实体识别是一项比较关键的NLP任务，具有广泛的**应用场景**，例如在对话意图理解（NLU）中，通过提取出相应的实体词，能够帮助系统更加准确地理解用户的需求，比如根据用户的问题提取出"天气"，"北京"，"今天"这样的词汇，大概率就能知道用户在问些什么；在微博场景中，应用命名实体识别提取出微博短文中重要的实体词，也有利于微博信息的汇总，或者事件热度的统计。

NER任务一般会被建模成序列标注任务，也就是说，模型的输入是待识别的一串文本序列，模型的输出就是该文本序列对应的标签序列，不同于文本分类任务，这是一种序列到序列的任务。我们来举个例子： 

| 姚       | 明       | 担   | 任   | 中             | 国             | 篮             | 协             | 主   | 席   |
| -------- | -------- | ---- | ---- | -------------- | -------------- | -------------- | -------------- | ---- | ---- |
| B-Person | I-Person | O    | O    | B-Organization | I-Organization | I-Organization | I-Organization | O    | O    |

这句话中的每个字分别对应着一个标签， 模型的输入就是上边的文本，模型的输出就是下面的标签序列，我们通过这样的标签序列就能识别出原始文本中的实体。 
具体地，上边这串文本中，"姚明"对应着Person实体，其中"姚"字是"Person"实体的起始字，所以设置标签为"B-person"，其中标签前边的B代表Begin这个单词；"明"字是"Person"实体的中间字，所以设置标签为"I-Person"，其中标签前边的I代表Intermediate这个单词。 "中国篮协"对应这Organization实体，相应标签"B-Organization"和"I-Organization"的解读和Person实体是一致的。最后的标签"O"代表"other"，表示其他实体类型的标签。

看到这里，相信你已经知道，本节的NER任务要建模完成一件什么事情了，即建模一个序列到序列的模型来找出文本中蕴含的实体。