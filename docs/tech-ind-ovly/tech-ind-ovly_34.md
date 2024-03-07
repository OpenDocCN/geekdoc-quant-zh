# MACD-Histogram [ChartSchool]

### 目录

+   [MACD-Histogram](#macd-histogram)

    +   [介绍](#introduction)

    +   [计算](#calculation)

    +   [去除的四个步骤](#four_steps_removed)

    +   [解释](#interpretation)

    +   [峰谷分歧](#peak-trough_divergence)

    +   [倾斜分歧](#slant_divergence)

    +   [结论](#conclusions)

    +   [与SharpCharts一起使用](#using_with_sharpcharts)

    +   [建议的扫描](#suggested_scans)

        +   [MACD-Histogram 转为正数](#macd-histogram_turns_positive)

        +   [MACD-Histogram 转为负数](#macd-histogram_turns_negative)

    +   [进一步研究](#further_study)

## 介绍

由Thomas Aspray于1986年开发，MACD-Histogram衡量了MACD与其信号线（MACD的9日EMA）之间的距离。与MACD一样，MACD-Histogram也是一个在零线上下波动的振荡器。Aspray开发了MACD-Histogram来预测MACD中的信号线交叉。因为MACD使用移动平均线，而移动平均线滞后于价格，信号线交叉可能会来得晚，并影响交易的风险收益比。MACD-Histogram中的多头或空头分歧可以提醒图表分析师即将发生的MACD中的信号线交叉。查看我们的[ChartSchool文章](/school/doku.php?id=chart_school:technical_indicators:moving_average_convergence_divergence_macd "chart_school:technical_indicators:moving_average_convergence_divergence_macd")了解更多关于MACD的信息。

## 计算

```py
MACD: (12-day EMA - 26-day EMA) 

Signal Line: 9-day EMA of MACD

MACD Histogram: MACD - Signal Line

```

标准MACD是12日指数[移动平均线](/school/doku.php?id=chart_school:technical_indicators:moving_averages "chart_school:technical_indicators:moving_averages")（EMA）减去26日EMA。收盘价用于形成移动平均线，因此MACD。MACD的9日EMA被绘制在旁边，作为一个信号线，用于识别指标的转折点。MACD-Histogram代表MACD和其9日EMA信号线之间的差异。当MACD高于其9日EMA时，直方图为正，当MACD低于其9日EMA时，直方图为负。

![MACD - 示例](../Images/3ce03c762d1297743e8a8026a569b750.jpg "MACD - 示例")

## 去除的四个步骤

MACD-Histogram是一个指标的指标。事实上，MACD也是一个指标的指标。这意味着MACD-Histogram与基础证券价格相隔四个步骤。换句话说，它是价格的第四导数。

+   第一导数：12日EMA和26日EMA

+   第二导数：MACD（12日EMA减去26日EMA）

+   第三导数：MACD信号线（MACD的9日EMA）

+   第四导数：MACD-Histogram（MACD减去MACD信号线）

该指标的基础是证券的价格。从实际价格到MACD-Histogram需要四个步骤。谈论数据的处理。虽然这不一定是坏事，但图表分析师在分析MACD-Histogram时应牢记这一点。这是一个指标的指标。因此，它旨在预测MACD中的信号，而MACD又旨在识别基础证券价格的变化[动量](/school/doku.php?id=chart_school:technical_indicators:rate_of_change_roc_and_momentum "chart_school:technical_indicators:rate_of_change_roc_and_momentum")。

## 解释

与MACD一样，MACD-Histogram也旨在识别收敛、背离和交叉。然而，MACD-Histogram是测量MACD与其信号线之间的距离。当MACD高于其信号线时，直方图为正值。随着MACD进一步背离其信号线（向上），正值增加。当MACD和其信号线收敛时，正值减少。当MACD穿过零线时，MACD-Histogram为负值。当MACD低于其信号线时，指标为负值。随着MACD进一步背离其信号线（向下），负值增加。相反，当MACD收敛于其信号线时，负值减少。

![](../Images/02bb64289386dab91b16988721b2b986.jpg)

图表1显示了Darden Restaurants (DRI)的MACD和MACD-Histogram。在9月底发生了一个空头信号线交叉，这使得MACD-Histogram变为负值。在12月初发生了一个多头信号线交叉，这使得MACD-Histogram在该月的其余时间内为正值。随着MACD进一步远离其信号线（绿线），出现了背离期和随着MACD接近其信号线（红线）的收敛期。

## 峰谷背离

MACD-Histogram通过形成牛市和[熊市背离](/school/doku.php?id=chart_school:glossary_b#bearish_divergence "chart_school:glossary_b")来预测MACD中的信号线交叉。这些背离信号表明MACD正在收敛于其信号线，并可能准备交叉。有两种类型的背离：峰谷和斜线。峰谷背离在MACD-Histogram中形成两个峰值或两个谷值。当MACD形成一个较低低点，而MACD-Histogram形成一个较高低点时，就形成了峰谷牛市背离。明确定义的谷值对于峰谷背离的稳健性至关重要。图表2显示了卡特彼勒（Caterpillar）MACD-Histogram中的一个牛市背离。请注意，MACD在6月至7月间走到了一个较低低点，但MACD-Histogram形成了一个较高低点（谷值）。有两个明显的谷值。这种牛市背离预示了7月中旬的多头信号线交叉和一次大涨。 

![MACD-Histogram - 图表2](../Images/ab246bbc508d9cc394d43a23a5b751bf.jpg "MACD-Histogram - 图表2")

图表 3 显示 Aeropostale（ARO）在 2009 年 8 月至 9 月出现了看跌背离。MACD 在 9 月达到新高，但 MACD-Histogram 形成了一个较低的高点。请注意，MACD-Histogram（红线）上有两个明确的峰值（更高），中间有一个低点。随后的看跌信号线交叉预示了股票的急剧下跌。

![MACD-Histogram - 图表 3](../Images/256f789aa3f3eda786387925dc8466ac.jpg "MACD-Histogram - 图表 3")

## 倾斜背离

正如其名称所示，倾斜背离形成时没有明确定义的峰值或谷值。与两个反应高点不同，MACD-Histogram 只是向零线倾斜。这种朝零线倾斜反映了 MACD 和其信号线之间的收敛。换句话说，它们彼此越来越接近。当 MACD 远离其信号线并且 MACD-Histogram 扩大时，动量显示出强劲。当 MACD 靠近其信号线并且 MACD-Histogram 收缩时，动量减弱。收缩的 MACD-Histogram 是信号线交叉的第一步。

图表 4 显示波音（Boeing）在 MACD-Histogram 中出现了经典的倾斜背离。在 2009 年 6 月的空头信号线交叉后，MACD 迅速下降。MACD 在 7 月中旬达到新低，但 MACD-Histogram 保持远高于先前的低点。事实上，MACD-Histogram 在 6 月底触底并形成了一种看涨的倾斜背离。粗红线显示了 MACD 与其信号线之间的距离。有时在图表上很难判断距离，因此这些线突出了 6 月 26 日和 7 月 8 日之间的差异。这种倾斜背离预示了 7 月中旬的看涨信号线交叉和股票的急剧上涨。

![MACD-Histogram - 图表 4](../Images/0656008c452b2a376f0abef254989b97.jpg "MACD-Histogram - 图表 4")

图表 5 显示迪士尼（Disney）在 2008 年 5 月出现了看跌的倾斜背离。请注意，MACD 在 5 月 16 日继续达到新高，但 MACD-Histogram 在 5 月 8 日达到峰值并形成了倾斜背离。MACD 的上涨动能减弱，指标移动到其信号线下方，预示股票的急剧下跌。这张图表还显示了 3 月至 4 月间的一个不错的看涨背离。

![MACD-Histogram - 图表 5](../Images/240251697f522a74972a0bb308390ed7.jpg "MACD-Histogram - 图表 5")

## 结论

MACD-Histogram 是一个旨在预测 MACD 信号线交叉的指标。通过延伸，它被设计为这些信号线交叉的早期警报系统，这些信号线交叉是 MACD 信号中最频繁的。MACD-Histogram 中的背离可用于过滤信号线交叉，从而减少信号数量。即使有过滤器，MACD-Histogram 背离的稳健性仍然是一个问题。短而浅的背离比长而大的背离更常见。换句话说，几天内发展出浅动作的背离通常比几周内发展出更明显动作的背离不够稳健。信号线交叉提供了最终确认，但积极的交易者可能会尝试在交叉之前通过使自己的动作尽可能接近零线来改善回报风险比。这通常发生在 -.20 和 +.20 之间的 MACD-Histogram。

## 使用 SharpCharts

MACD 包含 MACD-Histogram，但是 MACD-Histogram 可以作为独立指标显示。这样更容易识别背离和交叉点。MACD-Histogram 可以设置为基础证券价格图表的指标之上、之下或之后。直方图占据了很多图表空间，因此最好将其放置在主窗口之上或之下。也可以在主窗口中显示不带直方图的 MACD。选择 MACD 作为指标，并将信号线数字从 9 改为 1（9,26,1）。这将删除信号线和直方图。信号线可以通过点击高级指标选项并添加一个 9 天的 EMA 来单独添加。

[点击此处查看实时图表](http://stockcharts.com/h-sc/ui?s=$INDU&p=D&b=5&g=0&id=p59749230423&listNum=30&a=199515976 "http://stockcharts.com/h-sc/ui?s=$INDU&p=D&b=5&g=0&id=p59749230423&listNum=30&a=199515976")，展示 MACD-Histogram。

![MACD-Histogram - 图表 6](../Images/f147f387e412e93098fbcbbed505f1ba.jpg "MACD-Histogram - 图表 6")

![MACD - 图表 7](../Images/d0e0483cce2b025663909f8a8430f885.jpg "MACD - 图表 7")

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

欲了解有关MACD-Histogram扫描的语法，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#macd_histogram_macd_hist "http://stockcharts.com/docs/doku.php?id=scans:indicators#macd_histogram_macd_hist")。

## 进一步学习

技术分析 - 积极投资者的强大工具提供了一套完整的市场预测课程，由MACD的创始人编写。短期、中期和长期策略均有详细解释，其中许多包含MACD。

| **技术分析 - 积极投资者的强大工具** 杰拉德·阿普尔 |
| --- |
| [![](../Images/a2673256615cb182a677e60a34c2b755.jpg)](http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors "http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors") |
| [![立即购买](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "立即购买")](http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors "http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors") |
