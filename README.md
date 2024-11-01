## 重磅发布：基于22GB超大规模语料的RIME中文语言模型与词库构建

### 项目简介
  在庞大且多样的中文语料库基础上，我们构建了一个性能优异、覆盖面广的中文语言模型和高效的词库。此次发布的语言模型和词库构建，融合了来自知乎问答、微博、百度百科、维基百科、新闻报道、酒店外卖评论、法律文献、地区描述、文学作品以及诗词等多领域的内容，总体语料规模高达22GB。该项目不仅为中文自然语言处理提供了丰富的语料支持，更是通过精准的词频统计、分词策略以及多层次剪枝技术打造了一个能够满足高效、精确使用需求的模型；
  同时项目中维护的单字拼音词典涵盖cjk基本区到扩展G区以及康熙部首区，基于汉典基础上手动维护更多读音，可能是单文本词库中比较全面的；
  项目中的rime词库是全部带声调的，所有的词频是基于词组和拼音双键统计的，区别了如："那里 哪里" 这种类似场景的词频，同时单字词频也是在词组语句中加上拼音最后拆解为单字及其对应拼音的组合，因此单字词频也是区分多音字的 迁移到你的方案：[点击迁移](https://github.com/amzxyz/rime_grammar_model_dicts/wiki/%E5%B0%86%E9%A3%9E%E5%A3%B0%E8%AF%8D%E5%BA%93%E7%94%A8%E4%BA%8E%E4%BD%A0%E7%9A%84%E9%A1%B9%E7%9B%AE)

[使用及构建教程详见：](https://github.com/amzxyz/rime-build-grammar-word-frequency/wiki/%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B%EF%BC%9ARime-%E8%BE%93%E5%85%A5%E6%B3%95%E8%AF%AD%E8%A8%80%E6%A8%A1%E5%9E%8B%E6%9E%84%E5%BB%BA%E5%85%A8%E6%B5%81%E7%A8%8B)

[模型及词库下载地址：](https://pan.baidu.com/s/1IjQpF80htJYwOnT9KNgHUg?pwd=rime)

文件版本对应说明：v是版本号，n是模型级别，m是百兆尺寸
|文件大小|2级模型|3级模型|
|------|------|------|
|100M|v1n2m1|v1n3m1|
|300M|v1n2m3|v1n3m3|
|500M|v1n2m5|v1n3m5|

数据来源与语料构建
我们从多个数据源精心采集了22GB的中文文本语料库，包括但不限于：

**知乎问答：** 包含用户生成的问答内容，涵盖生活、科技、历史等各类话题。

**微博：** 收集了微博社交平台的热议话题、流行语等，呈现出丰富的社交网络语言特色。

**百度百科 & 维基百科：** 提供中文百科类权威内容，提升模型对知识性和专业性词汇的覆盖。

**新闻报道：** 涵盖财经、时政、体育等多领域新闻资讯，强化模型对新闻文本的语境理解。

**酒店外卖评论：** 收集来自日常点评的真实用户评论，增加模型对日常用语的敏感度。

**法律文献：** 包含法规条文、判例等，增强模型的法律相关语料理解。

**文学作品：** 汇集了诗词、散文、小说等文学文本，提升模型在文学表达方面的表现力。

这套多样化的语料库，不仅覆盖广泛，还具有高质量、丰富的上下文内容，为模型在不同语境中的表现提供了强有力的支撑。

### 模型构建与技术优势
1. 多级 n-gram 语言模型
在大规模数据的支持下，我们采用了 n-gram 模型进行多级语言建模。具体包括了 unigram（单字模型）、bigram（双字模型）、trigram（三字模型）以及更高级的四字模型。这种分级的 n-gram 设计让模型可以灵活地应用于短语和句子的预测与生成中，实现了以下几项关键优势：

短语预测：通过 n-gram 模型，可以根据前后字词来预测下一字词，更适合中文输入法的联想功能。

多音字消歧：加入了拼音标注，特别适用于多音字的处理，使模型能准确识别并输出正确的词汇。

语境感知：通过 n-gram 的上下文设计，模型能够在具体语境下生成更加自然、连贯的句子。

2. 分词与词频加权
为了提高模型的效率和准确性，我们对语料库进行了精细的分词处理与词频加权操作：

使用结巴分词的搜索模式分词，广泛捕捉词汇组合，最大化词汇多样性。

采用了 TF-IDF 加权算法 对词频进行了加权，使模型能够在生成过程中更偏向高权重词汇。

剪枝操作去除了低频词汇，减少噪声，提高词库效率，构建了更为高效、实用的语言模型。

3. 自定义词库
基于22GB语料的丰富内容，我们构建了大规模的自定义词库，涵盖了文学、法律、百科等领域的专用词汇。这一词库在中文拼音输入、联想和短语识别等应用场景中表现优异，提供了以下优势：

广泛词汇覆盖：词库涵盖了从流行网络用语到专业法律术语的广泛词汇，使得模型在日常和专业使用场景中都能表现出色。

多音字支持：单字和多字词频中均加入拼音标注，通过词+拼音的双键统计方法，准确处理多音字，避免词意歧义。

多级词库优化：词库按照单字和多字分别统计、构建，同时分为大字集和小字集，满足不同场景下对词库大小和性能的需求。

性能与应用场景

得益于22GB的多源数据和优化算法，使得rime在整句和词语提升巨大，大大提高了中文输入效率。
