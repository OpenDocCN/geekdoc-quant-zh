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

![PPO - 电子表格 1](img/feeb3985cc37a52c91cea9e164ebbe18.jpg "PPO - 电子表格 1")

点击此处下载此电子表格示例。")

![PPO - 图表 1](img/1fa37710aaf5da2b2c5b012d4b48e61e.jpg "PPO - 图表 1")

标准 PPO 基于 12 日指数移动平均线（EMA）和 26 日 EMA，但这些参数可以根据投资者或交易者的偏好进行更改。收盘价格用于计算移动平均线，因此 PPO 信号应根据收盘价格进行衡量。PPO 的 9 日 EMA 被绘制为信号线，以识别指标的上升和下降。

## 解释

与 MACD 一样，PPO 反映了两个移动平均线的收敛和分歧。当较短的移动平均线高于较长的移动平均线时，PPO 为正。随着较短的移动平均线远离较长的移动平均线，指标进一步进入正区域。这反映了强劲的上行动量。当较短的移动平均线低于较长的移动平均线时，PPO 为负。当较短的移动平均线远离较长的移动平均线（变得更负）时，负读数增加。这反映了强劲的下行动量。直方图代表 PPO 和其 9 日 EMA 信号线之间的差异。当 PPO 高于其 9 日 EMA 时，直方图为正，当 PPO 低于其 9 日 EMA 时，直方图为负。PPO 直方图可用于预测 PPO 中的信号线交叉。有关信号详细信息，请参阅 MACD 直方图的 ChartSchool 文章。

## MACD、PPO 和价格

MACD 水平受到证券价格的影响。高价证券的 MACD 值将高于或低于低价证券，即使波动性基本相等。这是因为 MACD 基于两个移动平均线的绝对差异。图表 2 显示了谷歌的 MACD 和 PPO 以进行比较。12 日 EMA 约为 495，26 日 EMA 约为 512，差值为-17（两位数）。请注意，谷歌的 MACD 在上升和下降时都达到了两位数，但百分比价格振荡器范围从+2.5 到-3.5。MACD 值看起来较高，因为谷歌的价格相对较高。道琼斯工业指数的 MACD，超过 10,000，经常达到三位数。然而，PPO 范围从-2 到+2，这是一个更可定义的范围。

![PPO - 图表 2](img/b68ad8f268f627526c03d429d6b7cf76.jpg "PPO - 图表 2")

尽管指标线看起来相同，但 MACD 和 PPO 之间通常存在细微差异。在谷歌的例子中，请注意 PPO 跌破了二月低点，但 MACD 尚未跌破其二月低点。PPO 的较低低点显示了扩大的下行动量。

## 大幅价格变动

由于 MACD 是基于绝对水平的，大幅价格变动会在较长时间内影响 MACD 水平。如果一支股票从 20 涨到 100，其 MACD 水平在 20 左右会比在 100 左右要小得多。PPO 通过以百分比形式显示 MACD 值来解决这个问题。图表 3 显示了百度（BIDU）在 12 个月内从 25 涨到 75。在 25-30 左右的 MACD 值通常会比 70-80 左右的 MACD 值要小。请注意，MACD 突破了 7 月和 3 月的高点，但 PPO 没有突破这些相应的高点。还要注意，当 PPO 超过+5 时，百度会变得超买。

![PPO - 图表 3](img/babd0c1366955faf4d73da738a5fe4d6.jpg "PPO - 图表 3")

## 比较不同证券

由于百分比价格振荡器（PPO）是 MACD 的百分比版本，其值可以与其他证券进行比较。戴尔（DELL）和惠普（HPQ）属于同一行业集团，但其股价水平不同。截至 2010 年 5 月底，DELL 的股价在高十几美元，而 HPQ 的股价在中 40 美元。绝对价格水平与基本面无关，但会影响 MACD 水平。HPQ 的 MACD 无疑会高于 DELL。然而，我们可以应用百分比价格振荡器（PPO）来比较动量。首先，注意到 DELL 的 PPO 范围为-4 至+4，共 8 个点）。HPQ 的 PPO 范围为-3 至+2，共 5 个点。我们可以立即看出 DELL 比 HPQ 更具波动性，因为其 PPO 范围更大。其次，我们可以看到 DELL 在 3 月至 4 月的上涨动量比 HPQ 更强。DELL 的 PPO 从负值区域上升并超过 4。HPQ 的 PPO 在 DELL 之前转为正值，但未超过 1.6。

![PPO - 图表 4](img/3a830512b30d595878959d86e2cf2bc1.jpg "PPO - 图表 4")

![PPO - 图表 5](img/d1c7e0c90b92aaf0ed49acbbfe7dc18c.jpg "PPO - 图表 5")

## 结论

百分比价格振荡器（PPO）产生与 MACD 相同的信号，但作为 MACD 的百分比版本提供了一个额外的维度。道琼斯工业指数（价格约 11000）的 PPO 水平可以与 IBM（价格约 122）的 PPO 水平进行比较，因为 PPO“水平化”了竞争环境。此外，即使价格翻倍或翻三倍，也可以比较一个证券的 PPO 水平，这对于 MACD 来说并非如此。尽管具有优势，但 PPO 仍不是最佳振荡器来识别超买或超卖条件，因为运动是无限的（理论上）。RSI 和随机指标的水平是有限的，这使它们更适合识别超买和超卖水平。

## 使用 SharpCharts

PPO 可以设置为证券价格图表的上方、下方或后方的指标。一旦从下拉列表中选择指标，将显示默认参数设置（12,26,9）。这些参数可以调整以增加或减少灵敏度。较慢的长期移动平均线与较快的短期移动平均线组合将增加灵敏度。通过将信号线参数设置为 1，可以移除直方图。在显示证券价格图表后面的 PPO 时，这很有帮助。用户甚至可以通过将 9 日 EMA 应用于 PPO 来重新添加信号线。单击“高级选项”以将移动平均线添加为指标的叠加层。[点击此处查看 PPO 的实时示例](http://stockcharts.com/h-sc/ui?s=$INDU&p=D&yr=0&mn=6&dy=0&id=p81462571466&listNum=30&a=201062788 "http://stockcharts.com/h-sc/ui?s=$INDU&p=D&yr=0&mn=6&dy=0&id=p81462571466&listNum=30&a=201062788")。

![PPO - 图表 7](img/05c008550c47d098135d4d45fd4708c9.jpg "PPO - 图表 7")

![PPO - 图表 6](img/d4aff4f51a1507d181bc90a7345f3b82.jpg "PPO - 图表 6")

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
