# NLTK:NLP 中的安装、环境和应用程序

> 原文：<https://blog.quantinsti.com/nltk/>

由纳曼·斯旺卡

在本文中，我们将研究 NLTK 的一些最广泛使用的特性，并在构建情感分析模型时使用它们。处理自然语言数据是基于新闻的自动交易系统的核心，因此从算法交易员的角度来看，这是一项令人兴奋的技能。

我们建议您温习一下 Python 技能，以便从本文中获得最大收益。您可以阅读我们以前的一些文章，如 [Python for trading](/python-trading/) 、 [Python libraries](/python-trading-library/) 或查看我们的 [Python for trading](https://quantra.quantinsti.com/course/python-for-trading) 课程，通过交互式编码练习以结构化的方式进行学习。

以下是我们将涉及的主题:

*   [如何安装 NLTK](#how-to-install-nltk)
*   [NLTK 文集](#nltk-corpus)
*   [NLTK VADER 情绪分析](#nltk-vader-sentiment-analysis)
*   [NLTK 记号赋予器](#nltk-tokenizers)
*   [NLTK 停用词](#nltk-stopwords)
*   [NLTK 词干分析器](#nltk-stemmers)
*   [列车情绪分析模型](#train-sentiment-analysis-model)

NLTK 是自然语言工具包的首字母缩写，由宾夕法尼亚大学的研究人员开发，试图支持他们在 2001 年对 NLP 的研究。从那时起，NLTK 已经被全球的研究者和 NLP 实践者广泛采用。这是一个用 Python 编写的开源库，有大型社区支持。NLTK 的开发者声称它提供了 50 多种易于使用的资源接口，涵盖了你在语言处理方面的所有需求。

## 如何安装 NLTK

可以使用 pip 包安装程序来安装 NLTK。最近 NLTK 已经[放弃了对 Python 2 的支持](https://twitter.com/NLTK_org/status/1249489353950121984),所以请确保您运行的是 Python 3.5 及更高版本。检查 Python 的安装版本，并通过运行下面提供的代码安装 NLTK。