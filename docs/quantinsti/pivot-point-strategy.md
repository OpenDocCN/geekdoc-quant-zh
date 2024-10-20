# 支点战略

> 原文：<https://blog.quantinsti.com/pivot-point-strategy/>

在这个项目中，我们用支点分析不同的日内交易策略。在定义了计算支点的不同方法后，我们用最经典的策略和教科书中通常教授的不同方法进行回溯测试。

要了解 Pivot Point 以及如何用它来预测交易市场的动向，请阅读这篇博客。

本文是作者提交的最后一个项目，作为他们在 QuantInsti 算法交易( [EPAT](https://www.quantinsti.com/epat) )高管课程的一部分。请务必查看我们的[项目页面](/tag/epat-trading-projects/)，看看我们的学生正在构建什么。

## 关于作者

![](img/1a04bd4c5be91c7fcd0a00354ffb0d67.png)

Morabanc Asset Management 的多资产投资组合经理 Tomás garcía-purri OS 在金融领域拥有超过 10 年的经验。他的优势包括经济分析、资产配置和全球宏观策略。托马斯是特许金融分析师(CFA)、特许另类投资分析师(CAIA)，拥有 IEB 金融市场硕士学位。他还在几所大学和商学院任教。

### **简介**

支点可能诞生于芝加哥，是交易者计算支撑位和阻力位的常用技术。它出现在大多数专门研究技术分析的教科书和课程中(如 CMT 或 CFTe)，也是技术分析软件中最常见的指标。

然而，与大多数技术指标一样，公共学术研究很少，大多数后验测试要么是私人的(即专有研究)，要么是在博客等中进行的。

有不同的方法来计算轴心点级别。我们测试了以两种不同方式计算中心支点的策略:

*   作为前一天收盘、最高和最低价格之间的平均值；
*   包括当日开盘；
*   将开盘价加两次，不加收盘价(伍迪方法)。

收盘价是 15:59。剩余水平计算如下:

|  | **经典/伍迪** | **奸党** | **斐波那契** |
| 支持 1 (S1) | 2 *枢轴点- H | 枢轴点- (0.0916 *范围) | 枢轴点- (0.382 *范围) |
| 阻力 1(R1) | 2 *枢轴点- L | 轴心点+ (0.0916 *范围) | 枢轴点+ (0.382 *范围) |
| 支持 2 (S2) | 枢轴点-高-低 | 枢轴点- (0.183 *范围) | 枢轴点- (0.618 *范围) |
| 阻力 2 (R2) | 枢轴点+高-低 | 轴心点+ (0.183 *范围) | 轴心点+ (0.618 *范围) |
| 支持 3 (S3) | S1 - H - L | 枢轴点- (0.275 *范围) | 轴心点- (1 *范围) |
| 电阻 3 (R3) | R1+高-低 | 枢轴点+ (0.275 *范围) | 轴心点+ (1 *范围) |
| H =上期高 L =上期低范围=上期高-上期低 |

图 1:轴心点级别

在这个 EPAT 的期末项目中，我们分析了在芝加哥商品交易所上市的期货(迷你标准普尔 500、国债、欧元兑美元和黄金)的不同支点策略。

### **方法论**

为了对策略进行回溯测试，我们使用了 Python 和 Pandas、Numpy、Matplot 和 QuantStats 库。

重要的是要考虑可能对结果产生影响的分析的不同方面:

*   这项研究是用一分钟的日内数据进行的。每分钟的收盘价和实际执行策略的价格(滑点)之间可能有差异，没有什么能保证有足够的交易量。此外，佣金、费用和税收也没有考虑在内。尽管如此，选择的产品具有显著的流动性和较低的佣金成本，因此我们估计影响较小(减去样本回测的累积回报约-0.25%/-0.75%)。
*   我们使用的是未来的第一个合同，所以没有考虑展期。在研究样本中，至少有一次滚动，这将影响第二天枢轴点的计算，从而影响当天的结果。
*   由于计算上的困难，最好不要在周日进行交易(为了周一的中枢点而取消这一天，这是根据周五的水平计算的)。

### **回溯测试**

使用 250 天的样本和 30 天的样本外分析来分析结果。

最初的想法是测试教科书中解释的最经典的策略(即，在支撑位买入，在阻力位卖出，或者在价格高于支点时买入，在价格低于支点时卖出，等等)。然而，糟糕的结果让我们认为它们不再有效了。

我们分析了两种替代策略:

**策略一:**价格突破阻力时买入。在每个抗性的分解中加+1 契约。当价格突破支撑位时卖出。每次休息增加 1 份合同。头寸必须介于-3 和+3 合约之间。在一天结束时平仓。这个策略和教科书上说的正好相反。

**策略 2:** 策略 1 的一个稍微复杂一点的版本。如果价格在支点上方开盘，如果价格在支点下方交叉，卖出-2 合约，在支撑 1 处增加-1，目标在支撑 2 和 3 处(在支撑 1 处增加+2，在支撑 2 处增加+1)，并在阻力处停止。如果价格在支点以下开盘，当价格穿过中心支点时买入+2，增加阻力 1 +1，目标在阻力 2 和 3 (-2 在阻力 2 和-1 在阻力 3)，在支撑处止损。在一天结束时平仓。

#### **BT 策略 1**

总的来说，结果一般，虽然比教科书版本好一些。考虑到级别相对相似，计算枢轴点的方法之间的差异很小。在任何情况下，似乎给出最佳结果或至少是最稳定的结果的方法是包括打开的经典方法。

使用这种策略的唯一显著结果是在欧元兑美元上，但是在样本之外不被支持，看起来更像是一种巧合而不是策略的原因。

您可以在附录 1 中找到结果摘要。

#### **BT 策略二**

更有趣的是第二种策略的结果。

使用 MiniSP 获得的结果尤为突出。

该策略在整个分析期内表现稳定，在 8 月份表现强劲:

![](img/2d80b9bf901631e0c0531e304d3de519.png)

<small>图表 1:策略 2。累积回报与基准 MiniSP</small>

虽然提款比买入并持有策略高，但潜在回报也更高，并补偿了高 Calmar 比率显示的风险。

这种一致性保留在样本之外:

![](img/e47ed5c19ecb8bd5b0fb03753f2872c0.png)

<small>图二:策略二。样本的累积回报与基准 MiniSP 的比较</small>

就黄金而言，我们发现了积极的结果，尽管没那么丰富多彩:

![](img/7ed1c401ae89c9dfb0420f5514d8acac.png)

<small>图表 3:策略 2。累积回报与基准黄金</small>

他们不会置身样本之外。或许是因为 8 月份开始的强劲趋势:

![](img/b68ddc4ca775696cabfda7033f23d8ad.png)

图表 4:策略 2。样本外的累积回报与基准黄金

类似地，欧元兑美元重复这一模式，但幅度较小，而美国国债表现良好，尽管在样本外，它在回溯测试期末的表现类似于黄金:似乎这一系统在非常时髦的市场中表现更差。

![](img/def78c6f644e29dba1b69c52a67e09ea.png)

<small>图表 5:策略 2。累积回报与基准欧元兑美元</small>

![](img/4dc236e43ade7a9a867151d4c3054549.png)

<small>图表 6:策略二。样本的累积回报与基准欧元兑美元</small>

![](img/6044012171d5133ed711bec41dc6bab5.png)

<small>图表 7:策略二。累积回报与基准国债期货</small>

![](img/4d62cae6e208ce77e36e7822cd0e1204.png)

<small>图表 8:策略二。样本外基准国债期货的累积收益</small>

主要统计数据的汇总见附录 2。

## **结论**

我们可以强调这些主要结论:

*   枢轴点计算差异不会对简单系统的结果产生重大影响。
*   教科书上教的传统交易策略似乎不再管用了。同样，最简单或最明显的策略也不管用(无论是购买还是相反)。但是对传统策略的小修改似乎确实有效，并给继续研究带来了一些希望。
*   似乎均值回归策略比动量策略更有效。总而言之，在非常时尚的市场中，没有人能打败简单的买入并持有。
*   继续研究并试图找到添加到策略中的指标是很有趣的，特别是那些使策略根据市场类型从[动量](https://quantra.quantinsti.com/course/momentum-trading-strategies)旋转到平均回归的指标。

## **参考书目**

**书籍:**

*   烛台和支点交易，约翰 l .人，威利 2007 年。
*   期货市场的计算机分析。

**杂志:**

*   股票和商品第 18:2 (16-22):枢轴点。
*   《股票与商品》第 24:3 节(72-73): [用支点预测反转。](http://stockcharts.com/h-mem/tascredirect.html?artid=%5CV24%5CC03%5C054DEVC.pdf)

**工作报告:**

威林斯基、安东尼&尼奇扎伊、托马什&贝拉、阿内塔&博什斯基、皮奥特。(2013).基于支点层次概念的投资策略有效性研究。理论与应用计算机科学杂志。7.42-55.

**网页:**

股票图表、图表学校技术指标和叠加枢纽点:[https://school.stockcharts.com/doku.php?id =技术指标:枢纽点](https://school.stockcharts.com/doku.php?id=technical_indicators:pivot_points)

X-Trader.net[特殊支点](https://www.x-trader.net/foro/viewtopic.php?f=49&t=20210&sid=b4ab42af3a958f2f82bb6237967a1568):https://www.x-trader.net/foro/viewtopic.php?t=20210[T3](https://www.x-trader.net/foro/viewtopic.php?t=20210)

**附录 1:策略 1 回溯测试**

**表 1:策略 1 回测总结**

|  | **国债期货** | **黄金** | **迷你 SP** | 【T0 美元】T1 | **样本中的欧元兑美元** |
|  | 策略 1 | 买入并持有 | 策略 1 | 买入并持有 | 策略 1 | 买入并持有 | 策略 1 | 买入并持有 | 策略 1 | 买入并持有 |
| 开始时期 | 05/02/2019 | 05/02/2019 | 05/02/2019 | 05/02/2019 | 05/02/2019 | 05/02/2019 | 05/02/2019 | 05/02/2019 | 21/08/2019 | 21/08/2019 |
| 终结期 | 21/08/2019 | 21/08/2019 | 21/08/2019 | 21/08/2019 | 21/08/2019 | 21/08/2019 | 21/08/2019 | 21/08/2019 | 20/09/2019 | 20/09/2019 |
| 上市时间 | 58.0% | 100% | 52.0% | 100% | 55.0% | 100% | 71.0% | 100% | 52.0% | 100% |
| 交易数量 | One hundred and seventy |  | One hundred and seventy-one |  | One hundred and sixty-six |  | One hundred and eighty-nine |  | Twenty-eight |
| 累积回报 | 0.61% | 7.09% | 5.5% | 14.25% | 10.12% | 7.02% | -7.28% | -2.77% | -2.02% | -0.25% |
| CAGR% | 1.14% | 13.54% | 10.43% | 27.99% | 19.56% | 13.4% | -13.08% | -5.07% | -22.03% | -3.02% |
| 夏普 | Zero point two three | Two point five one | Zero point five eight | One point five eight | One point one seven | Zero point eight four | -1.1 | -0.81 | -2.57 | -0.44 |
| 索尔蒂诺 | Zero point four | Four point six one | One point one eight | Two point eight six | Two point zero five | One point one four | -1.86 | -1.13 | -2.74 | -0.65 |
| 最大压降 | -2.42% | -1.59% | -8.06% | -5.54% | -7.08% | -6.98% | -12.26% | -3.63% | -3.16% | -1.87% |
| 最长 DD 天 | One hundred and fourteen | fifty-six | One hundred and eleven | One hundred and thirteen | One hundred and five | Sixty-one | One hundred and ninety | One hundred and fifty-three | Fifteen | Twenty-five |
| 波动性(安。) | 3.74% | 3.5% | 13.24% | 11.13% | 10.99% | 10.93% | 8.44% | 4.32% | 6.38% | 4.45% |
| 卡尔马尔 | Zero point four seven | Eight point five four | One point two nine | Five point zero five | Two point seven six | One point nine two | -1.07 | -1.4 | -6.97 | -1.61 |
| 斜交 | Two point two four | Zero point nine two | Three point one two | One point six seven | One point seven eight | -1.06 | One point six seven | Zero point two one | -2.95 | Zero point three seven |
| 峭度 | Thirteen point six eight | Three point one six | Eighteen point seven six | Nine point zero five | Eleven point two five | Five point one one | Four point one six | Two point eight two | Eleven point zero seven | Zero point one four |
| 预期每日百分比 | 0.0% | 0.03% | 0.03% | 0.07% | 0.05% | 0.03% | -0.04% | -0.01% | -0.07% | -0.01% |
| 预期每月% | 0.09% | 0.98% | 0.77% | 1.92% | 1.39% | 0.97% | -1.07% | -0.4% | -1.02% | -0.13% |
| 预期年百分比 | 0.61% | 7.09% | 5.5% | 14.25% | 10.12% | 7.02% | -7.28% | -2.77% | -2.02% | -0.25% |
| 每日风险值 | -0.38% | -0.33% | -1.34% | -1.08% | -1.09% | -1.1% | -0.91% | -0.46% | -0.73% | -0.47% |
| 预期短缺(cVaR) | -0.55% | -0.55% | -1.83% | -1.83% | -1.63% | -1.63% | -1.06% | -1.06% | -1.31% | -1.31% |
| 支付比率 | One point four eight | Two point five one | Two point seven one | Three point two four | Zero point nine | Two point three four | One point seven eight | Two point two three | Zero point seven three | Two point five three |
| 利润因素 | Zero point zero six | Zero point six five | Zero point one nine | Zero point four | Zero point three six | Zero point one eight | Zero point one nine | Zero point one five | Zero point five three | Zero point zero seven |
| 常识比率 | Zero point zero six | Zero point eight eight | Zero point three | Zero point five one | Zero point three two | Zero point one seven | Zero point three one | Zero point one four | Zero point two four | Zero point zero eight |
| CPC 指数 | Zero point zero four | Zero point nine one | Zero point one eight | Zero point six six | Zero point one seven | Zero point two five | Zero point one one | Zero point one five | Zero point two two | Zero point zero nine |
| 尾部比率 | One | One point three four | one point six | One point two nine | Zero point eight nine | Zero point nine three | One point six two | Zero point nine five | Zero point four six | One point zero nine |
| 异常胜率 | Nine point five two | Six point three seven | Nine point nine four | Seven point seven three | Eight point eight four | Six point seven six | Four point three five | Ten point one five | Six point eight five | Three point two seven |
| 异常损失率 | Three point zero three | Two point eight eight | Three point two one | Three point zero seven | Three point six four | Three point one two | One point eight nine | Three point three eight | One point eight two | Three point seven one |
| 动目标检测 | 0.44% | 2.43% | -3.03% | 6.37% | 2.66% | -1.98% | -3.92% | 0.3% | -2.8% | 0.74% |
| 3M | 0.49% | 5.01% | 8.26% | 17.57% | 12.26% | 2.31% | 1.21% | -0.54% | -2.02% | -0.25% |
| 6M | 0.09% | 6.94% | 8.08% | 13.22% | 5.21% | 5.32% | -6.9% | -1.76% | -2.02% | -0.25% |
| 本年开始至今 | 0.61% | 7.09% | 5.5% | 14.25% | 10.12% | 7.02% | -7.28% | -2.77% | -2.02% | -0.25% |
| 1Y | 0.61% | 7.09% | 5.5% | 14.25% | 10.12% | 7.02% | -7.28% | -2.77% | -2.02% | -0.25% |
| 最好的一天 | 1.48% | 1.05% | 5.5% | 4.56% | 4.24% | 2.19% | 2.5% | 0.94% | 0.45% | 0.65% |
| 最糟糕的一天 | -0.77% | -0.57% | -2.53% | -1.69% | -2.1% | -3.51% | -1.18% | -0.94% | -1.78% | -0.5% |
| 最佳月份 | 0.94% | 2.43% | 8.41% | 8.15% | 3.38% | 7.31% | 4.64% | 2.28% | 0.8% | 0.74% |
| 最差月份 | -0.79% | -0.47% | -3.03% | -1.68% | -1.94% | -6.94% | -6.81% | -3.03% | -2.8% | -0.99% |
| 平均值。减少 | -0.47% | -0.39% | -1.94% | -1.48% | -1.69% | -1.44% | -6.2% | -2.8% | -1.75% | -1.0% |
| 平均值。提款天数 | Nineteen | nine | Twenty | Fifteen | Seventeen | eight | Ninety-six | Ninety-eight | eight | Thirteen |
| 回收系数 | Zero point two five | Four point four seven | Zero point six eight | Two point five seven | One point four three | One point zero one | -0.59 | -0.76 | -0.64 | -0.13 |

**附录二:** **策略二回测总结**

**表 2:策略 2 Mini S & P 回测总结**

|  | 迷你 S & P 500 |  | **Mini S & P 500 出样** |
| 开始时期 | 05/02/2019 | 05/02/2019 | 21/08/2019 | 21/08/2019 |
| 终结期 | 21/08/2019 | 21/08/2019 | 20/09/2019 | 20/09/2019 |
| 上市时间 | 67.0% | 100% | 65.0% | 100% |
| 交易数量 | Two hundred and eleven |  | Thirty-four |  |
| 累积回报 | 45.03% | 6.51% | 5.12% | 3.74% |
| CAGR% | 99.15% | 12.39% | 83.65% | 56.27% |
| 夏普 | Two point six two | Zero point seven nine | Two point seven six | Two point five seven |
| 索尔蒂诺 | Five point two six | One point zero six | Five point nine eight | Three point six nine |
| 最大压降 | -6.31% | -7.11% | -2.98% | -2.78% |
| 最长 DD 天 | Ninety | Sixty-one | Ten | Twelve |
| 波动性(安。) | 18.77% | 10.95% | 15.14% | 11.87% |
| 卡尔马尔 | Fifteen point seven two | One point seven four | Twenty-eight point one one | Twenty point two four |
| 斜交 | One point four two | -1.08 | One point three | -1.39 |
| 峭度 | Six point six two | Five point one eight | Two point six one | Seven point four six |
| 预期每日百分比 | 0.19% | 0.03% | 0.16% | 0.12% |
| 预期每月% | 5.45% | 0.9% | 2.53% | 1.85% |
| 预期年百分比 | 45.03% | 6.51% | 5.12% | 3.74% |
| 每日风险值 | -1.75% | -1.1% | -1.4% | -1.11% |
| 预期短缺(cVaR) | -2.95% | -2.95% | -1.52% | -1.52% |
| 支付比率 | One point zero one | One point eight nine | One point eight seven | Two point three seven |
| 利润因素 | Zero point seven eight | Zero point one seven | Zero point eight one | Zero point seven seven |
| 常识比率 | One point three four | Zero point one six | One point three nine | Two point five five |
| CPC 指数 | Zero point four one | Zero point one eight | Zero point seven six | One point two |
| 尾部比率 | One point seven one | Zero point nine two | One point seven one | Three point two nine |
| 异常胜率 | Four point two one | Eight point one seven | Four point one one | Five point nine nine |
| 异常损失率 | Two point seven three | Three point two five | Two point seven seven | Two point eight eight |
| 动目标检测 | 20.69% | -2.11% | 0.74% | 3.1% |
| 3M | 24.15% | 2.05% | 5.12% | 3.74% |
| 6M | 33.7% | 4.83% | 5.12% | 3.74% |
| 本年开始至今 | 45.03% | 6.51% | 5.12% | 3.74% |
| 1Y | 45.03% | 6.51% | 5.12% | 3.74% |
| 最好的一天 | 6.79% | 2.18% | 3.18% | 1.72% |
| 最糟糕的一天 | -4.31% | -3.54% | -1.52% | -2.78% |
| 最佳月份 | 20.69% | 7.25% | 4.35% | 3.1% |
| 最差月份 | -2.42% | -7.07% | 0.74% | 0.62% |
| 最佳年份 | 45.03% | 6.51% | 5.12% | 3.74% |
| 最糟糕的一年 | 45.03% | 6.51% | 5.12% | 3.74% |
| 平均值。减少 | -1.7% | -1.45% | -1.16% | -1.24% |
| 平均值。提款天数 | Ten | eight | four | seven |
| 回收系数 | Seven point one four | Zero point nine two | One point seven two | One point three four |

**表 3:策略 3 国债期货回测总结**

|  | **国债期货** |  | **样本外国债期货** |
| 开始时期 | 05/02/2019 | 05/02/2019 | 21/08/2019 | 21/08/2019 |
| 终结期 | 21/08/2019 | 21/08/2019 | 20/09/2019 | 20/09/2019 |
| 上市时间 | 68.0% | 100% | 68.0% | 100% |
| 交易数量 | Two hundred and twenty-seven |  | Thirty-one |  |
| 累积回报 | 6.89% | 7.09% | 1.86% | -0.52% |
| CAGR% | 13.14% | 13.54% | 25.13% | -6.17% |
| 夏普 | One point five three | Two point five one | One point eight four | -0.86 |
| 索尔蒂诺 | Two point seven four | Four point six one | Two point nine five | -1.22 |
| 最大压降 | -3.85% | -1.59% | -3.27% | -2.57% |
| 最长 DD 天 | One hundred and five | fifty-six | four | Sixteen |
| 波动性(安。) | 5.63% | 3.5% | 8.35% | 4.82% |
| 卡尔马尔 | Three point four one | Eight point five four | Seven point six nine | -2.4 |
| 斜交 | Zero point nine eight | Zero point nine two | Zero point two | Zero point two eight |
| 峭度 | Three point one three | Three point one six | One point zero six | Zero point five one |
| 预期每日百分比 | 0.03% | 0.03% | 0.06% | -0.02% |
| 预期每月% | 0.96% | 0.98% | 0.93% | -0.26% |
| 预期年百分比 | 6.89% | 7.09% | 1.86% | -0.52% |
| 每日风险值 | -0.55% | -0.33% | -0.8% | -0.52% |
| 预期短缺(cVaR) | -0.75% | -0.75% | -1.12% | -1.12% |
| 支付比率 | Two point one eight | Two point five six | Zero point eight six | One point six one |
| 利润因素 | Zero point three seven | Zero point six five | Zero point four two | Zero point one five |
| 常识比率 | Zero point six | Zero point eight eight | Zero point five one | Zero point one six |
| CPC 指数 | Zero point three nine | Zero point nine two | Zero point two three | Zero point one |
| 尾部比率 | one point six | One point three four | One point two one | One point zero seven |
| 异常胜率 | Five point zero eight | Seven point five eight | Three point six | Five point nine six |
| 异常损失率 | Two point one five | Three point three eight | One point four five | Two point nine nine |
| 动目标检测 | 3.53% | 2.43% | -1.1% | -0.89% |
| 3M | 4.06% | 5.01% | 1.86% | -0.52% |
| 6M | 5.53% | 6.94% | 1.86% | -0.52% |
| 本年开始至今 | 6.89% | 7.09% | 1.86% | -0.52% |
| 1Y | 6.89% | 7.09% | 1.86% | -0.52% |
| 最好的一天 | 1.45% | 1.05% | 1.41% | 0.7% |
| 最糟糕的一天 | -1.05% | -0.57% | -1.12% | -0.63% |
| 最佳月份 | 3.53% | 2.43% | 2.99% | 0.37% |
| 最差月份 | -0.8% | -0.47% | -1.1% | -0.89% |
| 最佳年份 | 6.89% | 7.09% | 1.86% | -0.52% |
| 最糟糕的一年 | 6.89% | 7.09% | 1.86% | -0.52% |
| 平均值。减少 | -0.72% | -0.39% | -1.1% | -1.11% |
| 平均值。提款天数 | Thirteen | nine | three | seven |
| 回收系数 | One point seven nine | Four point four seven | Zero point five seven | -0.2 |

**表 4:策略 2 欧元兑美元回测总结**

|  | 【T0 美元】T1 |  | **样本中的欧元兑美元** |
| 开始时期 | 05/02/2019 | 05/02/2019 | 21/08/2019 | 21/08/2019 |
| 终结期 | 21/08/2019 | 21/08/2019 | 20/09/2019 | 20/09/2019 |
| 上市时间 | 66.0% | 100% | 68.0% | 100% |
|  | Two hundred and twenty-seven |  | Thirty-three |  |
| 累积回报 | -2.28% | -2.77% | 1.49% | -0.25% |
| CAGR% | -4.18% | -5.07% | 19.77% | -3.02% |
| 夏普 | -0.4 | -0.81 | One point six five | -0.44 |
| 索尔蒂诺 | -0.63 | -1.13 | Two point six nine | -0.65 |
| 最大压降 | -10.87% | -3.63% | -1.29% | -1.87% |
| 最长 DD 天 | One hundred and eighty-seven | One hundred and fifty-three | Fifteen | Twenty-five |
| 波动性(安。) | 6.81% | 4.32% | 7.46% | 4.45% |
| R^2 | Zero point zero one | Zero point zero one | Zero | Zero |
| 卡尔马尔 | -0.38 | -1.4 | Fifteen point three one | -1.61 |
| 斜交 | One point two one | Zero point two one | Zero point four one | Zero point three seven |
| 峭度 | Four point six two | Two point eight two | One point four one | Zero point one four |
| 预期每日百分比 | -0.01% | -0.01% | 0.05% | -0.01% |
| 预期每月% | -0.33% | -0.4% | 0.74% | -0.13% |
| 预期年百分比 | -2.28% | -2.77% | 1.49% | -0.25% |
| 每日风险值 | -0.72% | -0.46% | -0.72% | -0.47% |
| 预期短缺(cVaR) | -0.87% | -0.87% | -0.98% | -0.98% |
| 支付比率 | One point two five | One point eight eight | One point zero five | Two point one four |
| 利润因素 | Zero point zero eight | Zero point one five | Zero point three six | Zero point zero seven |
| 常识比率 | Zero point zero nine | Zero point one four | Zero point four four | Zero point zero eight |
| CPC 指数 | Zero point zero four | Zero point one three | Zero point two four | Zero point zero eight |
| 尾部比率 | One point one five | Zero point nine five | One point two one | One point zero nine |
| 异常胜率 | Five point eight three | Eight point eight two | Three point six six | Five point seven eight |
| 异常损失率 | Two point one eight | Three point five three | One point three one | Two point five six |
| 动目标检测 | -1.78% | 0.3% | 0.82% | 0.74% |
| 3M | 3.43% | -0.54% | 1.49% | -0.25% |
| 6M | -4.71% | -1.76% | 1.49% | -0.25% |
| 本年开始至今 | -2.28% | -2.77% | 1.49% | -0.25% |
| 1Y | -2.28% | -2.77% | 1.49% | -0.25% |
| 最好的一天 | 2.2% | 0.94% | 1.38% | 0.65% |
| 最糟糕的一天 | -1.08% | -0.94% | -0.98% | -0.5% |
| 最佳月份 | 3.9% | 2.28% | 0.82% | 0.74% |
| 最差月份 | -4.13% | -3.03% | 0.67% | -0.99% |
| 最佳年份 | -2.28% | -2.77% | 1.49% | -0.25% |
| 最糟糕的一年 | -2.28% | -2.77% | 1.49% | -0.25% |
| 平均值。减少 | -5.65% | -2.8% | -0.99% | -1.0% |
| 平均值。提款天数 | Ninety-six | Ninety-eight | eight | Thirteen |
| 回收系数 | -0.21 | -0.76 | One point one six | -0.13 |

**表 5:策略 2 黄金回溯测试总结**

|  | 金色的 |  | 样品中的黄金 |
| 开始时期 | 05/02/2019 | 05/02/2019 | 21/08/2019 | 21/08/2019 |
| 终结期 | 21/08/2019 | 21/08/2019 | 20/09/2019 | 20/09/2019 |
| 上市时间 | 64.0% | 100% | 68.0% | 100% |
|  | Two hundred and eighteen |  | Thirty-eight |  |
| 累积回报 | 36.32% | 14.25% | -8.83% | 1.08% |
| CAGR% | 77.55% | 27.99% | -67.52% | 13.95% |
| 夏普 | Two point two eight | One point five eight | -3.87 | Zero point eight |
| 索尔蒂诺 | Four point six six | Two point eight six | -4.54 | One point two one |
| 最大压降 | -8.58% | -5.54% | -11.91% | -3.68% |
| 最长 DD 天 | Ninety-seven | One hundred and thirteen | Sixteen | Fifteen |
| 波动性(安。) | 17.97% | 11.13% | 18.94% | 11.72% |
| 卡尔马尔 | Nine point zero four | Five point zero five | -5.67 | Three point seven nine |
| 斜交 | One point five seven | One point six seven | -0.07 | Zero point two seven |
| 峭度 | Five point nine seven | Nine point zero five | Zero point three five | Two point two seven |
| 预期每日百分比 | 0.16% | 0.07% | -0.3% | 0.03% |
| 预期每月% | 4.53% | 1.92% | -4.52% | 0.54% |
| 预期年百分比 | 36.32% | 14.25% | -8.83% | 1.08% |
| 每日风险值 | -1.7% | -1.08% | -2.25% | -1.18% |
| 预期短缺(cVaR) | -2.53% | -2.53% | -2.52% | -2.52% |
| 支付比率 | One point nine eight | Two point seven five | Zero point six three | One point one five |
| 利润因素 | Zero point seven | Zero point four | Zero point five three | Zero point one seven |
| 常识比率 | One point four three | Zero point five one | Zero point three nine | Zero point one six |
| CPC 指数 | Zero point seven | Zero point five six | Zero point one three | Zero point one two |
| 尾部比率 | Two point zero four | One point two nine | Zero point seven two | Zero point nine two |
| 异常胜率 | Five point eight | Eight point nine six | Four point eight | Five point seven six |
| 异常损失率 | Two point four six | Three point four nine | One point five eight | Two point six nine |
| 动目标检测 | 9.61% | 6.37% | -10.28% | -0.37% |
| 3M | 35.57% | 17.57% | -8.83% | 1.08% |
| 6M | 34.04% | 13.22% | -8.83% | 1.08% |
| 本年开始至今 | 36.32% | 14.25% | -8.83% | 1.08% |
| 1Y | 36.32% | 14.25% | -8.83% | 1.08% |
| 最好的一天 | 5.5% | 4.56% | 2.33% | 2.22% |
| 最糟糕的一天 | -3.79% | -1.69% | -2.53% | -1.75% |
| 最佳月份 | 11.62% | 8.15% | 1.61% | 1.45% |
| 最差月份 | -3.38% | -1.68% | -10.28% | -0.37% |
| 最佳年份 | 36.32% | 14.25% | -8.83% | 1.08% |
| 最糟糕的一年 | 36.32% | 14.25% | -8.83% | 1.08% |
| 平均值。减少 | -2.53% | -1.48% | -4.57% | -1.45% |
| 平均值。提款天数 | Fourteen | Fifteen | seven | six |
| 回收系数 | Four point two three | Two point five seven | -0.74 | Zero point two nine |

如果你想学习算法交易的各个方面，那就去看看算法交易的高管课程( [EPAT](https://www.quantinsti.com/) )。课程涵盖统计学&计量经济学、金融计算&技术和算法&定量交易等培训模块。EPAT 教你在算法交易中建立一个有前途的职业所需的技能。[立即报名！](https://www.quantinsti.com/epat/)

免责声明:就我们学生所知，本项目中的信息是真实和完整的。所有推荐都是学生或 QuantInsti *不做任何保证的。学生和 QuantInsti* *否认与使用这些信息有关的任何责任。本项目中提供的所有内容仅供参考，我们不保证通过使用该指南您将获得一定的利润。/海外*