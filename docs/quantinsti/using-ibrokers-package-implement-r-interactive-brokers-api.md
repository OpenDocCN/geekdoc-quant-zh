# 使用 R: Ibrokers 交易 API 的交互式代理

> 原文：<https://blog.quantinsti.com/using-ibrokers-package-implement-r-interactive-brokers-api/>

![IBrokers - R Package for Trading with IB API](img/c28971258d003baf6a1af7de36da2799.png)

由[米林德·帕拉德卡](https://www.linkedin.com/in/milind-paradkar-b37292107/)

[Interactive Broker](https://www.google.co.in/aclk?sa=l&ai=DChcSEwjcoOS-y__ZAhWQJCsKHaXJBGYYABAAGgJzZg&sig=AOD64_2zZONyPB6qG2qL0wb6q0agbYvCcw&q=&ved=0ahUKEwis-9y-y__ZAhWLp48KHfrdDYYQ0QwIJA&adurl=)s(IB)是一家领先的美国电子经纪公司。Interactive Brokers 提供不同编程语言的 API 解决方案，如 Java。NET (C#)、C++、ActiveX 或 DDE 来构建自己的交易应用程序。除了这些编程语言，交易者还可以用 R 或 Python 在交互式代理上交易。

在我们之前的[文章](https://blog.quantinsti.com/implement-python-in-interactive-brokers-api/)中，我们介绍了刘辉博士写的 IBridgePy。 [IBridgePy](https://quantra.quantinsti.com/course/Automated-Trading-IBridgePY-Interactive-Brokers-Platform) 是一个交互式经纪人 C++ API 的包装器，允许人们使用 Python 进行交互式经纪人(IB)交易。这篇文章涵盖了网上研讨会“使用 Python 与交互式经纪人进行交易”的关键主题，该研讨会由刘辉博士主持，QuantInsti 主办。你可以点击这里观看刘辉博士网络研讨会[的录像。](https://www.youtube.com/watch?v=Cg3gejGX3Xk)

另一种被算法开发人员广泛用于数据分析、编码策略和回溯测试的流行编程语言是 R 编程。Interactive Brokers 与 QuantInsti <sup>TM</sup> 合作主办了一场网络研讨会，[“在 Interactive Brokers 上使用 R 进行交易”](https://www.youtube.com/watch?v=gdQ_svOV7kc)，该研讨会于 2017 年 3 月 2 日<sup>美国东部时间上午 10:00 举行。网上研讨会由 QuantInsti 总监 Anil Yadav 主持。Anil 还是 iRageCapital 的算法策略顾问，irage capital 是印度领先的 HFT 公司之一，他管理着一个使用 R 的交互式经纪人的股票期货投资组合。网上研讨会受到了观众的好评，它涵盖了所有相关主题，让您可以在实时市场上使用 R！您可以点击下面的下载按钮，获取网上研讨会中使用的相关 R 文件。</sup>

网上研讨会涵盖了以下主题:

*   安装 R-studio IDE
*   [I brokers 包的参考表](https://cran.r-project.org/web/packages/IBrokers/IBrokers.pdf)
*   TWS 构型
*   理解结构-回调、eWrapper、ProcessMessage
*   在 R 中查看帐户信息详细信息
*   下载 R 中的历史数据
*   在 R 控制台上打印实时数据
*   使用 R 脚本发送预定义订单
*   使用 R 脚本发送基于事件的订单

网上研讨会包括策略示例，还提到了开发人员在与 r。

这篇文章为所有的 R 程序员/爱好者、交互式经纪人的客户和想要成为交易者的人简要介绍了 IBrokers 包。

### **关于互动经纪人的 API**

在我们介绍 IBrokers 包之前，先简要介绍一下交互式代理(IB)为程序化交易提供的应用程序编程接口(API)。IB 是一家国际经纪公司，专门从事从股票到债券、期权到期货、外汇等产品的电子执行，所有这些都来自一个帐户。交易员工作站(TWS)是交互式经纪人广泛使用的桌面交易平台。Interactive Brokers 提供了几种 API 编程语言(Java、.Net，C++，ActiveX，DDE。)可用于链接到您的系统，并在您的 IB 帐户上进行交易。API 允许您通过 TWS 或 IB 网关进行连接。

1.  通过 TWS 连接要求您运行应用程序，但也允许您测试和确认您的 API 订单是否正常工作。
2.  通过 IB 网关连接允许您在没有运行大型图形用户界面(GUI)应用程序的情况下使用 API，但是不提供用于测试和确认 API 活动的界面。

### **API 的一些主要用途包括:**

1.  从 TWS 检索实时数据
2.  以编程方式执行订单(查看、修改和提交要执行的订单)
3.  访问帐户信息、连接状态。
4.  从 TWS 获得合同细节和新闻公告。

### **探索 IBrokers 包**

Jeffery Ryan 编写的 IBrokers 包是 TWS API 的纯 R 实现，它让您可以与 R 进行交互式代理交易。在本文中，我们将介绍该包中的一些重要函数。

要安装 IBrokers 包，请遵循 R 中的标准安装函数，即 install.packages()。

install.packages("IBrokers ")

### 【IBrokers 包中的一些重要函数:

#### **tws 连接功能**

此功能用于建立、检查或终止与 TWS 的连接。该函数返回一个 twsConnection 对象，供后续 TWS API 调用使用。

**举例:**

```py
# To establish a connection to TWS
tws = twsConnect()
# To check the connection to TWS
isConnected(tws)
# To disconnect 
twsDisconnect(tws)
```

#### **twsConnectionTime 函数**

此功能提供了连接到 TWS 的时间。

**举例:**

```py
library(IBrokers)
tws = twsConnect()
twsConnectionTime(tws)

[1] “20170227 10:10:38 IST”
```

#### **reqAccountUpdates 函数**

此功能用于从交互式经纪人处请求和查看账户详情。

**举例:**

```py
library(IBrokers)
tws = twsConnect()
accountInfo = reqAccountUpdates(tws)
head(accountInfo)
# [[1]]
# value       currency
# AccountCode            DU15157
# AccountOrGroup         DU15157   USD
# AccountReady           true
# AccountType            UNIVERSAL
# AccruedCash            0         USD
```

#### **tws 收缩功能**

此函数创建、测试或强制在 API 调用中使用的 twsContract。该函数返回的值是 twsContract 对象。

**举例:**

```py
contract = twsContract(0,"AAPL","STK","SMART","ISLAND", "","0.0","USD","","","",NULL,NULL,"0")
```

![](img/02e10d10689acdde58706f0f6ca8b4d0.png)

类似地，有一个 **twsCurrency** 函数，它是 twsContract 的包装器，使“货币/外汇”合约更容易指定。

#### **reqMktData 函数**

这个函数允许在 r 中处理流式市场数据。

**举例:**

```py
library(IBrokers)
tws = twsConnect()
symbol = twsSTK("AAPL")
reqMktData(tws,symbol)

```

![](img/6a9edb7dd9c2cbaa612eb917e8909e03.png)

#### **请求历史数据功能**

该函数用于从 TWS 请求历史数据。

**举例:**

```py
library(IBrokers)
tws = twsConnect(port=7497)
symbol = twsSTK("AAPL")
data_AAPL = reqHistoricalData(tws, symbol)
print (data_AAPL)

```

![](img/8f658167d4d03032ca0087d58af7b913.png)

#### **下单功能**

此功能用于向 TWS 下订单或取消订单。

**举例:**

```py
library(IBrokers)
tws = twsConnect()
id = as.numeric(reqIds(tws))
myorder = twsOrder(id, orderType="STP LMT", lmtPrice="108.01",
                   auxPrice="108.10",action="SELL",totalQuantity="10"
                   transmit=FALSE)    
placeOrder(tws, twsSTK("AAPL"), myorder))
```

![](img/655841307d2da3eff11955e261ba59ad.png)

这些是 IBrokers 包的一些关键功能。可以使用 R 中的其他统计包制定策略，然后使用 IBrokers 包中的函数通过 R 检索市场数据、查看账户信息和执行/修改订单。

***免责声明:** 互动经纪公司或其任何关联公司不以任何方式附属、认可或批准本软件。它没有任何保证，除非用户能够阅读并理解源代码，否则不应该在实际交易中使用。IBrokers 是 TWS API 的纯 R 实现。*

### **下一步**

接下来是一个[项目工作](https://blog.quantinsti.com/pair-trading-strategy-backtesting-using-quantstrat/)，解释配对交易策略和使用 Quantstrat 库的回溯测试。这个项目是由一名学生提交的，作为 QuantInsti 的算法交易培训计划(算法交易中的[执行计划)的一部分。](https://www.quantinsti.com/)

### **下载数据文件**

*   网络研讨会文件