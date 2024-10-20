# 使用 Python 将数据转化为见解并构建策略

> 原文：<https://blog.quantinsti.com/data-insights-trading-strategy-python-project-lokesh-kumar/>

这篇文章将帮助你学习如何分析数据，通过实时的股票市场数据和数据集获得洞察力。它还将帮助你学习如何使用 Python 编程创建自己的交易策略。

本项目中使用的完整数据文件和 python 代码也可以在本文末尾下载。

本文是作者提交的最后一个项目，作为他在 QuantInsti 的算法交易管理课程( [EPAT](https://www.quantinsti.com/epat) )的一部分。请务必查看我们的[项目页面](/tag/epat-trading-projects/)，看看我们的学生正在构建什么。

* * *

## **关于作者**

Lokesh Kumar 是孟买一家最大的美国银行的风险经理。他在银行和金融领域拥有超过 6 年的经验，曾在监管模型、信贷决策模型、宏观经济研究和分析领域工作。

![](img/3fa5544593085b4f7a9f59d9a9b596f6.png)

Lokesh 拥有德里大学经济学荣誉学士学位和马德拉斯经济学院金融经济学硕士学位。此外，他还持有风险管理证书(FRM-美国 GARP)。他也是 EPAT 大学的校友。

* * *

## **研究动机**

我是一名经济学学生和风险经理。过去 6 年来，我一直在使用各种统计软件(R、SAS、STATA、EVIEWS)进行数据分析、统计、计量经济学、机器学习建模，但从未有机会处理印度股票数据。

这个项目被证明是一个踏脚石，跟随我的兴趣，并在印度股票市场的职业生涯。此外，我已经跟踪印度金融市场和全球新闻 5 年了。

* * *

## **数据**

*   用于分析的数据包括这些变量。
*   每个部门 2 只(流动性强、波动性大、年回报率正)股票。
*   数据的频率是每天。

* * *

## **型号**

动量、均值回归和配对交易:分析-超额回报、夏普比率、最大提取、提取持续时间、样本内和样本外测试、绝对回报、相对回报、盈利能力分析。

* * *

## **回溯测试模型**

评估战略绩效

* * *

## **项目摘要**

这个项目研究股票价格的行为和运动。我们分析了 2010 年 10 月至 2018 年 12 月期间 Nifty 行业指数的详尽股票列表中的 20 只股票；基于较高的年平均滚动回报率和波动性，考虑每个行业的 2 只股票。

我们研究了股票价格和交易量数据，建立了 3 个策略——基于交易量和价格、均值回归和趋势跟踪(RSI)。我们发现没有一种特定的策略对所有的股票都有效。

我们评估了策略的性能，发现了高回报率和命中率。我们还对 2019 年 1 月至 2019 年 3 月的小样本期间进行了样本外测试，以观察我们是否可以在实时市场中使用这些策略，然后我们可以产生多少利润。

* * *

## **简介**

我们的目标是使用不同的建模方法来确定进场点和出场点，高信心地做多和做空交易。我们专注于构建能够产生高回报且易于实施的战略。

首先，我们探讨了量价关系，因为有许多基于量价的技术指标。如果交易量随着价格的上涨而增加，那么上升趋势就是强劲健康的，当市场进入反趋势时，上升趋势就会减弱。

第二，我们探索了横截面均值回归策略，该策略试图利用来自同一行业的两只证券之间的暂时错误定价。

第三，我们探索了趋势跟踪策略，即当价格上涨时做多，当价格下跌时做空。我们计算了相对强度指数(RSI ),该指数评估股票价格的超买和超卖情况。

* * *

## **数据挖掘**

我们从印度股票市场的每一个板块中选择了两只股票。我们首先看了漂亮的行业指数和每个指数中包含的股票列表。这些指数由流动性最强、资本化程度最高的股票组成，反映了每个行业的行为和表现。

我们使用 20 天滚动窗口，根据平均年化滚动回报和滚动波动性分析了总共 126 只股票。

我们根据高波动性、高回报和正回报最终确定了每个行业的两只股票。

我们从雅虎财经中提取了 2010 年 1 月至 2018 年 12 月期间的股价和成交量数据。

最终数据集由 2010 年 10 月至 2018 年 12 月期间的 20 只股票组成。所有 20 只股票的数据都是从 2010 年 10 月开始的。

用于分析的股票列表:

| **Sr 号** | **符号** | **公司名称** | **行业** |
| one | 阿波罗泰尔 | 阿波罗轮胎有限公司 | 汽车 |
| Two | 阿肖克利 | 阿肖克·利兰有限公司 | 汽车 |
| three | 声望 | 威望地产项目有限公司 | 建筑 |
| four | 上世界 | 奥贝罗伊房地产有限公司 | 建筑 |
| five | 朱布尔福德 | 喜洋洋食品厂有限公司 | 生活消费品 |
| six | UBL | 联合酿酒有限公司 | 生活消费品 |
| seven | 陆军一等兵(Private First Class) | 电力金融有限公司 | 金融服务 |
| eight | RECLTD | 雷克有限公司 | 金融服务 |
| nine | 尼泰克 | 尼伊特技术有限公司 | 信息技术 |
| Ten | 我的天 | 明德树有限公司 | 信息技术 |
| Eleven | 今天 | 今日电视网络有限公司 | 媒体和娱乐 |
| Twelve | INOXLEISUR | 伊诺克斯休闲有限公司 | 媒体和娱乐 |
| Thirteen | 威尔公司 | 韦尔斯普林有限公司 | 金属 |
| Fourteen | HINDALCO | 欣达尔科工业有限公司 | 金属 |
| Fifteen | 阿尔科法尔马 | 奥罗宾多制药有限公司 | 制药公司 |
| Sixteen | 百康 | 百康有限公司 | 制药公司 |
| Seventeen | 印度的 | 印度银行 | 公共银行 |
| Eighteen | 班克 boarda | 巴罗达银行 | 公共银行 |
| Nineteen | 联邦银行 | 联邦银行有限公司 | 私营银行 |
| Twenty | 轴心银行 | Axis 银行有限公司 | 私营银行 |

* * *

## **数据分析**

我们计算了股票收益率、命中率和累计盈亏的描述性统计量。

**以下是项目中使用的每个策略的技术说明:**

在**基于成交量和价格的交易策略**中，如果当前成交量小于最近 3 天的[移动平均](/moving-average-trading-strategies/)成交量，且当前价格小于最近 3 天的移动平均价格，我们将生成做空信号。我们尝试了不同的短时间框架，如 3、4、5、14 天，但 3 天是最好的结果，也试图产生长信号，但这并没有给任何股票带来积极的结果，所以我们只进行了卖空交易。

在**均值回复配对交易策略**中，我们考虑了来自每个部门的 2 只类似股票，计算了价格比，并检查了价格比(价差或 P <sub>S1</sub> /P <sub>S2</sub> )是否是协整的，那么这些股票是均值回复的，可以应用配对交易策略。

我们发现许多价格比率不是协整的。我们使用扩展的 Dicky Fuller (ADF)检验来检验协整性。我们创造了信号——当价差低于低波段时在 S1 做多，当价差高于移动平均线时在 S1 做多，当价差高于高波段时在 S1 做空，当价差低于移动平均线时在 S1 做空，并在 S2 建立相反的头寸。

我们尝试了不同的时间框架，如 5 天、14 天、21 天来计算滚动回报和波动性，但 5 天给出了最佳结果，还尝试了+/- 1 或+/- 2 标准差来计算上下波动带，并根据结果最终确定了+/- 1 标准差。

在**趋势跟踪 RSI 策略**中，70 或以上的值表明证券超买，因此股票做空，30 或以下的值表明证券超卖，因此股票做多。我们用 21 天的时间来计算 RSI。然而，我们研究了不同的时间框架，如 5、14、21、30、60 天，但 21 天的结果最好。

* * *

## **主要发现**

我们提供了 20 只股票的汇总统计数据。负偏度表示收益的分布是负偏的。

过度峰度(峰度大于 3)表明收益分布具有较厚的尾部(较高的极端结果)。

| **符号** | **表示** | **Std。偏差** | **最小值** | **最大值** | **第 25 百分位** | **第 50 百分位** | **第 75 百分位** | **偏斜度** | **峰度** |
| 阿波罗泰尔 | Zero point zero six | Two point five one | -29.37 | Ten point one six | -1.34 | Zero point zero six | One point four three | -0.96 | Eleven point zero seven |
| 阿肖克利 | Zero point zero five | Two point three nine | -15.09 | Twelve point eight one | -1.30 | Zero | One point three four | Zero point zero two | Two point nine two |
| 声望 | Zero point zero one | Two point eight two | -13.35 | Sixteen point six two | -1.69 | -0.12 | One point five | Zero point four three | Two point one two |
| 上世界 | Zero point zero two | Two point three five | -11.70 | Sixteen point zero six | -1.32 | -0.10 | One point one three | Zero point seven two | Three point eight three |
| 朱布尔福德 | Zero point zero eight | Two point four nine | -11.91 | Fifteen point zero three | -1.25 | Zero | One point three four | Zero point one six | Three point one two |
| UBL | Zero point zero six | Two point five three | -12.67 | Seventeen point one eight | -1.16 | -0.02 | One point zero eight | Zero point seven eight | Six point six one |
| 陆军一等兵(Private First Class) | -0.03 | Two point seven two | -15.52 | Thirteen point four | -1.62 | -0.08 | One point five seven | Zero point zero seven | One point six six |
| RECLTD | -0.02 | Two point five nine | -13.55 | Twelve point nine nine | -1.47 | -0.07 | One point five | -0.04 | One point five seven |
| 尼泰克 | Zero point zero eight | Two point three six | -12.60 | Thirteen point nine one | -1.26 | -0.04 | One point two six | Zero point three five | Three point zero five |
| 我的天 | Zero point zero nine | Two point zero four | -18.36 | Nine point four two | -0.99 | Zero point zero three | One point zero nine | -0.13 | Six point one five |
| 今天 | Zero point zero eight | Three point zero four | -18.15 | Eighteen point two three | -1.44 | -0.19 | One point three | One point one six | Seven point four five |
| INOXLEISUR | Zero point zero six | Two point six four | -15.21 | Sixteen point nine | -1.38 | -0.09 | One point two six | Zero point seven four | Four point seven |
| 威尔公司 | -0.03 | Three point three one | -31.45 | Eighteen point two three | -1.76 | -0.19 | One point six four | -0.24 | Eight point one nine |
| HINDALCO | Zero | Two point five two | -10.17 | Twelve point six eight | -1.57 | -0.06 | One point five two | Zero point one three | One point two five |
| 阿尔科法尔马 | Zero point zero nine | Two point five one | -18.44 | Twelve point four four | -1.31 | Zero | One point four eight | -0.03 | Three point one three |
| 百康 | Zero point zero seven | Two point zero four | -12.46 | Fourteen point four seven | -1.02 | Zero point zero one | One point zero eight | Zero point five six | Five point one two |
| 印度的 | -0.01 | Two point seven four | -13.11 | Nineteen point one two | -1.56 | -0.11 | One point two seven | Zero point nine three | Five point six six |
| 班克 boarda | -0.02 | Two point five three | -17.89 | Twenty-seven point three three | -1.38 | -0.03 | One point two eight | Zero point eight five | Twelve point zero six |
| 联邦银行 | Zero point zero three | Two point one nine | -13.04 | Seventeen point four seven | -1.21 | -0.04 | One point one eight | Zero point three | Four point seven eight |
| 轴心银行 | Zero point zero four | Two point one three | -9.96 | Fourteen point six | -1.15 | -0.02 | One point one nine | Zero point two | Three point zero three |

### **基于数量/价格的卖空策略**

我们对所有 20 只股票都采用了这种策略。数据显示，这种策略导致平均 55%的命中率和 9.7%的年化回报。累计 PnL 显示，2010 年 10 月的投资额(1 卢比)在 2018 年 12 月平均为 2.291 卢比。

| **符号** | **#积极交易** | **#总交易量** | **命中率** | **累积 PnL** | 平均。年化回报率 |
| 阿波罗泰尔 | Three hundred and twenty-four | Six hundred and five | 54% | Two point two nine four | 10.9% |
| 阿肖克利 | Three hundred and twenty-eight | Five hundred and seventy-six | 57% | Three point zero eight nine | 15.1% |
| 声望 | Four hundred and twenty-one | Six hundred and ninety-five | 61% | Four point seven zero three | 21.4% |
| 上世界 | Four hundred and five | Six hundred and eighty-three | 59% | Four point two five one | 19.8% |
| 朱布尔福德 | Three hundred and forty | Six hundred and one | 57% | Two point three two five | 11.1% |
| UBL | Three hundred and eighty-one | Six hundred and sixty-nine | 57% | Two point seven one two | 13.3% |
| 陆军一等兵(Private First Class) | Two hundred and ninety-two | Five hundred and sixty-two | 52% | One point four eight six | 5.1% |
| RECLTD | Three hundred and three | Six hundred and five | 50% | One point two two five | 2.6% |
| 尼泰克 | Three hundred and forty-six | Six hundred and sixty-nine | 52% | One point zero five two | 0.6% |
| 我的天 | Three hundred and forty-three | Six hundred and seventeen | 56% | Two point one zero five | 9.8% |
| 今天 | Four hundred and thirty-six | Seven hundred and fifty-one | 58% | Two point four four six | 11.8% |
| INOXLEISUR | Three hundred and eighty-four | Seven hundred and forty-nine | 51% | One point zero zero two | 0.0% |
| 威尔公司 | Four hundred and sixteen | Six hundred and ninety-one | 60% | Four point two seven one | 19.9% |
| HINDALCO | Two hundred and ninety-one | Five hundred and seventy-three | 51% | One point four zero two | 4.3% |
| 阿尔科法尔马 | Two hundred and ninety-five | Five hundred and sixty-three | 52% | Two point zero eight nine | 9.6% |
| 百康 | Three hundred and twenty-nine | Six hundred and twenty-two | 53% | One point eight eight six | 8.3% |
| 印度的 | Three hundred and seventy-two | Six hundred and thirty-nine | 58% | Two point seven five | 13.5% |
| 班克 boarda | Three hundred and thirteen | Six hundred and one | 52% | One point four five five | 4.8% |
| 联邦银行 | Three hundred and twenty-four | Five hundred and ninety-five | 54% | One point eight seven six | 8.2% |
| 轴心银行 | Two hundred and ninety-six | Five hundred and fifty-three | 54% | One point four zero two | 4.3% |

### **均值回归对交易策略**

在我们的分析中，我们发现只有 2 对股票是协整的。PFC & RECLLTD 的 p 值小于 10%的显著性水平，TVTODAY & INOXLEISUR 的 p 值小于 1%的显著性水平。

数据显示，这种策略导致平均 52%的命中率和 13.7%的年化回报。累计 PnL 显示，2010 年 10 月的投资额(2 卢比)在 2018 年 12 月平均变成了(5.677 卢比)。

| **符号** | **#积极交易** | **#总交易量** | **命中率** | **累积 PnL** | 平均。年化回报率 |
| 陆军一等兵(Private First Class) | One thousand four hundred and seventy-five | Two thousand eight hundred and ninety-six | 51% | Four point six zero one | 11.0% |
| RECLTD |
| 今天 | One thousand five hundred and twenty-one | Two thousand eight hundred and seventy-nine | 53% | Six point seven five three | 16.4% |
| INOXLEISUR |

### **趋势跟随 RSI 策略**

我们为 NIITTECH 开发了这种策略，因为基于数量和价格的卖空策略未能产生良好的回报，而且这对组合没有进行协整。

数据显示，这种策略导致平均 69%的命中率和 6.5%的年化回报。累计 PnL 显示，2010 年 10 月的投资额(1 卢比)在 2018 年 12 月平均为(1.652 卢比)。

| **符号** | **#积极交易** | **#总交易量** | **命中率** | **累积 PnL** | 平均。年化回报率 |
| 尼泰克 | Forty-six | Sixty-seven | 69% | One point six five two | 6.5% |

### **样本外回测**

我们根据 2010 年 10 月至 2018 年 12 月期间的历史数据优化了策略。

我们运行一个样本外回溯测试，看看如果我们可以在市场上使用这些策略来产生利润，该策略的表现如何。分析中使用的样本外回测期为 2019 年 1 月至 2019 年 3 月。

### **基于数量/价格的卖空策略**

根据历史数据结果，我们对过去产生超过 10%回报率的股票测试了这一策略，并观察了如果我们在 2019 年 1 月至 2019 年 3 月期间将资金投入市场，这一策略会如何表现。

数据显示，这种策略导致平均 55%的命中率和 25.3%的年化回报。

| **符号** | **#积极交易** | **#总交易量** | **命中率** | **累积 PnL** | 平均。年化回报率 |
| 阿波罗泰尔 | Twelve | Nineteen | 63% | One point zero zero two | 0.8% |
| 阿肖克利 | Ten | Seventeen | 59% | One point zero two five | 10.8% |
| 声望 | Sixteen | Twenty-four | 67% | One point one seven three | 93.1% |
| 上世界 | seven | Sixteen | 44% | Zero point nine six | -15.4% |
| 朱布尔福德 | six | Thirteen | 46% | Zero point nine nine six | -1.8% |
| UBL | six | Sixteen | 38% | Zero point nine four six | -20.5% |
| 今天 | Sixteen | Twenty-two | 73% | One point one five six | 82.3% |
| 威尔公司 | Seventeen | Twenty-seven | 63% | One point one six eight | 90.0% |
| 印度的 | seven | Fifteen | 47% | Zero point nine seven one | -11.3% |

### **均值回归对交易策略**

数据显示，这种策略导致平均 45%的命中率和 5.4%的年化收益。

| **符号** | **#积极交易** | **#总交易量** | **命中率** | **累积 PnL** | 平均。年化回报率 |
| 陆军一等兵(Private First Class) | Forty | Eighty-three | 48% | Two point two zero two | 48.8% |
| RECLTD |
| 今天 | Forty | Ninety-five | 42% | One point seven eight one | -38.1% |
| INOXLEISUR |

### **趋势跟随 RSI 策略**

数据显示，这种策略导致平均 50%的命中率和 4.5%的年化收益。

| **符号** | **#积极交易** | **#总交易量** | **命中率** | **累积 PnL** | 平均。年化回报率 |
| 尼泰克 | Two | four | 50% | One point zero one one | 4.5% |

* * *

## **限制**

为了计算回报，我们没有包括交易成本。

* * *

## **实施方法**

这是一个完全活的项目，可以很容易地在交易系统中实现。

**基于数量和价格的卖空策略**

如果当天交易量低于过去 3 天的平均交易量，当天收盘价低于过去 3 天的平均收盘价，则在第二天以开盘价买入股票，以收盘价卖出股票。

**均值回归对交易策略**

如果当日价差(股票 1/股票 2 的价格比)低于下限(价差的 5 天移动平均值-价差的 5 天移动标准差)，第二天在股票 1 中做多。

如果当日价差(股票 1/股票 2 的价格比)超过价差的 5 天移动平均线，第二天在股票 1 处做多。

如果当日价差(股票 1/股票 2 的价格比)高于上限(价差的 5 天移动平均线+价差的 5 天移动标准差)，第二天在股票 1 中做一个短线。

如果当天的价差(股票 1/股票 2 的价格比)低于价差的 5 天移动平均线，在第二天做空股票 1。同时在 stock2 中取相反的位置。

如果多空信号是新的，以开盘价交易，否则以收盘价交易。

**趋势跟随 RSI 策略**

如果当天 RSI 低于 30，第二天做多股票。

如果当日 RSI 超过 70，第二天做空该股。

如果多空信号是新的，以开盘价交易，否则以收盘价交易。

* * *

### 结论

我们研究了股票价格和交易量数据，建立了 3 个策略——基于交易量和价格、均值回归和趋势跟踪(RSI)。

我们发现没有一个特定的策略对所有的股票都有效。我们评估了策略的性能，发现了较高的总体回报率和命中率。

然而，我们可以探索我们在课程中学到的许多其他策略，并产生比这些策略更高的回报。

如果你想学习算法交易的各个方面，那就去看看算法交易(EPAT) 的[高管课程。该课程包括各种培训模块，让你具备在算法交易中建立一个有前途的职业生涯所需的技能。](https://www.quantinsti.com/epat/)

* * *

**参考书目**

*   [NSE 行业指数](https://www.nseindia.com/products/content/equities/indices/sectoral_indices.htm)
*   [EPAT 项目](https://www.quantinsti.com/category/project-work-epat)

* * *

**文件在下载**

*   Python 中的项目编码策略
*   R 中的项目代码数据提取

* * *

免责声明:就我们学生所知，本项目中的信息是真实和完整的。学生或 QuantInsti 不保证提供所有推荐。学生和 QuantInsti 否认与这些信息的使用有关的任何责任。本项目中提供的所有内容仅供参考，我们不保证通过使用该指南您将获得一定的利润。