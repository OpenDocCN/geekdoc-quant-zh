# 算法交易的基本分析

> 原文：<https://blog.quantinsti.com/fundamental-analysis-performed-algorithmic-trading/>

根据基本面制定策略的投资者与基于定量分析的交易者有很大不同。将策略建立在技术分析基础上的量化交易者能够每分钟扫描数千张图表，这些图表配有一系列指标、比率和数据点，找到适合他们的[算法交易策略](/algorithmic-trading-strategies/)的合适工具。另一方面，基本面分析是不同的。基本面不会像价格变化那样每分钟都在变化。资产负债表、损益表、存货清单、现金流量表这些东西每个季度最多提供一次。考虑到这一点，有没有一种方法可以像定量分析师分析价格-交易量运动那样分析基本面？你能自动完成这个过程并从中创造出一个算法交易策略吗？这个博客会帮你做到这一点。

## **积木！**

![algo trading in a nutshell](img/b219826f8eea955ee32521722c5825e1.png)什么是[算法交易策略](/algorithmic-trading-strategies/)？很简单，当然，有数据、策略(算法)和经纪人的 API，可以让你按照策略执行交易。现在让我们深入研究每一部分。

## **数据**

这是等式中最关键的部分。你从哪里获得一家公司的统一、结构化、准确的基本面数据，最重要的是以一种机器(算法)可以理解的格式？这里列出了一些著名的基本面数据来源，它们以数据的准确性、多样性和大量交易工具的可用性而闻名。

| 数据源 | 覆盖的市场 | 提供的数据点 | 定价 | 数据格式 | 更多信息 |
| Quandl | 主要是美国和加拿大证券。并且可以从全球(~67 个国家)市场选择证券 | 90–200 个数据点可用美国&加拿大证券。59 为全球指标 | 起价 49 美元/用户 pm，最高可达 1000 美元/用户 pm | CSV，JSON，XML | [点击这里](https://blog.quandl.com/api-for-stock-data) |
| 彭博 | 访问所有资产类别的 3500 万种工具，这些工具来自 330 多个交易所 | 关键基础数据、见解、研究报告等。 | $ 1500-$ 3000 一个月 | CSV，JSON，XML | [点击这里](https://www.bloomberg.com/professional/product/market-data/) |
| SEC.gov(埃德加) | 美国证券包括 12000 多家公司 | 各种公司形式(10Q、10K、8K、S1、F6 等。) | 自由存取，用于手动数据存取。已付(大约。1200 美元/年)用于通过第三方 API 进行算法交易 | XML，HTML，JSON | [点击这里](https://www.sec.gov/edgar/searchedgar/companysearch.html) |
| 晨星 | 全球 26000 多家公司 | 关键基础数据、见解、研究报告等。 | 定制价格，你得和他们联系 | 通过 API 和 XML | [点击这里](http://corporate.morningstar.com/us/%20asp/subject.aspx?xmlfile=8655.xml) |

此外，为了以防万一，您还可以查看以下数据源:

*   [本辛加](http://cloud.benzinga.com/)
*   [资产宏观](https://www.assetmacro.com/)
*   [Airex 市场](https://airexmarket.com/)
*   S & P 全球网络优势
*   [EventVestor](/statistical-arbitrage/)
*   [事实集](https://blog.quantinsti.com/statistical-arbitrage/)

## **需要采取的预防措施:**

因为基本面数据的本质不同于你通常的价格数据。你的[算法交易策略](/algorithmic-trading-strategies/)可能会因为不太正确的数据而做出错误的决定。例如，一些公司可能会在他们的报告中撒谎，关于他们为什么会这样做有多种原因，但最主要的是为了让他们看起来更好。这里有一些这样的例子，

1.  如果公司在报告的收益中包括应收账款。这笔钱还没有进入他们的账户，但公司认为这笔钱肯定会在某个时候到来。但对于基本面交易员来说，这可能是一个巨大的错误
2.  有时，公司会展示通过向自己的相关公司销售产品而获得的销售数字
3.  报告可能不会显示前三个季度的任何税收成分，但在最后一个季度有一个大的税收成分

这种事情在审计中出现，审计师让公司解决这些问题，但问题是重要的审计是每年进行的，你可能已经根据预审计的数据做出了交易决定。那么我们如何避免这些事情呢？你可以遵守一些基本规则:

1.  只考虑那些有准确披露数据历史的公司
2.  包括针对少量或不可靠股票的定性过滤器
3.  确保回溯测试的时间足够长
4.  在进行[回溯测试](https://blog.quantinsti.com/backtesting/)时要注意远期风险，这意味着未来可能发生的影响股票表现的事情通常不会出现在资产负债表上

## **基于基本面的交易策略示例**

现在让我们深入到一个实际的基于基本面数据的算法交易策略。我们在这方面得到了 Quantopian 的帮助。Quantopian 已经与晨星合作开发基本面数据，在你的[算法交易策略](https://blog.quantinsti.com/algorithmic-trading-strategies/)中，有超过 600 个指标可以利用。Quantopian 的专职分析师 Peter Poon 开发了一种基本面策略算法，他称之为“*一种利用基本面数据的量化价值投资策略*”。这就是这个策略的全部内容。

1.  选择不超过 15 只符合以下规则的股票:市盈率< 12, P/B < 2, ROE > 15%，市值> 1 亿美元
2.  保持选择一年，并在下一年重新进行选择

You can sign up for our ‘[Python for Trading](https://quantra.quantinsti.com/course/python-for-trading?utm_source=qiblog&utm_medium=blog&utm_campaign=qiblog)’ course that will teach (actually hand-hold you) to code your own [algorithmic trading strategy](https://blog.quantinsti.com/algorithmic-trading-strategies/). Here’s how the strategy performed during the backtest: ![backtesting strategy](img/559d91d083bf0bff66a2c7c18f42dde9.png) Performance in numbers: ![strategy backtesting performance](img/468f25e03445ed775b867fc952ad010e.png) Peter thinks the strategy results are in good agreement with the traditional value investing. The selected stocks in this [algorithmic trading strategy](https://blog.quantinsti.com/algorithmic-trading-strategies/) outperformed the market by almost twice. However, backtesting results are on paper, there are multiple factors (more in number than quantitative trading) that affect fundamentals of a company and its performance. [Developing a strategy](https://blog.quantinsti.com/5-factors-will-make-trading-strategy-work/) that includes all of them is a mammoth task. Having said that, the markets are already moving towards algorithmic trading and slowly all sorts of data are being made available in machine-readable format. For example, news, social media and economic events based feeds are prevalent today.

## **结论**

将基本面纳入算法交易策略，并让它来承担重任，这是前进的方向。这种方法提供了传统基本面交易者无法获得的新的可能性。通过我们的自学门户 [Quantra](https://quantra.quantinsti.com/courses?utm_source=qiblog&utm_medium=blog&utm_campaign=qiblog) 和我们的综合虚拟课堂课程[算法交易高管课程(EPAT)](https://www.quantinsti.com/epat/) <u>，迈出学习算法交易的第一步。</u>