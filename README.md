# benruonewsCorpus

lastUpdate: 2022-09-26

本若简报是一个通过每天（自2019年3月12日开始）收集、整理和发布积累的中文短新闻数据集。

## 数据文件解释

### news.csv

主要的原始数据集（从数据库导出到csv格式），后续会不定期同步和更新，此次同步到2022年9月26日，一共24177条，其字段意义解释如下：

- id: 短新闻唯一ID
- publish_date：在微信公众号“本若简闻”发布的日期
- power：每日的短新闻排序，中、后期才增加的字段，目前在NLP应用中无用
- content：短新闻内容，目前主要是在阅读source处新闻后人工摘要形成
- source：短新闻来源链接，可以有多条
- last_update：短新闻收集整理的具体时间

### questions.csv

针对2021年8月底的news.csv，人工整理的654个问题，目前暂时没有后续更新计划，其字段意义解释如下：

- id：问题唯一ID
- questions：问题的内容
- length：问题的内容长度

### qa_pairs.csv

针对2021年8月底的news.csv和对应的questions.csv，通过ElasticSearch的协助，半自动版半人工的生成的20940条问题答案对（即模型监督学习使用的样本），其字段意义解释如下：

- id：样本的唯一ID
- q_id：原问题所在questions.csv的ID
- q_content：原问题的内容
- a_score：ElasticSearch的打分
- a_id：答案所在news.csv中的ID
- match：样本的label，第一轮通过ElastcSearch标记，第二轮人工校正标记
- a_content：答案的内容，可能是news.csv的整条新闻，也有可能是news.csv中某条新闻中的一段
- a_publish_date：答案原新闻的发布时间

## 应用方向简介

本数据集主要用于NLP模型的研究、探索和训练，目前已知的可应用方向有：

### 1. 问答

即通过问一个文本问题，训练一个模型，使用此数据集相关短新闻按顺序回答出来。此方向可以直接使用qa_pairs.csv作为样本进行有监督学习。

### 2. 摘要

即通过爬取source字段指定的新闻内容和数据集的content字段，形成文本生成方向的标签样本数据，用于训练文本生成模型。此方向需要爬虫获取source字段指定的新闻文本内容。

## 其他

目前数据集主要靠我业余人力维护，目前还比较简陋，请见谅。

最后，如果大家有其他方向获取和其他问题，可以联系我：guxiaoqun@aliyun.com。
