# 如何用 Python 下载外汇价格数据

> 原文：<https://blog.quantinsti.com/download-forex-price-data-yfinance-library-python/>

何塞·卡洛斯·冈萨雷斯·田中

在互联网上，你会找到许多下载外汇价格数据的来源，如 quandl，alpha vantage，brokers' APIs，yahoo finance 等。今天，我们将教你如何从雅虎财经获取外汇价格数据，从每天到每分钟的频率。

我知道你在想什么:*“有很多网站解释如何用雅虎财经库下载股票价格数据，但几乎没有关于如何用它下载外汇价格数据的内容”*。

我们都知道股票市场是一个投资的好地方。然而，当你有一个好的策略，外汇资产可以帮助你赚一大笔钱。作为一个探索这个神奇市场的 algo 交易者，yfinance 库将帮助我们轻松下载外汇价格数据。

*   [雅虎金融库安装](#yahoo-finance-library-installation)
*   [导入库](#import-libraries)
*   [每日外汇价格数据](#daily-forex-price-data)
*   [绘制收盘价](#plot-the-close-price)
*   [分钟外汇价格数据](#minute-forex-price-data)
*   [绘制分钟收盘价](#plot-the-minute-close-price)
*   [两个外汇对的每日数据](#daily-data-of-two-forex-pairs)
*   [绘制两个外汇对](#plot-the-two-forex-pairs)

* * *

## 雅虎财务库安装

太简单了！在我们进入下载部分之前，不要忘记在您的环境中安装这个库。您可以使用以下代码来实现这一点: