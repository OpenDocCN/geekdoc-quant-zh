# 技术指标和振荡器大全（三）



# 去趋势价格振荡器（DPO）

### 目录

+   去趋势价格振荡器（DPO）

    +   介绍

    +   计算

    +   位移移动平均线

    +   DPO 衡量什么？

    +   使用 DPO

    +   位移还是不位移

    +   结论

    +   与 SharpCharts 一起使用

    +   建议的扫描

    +   进一步研究

## 介绍

去趋势价格振荡器（DPO）是一种设计用于去除价格趋势并更容易识别周期的指标。DPO 不延伸到最后一个日期，因为它是基于一个位移的移动平均线。然而，与最近的对齐并不是问题，因为 DPO 不是动量振荡器。相反，DPO 用于识别周期的高点/低点并估计周期长度。

## 计算

```py
Price {X/2 + 1} periods ago less the X-period simple moving average.

X refers to the number of periods used to calculate the Detrended Price 
Oscillator. A 20-day DPO would use a 20-day SMA that is displaced by 11 
periods {20/2 + 1 = 11}. This displacement shifts the 20-day SMA 11 days to the left, which actually puts it in the middle of the look-back 
period. The value of the 20-day SMA is then subtracted from the price
in the middle of this look-back period. In short, DPO(20) equals price
11 days ago less the 20-day SMA.  

```

## 位移移动平均线

移动平均线的位移实际上使移动平均线居中。考虑一个 20 日简单移动平均线向左偏移 11 天。在移动平均线前面有 10 天，在移动平均线上有 1 天，在移动平均线后面有 9 天。实际上，这个移动平均线处于其回顾期的中间。计算中使用的价格大约一半在右侧，一半在左侧。图表 1 显示了标普 500 ETF（SPY）的 20 日 SMA（绿色虚线）和向左偏移 11 天的 20 日 SMA（粉色线）。结束值相同（106.84），但粉色移动平均线结束于 10 月 27 日，绿色移动平均线结束于 11 月 11 日，这是图表上的最后日期。另外，请注意“居中”的移动平均线（粉色线）更接近实际价格走势。

![图表 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/8419e6c154fd8618f4c8a5b69608bd6f.jpg "图表 1")

## DPO 衡量什么？

去趋势价格振荡器（DPO）衡量过去价格和移动平均线之间的差异。请记住，DPO 本身是向左位移的。随着价格在移动平均线上下移动，指标在零线上下振荡。图表 2 显示了标普 500 ETF（SPY），其中包含一个向左位移 -11 天的 20 日移动平均线。指标窗口中显示了 20 日 DPO。请注意，当价格高于移动平均线时，DPO 为正，当价格低于移动平均线时，DPO 为负。

![图表 2](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/ddda0101523677d0228d0be781a5ac45.jpg "图表 2")

## 使用 DPO

尽管这个指标看起来像是一个经典的振荡器，但它并不是为动量信号而设计的。位移移动平均线设置在过去，这就是为什么 DPO 显示在过去的原因。即使有了这种位移，DPO 的峰值和谷值也可以用来估计周期长度。DPO 滤除了较长的趋势，专注于较短的周期。图 3 显示了纳斯达克 100 ETF（QQQQ）的 DPO（20）在指标窗口中。通过观察峰值和谷值，我们可以看到一个 20 天的周期，低点分别在九月初、十月初、十一月初和十二月初。这些低点之间大约相隔 20 天。一月初的周期被错过了。

![图表 3](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/92fec60995e6bccf644e015e6c93204b.jpg "图表 3")

## 是否位移

可以将去趋势价格振荡器（DPO）向右水平位移。如果 DPO 设置为 20，则需要 11 个周期的位移才能使其与最近的价格对齐。这个位移数字来自顶部的公式（20/2 + 1）= 11。虽然位移可能看起来是个好主意，但实际上它确实违背了这个指标的目的，即识别周期。

![图表 4](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/5f769e9237eac25d48823cf47a1a7141.jpg "图表 4")

即使有正位移，DPO 波动也与价格不太匹配。在下面的示例中，DPO（20,11）的最后一个值仍然基于 11 天前的收盘价和移动平均值。请注意，当价格在 11 天前移动到中心移动平均线以下时（橙色框），DPO 变为负值。DPO 简单地不能匹配当前的价格走势。与 DPO 不同，价格在过去 12 天一直低于 20 天 EMA。百分比价格振荡器（PPO）更适合识别超买和超卖水平。PPO(1,20,1)显示了当前价格与正常的 20 天指数移动平均线之间的百分比差异。当价格相对远离它们的 20 天 EMA 时，就会出现超买/超卖情况。

![图表 5](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/e8e908501dd600de3df7a9b5d6726160.jpg "图表 5")

## 结论

去趋势价格振荡器显示了过去价格与简单移动平均线之间的差异。与其他价格振荡器相比，DPO 不是一个动量指标。相反，它只是设计用来通过其峰值和谷值识别周期。可以通过计算峰值或谷值之间的周期数来估计周期。用户可以尝试不同的较短和较长的 DPO 设置来找到最合适的。

## 使用 SharpCharts

去趋势价格振荡器（DPO）可以在 SharpCharts 的指标列表中找到。默认参数为 20 个周期，但可以根据需要进行调整以找到周期。用户还可以添加另一个逗号分隔的参数。逗号加上一个正数会将指标向右移动。 DPO 可以放置在价格图表的上方、下方或后面。[点击这里](http://stockcharts.com/h-sc/ui?s=SPY&p=D&b=5&g=0&id=p14005429311&listNum=30&a=191188211 "http://stockcharts.com/h-sc/ui?s=SPY&p=D&b=5&g=0&id=p14005429311&listNum=30&a=191188211") 查看去趋势价格振荡器的实时示例。

![图表 6](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/9edbeafb366991f09334999d5d3c547c.jpg "图表 6")

## 建议扫描

去趋势价格振荡器不适合用于扫描，因为该指标基于偏移移动平均线。20 天的 DPO 对应于 11 天前的价格，这对于扫描来说并不实用。DPO 还基于绝对水平，这使得它难以进行比较。一支股价为 100 美元的股票的 DPO 范围将比一支股价为 20 美元的股票宽得多。谷歌在一月初的股价约为 590 美元，DPO 约为 21。英特尔在一月初的股价约为 20.5 美元，DPO 约为 0.20，这要低得多。DPO 较低是因为英特尔的股价远低于谷歌。

## 进一步研究

| **技术分析** 查尔斯·柯克帕特里克 & 朱莉·R·达尔奎斯特 |
| --- |
| ![](http://store.stockcharts.com/products/technical-analysis-the-complete-resource-for-financial-market-technicians-2nd-edition "http://store.stockcharts.com/products/technical-analysis-the-complete-resource-for-financial-market-technicians-2nd-edition") |
| ![立即购买](http://store.stockcharts.com/products/technical-analysis-the-complete-resource-for-financial-market-technicians-2nd-edition "http://store.stockcharts.com/products/technical-analysis-the-complete-resource-for-financial-market-technicians-2nd-edition") |


# 价格运动便利性 

### 目录

+   价格运动便利性

    +   介绍

    +   SharpCharts 计算

    +   解释

    +   确认其他信号

    +   结论

    +   与 SharpCharts 一起使用

    +   建议扫描

        +   EMV 上穿零线

        +   EMV 下穿零线

    +   进一步研究

## 介绍

由理查德·阿姆斯开发，Ease of Movement（EMV）是一个基于成交量的振荡器，波动在零线上下。顾名思义，它旨在衡量价格运动的“便利性”。阿姆斯创建了 等量图 来直观显示价格范围和成交量。 Ease of Movement 将等量图提升到下一个水平，通过量化价格/成交量关系，并将结果显示为振荡器。一般来说，当振荡器处于正区域时，价格相对容易上涨。相反，当振荡器处于负区域时，价格相对容易下跌。

## SharpCharts 计算

EMV 公式有三部分：移动距离、成交量和高低范围。首先，移动距离是通过比较当前周期的中点与前一周期的中点（即高加低除以二）来计算的。当当前中点高于前一中点时，移动距离为正，当当前中点低于前一中点时，移动距离为负。移动距离在下面的公式中显示为分子。

```py
Distance Moved = ((H + L)/2 - (Prior H + Prior L)/2) 

Box Ratio = ((V/100,000,000)/(H - L))

1-Period EMV = ((H + L)/2 - (Prior H + Prior L)/2) / ((V/100,000,000)/(H - L))

14-Period Ease of Movement = 14-Period simple moving average of 1-period EMV

```

另外两部分构成了盒子比率，它使用了成交量和高低范围。等量图表也是基于成交量和高低范围。盒子比率是 EMV 的分母。请注意，成交量除以 100,000,000 以保持与其他数字的相关性。

相对较低的成交量和相对较大的高低范围将产生较小的分母（盒子比率），这意味着由于除以较小的数字，EMV 值将更大。如果 V/10000000 等于 2，高低范围等于 4，则盒子比率将为 0.50。低成交量的广泛范围意味着价格变动相对容易。换句话说，价格变动不需要太多成交量。

相对较小的高低范围和高成交量将产生较大的分母，这意味着 EMV 值将较小。如果 V/10000000 等于 4，高低范围等于 2，则分母为 2。这意味着价格变动困难，因为在大成交量下高低范围相对较小。

![电子表格](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/923efc16fee7603d95555cb8cbc4b00b.jpg "电子表格")

点击这里下载这个电子表格示例。")

## 解释

下面的示例显示了纳斯达克 100 ETF（QQQ）的 1 期 EMV 在下方指标窗口中。我使用等量柱，因为这些只显示给定期间的高低范围。蓝色箭头显示了两个小的 EMV 值。一个略微为正，另一个略微为负。这两天的成交量都高于平均水平，但高低范围适中甚至较小。这意味着尽管成交量相对较高，但价格难以上涨。

![图表 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/5504f8ecce8aece6a1f68f5216fdaa78.jpg "图表 1")

红色箭头显示了一个接近-3 的 EMV 值，这是非常负面的。这是因为成交量低，而高低范围很大。这意味着价格相对轻松下跌，几乎没有买盘或没有买盘压力。绿色箭头显示了一个接近+3 的 EMV 值。同样，成交量低，而高低范围很大。这意味着价格相对轻松上涨，几乎没有卖盘或没有卖盘压力。下面的图表显示了贾比尔电路（JBL）的 14 期 Ease of Movement 指标。这只是每个周期 EMV 值的 14 期简单移动平均线。

![图表 2](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/7a2d59780336200ed696974ccc2745a5.jpg "图表 2")

## 确认其他信号

Ease of Movement 最适合用来确认其他指标或图表分析。换句话说，它不是一个独立的指标。请记住，公式中的“移动距离”部分是正面/负面的驱动因素。当中点上升时，EMV 通常为正值，当中点下降时，EMV 通常为负值。这意味着 EMV 通常会随着基础证券价格的上涨和下跌而上升和下降。这种上升或下降的幅度取决于箱体比率。图表技术分析师可以使用 EMV 来确认价格图表上的突破或看涨指标信号。相反，进入负值区域可以用来确认价格图表上的突破或看跌指标信号。

![图表 3](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/b7b50efa36b9b54b59a83de21d87a27d.jpg "图表 3")

上面的示例显示了 Mosaic（MOS）在四月初出现熊市突破和六月中旬的牛市突破。在熊市突破之前，EMV 在两个月内恶化，并在三月份跌入负值区域。随着股票在一月至二月上涨，而 EMV 下降，上涨变得更加困难。MOS 在四月初下跌并且 EMV 再次跌入负值区域时，突破支撑位。在四月和五月大部分时间为负值后，EMV 从五月底到六月初改善，并进入正值区域。股票还形成了一个小的反向头肩形态，并突破了 50 的阻力位。

![图表 4](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/dabe39fe926887604c539a45dfd84164.jpg "图表 4")

第二个示例展示了 Valero Energy（VLO）的 EMV 信号，由 RSI 和价格图表确认。从一月到三月中旬，VLO 上涨，然后在三月底扭转并突破支撑位。请注意，EMV 在二月底突破了其低点，并在三月底深入负值区域。另外，请注意，RSI 跌至自一月初以来的最低水平。第二次逆转发生在 VLO 于七月中旬突破阻力位时。EMV 在此突破前开始改善，并在突破时处于坚定的正值状态。RSI 也通过突破其四月高点和超过 55 的移动来确认。

## 结论

Ease of Movement（EMV）将价格方向与成交量结合起来，创建了一个基于成交量的动量振荡器。由于它与价格变动密切相关，EMV 往往会紧密跟踪基础证券的价格。在大多数情况下，EMV 用于确认从价格图表或其他指标得出的信号。寻找更平滑的 EMV 线的图表分析师可以延长回溯期。

## 使用 SharpCharts

Ease of Movement（EMV）可以在图表下的“指标”部分找到。用户可以通过更改“参数”框中的数字来调整设置。指标可以放置在“价格后面”、“主窗口上方”或“主窗口下方”。在将其放置在价格后面时，更改颜色会有所帮助。图表分析师还可以使用“高级”指标选项添加移动平均线。

![图表 5](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/99d464f621f03e9596d5d50e8d129b95.jpg "图表 5")

![图表 6](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/5b2d14bb19d8a5dc2951b4bd42bd601e.jpg "图表 6")

## 建议的扫描

### EMV 突破零线

这个简单的扫描搜索股票，其中 EMV 从负值区域突破到正值区域。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily EMV(14) crosses 0] 
```

### EMV 跌破零线

这个简单的扫描搜索股票，其中 EMV 从正值区域突破到负值区域。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [0 crosses Daily EMV(14)] 
```

欲了解有关轻松移动扫描的语法详情，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#ease_of_movement_emv "http://stockcharts.com/docs/doku.php?id=scans:indicators#ease_of_movement_emv")。

## 进一步研究

| **成交量利润** 理查德·W·阿姆斯 小学教授 |
| --- |
| ![](http://store.stockcharts.com/products/profits-in-volume "http://store.stockcharts.com/products/profits-in-volume") |
| ![立即购买](http://store.stockcharts.com/products/profits-in-volume "http://store.stockcharts.com/products/profits-in-volume") |

网站：理查德·W·阿姆斯 小学教授拥有一个网站，提供更多关于 EquiVolume 的信息，包括可下载的电子书：[与 EquiVolume 交易](http://www.armsinsider.com/pdf/index.asp "http://www.armsinsider.com/pdf/index.asp")。


# 力量指数

### 目录

+   力量指数

    +   介绍

    +   计算

    +   解释

    +   趋势识别

    +   背离

    +   识别修正

    +   结论

    +   使用 SharpCharts

    +   建议扫描

        +   上涨趋势中的超卖

        +   下跌趋势中的超买

    +   进一步研究

## 介绍

力量指数是一种利用价格和成交量评估动力或确定可能转折点的指标。由亚历山大·埃尔德（Alexander Elder）开发，力量指数首次出现在他的经典著作*[《交易为生计》](http://store.stockcharts.com/products/the-new-trading-for-a-living "http://store.stockcharts.com/products/the-new-trading-for-a-living")*中。根据埃尔德的说法，股价运动有三个基本要素：方向、幅度和成交量。力量指数将这三者结合为一个振荡器，随着力量平衡的转移在正负区域波动。力量指数可用于加强总体趋势，识别可玩的修正或通过背离预示反转。

## 计算

```py
Force Index(1) = {Close (current period)  -  Close (prior period)} x Volume
Force Index(13) = 13-period EMA of Force Index(1)

```

1 期力量指数的计算很简单。只需将前一收盘价减去当前收盘价，然后乘以成交量。超过一天的力量指数只是过去 13 个周期的 1 期力量指数的指数移动平均值。例如，13 期力量指数是过去 13 个周期的 1 期力量指数值的 13 期指数移动平均值。

三个因素影响力量指数的数值。首先，当当前收盘价高于前一收盘价时，力量指数为正值。当当前收盘价低于前一收盘价时，力量指数为负值。其次，移动的幅度决定了成交量的乘数。较大的移动需要较大的乘数，从而相应地影响力量指数。较小的移动产生较小的乘数，降低了影响力。第三，成交量起着关键作用。大幅度的移动伴随大量成交产生高的力量指数数值。小幅度的移动伴随低成交量产生相对较低的力量指数数值。下表显示了辉瑞（PFE）的力量指数计算。第 27 行标记了最大的移动（+84 美分）和最大的成交量（162,619）。这种组合在表中产生了最大的力量指数值（136,600）。

![表 1 - 力量指数](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/9c4788762468800e591f64172bc5418a.jpg "表 1 - 力量指数")

上图展示了力量指数的运作方式。请注意，1 周期力量指数在零线上下波动，看起来相当锯齿状。Elder 建议使用 13 周期 EMA 平滑该指标，以减少正负交叉。图表分析师应该尝试不同的平滑周期，以确定最适合其分析需求的方法。

![图表 1  -  力量指数](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/331f37ba3fd3edb0c3e155b1a4b08c6f.jpg "图表 1  -  力量指数")

## 解读

如上所述，力量指数有三个元素。首先，有正面或负面的价格变动。正面的价格变动表示买方比卖方更强势，而负面的价格变动表示卖方比买方更强势。其次，有价格变动的幅度，即当前收盘价减去前一收盘价。"幅度"向我们展示了价格移动的距离。大幅上涨显示了强劲的买盘压力，而大幅下跌显示了强劲的卖盘压力。第三个也是最后一个元素是成交量，根据 Elder 的说法，成交量衡量了参与度。买方和卖方有多么投入？大幅上涨伴随着大量成交显示了买方的强烈投入。同样，大幅下跌伴随着大量成交显示了卖方的强烈投入。力量指数将这三个元素量化为一个指标，衡量买卖双方的压力。

## 趋势识别

力量指数可用于加强或确定趋势。所讨论的趋势，无论是短期、中期还是长期，都取决于力量指数的参数。虽然默认的力量指数参数为 13，但图表分析师可以使用更高的数字进行更平滑或更低的数字进行更少平滑。下图显示了家得宝（Home Depot）的 100 天力量指数和 13 天力量指数。请注意，13 天力量指数更加波动和锯齿状。100 天力量指数更加平滑，且穿过零线的次数较少。在这方面，100 天力量指数可用于确定中期或长期趋势。请注意，价格图表上的阻力突破与 100 天力量指数上的阻力突破相对应。100 天力量指数在 2 月中旬进入正区间并突破了阻力。该指标在整个上升趋势期间保持为正，并在 5 月中旬转为负。价格图表上 6 月初的支撑突破得到了力量指数上的支撑突破的确认。

![图表 2  -  力量指数](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/a3fa63c34e6f2181f8ac88ec3550c882.jpg "图表 2  -  力量指数")

## 背离

牛市和熊市背离可以提醒图表分析师潜在的趋势变化。背离是与振荡器相关的经典信号。当指标上升而证券下跌时，形成牛市背离。指标未确认价格的弱势，这可能预示着牛市趋势反转。当指标下跌而证券上涨时，形成熊市背离。尽管证券上涨，但指标下跌显示了潜在的弱势。这种差异可能预示着熊市趋势反转。

确认是牛市和熊市背离的重要部分。尽管背离信号表明有些不对劲，但需要指标或价格图表的确认。力量指数进入正区域或价格图表上的阻力突破可以确认牛市背离。力量指数进入负区域或价格图表上的支撑突破可以确认熊市背离。图表分析师还可以使用蜡烛图、移动平均线交叉、图案突破和其他形式的技术分析进行确认。

![图表 3  -  力量指数](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/83316043828e15bad30d905ef5e4d703.jpg "图表 3  -  力量指数")

上图显示了百思买（BBY）的力量指数（39）呈现一系列背离。绿色线显示牛市背离，而红色线显示熊市背离。当力量指数（39）穿过正区域（绿色虚线）时，确认牛市背离。当力量指数（39）穿过负区域（红色虚线）时，确认熊市背离。图表分析师还可以使用价格图表上的趋势线突破进行确认。

该图显示了力量指数的两个版本。力量指数（13）捕捉短期波动，更为敏感。力量指数（39）捕捉中期波动，更为平滑。39 天的力量指数产生较少的零线交叉，这些交叉持续时间更长。对于这些设置没有对错答案。这取决于交易目标、时间跨度和分析风格。

## 识别更正

力量指数可以与趋势跟踪指标结合使用，以识别该趋势内的短期修正。从超买水平回撤代表上升趋势内的短期修正。超卖反弹代表下降趋势内的短期修正。是的，修正可以向上或向下，这取决于更大趋势的方向。亚历山大·埃尔德建议使用 22 天 EMA 进行趋势识别，使用 2 天力量指数来识别修正。当 22 天 EMA 上升时，趋势是向上的，这意味着 2 天力量指数将用于识别买入的短期回撤。当 22 天 EMA 下降时，趋势是向下的，这意味着 2 天力量指数将用于识别卖出的短期反弹。这是一种适合积极交易者的激进策略。时间框架可以通过使用更长的移动平均线和力量指数的时间框架进行调整。例如，中期交易者可以尝试使用 100 天 EMA 和 10 天力量指数。

关于修正操作有两种思路。交易者可以在修正明显时立即行动，或者在有证据表明修正已结束时行动。让我们看一个使用 22 天 EMA 和 2 天力量指数的例子。请记住，这是设计用来识别更大趋势内非常短暂修正的。下面的图表显示了德州仪器（TXN）的 22 天 EMA 在 9 月中旬开始上升。

![图表 4 - 力量指数](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/78bd9f42e29733834512ed4370bbf434.jpg "图表 4 - 力量指数")

随着 22 天 EMA 上升，交易者在 2 天力量指数转为负数时寻找非常短期的回撤。交易者可以在力量指数转为负数时行动，或者等待其回到正数区域。在负数时行动可能会提高回报风险比，但修正可能会延长几天。等待力量指数再次转为正数显示出一些可能表明修正已结束的强势。绿色虚线显示了 2 天力量指数转为负数时的情况。

## 结论

力度指数同时使用价格和成交量来衡量买卖压力。价格部分涵盖趋势，而成交量部分确定强度。在最基本的情况下，技术分析师可以使用长期力度指数来确认基本趋势。当 100 天力度指数为正时，多头占优势。当 100 天力度指数为负时，空头占优势。有了这些信息，交易者可以寻找与更大趋势一致的短期设置，例如在更大的上升趋势中的多头设置或在更大的下降趋势中的空头设置。与所有指标一样，交易者应该将力度指数与其他指标和分析技术结合使用。

## 与 SharpCharts 一起使用

力度指数可作为 SharpCharts 的指标。一旦选择，用户可以将指标放置在基础价格图表的上方、下方或后方。将力度指数直接放在价格图表的顶部，可以突出相对于基础证券价格走势的波动。这可以更容易地识别多头和空头背离。技术分析师可以点击“高级选项”添加移动平均线、水平线或另一个指标到力度指数上。

![图表 5  -  力度指数](http://stockcharts.com/h-sc/ui?s=MSFT&p=D&yr=1&mn=0&dy=0&id=p81333023268&listNum=30&a=219526357 "http://stockcharts.com/h-sc/ui?s=MSFT&p=D&yr=1&mn=0&dy=0&id=p81333023268&listNum=30&a=219526357")

![SharpCharts  -  力度指数](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/3a417a568f0a13488f1a48e528715220.jpg "SharpCharts  -  力度指数")

## 建议的扫描

### 在上升趋势中被过度推销

此扫描搜索力度指数（100）处于正值区域且商品通道指数（20）处于超卖状态的股票。正值的力度指数确立了总体上升趋势。超卖的 CCI 标识了该上升趋势中的回调。此扫描仅作为一个起点。建议进一步审查和调整。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily FORCE(100) > 0] 
AND [Daily CCI(20) < -100]
```

### 在下降趋势中被过度买入

此扫描搜索力度指数（100）处于负值区域且商品通道指数（20）处于超买状态的股票。负值的力度指数确立了总体下跌趋势。超买的 CCI 标识了该下跌趋势中的修正反弹。此扫描仅作为一个起点。建议进一步审查和调整。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily FORCE(100) < 0] 
AND [Daily CCI(20) > 100]
```

有关力度指数扫描的语法详细信息，请参阅我们支持中心的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#force_index_force "http://stockcharts.com/docs/doku.php?id=scans:indicators#force_index_force")。

## 进一步研究

*走进我的交易室* 涵盖了从 A 到 Z 的交易内容。除了技术分析和交易系统外，读者还将学习交易心理学、风险控制、资金管理和记录保持。

| **走进我的交易室** 亚历山大·埃尔德 |
| --- |
| ![](http://store.stockcharts.com/products/come-into-my-trading-room-a-complete-guide-to-trading "http://store.stockcharts.com/products/come-into-my-trading-room-a-complete-guide-to-trading") |
| ![立即购买](http://store.stockcharts.com/products/come-into-my-trading-room-a-complete-guide-to-trading "http://store.stockcharts.com/products/come-into-my-trading-room-a-complete-guide-to-trading") |


# 质量指数 

### 目录

+   质量指数

    +   介绍

    +   SharpCharts 计算

    +   信号

    +   微调

    +   结论

    +   与 SharpCharts 结合使用

    +   建议扫描

        +   质量指数看涨反转

        +   质量指数看跌反转

    +   进一步研究

## 介绍

由唐纳德·多尔西（Donald Dorsey）开发，质量指数（Mass Index）利用高低范围来识别基于范围扩展的趋势反转。在这个意义上，质量指数是一个没有方向偏见的波动性指标。相反，质量指数识别可以预示当前趋势反转的范围膨胀。

## SharpCharts 计算

质量指数计算涉及四个部分：

```py
Single EMA = 9-period exponential moving average (EMA) of the high-low differential  

Double EMA = 9-period EMA of the 9-period EMA of the high-low differential 

EMA Ratio = Single EMA divided by Double EMA 

Mass Index = 25-period sum of the EMA Ratio 

```

![图表 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/4886b2591c4631833238106b2ba83c6c.jpg "图表 1")

计算相当简单。首先，单一 EMA 提供高低范围的平均值。其次，双重 EMA 对这种波动性指标进行第二次平滑。使用这两个指数移动平均数的比率对数据系列进行归一化。这个比率显示单一 EMA 相对于双重 EMA 变大的时候。最后一步，25 期总和，类似于移动平均线，进一步平滑数据系列。总的来说，随着高低范围的扩大，质量指数上升，随着高低范围的缩小，质量指数下降。下面展示了一个电子表格示例。

![电子表格 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/3e4307932289d84bc8164a84c6a7954d.jpg "电子表格 1")

一些电子表格数值有一分钱的偏差，因为指数移动平均计算的时间跨度不到三个月。SharpCharts 中的计算时间跨度为两年，这使指数移动平均计算更加稳健。点击这里下载这个电子表格示例。")

## 信号

唐纳德·多尔西寻找“反转膨胀”来发出趋势反转信号。根据多尔西的说法，当质量指数上升至 27 以上时会出现膨胀。然而，这种初始膨胀并不完成信号。多尔西等待这种膨胀反转，回落至 26.50 以下。一旦反转膨胀完成，交易者应该使用其他分析技术来确定下一步走势的方向。理想情况下，下跌趋势后出现反转膨胀将暗示看涨趋势反转。相反，上涨趋势后出现反转膨胀将暗示看跌趋势反转。

![图表 2](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/df48c1a6a50b160c0af3f138e2a3c813.jpg "图表 2")

上面的例子显示了 Chipotle 在 12 个月内质量指数产生两次逆转突出。在这两种情况下，当质量指数超过 27 时，趋势是向上的，这意味着预期看跌逆转。第一个信号预示着一个交易范围。第二个信号预示着急剧下降。寻找信号的图表分析师很可能需要放宽多尔西对逆转突出的要求，因为质量指数很少超过 27。需要异常波动才能将指数推至这个水平。

## 调整

图表分析师可以降低逆转突出的阈值以生成更多信号。波动性并非一刀切。换句话说，图表分析师可能需要比较一段时间内的质量指数水平，以识别历史高点和低点。接近历史范围高端的移动将表明波动性突出，可能预示着逆转。

下图显示了国际纸业的质量指数两次上升至 26 以上。尽管质量指数在 2011 年 8 月触及 27，但 26 水平似乎更适合作为逆转突出。还要记住，2011 年 8 月对整个股市来说是一个极端波动的时期，这个读数看起来像是一个异常值。当质量指数在 2011 年 8 月和 2012 年 5 月上升至 26 以上时，趋势是向下的，这表明随后会出现看涨逆转，图表分析师可以使用其他分析技术来识别这种逆转。

![图表 3](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/b668d2f65bdb4e14702dfb3112f53dfb.jpg "图表 3")

底部指标是 TRIX 振荡器，它是三次平滑指数移动平均的一期变化率。TRIX 类似于 MACD 的平滑版本。一旦逆转突出出现并建立了交易偏向，图表分析师可以使用 TRIX 生成方向信号。由于这些逆转突出发生时趋势向下，交易偏向是看涨的，只有看涨信号被考虑。绿色箭头显示了当 TRIX 移动超过其信号线以示价格上涨时。

## 结论

质量指数利用高低差异提供平滑的波动率测量。该指标通常在中 20 左右波动。接近历史范围高端的读数表明波动性增加，这增加了趋势逆转的可能性。尽管多尔西将突出阈值设定为 27，但图表分析师应考虑降低阈值以产生更多信号。请记住，质量指数没有方向偏见。方向偏见取决于现有趋势。与所有指标一样，图表分析师应使用其他分析技术来补充质量指数。

## 使用 SharpCharts

质量指数可以在图表下的“指标”部分找到。用户可以通过更改“参数”框中的数字来调整总结期。然后，指标可以被定位在“价格后面”、“主窗口上方”或“主窗口下方”。图表分析师可以使用“高级”选项添加水平线。这条线可用于设置反转膨胀信号的阈值。[点击这里查看实时示例](http://scharts.co/Rz7CZ1 "http://scharts.co/Rz7CZ1")。

![图表 4](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/96380e6c360c34942e3dadd240c28fb6.jpg "图表 4")

![SharpCharts](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/a0d33c33f1bf56a413179e5e95475ec3.jpg "SharpCharts")

## 建议扫描

### 质量指数看涨反转

此扫描搜索交易价格低于其 200 日移动平均线以定义长期下降趋势的股票。当质量指数移动到 26.5 以下时，将识别出看涨反转。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily Close < Daily SMA(200,Daily Close)] 
AND [26.5 x Daily MASS(25)] 
```

### 质量指数看跌反转

此扫描搜索交易价格高于其 200 日移动平均线以定义长期上升趋势的股票。当质量指数移动到 26.5 以下时，将识别出看跌反转。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily Close > Daily SMA(200,Daily Close)] 
AND [26.5 x Daily MASS(25)] 
```

有关用于质量指数扫描的语法的更多详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#mass_index_mass "http://stockcharts.com/docs/doku.php?id=scans:indicators#mass_index_mass")在支持中心。

## 进一步学习

这本书详细介绍了对任何交易员或投资者成功至关重要的 16 种简单而有效的策略。读者将学习振荡器技术、均值回归策略，甚至看到经过回测的结果。

| **短期交易策略** 拉里·康纳斯和塞萨尔·阿尔瓦雷斯 |
| --- |
| ![](http://store.stockcharts.com/products/short-term-trading-strategies-that-work "http://store.stockcharts.com/products/short-term-trading-strategies-that-work") |
| ![立即购买](http://store.stockcharts.com/products/short-term-trading-strategies-that-work "http://store.stockcharts.com/products/short-term-trading-strategies-that-work") |


# MACD（移动平均线收敛/发散振荡器）

### 目录

+   MACD（移动平均线收敛/发散振荡器）

    +   介绍

    +   计算

    +   解释

    +   信号线交叉

    +   中线交叉

    +   背离

    +   结论

    +   与 SharpCharts 一起使用

    +   建议的扫描

        +   MACD 看涨信号线交叉

        +   MACD 看跌信号线交叉

    +   进一步研究：

    +   额外资源

        +   股票与商品杂志文章

## 介绍

由杰拉尔德·阿普尔在七十年代末开发的移动平均线收敛/发散振荡器（MACD）是目前最简单和最有效的动量指标之一。MACD 通过从较长的移动平均线中减去较短的移动平均线，将两个趋势跟踪指标移动平均线转化为动量振荡器。因此，MACD 提供了趋势跟踪和动量的最佳结合。MACD 在零线上下波动，因为移动平均线收敛、交叉和发散。交易者可以寻找信号线交叉、中线交叉和背离来生成信号。由于 MACD 没有上下限，因此不太适用于识别超买和超卖水平。

注意：MACD 可以发音为“Mac-Dee”或“M-A-C-D”。

这里是一个示例图表，其中 MACD 指标显示在下方面板中：

![](http://stockcharts.com/h-sc/ui?s=QQQ&p=D&st=2009-01-01&en=2009-04-03&id=p70644026533&a=206516339 "http://stockcharts.com/h-sc/ui?s=QQQ&p=D&st=2009-01-01&en=2009-04-03&id=p70644026533&a=206516339")

点击图表查看实时示例。

## 计算

```py
MACD Line: (12-day EMA - 26-day EMA)

Signal Line: 9-day EMA of MACD Line

MACD Histogram: MACD Line - Signal Line

```

MACD 线是 12 天的指数移动平均线（EMA）减去 26 天的 EMA。这些移动平均线使用收盘价。MACD 线的 9 天 EMA 与指标一起绘制，作为信号线并识别转折点。MACD 柱状图表示 MACD 与其 9 天 EMA（信号线）之间的差异。当 MACD 线高于其信号线时，柱状图为正，当 MACD 线低于其信号线时，柱状图为负。

**12、26 和 9**这些数值是 MACD 中典型的设置，然而根据您的交易风格和目标，可以替换其他数值。

## 解释

正如其名称所示，MACD 主要关注两个移动平均线的收敛和分歧。当移动平均线彼此靠近时，就会出现收敛。当移动平均线彼此远离时，就会出现分歧。较短的移动平均线（12 天）更快，负责大部分 MACD 运动。较长的移动平均线（26 天）更慢，对基础证券价格变化反应较弱。

MACD 线在零线上下振荡，也被称为中心线。这些交叉信号表明 12 天 EMA 已经穿过了 26 天 EMA。当然，方向取决于移动平均线的方向。正 MACD 表示 12 天 EMA 高于 26 天 EMA。随着较短 EMA 进一步偏离较长 EMA，正值增加。**这意味着上涨动能正在增加。** 负 MACD 值表示 12 天 EMA 低于 26 天 EMA。随着较短 EMA 进一步偏离较长 EMA，负值增加。**这意味着下行动能正在增加。**

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/6470e8080db2c48f6cc0fffa1b79d642.jpg)

在上面的示例中，黄色区域显示了 MACD 线在负值区域，因为 12 天 EMA 低于 26 天 EMA。最初的交叉发生在九月底（黑色箭头），随着 12 天 EMA 进一步偏离 26 天 EMA，MACD 进一步进入负值区域。橙色区域突出显示了一段正 MACD 值的时期，即 12 天 EMA 高于 26 天 EMA。请注意，在此期间 MACD 线保持在 1 以下（红色虚线）。这意味着 12 天 EMA 和 26 天 EMA 之间的距离小于 1 点，这并不是一个很大的差异。

## 信号线交叉

信号线交叉是最常见的 MACD 信号。信号线是 MACD 线的 9 天 EMA。作为指标的移动平均线，它追踪 MACD 并更容易发现 MACD 转折点。当 MACD 向上转折并穿过信号线时，就会出现看涨交叉。当 MACD 向下转折并穿过信号线时，就会出现看跌交叉。交叉可能持续几天或几周，这完全取决于行情的强度。

在依赖这些常见信号之前需要进行尽职调查。在正负极端处的信号线交叉应该谨慎对待。尽管 MACD 没有上限和下限，但图表分析师可以通过简单的视觉评估来估计历史极端值。基础证券的强劲波动会增加交叉的数量。

下面的图表显示了 IBM 及其 12 日 EMA（绿色）、26 日 EMA（红色）和指标窗口中的 12,26,9 MACD。在六个月内有八次信号线交叉：四次上穿和四次下穿。有一些好的信号和一些坏的信号。黄色区域突出显示了 MACD 线在 2 以上激增达到正极端的时期。四月和五月出现了两次看跌的信号线交叉，但 IBM 继续上涨。尽管在激增后上涨动能减缓，但四月至五月的上涨动能仍然强于下行动能。五月的第三次看跌信号线交叉产生了一个良好的信号。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/260b097fff49af332eaa75a0d4888e42.jpg)

## 中轴线交叉

中轴线交叉是 MACD 信号中次常见的信号。当 MACD 线上穿零线变为正数时，就会出现看涨的中轴线交叉。这发生在基础证券的 12 日 EMA 上穿 26 日 EMA 时。当 MACD 下穿零线变为负数时，就会出现看跌的中轴线交叉。这发生在 12 日 EMA 下穿 26 日 EMA 时。

中轴线交叉可能持续几天或几个月。这完全取决于趋势的强度。只要有持续的上升趋势，MACD 就会保持正数。只要有持续的下降趋势，MACD 就会保持负数。下一个图表显示了普尔特房屋（PHM）在九个月内至少有四次中轴线交叉。由于这些中轴线交叉出现时出现了强劲的趋势，所以产生的信号效果很好。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/ef9768c2efe25ccc7f8d90fa8266cb74.jpg)

下面是康明斯公司（CMI）的图表，显示了五个月内七次中轴线交叉。与普尔特房屋不同，这些信号会导致许多震荡，因为在交叉后没有出现强劲的趋势。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/bb6bd2ca07b145df99225c34a8a666fa.jpg)

下一个图表显示了 3M（MMM）在 2009 年 3 月底出现了一个看涨的中轴线交叉，而在 2010 年 2 月初出现了一个看跌的中轴线交叉。这个信号持续了 10 个月。换句话说，12 日 EMA 在 10 个月内一直高于 26 日 EMA。这是一个强劲的趋势。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/7d8ae0da668d16533117ffb7520a2bb6.jpg)

## 分歧

分歧是指 MACD 与基础证券的价格走势出现分歧。当一项证券记录了更低的低点，而 MACD 形成了更高的低点时，就形成了看涨的分歧。证券的更低低点确认了当前的下跌趋势，但 MACD 的更高低点显示出更少的下跌动量。尽管下跌动量较小，但只要 MACD 保持在负值区域，下跌动量仍然超过上涨动量。减缓的下跌动量有时可能预示着趋势反转或大幅上涨。

下图显示了 2008 年 10 月至 11 月间谷歌（GOOG）的看涨分歧。首先，请注意我们使用收盘价来识别分歧。MACD 的移动平均线是基于收盘价的，我们也应该考虑证券的收盘价。其次，请注意在 10 月和 11 月底，谷歌和其 MACD 线都反弹时，都有明显的反应低点（低谷）。第三，请注意在 11 月份，随着谷歌形成更低的低点，MACD 形成了更高的低点。MACD 在 12 月初形成了一个看涨分歧，并通过信号线交叉确认了一次反转。谷歌通过突破阻力线确认了一次反转。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/6c395a340095fde1f1d9309082940cfb.jpg)

当一项证券记录了更高的高点，而 MACD 线形成了更低的高点时，就形成了看跌的分歧。证券的更高高点对于上涨趋势是正常的，但 MACD 的更低高点显示出更少的上涨动量。尽管上涨动量可能较小，但只要 MACD 是正的，上涨动量仍然超过下跌动量。逐渐减弱的上涨动量有时可能预示着趋势反转或大幅下跌。

在下图中，我们看到 Gamestop（GME）从 8 月至 10 月出现了一个大的看跌分歧。股票在 28 以上形成了更高的高点，但 MACD 线未达到先前的高点，并形成了更低的高点。随后的信号线交叉和 MACD 的支撑线突破是看跌的。在价格图表上，请注意在 11 月的回调反弹中，破裂的支撑线变成了阻力（红色虚线）。这次回调提供了第二次卖出或卖空的机会。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/bfc211a32cb951ad168c3f5874da1976.jpg)

分歧应该谨慎对待。在强劲的上涨趋势中，看跌的分歧很常见，而在强劲的下跌趋势中，看涨的分歧经常发生。是的，你没看错。上涨趋势通常以强劲的上涨开始，产生了上涨动量（MACD）的激增。尽管上涨趋势持续，但它的速度变慢，导致 MACD 从高点下降。上涨动量可能不那么强劲，但只要 MACD 线在零线以上，上涨动量仍然超过下跌动量。相反，在强劲下跌趋势开始时会发生相反的情况。

下图显示了标普 500 ETF（SPY）从 2009 年 8 月至 11 月出现的四次看跌背离。尽管上涨动量较小，但由于上涨趋势强劲，ETF 仍然继续上涨。请注意 SPY 如何继续保持较高高点和较低低点的系列。请记住，只要 MACD 为正值，上涨动量就比下跌动量强。随着上涨的延伸，其 MACD（动量）可能不那么积极（强劲），但仍然主要为正值。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/83e5b1f65e9c877cd1a3c88b597eb9a8.jpg)

## 结论

MACD 指标很特殊，因为它将动量和趋势结合在一个指标中。这种趋势和动量的独特融合可以应用于日线、周线或月线图表。MACD 的标准设置是 12 和 26 期 EMA 之间的差值。寻找更敏感性的图表分析师可以尝试更短的短期移动平均线和更长的长期移动平均线。MACD(5,35,5) 比 MACD(12,26,9) 更敏感，可能更适合周线图表。寻找更少敏感性的图表分析师可以考虑延长移动平均线。较不敏感的 MACD 仍会在零线上下波动，但中线交叉和信号线交叉会更少。

MACD 不是特别适用于识别超买和超卖水平。尽管可能识别出历史上超买或超卖的水平，但 MACD 没有任何上限或下限来限制其运动。在剧烈波动期间，MACD 可能会继续超出其历史极限。

最后，请记住，MACD 线是使用两个移动平均线的实际差值计算的。这意味着 MACD 值取决于基础证券的价格。一只 $20 的股票的 MACD 值可能在 -1.5 到 1.5 之间波动，而一只 $100 的股票的 MACD 值可能在 -10 到 +10 之间波动。不可能比较具有不同价格的一组证券的 MACD 值。如果要比较动量读数，应该使用百分比价格振荡器（PPO）而不是 MACD。

## 使用 SharpCharts

MACD 可以设置为在证券价格图上方、下方或后方的指标。将 MACD 放在价格图的“后方”可以方便地比较动量运动和价格运动。一旦从下拉菜单中选择指标，就会出现默认参数设置：(12,26,9)。这些参数可以调整以增加或减少灵敏度。MACD 柱状图会随指标一起显示，或者可以作为单独的指标添加。将信号线设置为 1 或留空，即 (12,26,1) 或 (12,26)，将删除 MACD 柱状图和信号线。可以通过从高级选项叠加菜单中选择“Exp. Moving Avg”来添加单独的信号线，而不带柱状图。

[点击这里](http://stockcharts.com/h-sc/ui?s=$INDU&p=D&b=5&g=0&id=p18754900449&listNum=30&a=199515976 "http://stockcharts.com/h-sc/ui?s=$INDU&p=D&b=5&g=0&id=p18754900449&listNum=30&a=199515976") 查看 MACD 指标的实时图表。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/1494f28ca800b8667187ec60de2c6f29.jpg)

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/71629e069342fd509cdea8278bfff443.jpg)

## 建议的扫描

这里有一些股票图表会员可以用来扫描各种 MACD 信号的示例扫描：

### MACD 多头信号线交叉

这个扫描显示出那些交易高于它们的 200 日移动平均线并且在 MACD 中有一个多头信号线交叉的股票。还要注意，MACD 必须为负以确保这种上升发生在回调之后。这个扫描只是作为进一步细化的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily Close > Daily SMA(200,Daily Close)] 
AND [Yesterday's Daily MACD Line(12,26,9,Daily Close) < Daily MACD Signal(12,26,9,Daily Close)] 
AND [Daily MACD Line(12,26,9,Daily Close) > Daily MACD Signal(12,26,9,Daily Close)] 
AND [Daily MACD Line(12,26,9,Daily Close) < 0]
```

### MACD 空头信号线交叉

这个扫描显示出那些交易低于它们的 200 日移动平均线并且在 MACD 中有一个空头信号线交叉的股票。还要注意，MACD 必须为正以确保这种下降发生在反弹之后。这个扫描只是作为进一步细化的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily Close < Daily SMA(200,Daily Close)] 
AND [Yesterday's Daily MACD Line(12,26,9,Daily Close) > Daily MACD Signal(12,26,9,Daily Close)] 
AND [Daily MACD Line(12,26,9,Daily Close) < Daily MACD Signal(12,26,9,Daily Close)] 
AND [Daily MACD Line(12,26,9,Daily Close) > 0]
```

有关用于 MACD 扫描的语法的更多详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#moving_average_convergence-divergence_macd "http://stockcharts.com/docs/doku.php?id=scans:indicators#moving_average_convergence-divergence_macd")在支持中心。

## 进一步研究：

从创作者那里，这本书提供了一个全面的研究，用于使用和解释 MACD。

| **技术分析 - 积极投资者的强大工具** 杰拉德·阿普尔 |
| --- |
| ![](http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors "http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors") |
| ![buynowbuttone.jpg](http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors "http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors") |

* * *

## 其他资源

### 股票与商品杂志文章

**[移动平均线收敛/发散（MACD）by 汤姆·哈特尔](http://stockcharts.com/h-mem/tascredirect.html?artid=\V09\C03\MACD.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V09\C03\MACD.pdf")**

1991 年 2 月 - 股票与商品 V. 9:3 (104-104)

**[马克·瓦库尔的移动平均线收敛/发散](http://stockcharts.com/h-mem/tascredirect.html?artid=\V15\C04\THEMOVI.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V15\C04\THEMOVI.pdf")**

1997 年 3 月 - 股票与商品


# MACD-Histogram 

### 目录

+   MACD-Histogram

    +   介绍

    +   计算

    +   去除的四个步骤

    +   解释

    +   峰谷分歧

    +   倾斜分歧

    +   结论

    +   与 SharpCharts 一起使用

    +   建议的扫描

        +   MACD-Histogram 转为正数

        +   MACD-Histogram 转为负数

    +   进一步研究

## 介绍

由 Thomas Aspray 于 1986 年开发，MACD-Histogram 衡量了 MACD 与其信号线（MACD 的 9 日 EMA）之间的距离。与 MACD 一样，MACD-Histogram 也是一个在零线上下波动的振荡器。Aspray 开发了 MACD-Histogram 来预测 MACD 中的信号线交叉。因为 MACD 使用移动平均线，而移动平均线滞后于价格，信号线交叉可能会来得晚，并影响交易的风险收益比。MACD-Histogram 中的多头或空头分歧可以提醒图表分析师即将发生的 MACD 中的信号线交叉。查看我们的 ChartSchool 文章了解更多关于 MACD 的信息。

## 计算

```py
MACD: (12-day EMA - 26-day EMA) 

Signal Line: 9-day EMA of MACD

MACD Histogram: MACD - Signal Line

```

标准 MACD 是 12 日指数移动平均线（EMA）减去 26 日 EMA。收盘价用于形成移动平均线，因此 MACD。MACD 的 9 日 EMA 被绘制在旁边，作为一个信号线，用于识别指标的转折点。MACD-Histogram 代表 MACD 和其 9 日 EMA 信号线之间的差异。当 MACD 高于其 9 日 EMA 时，直方图为正，当 MACD 低于其 9 日 EMA 时，直方图为负。

![MACD - 示例](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/3ce03c762d1297743e8a8026a569b750.jpg "MACD - 示例")

## 去除的四个步骤

MACD-Histogram 是一个指标的指标。事实上，MACD 也是一个指标的指标。这意味着 MACD-Histogram 与基础证券价格相隔四个步骤。换句话说，它是价格的第四导数。

+   第一导数：12 日 EMA 和 26 日 EMA

+   第二导数：MACD（12 日 EMA 减去 26 日 EMA）

+   第三导数：MACD 信号线（MACD 的 9 日 EMA）

+   第四导数：MACD-Histogram（MACD 减去 MACD 信号线）

该指标的基础是证券的价格。从实际价格到 MACD-Histogram 需要四个步骤。谈论数据的处理。虽然这不一定是坏事，但图表分析师在分析 MACD-Histogram 时应牢记这一点。这是一个指标的指标。因此，它旨在预测 MACD 中的信号，而 MACD 又旨在识别基础证券价格的变化动量。

## 解释

与 MACD 一样，MACD-Histogram 也旨在识别收敛、背离和交叉。然而，MACD-Histogram 是测量 MACD 与其信号线之间的距离。当 MACD 高于其信号线时，直方图为正值。随着 MACD 进一步背离其信号线（向上），正值增加。当 MACD 和其信号线收敛时，正值减少。当 MACD 穿过零线时，MACD-Histogram 为负值。当 MACD 低于其信号线时，指标为负值。随着 MACD 进一步背离其信号线（向下），负值增加。相反，当 MACD 收敛于其信号线时，负值减少。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/02bb64289386dab91b16988721b2b986.jpg)

图表 1 显示了 Darden Restaurants (DRI)的 MACD 和 MACD-Histogram。在 9 月底发生了一个空头信号线交叉，这使得 MACD-Histogram 变为负值。在 12 月初发生了一个多头信号线交叉，这使得 MACD-Histogram 在该月的其余时间内为正值。随着 MACD 进一步远离其信号线（绿线），出现了背离期和随着 MACD 接近其信号线（红线）的收敛期。

## 峰谷背离

MACD-Histogram 通过形成牛市和熊市背离来预测 MACD 中的信号线交叉。这些背离信号表明 MACD 正在收敛于其信号线，并可能准备交叉。有两种类型的背离：峰谷和斜线。峰谷背离在 MACD-Histogram 中形成两个峰值或两个谷值。当 MACD 形成一个较低低点，而 MACD-Histogram 形成一个较高低点时，就形成了峰谷牛市背离。明确定义的谷值对于峰谷背离的稳健性至关重要。图表 2 显示了卡特彼勒（Caterpillar）MACD-Histogram 中的一个牛市背离。请注意，MACD 在 6 月至 7 月间走到了一个较低低点，但 MACD-Histogram 形成了一个较高低点（谷值）。有两个明显的谷值。这种牛市背离预示了 7 月中旬的多头信号线交叉和一次大涨。 

![MACD-Histogram - 图表 2](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/ab246bbc508d9cc394d43a23a5b751bf.jpg "MACD-Histogram - 图表 2")

图表 3 显示 Aeropostale（ARO）在 2009 年 8 月至 9 月出现了看跌背离。MACD 在 9 月达到新高，但 MACD-Histogram 形成了一个较低的高点。请注意，MACD-Histogram（红线）上有两个明确的峰值（更高），中间有一个低点。随后的看跌信号线交叉预示了股票的急剧下跌。

![MACD-Histogram - 图表 3](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/256f789aa3f3eda786387925dc8466ac.jpg "MACD-Histogram - 图表 3")

## 倾斜背离

正如其名称所示，倾斜背离形成时没有明确定义的峰值或谷值。与两个反应高点不同，MACD-Histogram 只是向零线倾斜。这种朝零线倾斜反映了 MACD 和其信号线之间的收敛。换句话说，它们彼此越来越接近。当 MACD 远离其信号线并且 MACD-Histogram 扩大时，动量显示出强劲。当 MACD 靠近其信号线并且 MACD-Histogram 收缩时，动量减弱。收缩的 MACD-Histogram 是信号线交叉的第一步。

图表 4 显示波音（Boeing）在 MACD-Histogram 中出现了经典的倾斜背离。在 2009 年 6 月的空头信号线交叉后，MACD 迅速下降。MACD 在 7 月中旬达到新低，但 MACD-Histogram 保持远高于先前的低点。事实上，MACD-Histogram 在 6 月底触底并形成了一种看涨的倾斜背离。粗红线显示了 MACD 与其信号线之间的距离。有时在图表上很难判断距离，因此这些线突出了 6 月 26 日和 7 月 8 日之间的差异。这种倾斜背离预示了 7 月中旬的看涨信号线交叉和股票的急剧上涨。

![MACD-Histogram - 图表 4](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/0656008c452b2a376f0abef254989b97.jpg "MACD-Histogram - 图表 4")

图表 5 显示迪士尼（Disney）在 2008 年 5 月出现了看跌的倾斜背离。请注意，MACD 在 5 月 16 日继续达到新高，但 MACD-Histogram 在 5 月 8 日达到峰值并形成了倾斜背离。MACD 的上涨动能减弱，指标移动到其信号线下方，预示股票的急剧下跌。这张图表还显示了 3 月至 4 月间的一个不错的看涨背离。

![MACD-Histogram - 图表 5](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/240251697f522a74972a0bb308390ed7.jpg "MACD-Histogram - 图表 5")

## 结论

MACD-Histogram 是一个旨在预测 MACD 信号线交叉的指标。通过延伸，它被设计为这些信号线交叉的早期警报系统，这些信号线交叉是 MACD 信号中最频繁的。MACD-Histogram 中的背离可用于过滤信号线交叉，从而减少信号数量。即使有过滤器，MACD-Histogram 背离的稳健性仍然是一个问题。短而浅的背离比长而大的背离更常见。换句话说，几天内发展出浅动作的背离通常比几周内发展出更明显动作的背离不够稳健。信号线交叉提供了最终确认，但积极的交易者可能会尝试在交叉之前通过使自己的动作尽可能接近零线来改善回报风险比。这通常发生在 -.20 和 +.20 之间的 MACD-Histogram。

## 使用 SharpCharts

MACD 包含 MACD-Histogram，但是 MACD-Histogram 可以作为独立指标显示。这样更容易识别背离和交叉点。MACD-Histogram 可以设置为基础证券价格图表的指标之上、之下或之后。直方图占据了很多图表空间，因此最好将其放置在主窗口之上或之下。也可以在主窗口中显示不带直方图的 MACD。选择 MACD 作为指标，并将信号线数字从 9 改为 1（9,26,1）。这将删除信号线和直方图。信号线可以通过点击高级指标选项并添加一个 9 天的 EMA 来单独添加。

[点击此处查看实时图表](http://stockcharts.com/h-sc/ui?s=$INDU&p=D&b=5&g=0&id=p59749230423&listNum=30&a=199515976 "http://stockcharts.com/h-sc/ui?s=$INDU&p=D&b=5&g=0&id=p59749230423&listNum=30&a=199515976")，展示 MACD-Histogram。

![MACD-Histogram - 图表 6](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/f147f387e412e93098fbcbbed505f1ba.jpg "MACD-Histogram - 图表 6")

![MACD - 图表 7](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/d0e0483cce2b025663909f8a8430f885.jpg "MACD - 图表 7")

## 建议扫描

### MACD-Histogram 转为正值

首先，此扫描仅考虑股票交易价格高于它们的 200 天移动平均线，这意味着总体上是上涨趋势。其次，MACD-Histogram 从负区域移动到正区域。还要注意，MACD 必须为负以确保此上涨发生在回撤之后。此扫描仅作为进一步细化的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily Close > Daily SMA(200,Daily Close)] 
AND [Yesterday's Daily MACD Hist(12,26,9,Daily Close) < 0] 
AND [Daily MACD Hist(12,26,9,Daily Close) > 0] 
AND [Daily MACD Line(12,26,9,Daily Close) < 0]
```

### MACD-Histogram 转为负值

首先，此扫描仅考虑股票交易价格低于它们的 200 天移动平均线，这意味着总体上是下跌趋势。其次，MACD-Histogram 从正区域移动到负区域。还要注意，MACD 必须为正以确保此下跌发生在反弹之后。此扫描仅作为进一步细化的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily Close < Daily SMA(200,Daily Close)] 
AND [Yesterday's Daily MACD Hist(12,26,9,Daily Close) > 0] 
AND [Daily MACD Hist(12,26,9,Daily Close) < 0] 
AND [Daily MACD Line(12,26,9,Daily Close) > 0]
```

欲了解有关 MACD-Histogram 扫描的语法，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#macd_histogram_macd_hist "http://stockcharts.com/docs/doku.php?id=scans:indicators#macd_histogram_macd_hist")。

## 进一步学习

技术分析 - 积极投资者的强大工具提供了一套完整的市场预测课程，由 MACD 的创始人编写。短期、中期和长期策略均有详细解释，其中许多包含 MACD。

| **技术分析 - 积极投资者的强大工具** 杰拉德·阿普尔 |
| --- |
| ![](http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors "http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors") |
| ![立即购买](http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors "http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors") |


# 资金流指数（MFI）

### 目录

+   资金流指数（MFI）

    +   介绍

    +   计算

    +   解释

    +   超买/超卖

    +   背离和失败

    +   结论

    +   使用 SharpCharts

    +   建议扫描

        +   MFI 超卖

        +   MFI 超买

    +   进一步研究

## 介绍

资金流指数（MFI）是一种使用价格和交易量来衡量买卖压力的振荡器。由 Gene Quong 和 Avrum Soudack 创建，MFI 也被称为成交量加权 RSI。MFI 从每个周期的典型价格开始。当典型价格上涨时（买入压力），资金流是正的，当典型价格下跌时（卖出压力）是负的。然后将正负资金流的比率插入 RSI 公式中，以创建一个在零和一百之间移动的振荡器。作为与交易量相关的动量振荡器，资金流指数（MFI）最适合识别各种信号的反转和价格极端情况。

## 计算

资金流指数计算涉及几个步骤。下面的示例基于 14 周期的资金流指数，这是 SharpCharts 的默认设置和创建者推荐的设置。

```py
Typical Price = (High + Low + Close)/3

Raw Money Flow = Typical Price x Volume
Money Flow Ratio = (14-period Positive Money Flow)/(14-period Negative Money Flow)

Money Flow Index = 100 - 100/(1 + Money Flow Ratio)

```

首先，注意原始资金流是基本上是美元交易量，因为公式是交易量乘以典型价格。当典型价格从一个周期到下一个周期上涨时，原始资金流是正的，当典型价格下跌时是负的。当典型价格不变时，不使用原始资金流值。第 3 步中的资金流比率形成了资金流指数（MFI）的基础。正负资金流在回顾期（14）内求和，正资金流总和除以负资金流总和得到比率。然后应用 RSI 公式创建一个成交量加权指标。下表显示了从 Excel 电子表格中提取的计算示例。

![资金流指数 - 电子表格](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/10f9697b4bf60877d8b1d8c0a63739e1.jpg "资金流指数 - 电子表格")

点击这里")查看 Excel 电子表格中的 MFI 计算。

![资金流指数  -  图表 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/17b556cfdce83ec9616407b09365e409.jpg "资金流指数  -  图表 1")

## 解释

作为 RSI 的成交量加权版本，资金流动指数（MFI）可以类似于 RSI 进行解释。最大的区别当然是成交量。由于成交量被加入到计算中，资金流动指数的表现会与 RSI 有些许不同。理论表明，成交量领先价格。RSI 是一个动量振荡器，已经领先价格。结合成交量可以增加这种领先时间。

Quong 和 Soudack 使用资金流动指数确定了三种基本信号。首先，图表分析师可以寻找超买或超卖水平，以警示不可持续的价格极端。其次，可以利用看涨和看跌背离来预测趋势反转。第三，80 或 20 处的失败摆动也可用于识别潜在的价格反转。对于本文，背离和失败摆动被结合在一起形成一个信号组，增加鲁棒性。

## 超买/超卖

超买和超卖水平可用于识别不可持续的价格极端。通常，MFI 超过 80 被视为超买，MFI 低于 20 被视为超卖。强势趋势可能对这些经典的超买和超卖水平构成问题。当上涨趋势强劲时，MFI 可能变得超买（>80），价格可能继续上涨。相反，当下跌趋势强劲时，MFI 可能变得超卖（<20），价格可能继续下跌。Quong 和 Soudack 建议扩大这些极端以进一步确认信号。超过 90 的上涨是真正的超买，低于 10 的下跌是真正的超卖。超过 90 和低于 10 的走势是罕见的事件，表明价格走势不可持续。诚然，许多股票会长时间交易而不会达到 90/10 的极端。然而，图表分析师可以使用 StockCharts.com 的扫描引擎找到那些达到这些极端的股票。本文末尾提供了这些扫描的链接。

![资金流动指数 - 图表 2](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/0d6ae905c4754cc3f7d96e259cf1498b.jpg "资金流动指数 - 图表 2")

JB Hunt（JBHT）在 2009 年 10 月底和 2010 年 2 月初，当资金流动指数下跌至 10 以下时，变得超卖。前面的下跌足够尖锐，以产生这些读数，但超卖极端表明这些下跌是不可持续的。仅仅超卖水平还不足以转为看涨。需要某种形式的逆转或上升来确认价格确实已经转向。JBHT 通过大幅跳空和趋势线突破以及良好的成交量确认了第一个超卖读数。该股票通过良好成交量的阻力突破确认了第二个超卖读数。

![资金流动指数 - 图表 3](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/198a223ddb8dbb2969155ec4d424c816.jpg "资金流动指数 - 图表 3")

Aeropostale (ARO) 在 2009 年 9 月底和 12 月底，当资金流动指数上涨到 90 以上时，就变得超买。MFI 的极端值表明这些上涨是不可持续的，回调即将到来。第一个超买信号导致了一个相当大的下跌，但第二个没有。注意到 ARO 在第一个超买信号时达到顶峰，并在 10 月份形成了较低的高点。10 月底的支撑线突破标志着明显的趋势逆转。在 12 月的超买信号之后，ARO 上涨到 23 以上并保持稳定。出现了两个下跌间隙和一个支撑线突破，但这些都没有持续。价格走势比超买信号更强劲。ARO 最终突破了 24 的阻力位，并再次上涨至 28 以上。第二个信号没有起作用。

## 背离和失败摆动

失败摆动和背离可以结合起来产生更加稳健的信号。当 MFI 在 20 以下超卖，突破 20，回调时保持在 20 以上，然后突破先前的反应高点时，就会出现一个看涨的失败摆动。当价格下跌到一个更低的低点，但指标形成一个更高的低点，显示资金流动或动量改善时，就形成了一个看涨的背离。

在下面的 Aetna (AET) 图表中，于 2010 年 1 月至 2 月形成了一个看涨的背离和失败摆动。首先，注意股票在 2 月创下一个更低的低点，而 MFI 在 1 月的低点远高于其 1 月低点，形成了一个看涨的背离。其次，注意 MFI 在 1 月下跌到 20 以下，2 月保持在 20 以上，并在 2 月底突破了先前的高点。这个信号组合预示了 3 月的强劲上涨。

![资金流动指数 - 图表 4](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/6fa36a1c891904fffa48f95b380e943e.jpg "资金流动指数 - 图表 4")

当 MFI 在 80 以上超买，跌破 80，未能在反弹时超过 80，然后跌破先前的反应低点时，就会出现一个看跌的失败摆动。当股票创下一个更高的高点，而指标形成一个更低的高点时，就形成了一个看跌的背离，表明资金流动或动量恶化。

在上面的 Aetna 图表中，于 8 月至 9 月形成了一个看跌的背离和失败摆动。股票在 9 月创下新高，但 MFI 形成了一个明显较低的高点。当 MFI 在 8 月底超买到 80 以上时，形成了一个看跌的失败摆动，未能在 9 月反弹时达到 80，并在 9 月底的下跌中突破了先前的低点。

## 结论

资金流动指数是一种相当独特的指标，它将动量和成交量与 RSI 公式结合在一起。当指标高于 50 时，RSI 动量通常偏向多头，低于 50 时偏向空头。尽管 MFI 被认为是一个成交量加权的 RSI，但使用中线来确定多头或空头偏向效果不佳。相反，MFI 更适合识别潜在的超买/超卖水平、多头/空头背离以及多头/空头失败摆动。与所有指标一样，MFI 不应单独使用。可以将纯动量振荡器（如 RSI）或图表分析与 MFI 结合以增加信号的稳健性。

## 使用 SharpCharts

资金流动指数可作为 SharpCharts 指标使用，可以放置在基础证券的价格图表的上方、下方或后方。将 MFI 直接放在价格后面可以方便地将指标摆动与价格变动进行比较。默认设置为 14 周期，但可以根据分析需求进行调整。较短的时间框架使指标更敏感。较长的时间框架使其不太敏感。用户可以点击“高级选项”旁边的绿色箭头添加水平线以自定义超买和超卖水平。通过用逗号分隔数字添加两条线：（10,90）。

![资金流动指数  -  图表 5](http://stockcharts.com/h-sc/ui?s=IBM&p=D&yr=0&mn=6&dy=0&id=p62268879970&listNum=30&a=221699049 "http://stockcharts.com/h-sc/ui?s=IBM&p=D&yr=0&mn=6&dy=0&id=p62268879970&listNum=30&a=221699049")

![CCI - SharpCharts](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/42900cb4d85953c860dc6e6b17a3cdab.jpg "CCI - SharpCharts")

## 建议扫描

### MFI 超卖

此扫描搜索股价高于每股$20，每日交易量超过 100,000 股，并且资金流动指数超卖（<10）的股票。将其视为进一步分析和尽职调查的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily MFI(14) < 10]
```

### MFI 超买

此扫描搜索股价高于每股$20，每日交易量超过 100,000 股，并且资金流动指数超买（>90）的股票。将其视为进一步分析和尽职调查的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily MFI(14) > 90]
```

有关用于资金流动指数扫描的语法详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#money_flow_index_mfi "http://stockcharts.com/docs/doku.php?id=scans:indicators#money_flow_index_mfi")在支持中心。

## 进一步研究

| **专业交易员的技术分析** 康斯坦斯·布朗 |
| --- |
| ![](http://store.stockcharts.com/products/technical-analysis-for-the-trading-professional "http://store.stockcharts.com/products/technical-analysis-for-the-trading-professional") |
| ![立即购买](http://store.stockcharts.com/products/technical-analysis-for-the-trading-professional "http://store.stockcharts.com/products/technical-analysis-for-the-trading-professional") |


# 负量指数 (NVI) 

### 目录

+   负量指数 (NVI)

    +   简介

    +   SharpCharts 计算

    +   信号

    +   微调

    +   结论

    +   与 SharpCharts 一起使用

    +   建议的扫描

        +   看涨 NVI 信号线交叉

        +   看跌 NVI 信号线交叉

    +   进一步研究

## 简介

负量指数 (NVI) 是一个累积指标，利用成交量的变化来判断聪明的资金何时活跃。保罗·戴萨特在上世纪 30 年代首次开发了这个指标。事实上，市场技术协会于 1990 年选中戴萨特，以表彰他对技术分析的贡献。戴萨特的负量指数工作基于这样一个假设：聪明的资金在成交量减少的日子活跃，而不那么聪明的资金在成交量增加的日子活跃。

## SharpCharts 计算

负量指数有两个版本。在原始版本中，戴萨特通过在一个周期到另一个周期成交量减少时添加净进步来形成一个累积线。净进步等于上涨股票数减去下跌股票数。当成交量从一个周期增加到另一个周期时，累积 NVI 线保持不变。换句话说，什么也没做。股市逻辑的诺曼·福斯巴克通过用百分比价格变化替代净进步来调整了该指标。SharpCharts 公式使用了这个福斯巴克版本。

```py
1\. Cumulative NVI starts at 1000

2\. Add the Percentage Price Change to Cumulative NVI when Volume Decreases

3\. Cumulative NVI is Unchanged when Volume Increases

4\. Apply a 255-day EMA for Signals

```

![图表 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/238223476ef072cf5e4e92a71a9a0e2f.jpg "图表 1")

电子表格示例详细展示了计算过程。价格 % 变化乘以 100，以减少所需的小数位数。首先注意成交量 % 变化列。当这个值为负时，标普 500 的百分比变化被输入到 NVI 值列中。当这个值为正时，NVI 值列中不会出现任何内容。从 1000 开始，每个周期应用 NVI 值，以创建一个仅在成交量减少时变化的累积指标。

![电子表格](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/acc79417edd2413ca3c1c8ace0799444.jpg "电子表格")

点击此处下载此电子表格示例。")

## 信号

负量指数的传统用法非常简单。根据福斯巴克的说法，当 NVI 高于其 255 天 EMA 时，牛市的可能性较大；当 NVI 低于其 255 天 EMA 时，熊市的可能性较大。然而，福斯巴克指出这些可能性并不对称。当 NVI 高于其 255 天 EMA 时，牛市的可能性为 96%，但当 NVI 低于其 255 天 EMA 时，熊市的可能性仅为 53%。

![图表 2](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/4833a4998bab69992af8c63237523aaa.jpg "图表 2")

上图显示了道琼工业指数及其下方的 NVI。 即使有一个长期移动平均线，也有很多鞭策（错误信号）。 请注意，随着指标在 1998-1998 年间多次穿越 255 日 EMA 而上升，它如何来回摆动。 在 2001-2002 年间，随着道琼工业指数的交易变得波动，也有几次交叉。 从 2002 年底开始的信号不太容易出现鞭策，因为更强劲的趋势出现了。 图表分析师可以预期一些滞后，因为移动平均线滞后，并且使用 255 日 EMA 来生成信号。

## 微调

尽管 NVI 的设计初衷是针对主要股票指数，但图表分析师可以将 NVI 与 ETF、股票或任何具有交易量的东西一起使用。 请记住，该指标背后的理念有点不同寻常，因为在交易量增加时的价格变动基本上被忽略。

![图表 3](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/85171c4dfffa56717a0f923f7534ff52.jpg "图表 3")

上面的示例显示了消费者自由裁量 SPDR（XLY）及其 NVI 和两个指数移动平均线。 当 NVI 高于其 255 日 EMA（红色）时，总体趋势是向上的。 下跌到 100 日 EMA 以下显示了这一上升趋势中的修正。 图表分析师还可以通过绘制趋势线将基本技术分析应用于该指标。 从 2010 年 1 月到 2012 年 7 月有三个修正期（蓝线）。 突破这些趋势线标志着修正期的结束和上升趋势的恢复，对于 NVI 而言是如此。 这些突破信号还预示着基础资产（XLY）的重大价格波动。

## 结论

负量指数（NVI）是一种混合指标，结合了 Paul Dysart 和 Norman Fosback 的输入。 NVI 在交易量减少时计算价格变化，并在交易量增加时折扣价格变化。 假设是当交易量减少时聪明（知情）的资金在运作，而当交易量增加时不那么聪明（不知情）的资金在运作。 请记住，该指标是为广泛的市场指数和交易量设计的。 它可以用于股票和 ETF，但 NVI 并不总是按预期运作。 NVI 将与某些股票产生一些很好的看涨/看跌背离信号，但与其他股票完全不同步。 与所有指标一样，NVI 不应单独使用。 相反，图表分析师应将其与其他分析技术结合使用。

## 使用 SharpCharts

负量指标（NVI）可以在图表下方的指标部分找到。 NVI 被设置为累积指标，无法调整。 图表师可以通过更改参数框中的数字来调整指数移动平均线。 将参数设置为“1”将基本上删除移动平均线。 然后，可以将指标放置在主图表窗口后面、上面或下面。 在将其放置在主图表窗口的价格图之后时，有助于更改颜色。 图表师可以使用“高级”指标选项将另一个移动平均线或指标应用于 NVI。 下面的示例显示了应用于指标窗口中的 NVI 的变化率振荡器。 [点击这里](http://stockcharts.com/h-sc/ui?s=$COMPQ&p=D&yr=0&mn=8&dy=0&id=p79189698479&a=276034932 "http://stockcharts.com/h-sc/ui?s=$COMPQ&p=D&yr=0&mn=8&dy=0&id=p79189698479&a=276034932") 查看 NVI 实际操作的实时示例。

![图表 4](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/326a01cc2a8fe6ea2a16c7072c4c23fc.jpg "图表 4")

![图表 5](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/c49327ad7e2fe1489c514c9108f956f8.jpg "图表 5")

## 建议的扫描

### 看涨 NVI 信号线穿越

这个扫描显示了 NVI 已经穿过其信号线的股票，触发了一个看涨信号。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [NVI x NVI Signal(255)]

```

### 看跌 NVI 信号线穿越

这个扫描显示了 NVI 已经穿过其信号线的股票，触发了一个看跌信号。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [NVI Signal(255) x NVI]
```

有关用于 NVI 扫描的语法的更多详细信息，请参阅我们支持中心的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#negative_volume_index "http://stockcharts.com/docs/doku.php?id=scans:indicators#negative_volume_index")。

## 进一步研究

《金融市场技术分析》有一章专门讨论了交易量，另一章详细介绍了广度指标。 普林的书中有一章专门讨论如何将交易量纳入分析过程中。

| **金融市场技术分析** 约翰·J·墨菲 | **技术分析解密** 马丁·普林 |
| --- | --- |
| ![](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | ![](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |
| ![立即购买](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | ![立即购买](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |


# 成交量平衡（OBV）

### 目录

+   成交量平衡（OBV）

    +   介绍

    +   计算

    +   解释

    +   背离

    +   趋势确认

    +   结论

    +   与 SharpCharts 一起使用

    +   建议扫描

        +   OBV 和 ADL 中的牛市背离

        +   OBV 和 ADL 中的熊市背离

    +   进一步学习

    +   额外资源

        +   股票与商品杂志文章

## 介绍

成交量平衡（OBV）衡量买卖压力，是一个累积指标，将上涨日的成交量相加，下跌日的成交量相减。OBV 由乔·格兰维尔开发，并在他 1963 年的著作《格兰维尔股市利润的新关键》中介绍。它是最早衡量正向和负向成交量流动的指标之一。图表分析师可以寻找 OBV 和价格之间的背离来预测价格走势，或使用 OBV 来确认价格趋势。

## 计算

成交量平衡（OBV）线简单地是正向和负向成交量的累计总和。当收盘价高于前一个收盘价时，该时期的成交量为正。当收盘价低于前一个收盘价时，该时期的成交量为负。

```py

If the closing price is above the prior close price then: 
Current OBV = Previous OBV + Current Volume

If the closing price is below the prior close price then: 
Current OBV = Previous OBV  -  Current Volume

If the closing prices equals the prior close price then:
Current OBV = Previous OBV (no change)

```

![表 1  -  成交量平衡](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/8d2d3b0d1ad66223f7819274348f403c.jpg "表 1  -  成交量平衡")

上表中的数据来自沃尔玛（WMT）。成交量数据已四舍五入，并以千为单位显示。换句话说，8200 实际上等于 820 万股。首先，我们必须确定沃尔玛是收盘上涨（+1）还是下跌（-1）。这个数字现在被用作成交量乘数，用于计算正向或负向成交量。最后一列（OBV）形成正向/负向成交量的累计总和。因为 OBV 必须从某个地方开始，第一个值（8200）只是等于第一个时期的正向/负向成交量。下面的图表显示了沃尔玛的成交量和 OBV。

![表 1  -  成交量平衡](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/7401aa3a9f1a60384446199b914fd426.jpg "表 1  -  成交量平衡")

## 解释

格兰维尔理论认为成交量先于价格。当上涨日的成交量超过下跌日的成交量时，OBV 上升。当下跌日的成交量更强时，OBV 下降。上升的 OBV 反映了正向的成交量压力，可能导致价格上涨。相反，下降的 OBV 反映了负向的成交量压力，可能预示价格下跌。格兰维尔在他的研究中指出，OBV 通常会在价格之前移动。如果 OBV 上升而价格要么持平要么下跌，预计价格会上涨。如果 OBV 下降而价格要么持平要么上涨，预计价格会下跌。

OBV 的绝对值并不重要。图表分析师应该关注 OBV 线的特征。首先，定义 OBV 的趋势。其次，确定当前趋势是否与基础证券的趋势相匹配。第三，寻找潜在的支撑或阻力水平。一旦突破，OBV 的趋势将改变，这些突破可以用来生成信号。此外，请注意 OBV 是基于收盘价的。因此，在寻找背离或支撑/阻力突破时应考虑收盘价。最后，成交量的激增有时可能会使指标失真，导致急剧波动，需要一段时间来稳定。

## 背离

多头和空头背离信号可以用来预测趋势反转。这些信号真正基于成交量领先价格的理论。当 OBV 上升或形成高点时，即使价格下跌或形成低点时，就形成了多头背离。当 OBV 下降或形成低点时，即使价格上涨或形成高点时，就形成了空头背离。OBV 与价格之间的背离应该提醒图表分析师，价格可能会发生反转。

星巴克（SBUX）的图表显示，7 月份形成了一个多头背离。在价格图表上，SBUX 在 7 月初的时候低于了 6 月的低点。然而，OBV 保持在 6 月的低点之上，形成了一个多头背离。OBV 在 SBUX 突破阻力之前就已经突破了阻力。这是一个经典的成交量领先价格的案例。SBUX 一周后突破了阻力，并继续上涨超过 20，获得了 30%以上的收益。第二张图显示了在德州仪器（TXN）交易区间内交易时，OBV 上升。在交易区间内 OBV 上升表示积累，这是多头的。

![图表 2  -  成交量平衡](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/3c66257c4c1d656de9c3952372f53f85.jpg "图表 2  -  成交量平衡")

![图表 3  -  成交量平衡](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/3b1cf99f5a0393fa0adfde99f624ccb5.jpg "图表 3  -  成交量平衡")

梅德特龙（MDT）的图表显示，成交量领先价格下跌的空头背离。蓝色虚线标识了背离期。MDT 上涨（从 43 涨到 45），而 OBV 下降。此外，请注意，OBV 在这个背离期间突破了支撑。随着突破 2 月低点，OBV 的上升趋势逆转。另一方面，MDT 仍在上涨。最终成交量赢得了胜利，随着 MDT 跟随成交量下跌，跌至 30 美元以下。第二张图显示了瓦莱罗能源（VLO）在 4 月形成空头背离，并在 5 月确认支撑突破。

![图表 4  -  成交量平衡](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/44f968a3528d1665f5b1e438e9041dcb.jpg "图表 4  -  成交量平衡")

![图表 5  -  成交量平衡指标](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/6dc60f820cd463f1e2cb27a52bce6e91.jpg "图表 5  -  成交量平衡指标")

## 趋势确认

OBV 可以用来确认价格趋势、上涨突破或下跌突破。Best Buy（BBY）的图表显示了三个确认信号以及价格趋势的确认。OBV 和 BBY 在 12 月至 1 月下跌，在 3 月至 4 月上涨，在 5 月至 8 月下跌，在 9 月至 10 月上涨。OBV 的趋势与 BBY 的趋势相匹配。

![图表 6  -  成交量平衡指标](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/de98496a3304efd34075756fbc8765d7.jpg "图表 6  -  成交量平衡指标")

OBV 还确认了 BBY 的趋势反转。注意 BBY 如何在 2 月底突破了下降趋势线，而 OBV 在 3 月确认了阻力突破。BBY 在 4 月底突破了上升趋势线，而 OBV 在 5 月初确认了支撑线突破。BBY 在 9 月初突破了下降趋势线，而 OBV 在一周后确认了趋势线突破。这些一致的信号表明正成交量和负成交量与价格协调一致。

有时 OBV 与基础证券步调一致。在这种情况下，OBV 确认了基础趋势的强势，无论是上涨还是下跌。Autozone（AZO）的图表显示了价格为黑线，OBV 为粉线。从 2009 年 11 月至 2010 年 10 月，两者都稳步上升。正成交量在整个上涨过程中保持强劲。

![图表 7  -  成交量平衡指标](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/69c39979a9df8c350116ab318cf8cd9a.jpg "图表 7  -  成交量平衡指标")

## 结论

成交量平衡指标（OBV）是一个简单的指标，利用成交量和价格来衡量买盘和卖盘的压力。当正成交量超过负成交量且 OBV 线上升时，买盘明显。当负成交量超过正成交量且 OBV 线下降时，卖盘存在。技术分析师可以使用 OBV 来确认基本趋势或寻找可能预示价格变化的背离。与所有指标一样，重要的是将 OBV 与技术分析的其他方面结合使用。它不是一个独立的指标。OBV 可以与基本的图表分析结合使用，或者确认来自动量振荡器的信号。

## 使用 SharpCharts

在 SharpCharts 中，On Balance Volume（OBV）作为一个指标是可用的。选择后，OBV 可以放置在基础证券的价格图之上、之下或之后。将其放在图表之后使得比较 OBV 和基础证券变得容易。图表分析师还可以通过选择高级选项向 OBV 添加移动平均线或另一个指标，该选项位于指标位置的右侧。[点击这里](http://stockcharts.com/h-sc/ui?s=IBM&p=D&yr=0&mn=6&dy=0&id=p32660999348&listNum=30&a=216754758 "http://stockcharts.com/h-sc/ui?s=IBM&p=D&yr=0&mn=6&dy=0&id=p32660999348&listNum=30&a=216754758")查看带有 On Balance Volume 的实时图表。

![SharpCharts  -  On Balance Volume](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/6d9811e81290ada70b6f74573e453189.jpg "SharpCharts  -  On Balance Volume")

![SharpCharts  -  On Balance Volume](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/1ac18b19be874bdbd1dc3c380c6a802f.jpg "SharpCharts  -  On Balance Volume")

## 建议的扫描

### OBV 和 ADL 的看涨背离

这个扫描从股票的基础开始，这些股票在过去 60 天的平均价格至少为$10，每日交易量为 100,000。通过查找价格低于 65 日 SMA 和 20 日 SMA，但 OBV 和积累/分布线高于 65 日 SMA 和 20 日 SMA 的股票，可以找到潜在的看涨背离。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [Daily Close < Daily SMA(65,Daily Close)] 
AND [Daily AccDist > Daily AccDist Signal (65)] 
AND [Daily OBV > Daily OBV Signal(65)] 
AND [Daily Close < Daily SMA(20,Daily Close)] 
AND [Daily AccDist > Daily AccDist Signal (20)] 
AND [Daily OBV > Daily OBV Signal(20)]
```

### OBV 和 ADL 的看跌背离

这个扫描从股票的基础开始，这些股票在过去 60 天的平均价格至少为$10，每日交易量为 100,000。通过查找价格高于 65 日 SMA 和 20 日 SMA，但 OBV 和积累/分布线低于 65 日 SMA 和 20 日 SMA 的股票，可以找到潜在的看跌背离。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [Daily Close > Daily SMA(65,Daily Close)] 
AND [Daily AccDist < Daily AccDist Signal (65)] 
AND [Daily OBV < Daily OBV Signal(65)] 
AND [Daily Close > Daily SMA(20,Daily Close)] 
AND [Daily AccDist < Daily AccDist Signal (20)] 
AND [Daily OBV < Daily OBV Signal(20)]
```

有关 OBV 扫描的语法细节，请参阅我们支持中心的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#on_balance_volume "http://stockcharts.com/docs/doku.php?id=scans:indicators#on_balance_volume")。

**注意**：为了扫描的目的，在交易日内，每日交易量数据是不完整的。在运行基于 OBV 等基于交易量的指标的扫描时，请确保基于“上次市场收盘价”。其他基于交易量的指标的示例包括积累/分布、Chaikin 货币流和 PVO。

## 进一步研究

这本书通过简单明了的解释涵盖了所有内容。墨菲涵盖了所有主要的图表模式和指标，包括 OBV。一个完整的章节专门讨论了理解交易量和未平仓合约。

| **金融市场技术分析** 约翰·J·墨菲 |
| --- |
| ![](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") |
| ![立即购买](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") |

* * *

## 其他资源

### 股票与商品杂志文章

**[布鲁斯·R·法伯的平衡量指标](http://stockcharts.com/h-mem/tascredirect.html?artid=\V12\C07\ONBALAN.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V12\C07\ONBALAN.pdf")**

1994 年 6 月 - 股票与商品

**[斯图尔特·伊文斯的平衡量](http://stockcharts.com/h-mem/tascredirect.html?artid=\V17\C05\036OBV.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V17\C05\036OBV.pdf")**

1999 年 4 月 - 股票与商品

**[D.W.戴维斯的平衡量日内交易](http://stockcharts.com/h-mem/tascredirect.html?artid=\V22\C01\004DAVE.PDF "http://stockcharts.com/h-mem/tascredirect.html?artid=\V22\C01\004DAVE.PDF")**

2003 年 12 月 - 股票与商品


# 百分比价格振荡器 

### 目录

+   百分比价格振荡器

    +   介绍

    +   计算

    +   解释

    +   MACD、PPO 和价格

    +   大幅价格变动

    +   比较不同证券

    +   结论

    +   使用 SharpCharts

    +   建议扫描

        +   PPO 阳市信号线交叉

        +   PPO 熊市信号线交叉

    +   进一步研究

## 介绍

百分比价格振荡器（PPO）是一种动量振荡器，它以较大移动平均线的百分比来衡量两个移动平均线之间的差异。与其表兄 MACD 一样，百分比价格振荡器显示有信号线、直方图和中线。信号通过信号线交叉、中线交叉和背离产生。由于这些信号与 MACD 相关的信号没有区别，本文将重点介绍两者之间的一些区别。首先，PPO 读数不受证券价格水平的影响。其次，即使不同证券的价格存在较大差异，也可以比较不同证券的 PPO 读数。有关两者共同信号的信息，请参阅 ChartSchool 上关于 MACD 的文章。

## 计算

```py
Percentage Price Oscillator (PPO): {(12-day EMA - 26-day EMA)/26-day EMA} x 100

Signal Line: 9-day EMA of PPO

PPO Histogram: PPO - Signal Line

```

虽然 MACD 衡量两个移动平均线之间的绝对差值，但 PPO 通过将差值除以较慢的移动平均线（26 天 EMA）使其成为相对值。PPO 简单地是 MACD 值除以较长的移动平均线。结果乘以 100，将小数点移动两位。下表显示了英特尔（INTC）的 12 天 EMA、26 天 EMA、MACD 和 PPO 的值。英特尔的价格在低 20 美元左右，MACD 值范围从 -44 美分到 +64 美分。PPO 将这些值转换为百分比，范围从 -2.01 到 +2.85。使用百分比更容易随时间比较水平。-2.01 相当于 -2.01%，而 +2.85 相当于 +2.85%。

![PPO - 电子表格 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/feeb3985cc37a52c91cea9e164ebbe18.jpg "PPO - 电子表格 1")

点击此处下载此电子表格示例。")

![PPO - 图表 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/1fa37710aaf5da2b2c5b012d4b48e61e.jpg "PPO - 图表 1")

标准 PPO 基于 12 日指数移动平均线（EMA）和 26 日 EMA，但这些参数可以根据投资者或交易者的偏好进行更改。收盘价格用于计算移动平均线，因此 PPO 信号应根据收盘价格进行衡量。PPO 的 9 日 EMA 被绘制为信号线，以识别指标的上升和下降。

## 解释

与 MACD 一样，PPO 反映了两个移动平均线的收敛和分歧。当较短的移动平均线高于较长的移动平均线时，PPO 为正。随着较短的移动平均线远离较长的移动平均线，指标进一步进入正区域。这反映了强劲的上行动量。当较短的移动平均线低于较长的移动平均线时，PPO 为负。当较短的移动平均线远离较长的移动平均线（变得更负）时，负读数增加。这反映了强劲的下行动量。直方图代表 PPO 和其 9 日 EMA 信号线之间的差异。当 PPO 高于其 9 日 EMA 时，直方图为正，当 PPO 低于其 9 日 EMA 时，直方图为负。PPO 直方图可用于预测 PPO 中的信号线交叉。有关信号详细信息，请参阅 MACD 直方图的 ChartSchool 文章。

## MACD、PPO 和价格

MACD 水平受到证券价格的影响。高价证券的 MACD 值将高于或低于低价证券，即使波动性基本相等。这是因为 MACD 基于两个移动平均线的绝对差异。图表 2 显示了谷歌的 MACD 和 PPO 以进行比较。12 日 EMA 约为 495，26 日 EMA 约为 512，差值为-17（两位数）。请注意，谷歌的 MACD 在上升和下降时都达到了两位数，但百分比价格振荡器范围从+2.5 到-3.5。MACD 值看起来较高，因为谷歌的价格相对较高。道琼斯工业指数的 MACD，超过 10,000，经常达到三位数。然而，PPO 范围从-2 到+2，这是一个更可定义的范围。

![PPO - 图表 2](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/b68ad8f268f627526c03d429d6b7cf76.jpg "PPO - 图表 2")

尽管指标线看起来相同，但 MACD 和 PPO 之间通常存在细微差异。在谷歌的例子中，请注意 PPO 跌破了二月低点，但 MACD 尚未跌破其二月低点。PPO 的较低低点显示了扩大的下行动量。

## 大幅价格变动

由于 MACD 是基于绝对水平的，大幅价格变动会在较长时间内影响 MACD 水平。如果一支股票从 20 涨到 100，其 MACD 水平在 20 左右会比在 100 左右要小得多。PPO 通过以百分比形式显示 MACD 值来解决这个问题。图表 3 显示了百度（BIDU）在 12 个月内从 25 涨到 75。在 25-30 左右的 MACD 值通常会比 70-80 左右的 MACD 值要小。请注意，MACD 突破了 7 月和 3 月的高点，但 PPO 没有突破这些相应的高点。还要注意，当 PPO 超过+5 时，百度会变得超买。

![PPO - 图表 3](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/babd0c1366955faf4d73da738a5fe4d6.jpg "PPO - 图表 3")

## 比较不同证券

由于百分比价格振荡器（PPO）是 MACD 的百分比版本，其值可以与其他证券进行比较。戴尔（DELL）和惠普（HPQ）属于同一行业集团，但其股价水平不同。截至 2010 年 5 月底，DELL 的股价在高十几美元，而 HPQ 的股价在中 40 美元。绝对价格水平与基本面无关，但会影响 MACD 水平。HPQ 的 MACD 无疑会高于 DELL。然而，我们可以应用百分比价格振荡器（PPO）来比较动量。首先，注意到 DELL 的 PPO 范围为-4 至+4，共 8 个点）。HPQ 的 PPO 范围为-3 至+2，共 5 个点。我们可以立即看出 DELL 比 HPQ 更具波动性，因为其 PPO 范围更大。其次，我们可以看到 DELL 在 3 月至 4 月的上涨动量比 HPQ 更强。DELL 的 PPO 从负值区域上升并超过 4。HPQ 的 PPO 在 DELL 之前转为正值，但未超过 1.6。

![PPO - 图表 4](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/3a830512b30d595878959d86e2cf2bc1.jpg "PPO - 图表 4")

![PPO - 图表 5](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/d1c7e0c90b92aaf0ed49acbbfe7dc18c.jpg "PPO - 图表 5")

## 结论

百分比价格振荡器（PPO）产生与 MACD 相同的信号，但作为 MACD 的百分比版本提供了一个额外的维度。道琼斯工业指数（价格约 11000）的 PPO 水平可以与 IBM（价格约 122）的 PPO 水平进行比较，因为 PPO“水平化”了竞争环境。此外，即使价格翻倍或翻三倍，也可以比较一个证券的 PPO 水平，这对于 MACD 来说并非如此。尽管具有优势，但 PPO 仍不是最佳振荡器来识别超买或超卖条件，因为运动是无限的（理论上）。RSI 和随机指标的水平是有限的，这使它们更适合识别超买和超卖水平。

## 使用 SharpCharts

PPO 可以设置为证券价格图表的上方、下方或后方的指标。一旦从下拉列表中选择指标，将显示默认参数设置（12,26,9）。这些参数可以调整以增加或减少灵敏度。较慢的长期移动平均线与较快的短期移动平均线组合将增加灵敏度。通过将信号线参数设置为 1，可以移除直方图。在显示证券价格图表后面的 PPO 时，这很有帮助。用户甚至可以通过将 9 日 EMA 应用于 PPO 来重新添加信号线。单击“高级选项”以将移动平均线添加为指标的叠加层。[点击此处查看 PPO 的实时示例](http://stockcharts.com/h-sc/ui?s=$INDU&p=D&yr=0&mn=6&dy=0&id=p81462571466&listNum=30&a=201062788 "http://stockcharts.com/h-sc/ui?s=$INDU&p=D&yr=0&mn=6&dy=0&id=p81462571466&listNum=30&a=201062788")。

![PPO - 图表 7](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/05c008550c47d098135d4d45fd4708c9.jpg "PPO - 图表 7")

![PPO - 图表 6](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/d4aff4f51a1507d181bc90a7345f3b82.jpg "PPO - 图表 6")

## 建议的扫描

### PPO 看涨信号线交叉

此扫描显示了交易价格高于其 200 日移动平均线并在 PPO 中出现看涨信号线交叉的股票。同时注意，PPO 需要为负值，以确保此上升发生在回调之后。这个扫描只是作为进一步细化的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily Close > Daily SMA(200,Daily Close)] 
AND [Yesterday's Daily PPO Line(12,26,9,Daily Close) < Daily PPO Signal(12,26,9,Daily Close)] 
AND [Daily PPO Line(12,26,9,Daily Close) > Daily PPO Signal(12,26,9,Daily Close)] 
AND [Daily PPO Line(12,26,9,Daily Close) < 0]
```

### PPO 看跌信号线交叉

此扫描显示了交易价格低于其 200 日移动平均线并在 PPO 中出现看跌信号线交叉的股票。同时注意，PPO 需要为正值，以确保此下降发生在反弹之后。这个扫描只是作为进一步细化的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily Close < Daily SMA(200,Daily Close)] 
AND [Yesterday's Daily PPO Line(12,26,9,Daily Close) > Daily PPO Signal(12,26,9,Daily Close)] 
AND [Daily PPO Line(12,26,9,Daily Close) < Daily PPO Signal(12,26,9,Daily Close)] 
AND [Daily PPO Line(12,26,9,Daily Close) > 0]
```

有关 PPO 扫描的语法详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#percentage_price_oscillator_ppo "http://stockcharts.com/docs/doku.php?id=scans:indicators#percentage_price_oscillator_ppo")在支持中心。

## 进一步研究

| **技术分析-活跃投资者的强大工具** 杰拉德·阿普尔 |
| --- |
| ![](http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors "http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors") |
| ![立即购买](http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors "http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors") |


# 百分比成交量振荡器 

### 目录

+   百分比成交量振荡器

    +   介绍

    +   计算

    +   解释

    +   验证突破

    +   微调 PVO

    +   结论

    +   与 SharpCharts 一起使用

    +   建议的扫描

        +   PPO 带 PVO 正面的 PPO 穿越

        +   PVO 带 PVO 正面的 PPO 穿越

    +   进一步研究

## 介绍

百分比成交量振荡器（PVO）是一个用于成交量的动量振荡器。PVO 以较大移动平均线的百分比来衡量两个基于成交量的移动平均线之间的差异。与 MACD 和百分比价格振荡器（PPO）一样，它显示有信号线、直方图和中线。当较短的成交量 EMA 高于较长的成交量 EMA 时，PVO 为正；当较短的成交量 EMA 低于较长的成交量 EMA 时，PVO 为负。该指标可用于定义成交量的涨跌，然后可用于确认或否定其他信号。通常，当 PVO 上升或为正时，突破或支撑突破得到验证。

## 计算

```py
Percentage Volume Oscillator (PVO): 
((12-day EMA of Volume - 26-day EMA of Volume)/26-day EMA of Volume) x 100

Signal Line: 9-day EMA of PVO

PVO Histogram: PVO - Signal Line

```

PVO 的默认设置为 (12,26,9)，与 MACD 或 PPO 相同。这意味着当 12 天成交量 EMA 上穿 26 天成交量 EMA 时，PVO 为正。当 12 天成交量 EMA 下穿 26 天成交量 EMA 时，PVO 为负。

正负程度取决于远近。PVO 等于 5 表示 12 天成交量 EMA 比 26 天成交量 EMA 高 5%。PVO 等于 -3% 表示 12 天成交量 EMA 比 26 天成交量 EMA 低 3%。

PVO-Histogram 的作用类似于 MACD 和 PPO 直方图。当 PVO 在其信号线（9 天 EMA）上方交易时，PVO-Histogram 为正。当 PVO 低于其信号线时，PVO-Histogram 为负。请注意，PVO 乘以 100，以将小数点移动两位。

![PVO - 图表 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/b54195ea4b3aa6bfb9b5a5020652ba51.jpg "PVO - 图表 1")

## 解释

一般来说，当 PVO 为正时，成交量高于平均水平，当 PVO 为负时，成交量低于平均水平。负值且上升的 PVO 表明成交量水平正在增加。正值且下降的 PVO 表明成交量水平正在减少。图表分析师可以利用这些信息来确认或否定价格图表上的运动。

尽管 PVO 基于动量振荡器公式，但重要的是要记住移动平均滞后。12 天的 EMA 携带了 12 天的成交量数据，数据更多地加权于最新数据。26 天的 EMA 滞后更多，因为它包含了 26 天的数据。这意味着 PVO(12,26,9)有时可能与价格走势不同步。

## 验证突破

百分比成交量振荡器（PVO）可用于确认支撑或阻力的突破。我们都听说过成交量验证价格走势。在成交量增加的情况下支撑位的突破比成交量较低的情况下更具可信度。同样，成交量扩大的情况下阻力位的突破显示出更多的买盘兴趣，从而增加成功的机会。

下图显示了 Volero（VLO）的 PVO(12,26,9)确认了继续图案的突破。随着 PVO 在 8 月下降，成交量直到 9 月中旬才下降。然后 PVO 转向上升，但直到 10 月下旬才进入正区域。这意味着 12 天成交量 EMA 最终超过了 26 天 EMA，成交量在增加。VLO 在第一个 PVO 交叉时仍然停留在继续图案中，但在第二个 PVO 交叉时突破了图案阻力。成交量证实了突破，VLO 继续上涨。

![PVO - 图表 2](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/5db7c11cefa5ac6717d346e778f8ae86.jpg "PVO - 图表 2")

阿彻丹尼尔斯中部（ADM）的图表显示了 PVO 确认的支撑和阻力突破。股票在 8 月初突破了阻力位，同时 PVO 急剧上升进入正区域。在上涨突破时成交量扩大是看涨的。经过三个月的上涨，股票在跳空和 PVO 的另一次激增中突破了支撑位。请注意 PVO 两次激增到 20。这意味着 12 天成交量 EMA 比 26 天成交量 EMA 高约 20%。

![PVO - 图表 3](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/93399ac4dc2ba9984aa5cbbc6c99a1a9.jpg "PVO - 图表 3")

## 微调 PVO

图表分析师可以微调 PVO 以突出特定时期的成交量激增。一年大约有 250 个交易日。因此，250 天的 EMA 将代表平均年度成交量，重点放在最近的时期。将其用于 PVO 中的长期 EMA，我们可以选择一个短期 EMA 来突出高于这个平均值的成交量激增。当 1 天成交量高于 250 天成交量 EMA 时，PVO(1,250)将为正。当 5 天成交量 EMA 高于 250 天 EMA 时，PVO(5,250)将为正。

Merck（MRK）的图表显示了带有 5 日 EMA 的蓝色和 250 日 EMA 的红色的成交量柱。 PVO（1,250）显示在第一个指标窗口中（绿色），而 PVO（5,250）显示在较低的指标窗口中（黑色）。 信号线未显示，因为没有输入参数。 PVO（5,250,9）将显示带有 9 日 EMA 的 PVO 作为信号线。

![PVO - 图表 4](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/fd428c3cb8aa1e29dcd23584d921fcef.jpg "PVO - 图表 4")

从上面的图表中，我们可以看到当一个成交量柱突破 250 日 EMA 时（绿色箭头），PVO（1,250）变为正。 当 5 日成交量 EMA 移动到 250 日成交量 EMA 之上时（蓝色箭头），PVO（5,250）变为正。 正如人们所预期的那样，PVO（1,250）更频繁地穿过零线，速度稍快一点。 基本上，当 PVO（1,250）为正时，成交量高于平均水平，为负时低于平均水平。 在高于平均水平的成交量上突破比低于平均水平的更稳健。 支撑突破也是如此。

## 结论

百分比成交量振荡器（PVO）是应用于成交量的动量指标。 成交量不趋势，因此这种振荡器可能非常波动。 PVO 不太适合牛市和熊市的背离。 相反，图表分析师最好寻找成交量增加并进入正区域的迹象，以及成交量减少并进入负区域的迹象。 成交量增加可以验证支撑或阻力突破。 同样，低成交量下的激增或重要支撑突破可能不够稳健。 与所有技术指标一样，重要的是将百分比成交量振荡器（PVO）与技术分析的其他方面结合使用，例如图表模式和动量振荡器。

## 使用 SharpCharts

PVO 可以设置为证券价格图的上方、下方或后方的指标。 一旦从下拉列表中选择指标，将显示默认参数（12,26,9）。 可以根据下面的示例调整这些参数。 单击“高级选项”以向指标添加移动平均线或水平线。 在下面的示例中，成交量被添加为指标两次，以显示两个移动平均线。 第二个成交量指标被放置在第一个成交量指标的后面（在 ind 后面），并且 EMA 设置为 250，使用高级选项。 [点击这里查看 PVO 的实时示例](http://stockcharts.com/h-sc/ui?s=IBM&p=D&yr=0&mn=6&dy=0&id=p28625227150&listNum=30&a=217316123 "http://stockcharts.com/h-sc/ui?s=IBM&p=D&yr=0&mn=6&dy=0&id=p28625227150&listNum=30&a=217316123")。

![PVO - 图表 5](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/03f663e028d13e2be279d12c217d323e.jpg "PVO - 图表 5")

![PVO - 图表 6](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/6fcb0223599ee4eb2bebc7809261a011.jpg "PVO - 图表 6")

## 建议扫描

### PPO 穿越上行，PVO 为正

此扫描显示了 PPO(12,26,9) 上穿 PPO 信号线并且 PVO(12,26,9) 进入正区域以显示成交量增加的股票。此扫描仅作为进一步细化的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily PPO Line(12,26,9,Daily Close) crosses Daily PPO Signal(12,26,9,Daily Close)] 
AND [Daily PVO Line(12,26,9) crosses 0]
```

### PPO 穿越下行，PVO 为正

此扫描显示了 PPO(12,26,9) 下穿 PPO 信号线并且 PVO(12,26,9) 进入正区域以显示成交量增加的股票。此扫描仅作为进一步细化的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily PPO Signal(12,26,9,Daily Close) crosses Daily PPO Line(12,26,9,Daily Close)] 
AND [Daily PVO Line(12,26,9) crosses 0]
```

有关用于 PVO 扫描的语法的更多详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#percentage_volume_oscillator "http://stockcharts.com/docs/doku.php?id=scans:indicators#percentage_volume_oscillator")在支持中心。

**注意**：为了扫描目的，交易日内的每日成交量数据是不完整的。在运行基于成交量的指标（如 PVO）的扫描时，请确保基于“最后市场收盘价”进行扫描。其他基于成交量的指标的示例包括积累/分布、钱德动量流和能量潮指标。

## 进一步研究

约翰·墨菲的书涵盖了技术分析的所有基础知识，其中有关成交量、未平仓合约和成交量指标的部分。墨菲讨论了成交量的重要性，并展示了许多图表示例。《技术分析入门》是一本附带 CD-Rom 的工作手册，其中包含超过 7 小时的视听呈现。普林格展示了如何应用、分析和解释图表以及成交量。

| **金融市场技术分析** 约翰·J·墨菲 |
| --- |
| ![](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") |
| ![立即购买](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") |


# 价格相对 / 相对强度 

### 目录

+   价格相对 / 相对强度

    +   介绍

    +   计算

    +   解释

    +   趋势识别

    +   看涨/看跌背离

    +   结论

    +   使用 SharpCharts

    +   进一步研究

    +   额外资源

        +   股票与商品杂志文章

## 介绍

价格相对指标通过比率图表将一个证券的表现与另一个证券进行比较。这个指标也被称为相对强度指标，有时也被称为相对强度比较。通常，价格相对指标用于比较股票与基准指数（如标普 500 指数）的表现。图表分析师还可以使用价格相对指标来比较股票与其所属行业或板块的表现。这样可以确定一支股票是领先还是落后于同行。价格相对指标还可以用于找到在整体市场下跌期间表现更好的股票，或在整体市场上涨期间表现疲软的股票。

**注意：** 在 StockCharts.com 上，使用**比率股票代码**来创建价格相对指标。比率符号由两个股票代码用冒号连接在一起组成（例如，“IBM:$SPX”，“$INDU:$GOLD”）。比率股票代码的值等于第一个符号的收盘价除以第二个符号的收盘价。

## 计算

```py
Price Relative = Base Security / Comparative Security

Ratio Symbol Close = Close of First Symbol / Close of Second Symbol
Ratio Symbol Open  = Open of First Symbol / Close of Second Symbol
Ratio Symbol High  = High of First Symbol / Close of Second Symbol
Ratio Symbol Low   = Low of First Symbol / Close of Second Symbol

```

价格相对指标简单地是基础证券除以比较证券。通常，基础证券是一支股票，基准是标普 500 指数。例如，图表分析师可以使用价格相对指标显示星巴克（SBUX）相对于标普 500 指数（$SPX）的表现。这只是星巴克的价格除以标普 500 指数。星巴克属于消费者自由选择行业。图表分析师还可以查看星巴克相对于消费者自由选择 SPDR（XLY）的表现，使用适当的[比率符号](http://stockcharts.com/docs/doku.php?id=data#ratio_symbols_relative_strength "http://stockcharts.com/docs/doku.php?id=data#ratio_symbols_relative_strength")（SBUX:XLY）。图表分析师还可以查看板块表现相对于标普 500 指数（XLY:$SPX）。

![价格相对 - 电子表格 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/652e553429404caea6d41eec0a33baca.jpg "价格相对 - 电子表格 1")

点击这里下载此电子表格示例。")

上表显示了星巴克/标普 500 价格相对性。第二行中的第一个值为 0.0256（30.66/1197.75）。当星巴克的涨幅超过标普 500 或跌幅低于标普 500 时，这个比率会增加。当星巴克的涨幅低于标普 500 或跌幅超过标普 500 时，这个比率会减少。为了参考，表中还显示了星巴克和标普 500 的百分比变化。星巴克的百分比变化减去标普 500 的百分比变化也等于价格相对性的日变化。在第二行中，注意到星巴克下跌了 2.66%，而标普 500 下跌了 1.62%。价格相对性下降（-1.04%），因为星巴克的跌幅超过了标普 500。第三行显示价格相对性上升，因为星巴克（+0.50%）的涨幅高于标普 500（+0.02%）。下图展示了价格相对性的实际情况。

![价格相对性 - 图表 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/28ad925566edc9c87372ac5abf21f805.jpg "价格相对性 - 图表 1")

## 解释

价格相对性用于衡量相对强度，在进行股票选择时非常重要。许多投资组合经理将自己的表现与标普 500 等基准进行比较。他们的目标是跑赢该基准。为了实现这一目标，经理们经常寻找表现相对强劲的股票。这就是价格相对性的作用。当一支股票表现出相对强劲并跑赢其基准时，价格相对性上升。相反，当一支股票表现出相对弱势并跑输其基准时，价格相对性下降。

有几种方法可以使用价格相对性。首先，图表分析师可以进行简单的趋势分析，以确定价格相对性的方向。这可以基于实际趋势、支撑/阻力突破、移动平均线或其他指标。其次，图表分析师可以寻找相对强度的牛市和熊市背离，以警示股价可能出现逆转。

## 趋势识别

图表分析师可以应用基本趋势分析或移动平均线来确定价格相对性的方向。与任何价格图表一样，当出现更高的高点和更高的低点时，价格相对性就会呈上升趋势。相反，当出现更低的低点和更低的高点时，价格相对性就会呈下降趋势。图表分析师还可以应用所选的移动平均线。当价格相对性交易在其 150 日简单移动平均线以下时，可能存在长期下降趋势。另外，当价格相对性交易在其 150 日简单移动平均线以上时，可能存在长期上升趋势。

![价格相对性 - 图表 2](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/d4a23d4173a9f3da488a65930921d4e9.jpg "价格相对性 - 图表 2")

上图显示了惠普（HPQ）的价格相对（HPQ:$SPX）。15 天 SMA 应用于 HPQ 价格和价格相对。首先，请注意，价格相对在 6 月中旬突破阻力，标志着上升趋势的开始。在 12 月期间，价格相对继续表现出更高的高点和更高的低点。价格相对在 12 月下旬达到顶峰，并在 2 月下旬形成较低的高点。随后，跌破 150 天 SMA 标志着下降趋势的开始和表现不佳期。

## 阳市/熊市背离

在价格下跌期间，价格相对的牛市背离信号相对强势。在下跌期间表现最佳的股票往往是市场反转时的领导者。下图显示了杜邦（DD）的价格相对（DD:$SPX）。尽管股票从 4 月下旬下跌到 7 月初，价格相对却上升，表明在这一下跌过程中相对强势。杜邦的表现比整体市场好。随后，当市场反转并在 7 月开始上涨时，该股成为领头羊。请注意，价格相对和股票在 7 月下旬突破阻力（蓝线）。  

![价格相对 - 图表 3](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/bc7bbd83703a986ac1f5a5b60f26e951.jpg "价格相对 - 图表 3")

在价格上涨期间，价格相对弱势的熊市背离信号。股票在上涨过程中表现不佳，通常在市场反转时率先下跌。下图显示了万事达卡（MA）的价格相对（MA:$SPX）。在 2 月初急剧下跌后，股票在 4 月下旬升至新的反应高点。价格相对没有确认，并形成了一个明显较低的高点，形成了熊市背离。此外，请注意，价格相对在股票从 3 月第二周上涨到 4 月下旬时是平的（蓝线）。这些上涨过程中的相对弱势迹象预示着 5 月份的急剧下跌。

![价格相对 - 图表 4](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/924552fccc63461a9fa23d0ffecca853.jpg "价格相对 - 图表 4")

## 结论

尽管本文侧重于使用价格相对性进行股票分析，但价格相对性也可以用于广泛的市场分析。股市可以分为九个由行业 SPDR 代表的部门。图表分析师可以维护这九个部门的价格相对性图表，以确定领先者和落后者。当科技和消费者自由选择部门领先时，市场处于进攻模式。当消费品、医疗保健和公用事业部门领先时，市场处于防御模式。确定了领先部门后，图表分析师可以在这些部门内寻找领先股票。可以避免显示相对弱势的部门，以帮助缩小搜索范围。与所有指标一样，重要的是将价格相对性与其他技术分析工具结合使用。动量振荡器和图表模式可用于确认或否定相对强势或相对弱势。

## 使用 SharpCharts

通过在 SharpCharts 中使用“价格”指标和[“比率”股票代码](http://stockcharts.com/docs/doku.php?id=data#ratio_symbols_relative_strength "http://stockcharts.com/docs/doku.php?id=data#ratio_symbols_relative_strength")（例如，“IBM:$SPX”），可以获得价格相对性。首先，选择“价格”指标。其次，在参数框中，输入基础证券的符号，然后加上冒号（“:”），然后是比较证券的符号。

请注意，您还可以在比率符号中使用两个“伪符号” - “$SECTOR”和“$INDUSTRY”。我们将自动用适当的部门或行业 ETF/指数替换这些符号。例如，“IBM:$SECTOR”等同于“IBM:XLK”。

价格相对性可以放置在基础证券的价格图表的上方、下方或后方。将指标放置在“价格后面”可以方便比较这两条线。下图显示了价格相对性（粉色）在价格图表后面的情况。请注意 8 月的看涨背离和 12 月的看跌背离。使用“高级选项”可以向价格相对性添加移动平均线或另一个指标。[点击这里查看实时示例](http://stockcharts.com/h-sc/ui?s=XLY&p=D&yr=0&mn=6&dy=0&id=p08051994524&listNum=30&a=220460939 "http://stockcharts.com/h-sc/ui?s=XLY&p=D&yr=0&mn=6&dy=0&id=p08051994524&listNum=30&a=220460939")。

![价格相对性 - 图表 5](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/8750fa63f1c6716db84fec380fb89bcb.jpg "价格相对性 - 图表 5")

![价格相对性 - SharpCharts](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/a7c258055e692915c66fcdd4347d1438.jpg "价格相对性 - SharpCharts")

## 进一步研究

马菲的书在跨市场分析章节中涵盖了相对强度分析。马菲还研究了各个行业的相对强度，并展示了如何将相对强度应用于个别股票。

《技术分析解释》一书介绍了相对强度的概念。普林展示了图表示例来确定相对强度，并教导读者如何将相对强度与其他指标结合运用。

| **金融市场技术分析** 约翰·J·墨菲 | **马丁·普林的技术分析解释** 马丁·普林 |
| --- | --- |
| ![](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | ![](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |
| ![立即购买](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | ![立即购买](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |

* * *

## 其他资源

### 股票与商品杂志文章

**[马丁·普林的相对强度](http://stockcharts.com/h-mem/tascredirect.html?artid=\V19\C07\079RS.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V19\C07\079RS.pdf")**

2001 年 6 月 - 股票与商品 V. 19:7 (42-46)

**[工作资金：使用史蒂夫·沃特金斯的相对强度](http://stockcharts.com/h-mem/tascredirect.html?artid=\V21\C05\101WATK.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V21\C05\101WATK.pdf")**

2003 年 4 月 - 股票与商品


# 知识确定事物（KST）

### 目录

+   知识确定事物（KST）

    +   SharpCharts 计算

    +   解释

    +   背离

    +   强势趋势

    +   时间框架

    +   进一步调整

    +   结论

    +   与 SharpCharts 一起使用

    +   建议扫描

        +   看涨 KST 信号线交叉

        +   看跌 KST 信号线交叉

    +   进一步研究

由 Martin Pring 开发，知识确定事物（KST）是基于四个不同时间框架的平滑变化率的动量振荡器。Pring 在 1992 年的一篇文章中将这个指标称为“总变化率（KST）”*Stocks & Commodities*杂志。简而言之，KST 衡量了四个不同价格周期的价格动量。它可以像任何动量振荡器一样使用。图表分析师可以寻找背离、超买/超卖读数、信号线交叉和中线交叉。Pring 经常在 KST 上应用趋势线。尽管趋势线信号并不经常发生，但 Pring 指出这种突破会加强信号线交叉。

## SharpCharts 计算

即使 KST 的公式看起来很复杂，但它实际上是一个相当直观的指标。它只是四个不同变化率的加权平均值，经过平滑处理。例如，计算 10 周期的变化率，然后用 10 周期的简单移动平均进行平滑处理。下图显示了四个不同的变化率指标及其适当的移动平均线进行平滑处理。

![图表 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/a4dbc72c6b453c582aa2cb189599285f.jpg "图表 1")

下方的公式框显示了四种不同组合及其默认设置。这些组合然后被加权和求和。最短的时间框架承载最小的权重（1），而最长的时间框架承载最大的权重（4）。添加了一个 9 周期的简单移动平均线作为信号线。

```py
RCMA1 = 10-Period SMA of 10-Period Rate-of-Change 
RCMA2 = 10-Period SMA of 15-Period Rate-of-Change 
RCMA3 = 10-Period SMA of 20-Period Rate-of-Change 
RCMA4 = 15-Period SMA of 30-Period Rate-of-Change 

KST = (RCMA1 x 1) + (RCMA2 x 2) + (RCMA3 x 3) + (RCMA4 x 4)  

Signal Line = 9-period SMA of KST

```

默认参数如下：KST(10,15,20,30,10,10,10,15,9)。前四个数字代表变化率设置，后四个代表这些变化率指标的移动平均线，最后一个数字是信号线移动平均线。

![电子表格](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/e63854c97e7839a6671159ee47b66a4e.jpg "电子表格")

点击这里下载此电子表格示例") 并在家里尝试。

## 解释

KST 在零线上下波动。在最基本的情况下，当 KST 为正时，动量偏向多头，当 KST 为负时，动量偏向空头。正值意味着加权平滑的变化率值大多为正，并且价格上涨。负值表示价格下跌。

![图表 2](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/30578c37539f6cb30d853fc273e79471.jpg "图表 2")

在基本中线交叉之后，图表分析师可以寻找信号线交叉并判断总体方向。当 KST 在其信号线之上时，通常是上升的，当在其信号线之下时，通常是下降的。上升且为负的 KST 线表明下行动量正在减弱。相反，下降且为正的 KST 线表明上行动量正在减弱。

尽管 KST 可能有许多不同的信号，但基本的中线和信号线交叉通常是最可靠的。与 RSI 和随机振荡器不同，KST 没有上限或下限。这使得它相对不适合超买和超卖信号。

## 背离

多头和空头背离也可能出现信号，但图表分析师在使用这些信号时需要谨慎。基本变化率指标中的大多数背离并不会导致价格逆转。同样，MACD 和 RSI 中的背离也容易失败。最好在存在明显且明显的背离时使用背离。下面的示例显示了 BroadCom (BRCM)存在明显的多头背离和空头背离。这些背离最终会随后的信号线交叉（红色和绿色箭头）而完成。

![图表 3](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/4569f826c64ea4a8f64dc83b4017a8b7.jpg "图表 3")

## 强势趋势

图表分析师在强劲上升趋势中应谨慎处理空头信号线交叉和在强劲下降趋势中的多头信号线交叉。在强劲上升趋势中，KST 可能进入正区间并在较长时间内保持在正区间。指标将达到相对较高水平，然后转向下降，但永远不会进入负区间。这只是表明上行动量正在减缓。上行动量仍然强于下行动量，但上行动量不如之前的时期强劲。下面的示例显示了 Sherwin Williams (SHW)从 2011 年 11 月到 2012 年 8 月的强劲上升趋势。尽管 KST 波动上下，但它从未跌破零线，并且在整个时间内保持在正区间。空头信号线交叉只是表明上行动量减缓，而不是趋势改变。

![图表 4](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/2a2131c4f73144515731b38473df9fd6.jpg "图表 4")

## 时间框架

+   短期日线 = KST(10,15,20,30,10,10,10,15,9)

+   中期周线 = KST(10,13,15,20,10,13,15,20,9)

+   长期月线 = KST(9,12,18,24,6,6,6,9,9)

正如 Pring 的文章中所指出的，KST 可以用于短期、中期或长期时间框架。Pring 建议不仅仅在日线、周线和月线图表之间切换，而是建议根据每个时间框架调整设置。使用周线和月线设置时，KST 甚至更加平滑。这意味着图表分析师应该使用信号线交叉来检测价格的方向变化。中线交叉的滞后通常太大。下表显示了短期、中期和长期研究的变化率设置和移动平均设置。

![图表 5](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/ffce4972218595e8006e54413f427915.jpg "图表 5")

![图表 6](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/4c61b9b9b285d421836e97c95be174fc.jpg "图表 6")

![图表 7](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/cd1b8d2de245dec9c6e9d00f838c3d29.jpg "图表 7")

## 进一步调整

Pring 承认 KST 不是一个完美的指标。这种东西是不存在的。然而，KST 确实有其用途，Pring 鼓励图表分析师尝试不同的设置，因为一刀切并不适用于所有情况。公用事业和消费品股票波动性较小，可能需要更敏感的设置。科技股更具波动性，可能需要更不敏感的设置。

图表分析师还可以混合和匹配变化率设置和移动平均设置。下图显示了第一个指标窗口中的默认 KST 和第二个窗口中偏向短期变化率的 KST。第二个窗口显示的不是 KST(10,15,20,30,10,10,10,15,9)，而是 KST(30,20,15,10,10,10,10,10,9)。第一个变化率设置权重最小，第四个权重最大。请注意，前四个数字代表变化率设置。接下来的四个数字代表平滑这四个变化率指标的移动平均。最后一个数字是信号线。

![图表 8](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/260de45633af4ade9a5e6fb8539f3fea.jpg "图表 8")

## 结论

确信指标（KST）是基于四个不同时间周期的平滑变化率的动量振荡器。在这方面，它旨在捕捉四个不同的价格周期。KST 可以像其他无约束的动量振荡器一样使用，例如 MACD、百分比价格振荡器和 TRIX。事实上，KST 与 TRIX 非常相似。由于它是无约束的，KST 不适合识别超买和超卖条件。创造者 Martin Pring 更倾向于信号线交叉和趋势线突破来发出信号。与所有指标一样，KST 应与其他分析技术结合使用。

## 使用 SharpCharts

KST 可作为 SharpCharts 的指标。一旦选择，用户可以将指标放置在基础价格图的上方、下方或后方。将 KST 直接放在价格图的后面，突出了相对于基础证券价格走势的波动。用户可以应用“高级选项”来添加水平线。调整参数框中的数字将更改设置。

![图表 9](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/704b7a2d1667b1b7175417693311f40a.jpg "Chart 9")

![图表 10](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/2de9da5e750477532e424d062e8fce22.jpg "Chart 10")

## 建议的扫描

### 看涨 KST 信号线穿越

此扫描显示了 KST 处于正区域的股票。当 KST 穿过其信号线时，将触发一个看涨信号。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [KST > 0]
AND [KST x KST Signal]

```

### 看跌 KST 信号线穿越

此扫描显示了 KST 处于负区域的股票。当 KST 穿过其信号线时，将触发一个看跌信号。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [KST < 0]
AND [KST Signal x KST]
```

有关用于 KST 扫描的语法详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#pring_s_know_sure_thing "http://stockcharts.com/docs/doku.php?id=scans:indicators#pring_s_know_sure_thing")在支持中心。

## 进一步研究

《金融市场技术分析》一书专门讨论了动量振荡器及其各种用途。墨菲涵盖了变动率的利弊以及一些特定于变动率的示例。普林的书通过涵盖背离、交叉和其他信号来展示动量指标的基础知识。还有两章涵盖了具体的动量指标，并提供了大量示例。

| **《金融市场技术分析》约翰·J·墨菲** | **《技术分析解析》马丁·普林** |
| --- | --- |
| ![](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | ![](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |
| ![立即购买](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | ![立即购买](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |


# 马丁·普林的特别 K 

### 目录

+   马丁·普林的特别 K

    +   计算

    +   使用特别 K 来识别长期价格走势

    +   识别支持趋势短期买入和卖出信号

    +   使用 SharpCharts

    +   建议扫描

        +   特别 K 看涨短期交叉

        +   特别 K 看跌短期交叉

Pring 特别 K 是由马丁·普林创造的动量指标，将短期、中期和长期速度合并为一个完整系列，从而给我们真正的总循环性。它有两个功能，第一是在相对早期阶段识别主要趋势反转，第二是利用该信息来确定短期支持趋势的价格波动。以下是所有三种趋势，如何以叠加的动量格式表达：

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/1d9d84230a439e8ec9a21b4a7c98df08.jpg)

这里是（绿色）主要趋势和（橙色）特别 K，实际上是前一张图中显示的短期趋势。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/c0a24e023878568746056a540fbdca47.jpg)

在理想情况下，特别 K 应该在牛市和熊市转折点的价格峰值和谷值几乎同时出现。在大多数情况下，实际上是这样的。当这种情况发生时，关键是尽可能快地在事后识别这些转折点。该公式假定价格围绕着四年的商业周期循环。因此，当出现线性上升趋势，例如 90 年代股票的长期牛市时，特别 K 会领先于转折点。另外，当周期被截断时，例如 1987 年的崩盘，该指标会延迟。图 1 和图 2 显示，大多数时候价格和 SPK 同时反转。

***特别 K 的主要功能是识别主要趋势的转折点。*** 由于该指标在计算中还包括短期数据，因此一个附带的好处在于识别较小的趋势，用于交易目的，并将其与主要趋势的方向和成熟度放在背景中。让我们考虑这两个方面，从主要趋势识别开始。

## 计算

特别 K 是几种不同变化率加权平均数的总和。这些周期和权重是基于多年的市场观察而选择的。

```py

  Special K = 10 Period Simple Moving Average of ROC(10) * 1
            + 10 Period Simple Moving Average of ROC(15) * 2
            + 10 Period Simple Moving Average of ROC(20) * 3
            + 15 Period Simple Moving Average of ROC(30) * 4
            + 50 Period Simple Moving Average of ROC(40) * 1
            + 65 Period Simple Moving Average of ROC(65) * 2
            + 75 Period Simple Moving Average of ROC(75) * 3
            +100 Period Simple Moving Average of ROC(100)* 4
            +130 Period Simple Moving Average of ROC(195)* 1
            +130 Period Simple Moving Average of ROC(265)* 2
            +130 Period Simple Moving Average of ROC(390)* 3
            +195 Period Simple Moving Average of ROC(530)* 4

```

请注意，至少需要 725 个数据点才能准确计算此指标。如果数据较少，则计算的最后一行将被跳过。

## 使用特别 K 来识别长期价格走势

事后看来，很容易发现特别 K 的转折点，并将其与主要趋势的峰值和谷值联系起来，如下图中的垂直箭头所示。不幸的是，由于交易员和投资者是实时工作的，他们没有事后的便利。以下是几种帮助发现主要趋势转折点的技术，使用特别 K：

1.  由于特别 K 是一个相当参差不齐的指标，最适合用于趋势线构建。例如，如果违反了 9 个月或更长时间的趋势线，通常意味着特别 K 的主要趋势已经逆转，当指标改变趋势时，价格通常也会改变。

1.  通过特别 K 运行移动平均线是正常的。默认值是 100 天平滑的 100 天 SMA。平均线的交叉通常表示主要趋势方向的逆转。偶尔，就像所有移动平均线情况一样，会触发鞭策。然而，当与趋势线突破结合时，会触发更强大和更可靠的信号。在上面的第一个图表中显示了 2003 年和 2009 年美国股市底部的例子，MA 交叉和趋势线违规几乎同时发生。

1.  有时特别 K 会描绘价格模式。当它们被价格本身的某种趋势逆转所证实时，这通常代表了当前主要趋势逆转的有效指示。下面的 GLD 图表提供了两个例子。

![图 3](http://stockcharts.com/h-sc/ui?s=SPY&p=D&st=1995-01-01&en=2010-04-01&id=p27191194097&a=351268055 "http://stockcharts.com/h-sc/ui?s=SPY&p=D&st=1995-01-01&en=2010-04-01&id=p27191194097&a=351268055")

![图 4](http://stockcharts.com/h-sc/ui?s=$CRB&p=D&st=1995-01-01&en=2014-01-01&id=p91095913553&a=351269321 "http://stockcharts.com/h-sc/ui?s=$CRB&p=D&st=1995-01-01&en=2014-01-01&id=p91095913553&a=351269321")

![图 5](http://stockcharts.com/h-sc/ui?s=GLD&p=D&st=2008-01-02&en=2013-05-06&id=p98657791953&a=351279812 "http://stockcharts.com/h-sc/ui?s=GLD&p=D&st=2008-01-02&en=2013-05-06&id=p98657791953&a=351279812")

需要注意的是，计算特别 K 的初始绘图需要数年的数据。要真正欣赏到这个指标提供的长期视角，需要额外的 5-10 年数据。这样就可以看到所讨论的证券是否经历了预期的周期性波动。大多数情况下是这样的，但偶尔会发现一些不是这样的。

## 识别 Pro Trend 短期买入和卖出信号

对于短期交易者来说，把握的最重要的事情之一是，沿着主要趋势方向执行的交易比反周期方式生成的交易更有可能成功。确定主要趋势方向的客观方法是使用特别 K。显然，我们可以很容易地在事后知道实际的特别 K 峰值和谷底形成的位置，但在实时中我们没有这种奢侈。一个解决方案是确定其相对于其 100 日移动平均线的位置。正读数（即高于移动平均线）将表明主要是牛市，反之亦然。

当确定主要趋势方向为看涨时，从多头方向进行的交易将在特别 K 本身穿过其 10 日移动平均线时启动。下图中的橙色向上箭头表示这些交易。当特别 K 重新穿过其 10 日移动平均线时，交易将被平仓。空头交易将以相反的方式启动，即当特别 K 低于其长期移动平均线并穿过其 10 日移动平均线时。下图显示了道琼斯 UBS 商品指数的这样一个系统。绿色垂直线代表由特别 K/100 日移动平均线关系定义的牛市阶段的开始。

![图 6](http://stockcharts.com/h-sc/ui?s=DJP&p=D&st=2008-02-14&en=2010-07-24&id=p13988319489&a=351486397 "http://stockcharts.com/h-sc/ui?s=DJP&p=D&st=2008-02-14&en=2010-07-24&id=p13988319489&a=351486397")

注意，在熊市期间不会产生买入信号，只会有卖出信号（棕色，向下箭头）。 “示例卖出点”表现不佳，因为它发生在牛市期间，但不幸的是，系统仍处于熊市模式，因为特别 K 低于其 100 日移动平均线，显示这种方法远非完美。与所有技术指标一样，与其盲目地将此方法作为机械系统使用，不如将其作为警报使用，并使用其他指标作为“证据权重”方法中的过滤器。

- 马丁·普林

## 使用 SharpCharts

特别 K 可作为 SharpCharts 的指标使用。指标中的第一行是原始特别 K 值。第二行是原始特别 K 值的双重平滑移动平均线，作为信号线。

该指标可以放置在基础价格图的上方、下方或后方。将特别 K 直接放在价格图后面，突出了相对于基础证券价格走势的波动。

用户可以通过更改参数框中的数字来调整信号线设置。这两个参数指定了用于平滑的两个简单移动平均线的周期数。默认参数值为 100,100。用户还可以应用“高级选项”以添加水平线。

![图 7](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/c4aa55e49173996e5a6149af3749ca5d.jpg "图 7")

![图 8](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/25bb32c408525ebbbd173f21077dac7c.jpg "图 8")

## 建议扫描

### 特别 K 牛市短期交叉

此扫描显示特别 K 高于其信号线的股票。当特别 K 穿过其 10 日移动平均线时，将触发牛市信号。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Special K > Special K Signal(100,100)]
AND [Special K x SMA(10,Special K)]
```

### 特别 K 熊市短期交叉

此扫描显示特别 K 低于其信号线的股票。当特别 K 穿过其 10 日移动平均线时，将触发熊市信号。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Special K < Special K Signal(100,100)]
AND [SMA(10,Special K) x Special K]
```

有关特别 K 扫描使用的语法的更多详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#pring_s_special_k "http://stockcharts.com/docs/doku.php?id=scans:indicators#pring_s_special_k")。


# 变动率（ROC）

### 目录

+   变动率（ROC）

    +   简介

    +   计算

    +   解释

    +   趋势识别

    +   超买/超卖极端

    +   结论

    +   使用 SharpCharts

    +   建议扫描

        +   超卖率变动率

        +   超买变动率

    +   进一步研究

## 简介

变动率（ROC）指标，也简称为动量，是一个纯粹的动量振荡器，它衡量了价格从一个时期到下一个时期的百分比变化。 ROC 计算将当前价格与“n”个时期前的价格进行比较。 绘图形成一个振荡器，随着变动率从正数变为负数而在零线上下波动。 作为一个动量振荡器，ROC 信号包括中线交叉、背离和超买-超卖读数。 背离往往不会预示逆转，因此本文将不讨论背离。 尽管中线交叉容易出现鞭策，特别是短期内，但这些交叉可以用来识别整体趋势。 识别超买或超卖极端对变动率振荡器来说是很自然的。

## 计算

```py
ROC = [(Close - Close n periods ago) / (Close n periods ago)] * 100

```

![ROC - 电子表格 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/e68d80196e9cd3903aacafbdb04eb415.jpg "ROC - 电子表格 1")

点击这里下载此电子表格示例。")

![ROC - 图表 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/16f032d9a9d473d10b9a24fceae2cd0b.jpg "ROC - 图表 1")

上表显示了 2010 年 5 月道琼斯工业指数的 12 天变动率计算。 黄色单元格显示了从 4 月 28 日到 5 月 14 日的变动率。 实际上是 13 个交易日，但 28 日的收盘价作为 29 日的起点。 蓝色单元格显示了从 5 月 7 日到 5 月 25 日的 12 天变动率。

## 解释

如上所述，变动率指标是动量的最纯粹形式。它衡量了在一定时间内价格的百分比增加或减少。可以将其视为上升（价格变动）与横向（时间）的比例。一般来说，只要变动率保持为正，价格就会上涨。相反，当变动率为负时，价格就会下跌。随着上涨加速，变动率扩展到正区域。随着下跌加速，变动率深入负区域。变动率没有上限。上涨的空间是无限的。然而，有一个下限。证券只能下跌 100%，即降至零。即使有这些不对称的边界，变动率产生可识别的极端情况，表明了高买入和超卖条件。

## 趋势识别

尽管动量振荡器最适合交易范围或之字形趋势，但它们也可以用来定义基础趋势的整体方向。一年大约有 250 个交易日。这可以分为每半年 125 天，每季度 63 天和每月 21 天。趋势反转始于最短时间框架，逐渐扩展到其他时间框架。一般来说，当 250 天和 125 天的变动率都为正时，长期趋势是上涨的。这意味着现在的价格比 12 个月和 6 个月前要高。6 个或 12 个月前的多头头寸将是盈利的，买家将会很高兴。

![ROC - 图表 2](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/c7b37b048fe8667e8b873e883052356d.jpg "ROC - 图表 2")

图表 2 显示了 IBM 的 250 天、125 天、63 天和 21 天变动率。在过去三年中有三个大趋势。第一个是上涨的，因为 250 天的变动率在 2008 年 9 月之前大部分为正（1）。第二个是下跌的，因为指标从 2008 年 10 月至 2009 年 9 月变为负（2）。第三个是上涨的，因为指标在 2009 年 9 月底变为正（3）。尽管大的上升趋势仍在继续，IBM 在价格图表上趋于平稳，这影响了 125 天和 63 天的变动率。63 天的变动率（季度）自 2 月以来一直在负区域徘徊（4）。125 天的变动率（六个月）自 2009 年 4 月以来首次跌入负区域（5）。这显示了 IBM 的一些恶化情况，提醒要仔细观察该股。跌破六个月交易范围将是一个熊市发展（6）的迹象。

## 高买入/超卖极端

基本上有三种价格走势：上涨、下跌和横盘。 动量振荡器非常适合处理有规律波动的横盘价格走势。 这使得更容易识别极端点并预测转折点。 当价格趋势时，证券价格也会波动。 例如，上涨趋势由一系列高点和低点组成，价格在上涨时曲折前进。 回撤通常会根据百分比变动、经过的时间或两者同时发生的规则间隔而定期发生。 下跌趋势由一系列低点和高点组成，价格在下跌时曲折下降。 反向趋势上涨会回撤前一次下跌的一部分，并且通常会在前一高点以下达到峰值。 峰值可能会根据百分比变动、经过的时间或两者同时发生的规则间隔定期发生。 变动率指标可用于识别百分比变动接近过去预示转折点的水平的时期。

![ROC - 图表 3](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/a4ccb1f4d9d28a19dc93bb4a98be68d5.jpg "ROC - 图表 3")

图表 3 显示了 Aetna（AET）从 2009 年 4 月至 2010 年 4 月的上升趋势。 请注意股票如何曲折上升，形成一系列高点和低点。 由于总体趋势是上升的，变动率指标被用来识别短期超卖水平，作为参与更大上升趋势的机会。 短期超买信号被忽略，因为更大的趋势是上升的。 基于 5 月至 6 月的反弹，将-10%设定为超卖边界。 低于此水平的波动表明价格处于短期极端水平。 超买和超卖设置取决于基础证券的波动性。 更具波动性的股票可能会使用-15%作为超卖水平，而波动性较小的股票可能会使用-5%。 超卖读数作为警报，准备好转折点。 价格虽然超卖，但尚未实际转折。 记住，证券可能会变得超卖，并在下跌继续时保持超卖。 叠加了 20 天的移动平均线以识别实际的上升趋势。 在 10 月初变动率指标超卖后，AET 在 10 月底突破了其 20 天 SMA 以确认上升趋势（1）。 第二次超卖读数发生在 2 月初，AET 在 2 月底突破了其 20 天 SMA 以确认上升趋势（2）。

![ROC - 图表 4](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/a993f806dbac32a1bc8d7b66b85ddae7.jpg "ROC - 图表 4")

图表 4 显示了微软（MSFT）从 2007 年 11 月至 2009 年 3 月处于下降趋势。这个例子使用了一个 20 天的变动率指标来识别更大下降趋势中的超卖水平。时间周期的数量取决于个别证券和所需的交易时间框架。12 月底的高点出现在超买读数超过+10%的情况下。这意味着微软在 20 天内上涨超过 10%，大约一个月的时间。这是在更大的下降趋势中一个相当不错的反弹。下一个超买读数直到 4 月才出现，当变动率再次超过+10%。微软在 5 月突破了趋势线支撑，表明下降趋势将继续。下一个超买读数出现在 2008 年 8 月初。虽然花了一些时间，但股票最终在 9 月中旬和 10 月初再次突破了 24 的支撑位。

![ROC - 图表 5](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/20469b3708ff4c3653c405bdff5ddb32.jpg "ROC - 图表 5")

图表 5 显示了艾伯克龙比与菲奇（ANF）在 2006 年 10 月至 2008 年 2 月的交易范围内。20 天的变动率指标将超买设定为+10%，超卖设定为-10%。超买和超卖水平很好地识别了极端情况，但由于波动性较大，实际转折的时间更难确定。下一个图表通过使用指数移动平均线代替价格图来减少这种波动性。

![ROC - 图表 6](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/860eda756c50c7f025464e788594e554.jpg "ROC - 图表 6")

图表 6 显示了 ANF 作为一个 10 天的 EMA（黑色），实际价格图是不可见的。一个 30 天的 EMA 被叠加在上面作为信号线。此外，20 天的变动率指标显示了一个 5 天的 SMA 来平滑波动。使用 5 天的 SMA 会减少超买和超卖的读数。只关注买入信号，绿色虚线显示了当 ROC 超过-10%时的情况，绿色箭头显示了 10 天 EMA 穿过 30 天 SMA 时的情况。超卖读数通常较早，但移动平均线交叉通常较晚。这就是技术分析的生活。这里的重点是通过平滑数据来减少市场波动。使用 10 天 EMA 是因为它比 10 天 SMA 更快。使用 30 天 SMA 是因为它比 30 天 EMA 更慢。加快较短的移动平均线，减慢较长的移动平均线会产生稍微更快的信号。

## 结论

变动率振荡器测量价格变动的速度。变动率的上升反映了价格的急剧上涨。急剧下跌表示价格急剧下降。尽管图表分析师可以寻找多头和空头背离，但由于价格的急剧波动，这些形态可能会误导。持续的上涨通常始于大幅上涨。随后的上涨通常不那么尖锐，这导致变动率振荡器中形成空头背离。重要的是要记住，只要变动率保持为正，价格就在不断上涨。正读数可能比以前少，但正变动率仍反映价格上涨，而不是价格下跌。与所有技术指标一样，变动率振荡器应与技术分析的其他方面结合使用。

![ROC - Chart 7](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/026769ac86b1a7a02730e148e6677dbc.jpg "ROC - Chart 7")

## 使用 SharpCharts

变动率可以设置为一个指标，位于证券价格图表的上方、下方或后方。一旦从下拉列表中选择指标，就会显示默认参数设置（12）。可以调整此参数以增加或减少灵敏度。用户可以通过点击“高级选项”并选择叠加来添加移动平均线。移动平均线可用作信号线或仅用于平滑数据。还可以添加水平线以标记超买或超卖水平。[点击这里查看变动率的实时示例](http://stockcharts.com/h-sc/ui?s=$COMPQ&p=D&b=5&g=0&id=p79327039629&listNum=30&a=201216941 "http://stockcharts.com/h-sc/ui?s=$COMPQ&p=D&b=5&g=0&id=p79327039629&listNum=30&a=201216941")。

![ROC - SharpCharts](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/1dd0ac8a96ca6fced9795baacabde806.jpg "ROC - SharpCharts")

## 建议的扫描

### 超卖变动率

这个扫描显示出具有正 125 天变动率和超卖 21 天变动率（低于 -8%）的股票。一旦满足这些条件，当股票收盘价高于 20 天简单移动平均线时，就会触发一个多头信号。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily ROC(125,Daily Close) > 0] 
AND [Daily ROC(21,Daily Close) < -8] 
AND [Yesterday's Daily Close < Yesterday's Daily SMA(20,Daily Close)] 
AND [Daily Close > Daily SMA(20,Daily Close)]
```

### 超买变动率

这个扫描显示出具有负 125 天变动率和超买 21 天变动率（超过 8%）的股票。一旦满足这些条件，当股票收盘价低于 20 天简单移动平均线时，就会触发一个空头信号。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily ROC(125,Daily Close) < 0] 
AND [Daily ROC(21,Daily Close) > 8] 
AND [Yesterday's Daily Close > Yesterday's Daily SMA(20,Daily Close)] 
AND [Daily Close < Daily SMA(20,Daily Close)]
```

有关 ROC 扫描的语法细节，请参阅我们支持中心的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#rate_of_change_roc "http://stockcharts.com/docs/doku.php?id=scans:indicators#rate_of_change_roc")。

## 进一步研究

《金融市场技术分析》一书专门讨论了动量振荡器及其各种用途。墨菲涵盖了利弊以及一些特定于变动率的示例。普林的书展示了通过涵盖背离、交叉和其他信号来解释动量指标的基础知识。还有两章涵盖了具体的动量指标，并提供了大量示例。

| **金融市场技术分析** 约翰·J·墨菲 | **马丁·普林解读技术分析** 马丁·普林 |
| --- | --- |
| ![](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | ![](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |
| ![立即购买](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | ![立即购买](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |
