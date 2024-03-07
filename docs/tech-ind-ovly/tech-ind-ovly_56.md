# 威廉斯%R [图表学校]

### 目录

+   [威廉斯%R](#williams_r)

    +   [介绍](#introduction)

    +   [计算](#calculation)

    +   [解释](#interpretation)

    +   [超买/超卖](#overbought_oversold)

    +   [动量失败](#momentum_failure)

    +   [结论](#conclusions)

    +   [与SharpCharts一起使用](#using_with_sharpcharts)

    +   [建议的扫描](#suggested_scans)

        +   [威廉斯%R从超卖水平上升](#williams_r_turns_up_from_oversold_levels)

        +   [威廉斯%R从超买水平下降](#williams_r_turns_down_from_overbought_levels)

    +   [进一步研究](#further_study)

## 介绍

由Larry Williams开发，威廉斯%R是一个动量指标，是快速[随机振荡器](/school/doku.php?id=chart_school:technical_indicators:stochastic_oscillator_fast_slow_and_full "chart_school:technical_indicators:stochastic_oscillator_fast_slow_and_full")的倒数。也称为%R，威廉斯%R反映了收盘价相对于回顾期内最高价的水平。相比之下，随机振荡器反映了收盘价相对于最低价的水平。%R通过将原始值乘以-100来纠正反转。因此，快速随机振荡器和威廉斯%R产生完全相同的线，只是比例不同。威廉斯%R在0到-100之间振荡。0到-20的读数被认为是超买的。-80到-100的读数被认为是超卖的。毫不奇怪，从随机振荡器派生的信号也适用于威廉斯%R。

## 计算

```py
%R = (Highest High - Close)/(Highest High - Lowest Low) * -100

Lowest Low = lowest low for the look-back period
Highest High = highest high for the look-back period
%R is multiplied by -100 correct the inversion and move the decimal.

```

威廉斯%R的默认设置是14个周期，可以是天、周、月或日内时间框架。14个周期的%R将使用最近的收盘价，过去14个周期内的最高价和最低价。

![威廉斯%R - 电子表格1](../Images/51afcb57b78555587d0b04e2bf973269.jpg "威廉斯%R - 电子表格1")

[点击这里下载这个电子表格示例。](/school/lib/exe/fetch.php?media=chart_school:technical_indicators_and_overlays:williams_r:cs-percentr.xls "chart_school:technical_indicators_and_overlays:williams_r:cs-percentr.xls (13 KB)")

![威廉斯%R - 图表1](../Images/e422bdda4a35e63a679d03ff6e1c8b30.jpg "威廉斯%R - 图表1")

## 解释

与随机振荡器类似，威廉斯%R反映了收盘价相对于一定时间内的最高-最低范围的水平。假设最高价为110，最低价为100，收盘价为108。最高-最低范围为10（110-100），这是%R公式中的分母。最高价减去收盘价为2（110-108），这是分子。0.2除以10等于0.20。将这个数字乘以-100得到%R为-20。如果收盘价为103，威廉斯%R将为-70（（（110-103）/10）x -100）。

中线，-50，是一个重要的观察水平。威廉斯%R在0和-100之间波动，这使得-50成为中点。可以将其视为橄榄球场上的50码线。当进攻队越过50码线时，得分的机会更大。只要防守阻止进攻队越过50码线，防守就有优势。威廉斯%R穿过-50表示价格正在给定回顾期内的高低范围的上半部交易。这表明杯子是半满的。相反，穿过-50意味着价格正在给定回顾期内的底部交易。这表明杯子是半空的。

低读数（低于-80）表示价格接近给定时间段的低点。高读数（高于-20）表示价格接近给定时间段的高点。上面的IBM示例显示了三个14天范围（黄色区域），期末的收盘价（红色虚线）。当收盘价位于范围顶部时，威廉斯%R等于-9。当收盘价接近范围底部时，威廉斯%R等于-87。当收盘价位于范围中间时，收盘价等于-43。

## 超买/超卖

作为[边界振荡器](/school/doku.php?id=chart_school:technical_indicators:introduction_to_technical_indicators_and_oscillators#banded_oscillators)，威廉斯%R使得识别超买和超卖水平变得容易。该振荡器的范围从0到-100。无论证券是如何快速上涨或下跌，威廉斯%R始终在此范围内波动。传统设置使用-20作为超买阈值，-80作为超卖阈值。这些水平可以根据分析需求和证券特性进行调整。14天威廉斯%R的读数超过-20表示基础证券正在接近其14天高低范围的顶部。读数低于-80表示证券正在交易其高低范围的低端。

在查看一些图表示例之前，重要的是要注意，超买读数并不一定是熊市的信号。证券可以在强劲的上涨趋势中变得超买并保持超买状态。持续接近范围顶部的收盘水平表明持续的买盘压力。同样，超卖读数也不一定是看涨的。证券也可以在强劲的下跌趋势中变得超卖并保持超卖状态。持续接近范围底部的收盘水平表明持续的卖盘压力。

图表3显示了阿奇煤炭公司（ACI）的14天威廉指标%R经常触及超买和超卖水平。红色虚线标记了超买信号后下跌至-50以下的情况。绿色虚线标记了超卖信号后上涨至-50以上的情况。如上所述，超买并不一定是熊市信号，超卖也不一定是牛市信号。顶部和底部选择者可以在超买或超卖时采取行动，但等待确认动作通常是明智的。在超买信号后下跌至-50以下确认了下跌。在超卖信号后上涨至-50以上确认了上涨。

![威廉指标 - 图表 2](../Images/5a12e340ed89ce4488a03cf12ccb53a3.jpg "威廉指标 - 图表 2")

## 动量失败

未能重新进入超买或超卖区域表明了动量的变化，可能预示着重大价格波动。能够持续上移至-20以上显示出了强势。毕竟，需要买盘压力才能将%R推入超买区域。一旦一项证券通过多次进入超买区域显示出了强势，随后未能超过此水平的失败表明了动量的减弱，可能预示着下跌。

![威廉指标 - 图表 3](../Images/585d3c2879b10d235ab38ab3061382da.jpg "威廉指标 - 图表 3")

上图显示了思科公司的14天%R。该股票在2月至4月间表现强劲，出现了许多超买信号。即使在4月初跌破-80之后，%R又迅速回升至-20以上，显示出持续的强势。经过几周的超买信号后，%R在5月初暴跌至超卖水平。这次急剧的暴跌显示出强烈的卖压。随后的反弹未能达到-20以下，也未能达到超买区域。这是第二个弱势信号。在跌破-20以下后，跌破-50标志着动量的下降，股票急剧下跌。6月中旬再次在-20以下失败也导致了急剧下跌。

![威廉指标 - 图表 4](../Images/be7846a9f4a14899a4e36eff7425d7c1.jpg "威廉指标 - 图表 4")

上图显示了TJX公司（TJX）的28天威廉指标%R。图表分析师可以调整回溯期以适应其分析目标。较长的时间框架使指标变得不太敏感。在10月份超买后，指标下跌并在12月两次超卖。1月份的激增将%R推入超买区域，股票突破了通道阻力。这些都是有希望的迹象。在随后的回调中，%R保持在-80以上，并未超卖。这显示了潜在的强势。随后的上移超过-50预示着接下来几个月的急剧上涨。

## 结论

威廉斯%R是一种动量振荡器，它测量收盘价相对于一定时间内的高低范围的水平。除了上述信号外，图表分析师还可以使用%R来衡量某种证券的六个月趋势。125天的%R大约涵盖了6个月。当%R高于-50时，价格高于其6个月平均值，这与上升趋势一致。当%R低于-50时，读数与下降趋势一致。在这方面，%R可用于帮助定义更大的趋势（六个月）。与所有技术指标一样，重要的是将威廉斯%R与其他技术分析工具结合使用。成交量、[图表模式](/school/doku.php?id=chart_school:chart_analysis:chart_patterns "chart_school:chart_analysis:chart_patterns")和突破可以用来确认或否定威廉斯%R产生的信号。

![威廉斯%R - 图表5](../Images/869f99f54000240efce3365bff4ab23c.jpg "威廉斯%R - 图表5")

## 使用SharpCharts

威廉斯%R可作为SharpCharts的指标。默认设置为14，但用户可以选择更短的时间框架以产生更敏感的振荡器，或者选择更长的时间框架以产生更不敏感的振荡器。一旦选择，指标可以放置在基础价格图表的上方、下方或后面。单击“高级选项”以添加移动平均线、水平线或另一个指标。可以添加3天的SMA作为信号线。[点击这里查看实时示例](http://stockcharts.com/h-sc/ui?s=QQQQ&p=D&yr=0&mn=6&dy=0&id=p67764551359&listNum=30&a=219822109 "http://stockcharts.com/h-sc/ui?s=QQQQ&p=D&yr=0&mn=6&dy=0&id=p67764551359&listNum=30&a=219822109")。

![威廉斯%R - 图表6](../Images/5aa5b36643c4b574760eeff9ec4c1410.jpg "威廉斯%R - 图表6")

![威廉斯%R - SharpCharts](../Images/0bf13ab89cb754aa90f8109262e4fcc7.jpg "威廉斯%R - SharpCharts")

## 建议扫描

### 威廉斯%R从超卖水平上升

此扫描搜索交易在其200日移动平均线上方的股票，以定义长期上升趋势。当%R移动到-80以下时，识别回撤，当%R移动到-50以上时，发生随后的上涨。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily Close > Daily SMA(200,Daily Close)] 
AND [20 days ago Daily Williams %R(14) < -80] 
AND [Daily Williams %R(14) crosses -50]
```

### 威廉斯%R从超买水平下降

此扫描搜索交易在其200日移动平均线下方的股票，以定义长期下降趋势。当%R移动到-20以上时，识别超卖反弹，当%R移动到-50以下时，发生随后的下降。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily Close < Daily SMA(200,Daily Close)] 
AND [20 days ago Daily Williams %R(14) > -20] 
AND [-50 crosses Daily Williams %R(14)]
```

有关威廉斯%R扫描的语法详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#williams_r_williams_r "http://stockcharts.com/docs/doku.php?id=scans:indicators#williams_r_williams_r")在支持中心。

## 进一步研究

《金融市场技术分析》一书专门讨论了动量振荡器及其各种用途。墨菲涵盖了%R和随机振荡器的利弊以及一些具体示例。

Pring的书展示了动量指标的基础知识，涵盖了背离、交叉和其他信号。还有两章专门介绍了具体的动量指标，并附有大量示例。

| **金融市场技术分析** 约翰·J·墨菲 | **马丁·普林格的技术分析解析** 马丁·普林格 |
| --- | --- |
| [![](../Images/d9fb5f53997f0c87918070e360d1437d.jpg)](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | [![](../Images/907bb9e1dca336b6bedb79166d8efb0e.jpg)](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |
| [![立即购买](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "立即购买")](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | [![立即购买](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "立即购买")](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |
