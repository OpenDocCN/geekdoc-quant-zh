# Yves Hilpisch 博士在 Oanda 平台上的自动交易

> 原文：<https://blog.quantinsti.com/automated-trading-oanda-yves-hilpisch/>

伊夫·希尔皮施博士

Python 已经成为算法交易中最受欢迎的编程语言之一，因为它易于安装，免费使用，结构简单，并且有多种模块可用。在全球范围内，Quant 的 Algo 交易员和研究人员正在广泛使用 Python 进行原型开发、回溯测试、构建其专有的风险和订单管理系统，以及优化测试模块。

这篇博客文章强调了使用 Python 作为编程语言的算法交易的一些关键步骤。截图摘自 Yves Hilpisch 博士与 QuantInsti 合作举办的[网络研讨会。Hilpisch 博士是 Python 领域世界知名的权威，也是 Python Quants GmbH 的创始人，他有几本关于这个主题的书。他还在 QuantInsti 任教，quantin STI 是亚洲算法交易的先驱教育培训公司之一。](https://blog.quantinsti.com/automated-trading-with-python-webinar/)

所有显示的例子都是基于 [Oanda](http://oanda.com) 的平台和 API。关于 Python 和使用的库的背景信息可以在 O'Reilly 的书 Hilpisch，Yves(2014):《Python for Finance——分析大金融数据》中找到。本帖分为两部分。这篇文章强调了使用 python 连接 Oanda 平台和回溯测试交易策略的基础知识。下一篇文章将讨论如何处理流数据以及实时自动交易。

#### **主题**

*   连接到 Oanda 平台
*   数据检索
*   对交易策略进行编码和回溯测试

## **连接到 Oanda 平台**

没有数据，就没有回溯测试，也就没有明智的交易策略。对于有 python 经验的人来说，第一步是导入像 numpy 和 pandas 这样的库。但是，由于 Oanda 使用的是这个平台，我们还会导入一些特殊的平台，比如 oandapy。

自然，需要导入 Oanda 凭证。如果文件存储在磁盘上，则导入凭证的简单 python 程序如下所示。它将打入你的帐户 id 和令牌。一旦凭证准备就绪，就用一个 API 对象连接到 oanda。

![Importing Oanda API credentials](img/e3a8a316b1a741c09c6124fab30fec2c.png)

![2](img/5595ba9daee2f2a49751f2d4af0eb56b.png) ![3](img/c851c84bb675e1d8c64213783aefc4be.png)

由于 Oanda 有免费的 和全功能的练习账户，所以有很多用途，也很受欢迎。

有多种工具可以使用 Oanda 中创建的 API 对象进行检索，就像平台上交易的所有工具一样，例如 SPX 500、S & P 500 以及商品和货币对。

![available instruments in ooanda](img/41040b7d394070de6b50a54091136e62.png)

## **数据检索**

可以通过检索数据

*   定义开始和结束日期(范围)和
*   固定粒度(时间间隙)。
*   选择需要获取历史数据的仪器。

在下面的示例中，开始日期为 2016 年 2 月 3 日 日 日，结束日期为 2016 年 2 月 4 日日。粒度设置为“D ”,表示全天的数据。DE30_EUR 表示德国 DAX 交易所。

![data retrieval](img/fd0893c9c482574f7ab2f82bb79a2353.png)

运行这段代码会抛出一个 json 对象，如下所示

![6](img/70b816e87344f1162ac47048e4d178ef.png)

然而，对于回溯测试，我们需要更多这样的数据。因此，粒度被更改为一分钟，这给了我们更多的清晰度。需要创建一个**日期时间索引对象**。

![datetimeindex object](img/3ad81c93dd9a35db6e4a114a7bf2b794.png)

为了存储这些数据，我们打开了 HDFStore，它提供了简单、方便的数据存储。

![hdf store](img/2cddb54368677c5bf5702f4d0d3871b5.png)

一般来说，数据被保存在磁盘上以便于检索。需要注意的重要一点是，数据是分块检索的，因此必须追加到数据框对象中。请注意，granuality 设置为 M1，这意味着每一分钟。还可以设置数据的时区。如屏幕截图的最后一行所示，代码在 1.89 秒内执行。

![chunkwise data retrieve](img/50e39730e921aa2b588a977b5fb352b4.png)

突出显示的部分是将我们从 Oanda API 检索到的数据写入 database object 和 HDFStore 并保存在磁盘上的重要步骤。这是一种二进制存储格式。

![HDF store with converted time index](img/1d72b0c93e196e7994413fe4d5466ebd.png)

## **编码和回测交易策略**

或许测试一项策略的最佳方式是看看它的回报。在下面的代码中，我们计算了一个策略的对数回报，以便以后进行性能判断。

![log returns](img/2682036f39f3157fcbde59dd2a33e4c4.png)这是使用 numpy 函数以完全矢量化的方式完成的。

用于回溯测试的策略多年来一直非常流行，也是研究论文的一部分，它基于两种不同的趋势生成信号:一种是 5 次观察(读取分钟)的较短简单滚动平均值，另一种是 15 次观察的较长趋势。这个策略背后的想法很简单:如果短期趋势从下面穿过长期趋势，市场有上升趋势，如果反过来，市场在走下坡路，有更长的趋势。

![11](img/14ea8709d43f7af72186e8b312469cc7.png)

在可视化数据时，我们遇到了以下模式。

![12](img/8b8720bb5654c1e9656365ab850eea5b.png)

蓝线是我们从上述市场收集的基本数据，绿色曲线是短期趋势，红色曲线代表长期趋势。由于重叠，这种可视化没有给出趋势的完整图像，我们集中于 100 个观察点的样本。

![13](img/2fa3a98d3ed94b93e4bc2c2c0f06497b.png)

这里我们可以清楚地看到，当短期趋势从下方突破长期趋势时，现货价格(蓝色曲线)显示出上升趋势，而当绿色曲线从上方穿过红色曲线时，则显示出下降趋势。

一旦我们的策略是模仿市场，我们就可以产生信号，在满足某些条件时发布给市场。

在这种特殊情况下，我们将采取只做多策略。

![strategy calculation](img/39ff59a538e8f62ea3b942e3e82cb415.png)

使用上面的代码，我们生成一个信号，表示当存储在 dataframe 对象中的矢量化 t5 > t15 被满足时，我们做多，否则不做多。

下一步，我们利用上面计算的“回报”来评估我们交易策略的表现。

![strategy returns](img/fe6ef694a31c3391826a29bd9281987d.png)

绿色曲线代表我们的交易策略，而蓝色曲线代表市场回报。从图表中可以清楚地看出，我们在最左边(下降趋势)和最右边都在亏损。

![strategy result chart](img/5fff80107a43e7e8db2a3394ffe4b755.png)

计算“交易次数”是为了了解我们在实际交易中的实施成本。

![number of trades](img/a616eb61aebdedf9c1c94c722bc921fd.png)

在相当短的时间内，有 182 笔交易发生在这个策略中。所以，虽然交易不算高频，但同时也很活跃。

另一个有趣的统计数据可能是回报率的标准差(SD ),它让我们了解了分钟线回报率的波动性。我们在这里看到，市场交易策略的标准差比我们基于趋势的投资所设计的策略要高得多。这也是事实，因为我们没有投资更长的时间。

![standard deviation of returns](img/a46f0b550c152dcfcdcc92a00af9b5dd.png)

这样，我们可以看到我们的策略在从去年数据中选择的随机时间间隔内表现良好。因此，我们的下一步将是处理流数据和实时自动化。这些话题将是我们下一篇博文的一部分。

## 后续步骤

如果你想用 Python 构思和实现量化策略，这篇[博客文章](https://blog.quantinsti.com/python-trading/)将帮助你实现。你认为在自动化交易中 python 比其他语言更受青睐吗？见[为什么](https://blog.quantinsti.com/python-best-programming-language-algorithmic-trading/)。

如果你是一名程序员或科技专业人士，想开始自己的自动化交易平台。从日常从业者的实时互动讲座中学习自动交易。算法交易高管课程涵盖统计学&计量经济学、金融计算&技术和算法&量化交易等培训模块。[现在报名](https://www.quantinsti.com/courses/epat/scholarship-test/)！