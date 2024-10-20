# 在 R 中使用 Quantstrat 软件包的量化交易策略:一步一步指南

> 原文：<https://blog.quantinsti.com/quantitative-trading-strategy-using-r/>

在本帖中，我们将使用 R 构建一个[交易策略。在深入研究使用 R 的交易术语之前，让我们花一些时间来理解 R 是什么。r 是开源的。目前有超过 4000 个附加包，18000 多个 LinkedIn 群组成员和近 80 个 R Meetup 群组。这是一个完美的统计分析工具，尤其是数据分析。全面 R 档案网络的简明设置为 CRAN 提供了软件包列表以及所需的基本安装。根据需要进行的分析，有许多可用的软件包。为了实现交易策略，我们将使用名为 quantstrat 的软件包。](https://blog.quantinsti.com/how-to-design-quant-trading-strategies-using-r/)

### **任何基本交易策略的四步流程**

1.  假设形成
2.  测试
3.  改善
4.  生产

我们的假设被表述为“市场是均值回归的”。均值回归(Mean reversion)是一种理论，认为价格最终会回到平均值。第二步是测试假设，我们根据假设制定策略，并计算指标、信号和绩效指标。测试阶段可以分为三个步骤，获取数据、编写策略和分析输出。在这个例子中，我们考虑漂亮的蜜蜂。它是由高盛管理的一只 T2 交易所交易基金。NSE 具有巨大的仪器体积，因此我们考虑这一点。下图显示了相同的开盘价-最高价-最低价-收盘价。

我们设定了一个阈值来比较价格的波动。如果价格上升/下降，我们更新阈值列。收盘价与高波段和低波段进行比较。当穿过上带时，这是卖出的信号。同样，当穿越较低波段时，是买入信号。

**编码段可以概括如下，**

*   添加指标
*   添加信号
*   添加规则

下图给出了该策略输出的俯视图。

因此，我们的假设，市场是均值回复是支持的。因为这是回溯测试，所以我们有空间改进交易参数，提高我们的平均回报和实现的利润。这可以通过设置不同的阈值水平、更严格的进场规则、止损等来实现。人们可以选择更多的数据进行回溯测试，使用贝叶斯方法设置阈值，将波动性考虑在内。

一旦你对回溯测试结果支持的[交易策略](https://quantra.quantinsti.com/course/quantitative-trading-strategies-models)有信心，你就可以进入实时交易了。生产环境本身是一个很大的话题，超出了本文的范围。简单来说，这需要在一个[交易平台](https://www.quantinsti.com/category/programming-and-trading-tools/trading-platforms/)上编写策略。

如前所述，我们将使用 quantstrat 包构建模型。Quantstrat 提供了一个通用的基础架构，用于对基于信号的量化策略进行建模和回溯测试。它是一个高层次的抽象层(建立在 xts、FinancialInstrument、记事本等之上。)允许您用很少几行代码来构建和测试策略。

**quant strat 的主要特点是，**

*   支持包括指标、信号和规则的策略
*   允许将策略应用于多资产投资组合
*   支持市价、限价、止损和止损追踪订单类型
*   支持订单规模和参数优化

在这篇文章中，我们建立了一个包括指标、信号和规则的策略。

**对于一般的基于信号的模型，以下是应该考虑的对象，**

*   工具-包含市场数据
*   指标-来自市场数据的量化值
*   信号——市场数据和指标相互作用的结果
*   规则——利用市场数据、指标和信号生成订单。

事不宜迟，让我们讨论编码部分。我们更喜欢使用 R studio 进行编码，并坚持让你使用相同的。在[对策略](https://www.quantinsti.com/category/programming-and-trading-tools/python/)进行编程之前，您需要安装某些软件包。

下面一组命令安装必要的软件包。

```py
install.packages("quantstrat", repos="http://R-Forge.R-project.org")
install.packages("blotter", repos="http://R-Forge.R-project.org")
install.packages("FinancialInstrument", repos="http://R-Forge.R-project.org")
```

安装完软件包后，您可以导入它们以备将来使用。

```py
require(quantstrat)
```

从 csv 文件中读取数据并将其转换为 xts 对象。

```py
ym_xts
```

我们用股票、货币、初始权益和策略类型初始化投资组合。

```py
stock.str='NSEI' # stock we trying it on
currency('INR')
stock(stock.str,currency='INR',multiplier=1)
initEq=1000
initDate = index(NSEI[1])#should always be before/start of data
#Declare mandatory names to be used
portfolio.st='MeanRev'
account.st='MeanRev'
initPortf(portfolio.st,symbols=stock.str, initDate=initDate)
initAcct(account.st,portfolios='MeanRev', initDate=initDate)
initOrders(portfolio=portfolio.st,initDate=initDate)
```

如果你想在同一边交易不止一次，增加仓位限制。

```py
addPosLimit(portfolio.st, stock.str, initDate, 1, 1 )
```

创建策略对象。

```py
stratMR
```

我们建立一个函数来计算我们想要交易的阈值。如果价格变动超过阈值 1，我们将阈值更新为新价格。交易的新波段是阈值+/-阈值 2。输出是一个 xts 对象，尽管我们使用了重分类函数来确保。

```py
THTFunc<-function(CompTh=NSEI,Thresh=6, Thresh2=3){
numRow(tht+Thresh)){ tht<-xa[i]}
   if(xa[i]<(tht-Thresh)){ tht<-xa[i]}
   xb[i]
```

添加指标、信号和交易规则。

```py
stratMR
```

运行策略，看看订单簿。

```py
out<-try(applyStrategy(strategy=stratMR , portfolios='MeanRev') )
# look at the order book
getOrderBook('MeanRev')
end_t<-Sys.time()
```

更新投资组合并查看交易统计数据

```py
updatePortf('MeanRev', stock.str)
chart.Posn(Portfolio='MeanRev',Symbol=stock.str)
tradeStats('MeanRev', stock.str)
View(t(tradeStats('MeanRev')))
.Th2 = c(.3,.4)
.Th1 = c(.5,.6)
require(foreach)
require(doParallel)
registerDoParallel(cores=2)
stratMR<-add.distribution(stratMR,paramset.label='THTFunc',component.type= 'indicator',component.label = 'THTT',
                         variable = list(Thresh = .Th1),label = 'THTT1')
stratMR<-add.distribution(stratMR,paramset.label='THTFunc',component.type= 'indicator',component.label = 'THTT',
                         variable = list(Thresh2 = .Th2),label = 'THTT2')
results<-apply.paramset(stratMR, paramset.label='THTFunc', portfolio.st=portfolio.st, account.st=account.st, nsamples=4, verbose=TRUE)
stats
```

这是完整的代码

```py
require(quantstrat)
ym_xts (tht+Thresh)){ tht<-xa[i]}
   if(xa[i]<(tht-Thresh)){ tht<-xa[i]}
   xb[i]
```

### **下一步**

一旦你熟悉了这些基础知识，你可以看看如何在 R 中开始使用 [quantimod 包。或者如果你擅长 C++，看看用 C++](https://blog.quantinsti.com/a-guide-on-r-quantmod-package-how-to-get-started/) 编码的[策略的例子。](https://blog.quantinsti.com/an-example-of-a-trading-strategy-coded-in-c/)

如果你是一名散户交易者或专业技术人员，想要建立自己的自动化交易平台，今天就开始学习算法交易吧！从基本概念开始，如[自动交易架构](https://blog.quantinsti.com/algorithmic-trading-system-architecture/)、[市场微观结构](https://blog.quantinsti.com/market-microstructure/)、[策略回溯测试系统](https://blog.quantinsti.com/backtesting/)和[订单管理系统](https://blog.quantinsti.com/automated-trading-order-management-system/)。

*免责声明:股票市场的所有投资和交易都有风险。在金融市场进行交易的任何决定，包括股票或期权或其他金融工具的交易，都是个人决定，只能在彻底研究后做出，包括个人风险和财务评估以及在您认为必要的范围内寻求专业帮助。本文提到的交易策略或相关信息仅供参考。*