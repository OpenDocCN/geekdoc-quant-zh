# 价格相对 / 相对强度 [ChartSchool]

### 目录

+   [价格相对 / 相对强度](#price_relative_relative_strength)

    +   [介绍](#introduction)

    +   [计算](#calculation)

    +   [解释](#interpretation)

    +   [趋势识别](#trend_identification)

    +   [看涨/看跌背离](#bullish_bearish_divergences)

    +   [结论](#conclusions)

    +   [使用SharpCharts](#using_with_sharpcharts)

    +   [进一步研究](#further_study)

    +   [额外资源](#additional_resources)

        +   [股票与商品杂志文章](#stocks_commodities_magazine_articles)

## 介绍

价格相对指标通过比率图表将一个证券的表现与另一个证券进行比较。这个指标也被称为相对强度指标，有时也被称为相对强度比较。通常，价格相对指标用于比较股票与基准指数（如标普500指数）的表现。图表分析师还可以使用价格相对指标来比较股票与其所属行业或板块的表现。这样可以确定一支股票是领先还是落后于同行。价格相对指标还可以用于找到在整体市场下跌期间表现更好的股票，或在整体市场上涨期间表现疲软的股票。

**注意：** 在StockCharts.com上，使用**比率股票代码**来创建价格相对指标。比率符号由两个股票代码用冒号连接在一起组成（例如，“IBM:$SPX”，“$INDU:$GOLD”）。比率股票代码的值等于第一个符号的收盘价除以第二个符号的收盘价。

## 计算

```py
Price Relative = Base Security / Comparative Security

Ratio Symbol Close = Close of First Symbol / Close of Second Symbol
Ratio Symbol Open  = Open of First Symbol / Close of Second Symbol
Ratio Symbol High  = High of First Symbol / Close of Second Symbol
Ratio Symbol Low   = Low of First Symbol / Close of Second Symbol

```

价格相对指标简单地是基础证券除以比较证券。通常，基础证券是一支股票，基准是标普500指数。例如，图表分析师可以使用价格相对指标显示星巴克（SBUX）相对于标普500指数（$SPX）的表现。这只是星巴克的价格除以标普500指数。星巴克属于消费者自由选择行业。图表分析师还可以查看星巴克相对于消费者自由选择SPDR（XLY）的表现，使用适当的[比率符号](http://stockcharts.com/docs/doku.php?id=data#ratio_symbols_relative_strength "http://stockcharts.com/docs/doku.php?id=data#ratio_symbols_relative_strength")（SBUX:XLY）。图表分析师还可以查看板块表现相对于标普500指数（XLY:$SPX）。

![价格相对 - 电子表格 1](../Images/652e553429404caea6d41eec0a33baca.jpg "价格相对 - 电子表格 1")

[点击这里下载此电子表格示例。](/school/lib/exe/fetch.php?media=chart_school:technical_indicators_and_overlays:price_relative:cs-pricerelative.xls "chart_school:technical_indicators_and_overlays:price_relative:cs-pricerelative.xls (23 KB)")

上表显示了星巴克/标普500价格相对性。第二行中的第一个值为0.0256（30.66/1197.75）。当星巴克的涨幅超过标普500或跌幅低于标普500时，这个比率会增加。当星巴克的涨幅低于标普500或跌幅超过标普500时，这个比率会减少。为了参考，表中还显示了星巴克和标普500的百分比变化。星巴克的百分比变化减去标普500的百分比变化也等于价格相对性的日变化。在第二行中，注意到星巴克下跌了2.66%，而标普500下跌了1.62%。价格相对性下降（-1.04%），因为星巴克的跌幅超过了标普500。第三行显示价格相对性上升，因为星巴克（+0.50%）的涨幅高于标普500（+0.02%）。下图展示了价格相对性的实际情况。

![价格相对性 - 图表 1](../Images/28ad925566edc9c87372ac5abf21f805.jpg "价格相对性 - 图表 1")

## 解释

价格相对性用于衡量相对强度，在进行股票选择时非常重要。许多投资组合经理将自己的表现与标普500等基准进行比较。他们的目标是跑赢该基准。为了实现这一目标，经理们经常寻找表现相对强劲的股票。这就是价格相对性的作用。当一支股票表现出相对强劲并跑赢其基准时，价格相对性上升。相反，当一支股票表现出相对弱势并跑输其基准时，价格相对性下降。

有几种方法可以使用价格相对性。首先，图表分析师可以进行简单的趋势分析，以确定价格相对性的方向。这可以基于实际趋势、支撑/阻力突破、移动平均线或其他指标。其次，图表分析师可以寻找相对强度的牛市和熊市背离，以警示股价可能出现逆转。

## 趋势识别

图表分析师可以应用基本趋势分析或[移动平均线](/school/doku.php?id=chart_school:technical_indicators:moving_averages "chart_school:technical_indicators:moving_averages")来确定价格相对性的方向。与任何价格图表一样，当出现更高的高点和更高的低点时，价格相对性就会呈上升趋势。相反，当出现更低的低点和更低的高点时，价格相对性就会呈下降趋势。图表分析师还可以应用所选的移动平均线。当价格相对性交易在其150日简单移动平均线以下时，可能存在长期下降趋势。另外，当价格相对性交易在其150日简单移动平均线以上时，可能存在长期上升趋势。

![价格相对性 - 图表 2](../Images/d4a23d4173a9f3da488a65930921d4e9.jpg "价格相对性 - 图表 2")

上图显示了惠普（HPQ）的价格相对（HPQ:$SPX）。15天SMA应用于HPQ价格和价格相对。首先，请注意，价格相对在6月中旬突破阻力，标志着上升趋势的开始。在12月期间，价格相对继续表现出更高的高点和更高的低点。价格相对在12月下旬达到顶峰，并在2月下旬形成较低的高点。随后，跌破150天SMA标志着下降趋势的开始和表现不佳期。

## 阳市/熊市背离

在价格下跌期间，价格相对的[牛市背离](/school/doku.php?id=chart_school:glossary_b#bullish_divergence "chart_school:glossary_b")信号相对强势。在下跌期间表现最佳的股票往往是市场反转时的领导者。下图显示了杜邦（DD）的价格相对（DD:$SPX）。尽管股票从4月下旬下跌到7月初，价格相对却上升，表明在这一下跌过程中相对强势。杜邦的表现比整体市场好。随后，当市场反转并在7月开始上涨时，该股成为领头羊。请注意，价格相对和股票在7月下旬突破阻力（蓝线）。  

![价格相对 - 图表 3](../Images/bc7bbd83703a986ac1f5a5b60f26e951.jpg "价格相对 - 图表 3")

在价格上涨期间，价格相对弱势的[熊市背离](/school/doku.php?id=chart_school:glossary_b#bearish_divergence "chart_school:glossary_b")信号。股票在上涨过程中表现不佳，通常在市场反转时率先下跌。下图显示了万事达卡（MA）的价格相对（MA:$SPX）。在2月初急剧下跌后，股票在4月下旬升至新的反应高点。价格相对没有确认，并形成了一个明显较低的高点，形成了熊市背离。此外，请注意，价格相对在股票从3月第二周上涨到4月下旬时是平的（蓝线）。这些上涨过程中的相对弱势迹象预示着5月份的急剧下跌。

![价格相对 - 图表 4](../Images/924552fccc63461a9fa23d0ffecca853.jpg "价格相对 - 图表 4")

## 结论

尽管本文侧重于使用价格相对性进行股票分析，但价格相对性也可以用于广泛的市场分析。股市可以分为九个由行业SPDR代表的部门。图表分析师可以维护这九个部门的价格相对性图表，以确定领先者和落后者。当科技和消费者自由选择部门领先时，市场处于进攻模式。当消费品、医疗保健和公用事业部门领先时，市场处于防御模式。确定了领先部门后，图表分析师可以在这些部门内寻找领先股票。可以避免显示相对弱势的部门，以帮助缩小搜索范围。与所有指标一样，重要的是将价格相对性与其他技术分析工具结合使用。[动量振荡器](/school/doku.php?id=chart_school:technical_indicators:introduction_to_technical_indicators_and_oscillators#momentum_oscillators "chart_school:technical_indicators:introduction_to_technical_indicators_and_oscillators")和[图表模式](/school/doku.php?id=chart_school:chart_analysis:chart_patterns "chart_school:chart_analysis:chart_patterns")可用于确认或否定相对强势或相对弱势。

## 使用SharpCharts

通过在SharpCharts中使用“价格”指标和[“比率”股票代码](http://stockcharts.com/docs/doku.php?id=data#ratio_symbols_relative_strength "http://stockcharts.com/docs/doku.php?id=data#ratio_symbols_relative_strength")（例如，“IBM:$SPX”），可以获得价格相对性。首先，选择“价格”指标。其次，在参数框中，输入基础证券的符号，然后加上冒号（“:”），然后是比较证券的符号。

请注意，您还可以在比率符号中使用两个“伪符号” - “$SECTOR”和“$INDUSTRY”。我们将自动用适当的部门或行业ETF/指数替换这些符号。例如，“IBM:$SECTOR”等同于“IBM:XLK”。

价格相对性可以放置在基础证券的价格图表的上方、下方或后方。将指标放置在“价格后面”可以方便比较这两条线。下图显示了价格相对性（粉色）在价格图表后面的情况。请注意8月的看涨背离和12月的看跌背离。使用“高级选项”可以向价格相对性添加移动平均线或另一个指标。[点击这里查看实时示例](http://stockcharts.com/h-sc/ui?s=XLY&p=D&yr=0&mn=6&dy=0&id=p08051994524&listNum=30&a=220460939 "http://stockcharts.com/h-sc/ui?s=XLY&p=D&yr=0&mn=6&dy=0&id=p08051994524&listNum=30&a=220460939")。

![价格相对性 - 图表 5](../Images/8750fa63f1c6716db84fec380fb89bcb.jpg "价格相对性 - 图表 5")

![价格相对性 - SharpCharts](../Images/a7c258055e692915c66fcdd4347d1438.jpg "价格相对性 - SharpCharts")

## 进一步研究

马菲的书在跨市场分析章节中涵盖了相对强度分析。马菲还研究了各个行业的相对强度，并展示了如何将相对强度应用于个别股票。

《技术分析解释》一书介绍了相对强度的概念。普林展示了图表示例来确定相对强度，并教导读者如何将相对强度与其他指标结合运用。

| **金融市场技术分析** 约翰·J·墨菲 | **马丁·普林的技术分析解释** 马丁·普林 |
| --- | --- |
| [![](../Images/d9fb5f53997f0c87918070e360d1437d.jpg)](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | [![](../Images/907bb9e1dca336b6bedb79166d8efb0e.jpg)](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |
| [![立即购买](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "立即购买")](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | [![立即购买](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "立即购买")](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |

* * *

## 其他资源

### 股票与商品杂志文章

**[马丁·普林的相对强度](http://stockcharts.com/h-mem/tascredirect.html?artid=\V19\C07\079RS.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V19\C07\079RS.pdf")**

2001年6月 - 股票与商品 V. 19:7 (42-46)

**[工作资金：使用史蒂夫·沃特金斯的相对强度](http://stockcharts.com/h-mem/tascredirect.html?artid=\V21\C05\101WATK.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V21\C05\101WATK.pdf")**

2003年4月 - 股票与商品
