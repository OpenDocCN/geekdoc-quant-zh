# StochRSI 

### 目录

+   StochRSI

    +   介绍

    +   计算

    +   解释

    +   超买/超卖

    +   趋势识别

    +   结论

    +   与 SharpCharts 一起使用

    +   建议的扫描

        +   中期上升趋势中的超卖 StochRSI

        +   中期下降趋势中的超买 StochRSI

    +   进一步研究

## 介绍

由图沙尔·钱德和斯坦利·克罗尔开发的 StochRSI 是一个振荡器，它测量 RSI 相对于其一定时间段内的高低范围的水平。StochRSI 将随机指标公式应用于 RSI 值，而不是价格值。这使其成为指标的指标。结果是一个在 0 和 1 之间波动的振荡器。

在他们 1994 年的书籍《*新技术交易者*》中，钱德和克罗尔解释说，RSI 可以在长时间内在 80 和 20 之间振荡，而不会达到极端水平。请注意，用于超买和超卖的是 80 和 20，而不是更传统的 70 和 30。基于 RSI 的超买或超卖读数进入股票的交易者可能会发现自己不断地处于观望状态。钱德和克罗尔开发了 StochRSI 以增加灵敏度并产生更多的超买/超卖信号。

## 计算

```py
StochRSI = (RSI - Lowest Low RSI) / (Highest High RSI - Lowest Low RSI)

```

StochRSI 测量 RSI 相对于其一定周期内的高/低范围的价值。用于计算 StochRSI 的周期数在公式中转移到 RSI。例如，14 天 StochRSI 将使用当前的 14 天 RSI 值和 14 天 RSI 的高低范围。

+   当 RSI 在 14 天内处于最低点时，14 天 StochRSI 等于 0。

+   当 RSI 在 14 天内达到最高点时，14 天 StochRSI 等于 1。

+   当 RSI 处于其 14 天高低范围的中间时，14 天 StochRSI 等于 0.5。

+   当 RSI 接近其 14 天高低范围的低点时，14 天 StochRSI 等于 0.2。

+   当 RSI 接近其 14 天高低范围的高点时，14 天 StochRSI 等于 0.80。

![RSI - Spreadsheet 1](img/83b6cba9d8a97382016677172d47ad98.jpg "RSI - Spreadsheet 1")

点击这里查看一个 Excel 电子表格")，展示了 StochRSI 计算的开始。

## 解释

重要的是要记住，StochRSI 是一个指标的指标，这使得它成为价格的二阶导数。这意味着它距离基础证券的价格有两个步骤（公式）。价格经历了两次变化才变成了 StochRSI。将价格转换为 RSI 是一次变化。将 RSI 转换为随机振荡器是第二次变化。这就是为什么最终产品（StochRSI）看起来与原始产品（价格）大不相同。

![StochRSI - 图表 1](img/20ed1e9623985b93a14b16ef7f3adbfb.jpg "StochRSI - 图表 1")

StochRSI 具有与大多数有界动量振荡器相似的特征。首先，它可以用于识别超买或超卖条件。移动超过 .80 被认为是超买，而移动低于 .20 被认为是超卖。其次，它可以用于识别短期趋势。作为一个有界振荡器，中心线在 .50。当 StochRSI 一直在 .50 以上时，反映了上升趋势，而当一直在 .50 以下时，反映了下降趋势。由于这个指标相当波动，一些移动平均线的平滑可以帮助进行短期趋势识别。

## 超买/超卖

趋势识别是成功选择超买和超卖水平之间的关键。当大趋势向上时，重要的是寻找超卖条件，当大趋势向下时，寻找超买条件。换句话说，寻找与大趋势方向相同的交易。14 天 StochRSI 将被视为短期指标。因此，在寻找超买和超卖条件时，重要的是确定中期趋势。

图表 2 显示波音处于中期上升趋势，StochRSI(14) 在一月和二月变得超卖。首先，中期被认为是上升的，因为 10 天简单移动平均线高于 60 天简单移动平均线。在上升趋势中，超卖条件优于超买条件。从十二月到二月，StochRSI 至少四次变得超卖。值得一提的是，14 天 RSI 在此时间段内没有变得超卖，因为它的灵敏度较低。然而，超卖并不等同于看涨。它只是一个警告，需要留意反弹。仍然需要一个催化剂来巩固低点并信号实际的上升。在这个例子中，技术分析师可以寻找价格突破 10 天简单移动平均线或 StochRSI 突破 .50，即其中心线。

![StochRSI - 图表 2](img/4684ffd98a5ee367ffe1cf5f2aad5196.jpg "StochRSI - 图表 2")

图表 3 显示了 Flour Corp (FLR) 处于下降趋势中，而 StochRSI 记录了超买读数。首先，中期趋势向下，因为 10 天的简单移动平均线低于 60 天的简单移动平均线。这意味着超卖读数被忽略，而超买读数成为焦点。StochRSI 在 10 月中旬和 11 月初（红色箭头）上升到 0.80 以上。这些超买读数表明超卖反弹可能很快结束。确认的时机是当 StochRSI 再次下降到 0.50 以下（红色虚线）。图表技术分析师还可以观察股票是否跌破其 10 天的简单移动平均线，以信号短期下行趋势。

![StochRSI - 图表 3](img/19df9fc89d44e62c63aeec41694d9a98.jpg "StochRSI - 图表 3")

## 趋势识别

StochRSI 是一个相当波动的振荡器，经常出现超买和超卖情况。对于短期趋势识别，可以延长计算周期并应用短期移动平均线来平滑数据。当 StochRSI 的 10 天简单移动平均线高于 0.50 时，动量有利于价格上涨；当低于 0.50 时，价格下跌。图表 4 显示了 Chevron (CVX) 的 20 天 StochRSI 和指标的 5 天简单移动平均线。5 天简单移动平均线在 2 月中旬刚好在股票上涨后突破了 0.50。跳空和移动平均线突破 0.50 是短期看涨信号。2 月底形成了一个下降旗形/楔形。注意 CVX 如何在跳空区域找到支撑。上升趋势随着旗形/楔形突破继续，股票上涨至 80 以上。即使 StochRSI 在 3 月底跌破 0.50，5 天简单移动平均线仍然保持在 0.50 以上，维持上升趋势直到 4 月底。这个短期信号演变成了两个月的上升趋势。

![StochRSI - 图表 4](img/2fb2e755dbe320b3a945546e945b9343.jpg "StochRSI - 图表 4")

不幸的是，并非所有信号都是如此完美。即使使用 20 天 StochRSI 和 5 天简单移动平均线，也会出现误导，例如，在趋势中的整理可能导致 StochRSI 的 5 天简单移动平均线在 0.50 线上/下摆动，然后继续或逆转趋势。图表 5 显示了 Yahoo! 的 20 天 StochRSI 和其用于平滑的 5 天简单移动平均线。移动平均线在 2 月中旬突破了 0.50，将动量转为看涨。这之后，Yahoo! 在 3 月初第一天突破了阻力。随着股票在 3 月底以下降通道整理，StochRSI(20) 的 5 天简单移动平均线两次跌破了 0.50（红色椭圆）。这些下跌是短暂的，因为股票突破了通道阻力，StochRSI 上升到 0.80 以上显示出力量。趋势直到 5 天简单移动平均线跌破 0.50 并且 Yahoo! 跳空下跌才结束。

![StochRSI - 图表 5](img/40ea01fccb7ccba2d6768a1bcb6b58c2.jpg "StochRSI - 图表 5")

图表 6 显示了雅虎的 StochRSI 发出的一个熊市信号，但并没有立即生效。10 日 StochRSI 的 5 日 SMA 在 10 月第二周下跌至 0.50 以下，将动量转为熊市。雅虎突破支撑线以确认，但这一突破并没有持续，因为股价几天后飙升至 18 美元。随后的迅速恢复并回升至 17 美元以上形成了一个熊市陷阱。尽管雅虎股价飙升，但 10 日 StochRSI 的 5 日 SMA 仍然低于 0.50，动量没有确认。随后超过 17.50 美元的间隙被证明是一次耗竭间隙，因为雅虎在阻力位（18 美元）受阻，填补了间隙，再次突破支撑线并在 11 月急剧下跌。谈论波动性。

![StochRSI - 图表 6](img/7e2db67035caa76527c4ab377c9f5989.jpg "StochRSI - 图表 6")

## 结论

StochRSI 就像是强化版的 RSI。RSI 产生相对较少的信号，而 StochRSI 大幅增加了信号数量。会有更多的超买/超卖读数，更多的中线交叉，更多的好信号和坏信号。速度是有代价的。这意味着重要的是将 StochRSI 与技术分析的其他方面结合起来进行确认。上面的示例使用间隙、支撑/阻力突破和价格模式来确认 StochRSI 信号。图表分析师还可以使用其他互补指标，如累积/派发线或成交量平衡线。这些基于成交量的指标不会与动量振荡器重叠。图表分析师还应该尝试不同的设置，并在真实世界中使用 StochRSI 之前学习 StochRSI 的微妙之处。

## 使用 SharpCharts

StochRSI 指标可以使用 SharpCharts 工具作为指标进行绘制。 “参数”值指定了计算中使用的周期数（默认为 14）。指标可以设置在基础价格图之上、之下或之后。可以通过点击高级选项箭头（绿色）并添加叠加来应用移动平均线。[点击这里](http://stockcharts.com/h-sc/ui?s=QQQ&p=D&yr=0&mn=5&dy=0&id=p80628063848&listNum=30&a=203042536 "http://stockcharts.com/h-sc/ui?s=QQQ&p=D&yr=0&mn=5&dy=0&id=p80628063848&listNum=30&a=203042536") 查看 StochRSI 的实时示例。

![StochRSI - SharpCharts](img/6905798c23cbc7d7321a62468586ebf5.jpg "StochRSI - SharpCharts")

## 建议的扫描

### 中期上涨趋势中的超卖 StochRSI

这个扫描从过去三个月内平均价格大于$10 且平均成交量大于 40,000 的股票开始。第一个筛选器通过查找 10 日 SMA 大于 60 日 SMA 的股票来选择中期上涨趋势中的证券。然后，通过查找交易价格低于其 10 日 SMA 且 StochRSI(14)低于 0.10 的股票来选择短期超卖的股票。这个扫描通常会返回许多股票，可能需要进一步细化。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [Daily SMA(10,Daily Close) > Daily SMA(60,Daily Close)] 
AND [Daily Stoch RSI(14) < 0.1] 
AND [Daily Close < Daily SMA(10,Daily Close)]
```

### 中期下跌趋势中的超买 StochRSI

这个扫描从过去三个月平均价格超过$10 且平均交易量大于 40,000 的股票开始。第一个筛选器通过查找 10 日 SMA 小于 60 日 SMA 的证券来选择处于中期下跌趋势中的证券。然后，屏幕选择短期超买的股票，通过查找那些交易价格高于它们的 10 日 SMA 且 StochRSI(14)高于 0.90 的股票。这个扫描通常会返回许多股票，可能需要进一步细化。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [Daily SMA(10,Daily Close) < Daily SMA(60,Daily Close)] 
AND [Daily Stoch RSI(14) > 0.9] 
AND [Daily Close > Daily SMA(10,Daily Close)]
```

欲了解有关 StochRSI 扫描的语法的更多详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#stochastic_rsi_stoch_rsi "http://stockcharts.com/docs/doku.php?id=scans:indicators#stochastic_rsi_stoch_rsi")在支持中心中。

## 进一步研究

布朗将 RSI 带入新的层次，包括牛市和熊市范围，正面和负面反转，以及基于 RSI 的预测。一些安德鲁·卡德韦尔的方法，她的 RSI 导师，也在这本书中得到解释和完善。

| **专业交易技术分析** 康斯坦斯·布朗 |
| --- |
| ![](http://store.stockcharts.com/products/technical-analysis-for-the-trading-professional "http://store.stockcharts.com/products/technical-analysis-for-the-trading-professional") |
| ![立即购买](http://store.stockcharts.com/products/technical-analysis-for-the-trading-professional "http://store.stockcharts.com/products/technical-analysis-for-the-trading-professional") |
