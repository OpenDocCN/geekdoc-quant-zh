# 高位做空:EPAT 项目中的 Algo 交易策略

> 原文：<https://blog.quantinsti.com/shorting-high-algo-trading-strategy-r/>

![Shorting at High - Algo Trading Strategy in R](img/9470dac6b3076460658582fb393f57d6.png)

由[米林德·帕拉德卡](https://www.linkedin.com/in/milind-paradkar-b37292107)

Milind 的职业生涯始于 Gridstone Research，为纽约证券交易所上市公司构建收益模型和撰写收益报告，涵盖科技和房地产投资信托基金行业。Milind 还曾在 CRISIL 和德意志银行工作，在那里他参与了美国和 EMEA 地区涵盖资产支持证券(ABS)和债务抵押债券(CDO)的结构化融资交易的建模。

Milind 拥有孟买大学的金融 MBA 学位和孟买圣泽维尔学院的物理学学士学位。

### **构思**

算法交易(EPAT)高管课程(T1)让我接触到了学习算法交易所需的所有必要科目。作为 EPAT 项目工作的一部分，我尝试编码许多策略。因为我是算法交易的新手，所以我想编写最简单、最基本的策略。虽然简单和基本的，人们不应该低估这种策略的力量，因为它们可以产生良好的回报。

“高位做空”是我为项目工作制定的策略之一。这篇文章简要解释了这个策略和编码部分。我欢迎读者给建议，随机应变或使用策略。

### **战略简介**

策略是在日内交易中做空超过设定上涨百分比阈值(比如 8%-9%)的最佳股票。卖空股票的预期下跌量与执行代码时生成的指标表中预测的一样。

该代码分为两部分:

首先，我们在代码中设置一个高百分比阈值限制。在执行代码时，它扫描股票列表中的所有股票，并确定哪些股票超过了设定的阈值限制。

其次，对于每一只这样的股票，它会计算某些指标，如股票在过去一年中越过设定阈值的次数、这些时间内的平均上涨百分比、未来三天价格的平均绝对下跌、RSI、相关性等。这些指标可以用来确定哪只股票是做空的最佳选择。收盘时或根据个人的利润目标平仓。

### **R 中的策略代码**

**步骤 1:加载包，读取股票符号，初始化数据框**

首先，加载必要的 R 包。以百分比形式设置高阈值水平。代码中的下一行读取包含股票列表的 csv 文件。使用这个文件，我们创建一个包含符号的向量，以及另一个包含经纪人提供的每只股票的杠杆比率的向量。

在执行代码的第一部分后，我们还初始化了一个包含每只股票基本信息的数据框。只有那些超过给定阈值的股票将被包括在该数据框中。

```py
# Upload the required packages

library(xlsx);library(zoo);library(quantmod);library(rowr);library(TTR);

# Set the parameters here 

pc_up_level = 6  # Set the high percentage threshold level

noDays = 2       # No of lookback days

# Read the csv file that contains the Stock tickers to be scanned

test_tickers = read.csv("F&O Stock List.csv")

symbol = as.character(test_tickers[,4])          

leverage = as.character(test_tickers[,5])        

sig_finds = data.frame(0,0,0,0,0,0)

colnames(sig_finds) = c("Ticker","Leverage","Previous Price","Current Price","Abs Change","% Change")
```

**第二步:生成数据帧**

在下一步中，我们从 google finance 获取每只股票当天和前一天的 1 分钟盘中价格数据。我有相同的定制脚本。您可以使用自己的脚本从 Google finance 或任何其他来源下载数据。然后读取下载的文件，我们计算前一天收盘价的绝对价格变化和百分比价格变化。所使用的当前价格是在当天交易时间内运行代码时对应的最新价格。

如果计算出的价格变化百分比大于设定的阈值，我们将该股票添加到数据框中。对于这样的股票，数据框架增加了杠杆、前一天的收盘价、当前价格、价格的绝对变化和价格的百分比变化等信息。

对所有股票执行代码后得到的数据帧被写入一个 excel 文件，命名为“在 High.xlsx 做空”。从 google finance 下载的 R 目录下的所有股票文件都使用 unlink 命令删除。

```py
for(s in 1:length(symbol)){

 print(s) 

 # Custom function to download stock data from Google finance
 source("Stock price data.R") 
 intraday_price_data(symbol[s],noDays)

 dirPath = paste(getwd(),"/",sep="") # Specify the R directory 
 fileName = paste(dirPath,symbol[s],".csv",sep="") # Specify the filename 
 data = as.data.frame(read.csv(fileName)) # Read the downloaded file

 data_close =subset(data, select=(CLOSE), subset=(TIME == 1530))
 pdp = tail(data_close,1)[,1]
 lp = tail(data,1)[,3]

 # Compute absolute and the percentage change
 apc = round((lp - pdp),2)
 pc = round(((lp - pdp) / pdp) * 100,2)

 if (pc > pc_up_level ){

 # Create a temporary empty data frame, only if the Percentage change is significant
 sig_finds_temp = data.frame(0,0,0,0,0,0) 
 colnames(sig_finds_temp) = c("Ticker","Leverage","Previous Price","Current Price","Abs Change","% Change")

 sig_finds_temp = c(symbol[s],leverage[s],pdp,lp,apc,pc) 
 sig_finds = rbind(sig_finds, sig_finds_temp) # combines the previous and current data frame

 rm(sig_finds_temp) # deletes the temporary data frame 

 print(sig_finds)

 }

 # Deletes the downloaded stock price files for each ticker from the directory
 unlink(fileName) 

} 
# Write the results in an excel sheet
write.xlsx(sig_finds,"Shorting at High.xlsx")
```

示例:

我们把门槛定在 4%吧。我们的股票列表中有 146 个股票代码。当我们执行代码时，在 146 个股票代码中，代码列出了 6 只股票，它们在当天市场交易时间内超过了 4%的阈值。下表说明了执行代码后保存在“Shorting at High.xlsx”工作簿中的初始输出。

![Step 2 - Generating the data frame](img/22c4fbb6cd23e4fb43eb470b945d3da7.png)

**第三步:计算指标，确定做空的最佳股票**

这部分代码使用“在高位做空. xlsx”表中的股票代码。基于 1 年的回顾期，本节中的代码计算以下指标:

*   RSI -相对强度指数
*   计数——在给定的回顾期内，股票越过阈值的次数
*   平均高点% -股票高于阈值时的平均高点百分比
*   Abs 平均下降-卢比从平均最高百分比的绝对平均下降
*   下一个三维价格移动-这给出了未来三天的绝对价格变化
*   过去 15 天为负-过去 15 天股票为负的次数
*   股票的 1 年高点和 1 年低点
*   股票与 NIFTY 的相关性

```py
# Compute the different metrics which will be used in evaluating the best stock to short 
# Pull NIFTY data for the last 1 year
source("Stock price data.R") 
daily_price_data("NIFTY",1) 
dirPath = paste(getwd(),"/",sep="") 
fileName = paste(dirPath,"NIFTY",".csv",sep="")
nifty_data = as.data.frame(read.csv(file = fileName))
# Read the stock symbols from "Shorting at High.xlsx" workbook
test_tickers = read.xlsx("Shorting at High.xlsx",header=TRUE, 1, startRow=1, as.data.frame=TRUE)
t = nrow(test_tickers)

test_tickers$Count = 0; test_tickers$Avg_high = 0;
test_tickers$Avg_decline = 0; test_tickers$Next_3d_Change = 0;
test_tickers$Low_1Yr = 0; test_tickers$High_1Yr = 0;
test_tickers$Neg_Last15_days = 0 ; test_tickers$RSI = 0;
test_tickers$NIFTY_Correlation = 0

symbol = as.character(test_tickers[2:t,2])
noDays = 1
# Compute the metrics for each stock 
for (s in 1:length(symbol)){

 print(s)

 table_sig = data.frame(0,0,0,0,0,0,0) 
 colnames(table_sig) = c("Date","Days High in %","Days Close in %","RSI","Entry Price","Exit Price","Profit/Loss")

 source("Stock price data.R")
 daily_price_data(symbol[s],noDays) 
 dirPath = paste(getwd(),"/",sep="") 
 fileName = paste(dirPath,symbol[s],".csv",sep="") 
 data = as.data.frame(read.csv(file = fileName)) 
 N = nrow(data)

 # Initializing variables to zero
 nc = 0 ; Cum_hc_diff = 0;
 Cum_threshold_per = 0;Cum_next_3d_change = 0; 

 diff = data$HIGH - data$CLOSE

 rsi_data = RSI(data$CLOSE, n = 14, maType="WMA", wts=data[,"VOLUME"])

 for (i in 2:N) {

 days_close = (data$CLOSE[i] - data$CLOSE[i-1])*100/data$CLOSE[i-1]
 days_high = (data$HIGH[i] - data$CLOSE[i-1])*100/data$CLOSE[i-1]

 condition = ((days_high > pc_up_level) == TRUE)
 if (condition)
 {
 nc = nc + 1 

 date_table = data$DATE[i]

 high_per_table = round(days_high,2)
 close_price_per_table = format(round(days_close,2),nsmall = 2)

 rsi_table = format(round(rsi_data[i],2),nsmall = 2)

 entry_price = format(round(data$CLOSE[i-1]*(1+(pc_up_level/100)),2),nsmall = 2)
 exit_price = format(round(data$CLOSE[i],2),nsmall = 2)
 pl_trade = format(round(((data$CLOSE[i-1]*(1+(pc_up_level/100))) - data$CLOSE[i]),2),nsmall = 2)

 hc_diff = diff[i] # difference between day's high and day's close whenever the price crossed the threshold level.
 Cum_hc_diff = Cum_hc_diff + hc_diff # Cumulative of the difference for all trades
 Average_hc_diff = round(Cum_hc_diff / nc , 2) # Computing the average for difference between high and low.

 # Computes the total of Day's high's whenever price crossed the threshold.
 Cum_threshold_per = Cum_threshold_per + days_high 
 # Average of High's
 Average_threshold_per = round(Cum_threshold_per / nc , 2) 

 if ( i < (N - 5)){ # Captures the average next 3-day price movement
 next_3d_change = data$CLOSE[i+3] - data$CLOSE[i]
 Cum_next_3d_change = Cum_next_3d_change + (data$CLOSE[i+3] - data$CLOSE[i])
 Average_next_3d_change = round(Cum_next_3d_change / nc,2)
 }

 # Create a temporary dataframe to add values and then later merge with the final table 
 table_temp = data.frame(0,0,0,0,0,0,0) 
 colnames(table_temp) = c("Date","Days High in %","Days Close in %","RSI","Entry Price","Exit Price","Profit/Loss")
 table_temp = c(date_table,high_per_table,close_price_per_table,rsi_table,entry_price,exit_price,pl_trade) 
 table_sig = rbind(table_sig, table_temp) 
 rm(table_temp)

 } 

 }

 table_sig = table_sig[order(table_sig$Date),]

 # Write the individual results in an excel sheet
 name = paste(symbol[s]," past performance",".xlsx",sep="")
 write.xlsx(table_sig,name) 

 # load it back to format the excel sheet for column width
 wb = loadWorkbook(name)
 sheets = getSheets(wb)
 autoSizeColumn(sheets[[1]], colIndex=1:16)
 saveWorkbook(wb,name)

 # Price performance in the last 15 days, checks for many days the price change was negative. 
 nc_last_15 = 0 
 for ( p in (N-15):N){

 condition_1 = (((data$CLOSE[p] - data$CLOSE[p-1])< 0 ) == TRUE )
 if (condition_1)
 {
 nc_last_15 = nc_last_15 + 1
 }
 } 

 # Correlation between the ticker and NIFTY 
 Cor_coeff = round(cor(data$CLOSE , nifty_data$CLOSE),2)

 # Filling the “Shorting at High.xlsx” with the computed metrics

 e = s + 1
 test_tickers$Count[e] = nc
 test_tickers$Avg_high[e] = format(Average_threshold_per,nsmall = 2) # Indicates the Avg. percentage above the threshold in the past
 test_tickers$Avg_decline[e] = format(Average_hc_diff,nsmall = 2) # Indicates the Avg. decline in Absolute rupee terms from the Avg. high to the closing price in the past test_tickers$Next_3d_Change[e] = round(Average_next_3d_change,2) # Indicates the next 3 day price movement.
 test_tickers$Next_3d_Change[e] = format(Average_next_3d_change,nsmall = 2)
 test_tickers$Low_1Yr[e] = format(min(data$CLOSE),nsmall = 2) # 1 year low price
 test_tickers$High_1Yr[e] = format(max(data$CLOSE),nsmall = 2) # 1 year high price
 test_tickers$Neg_Last15_days[e] = nc_last_15 # Indicates how many times in the last 15 days has the price been negative.
 test_tickers$RSI[e] = round(tail(rsi_data,1),2)
 test_tickers$NIFTY_Correlation[e] = Cor_coeff # Computes the correlation between the Stock and NIFTY.

 unlink(fileName) # Deletes the downloaded stock price files for each ticker after processing the data

 rm("data","table_sig")

} # This closes the for loop 

test_tickers = test_tickers[-1,-1]
colnames(test_tickers) = c("Ticker", "Leverage","Previous Price","Current Price","Abs. Change","% Change","Count","Avg.High %","Abs Avg.Decline","Next 3-d price move","1-yr low","1-yr high","-Ve last 15-days","RSI","Nifty correlation")
# Write and format the final output file

write.xlsx(test_tickers,"Shorting at High.xlsx") 

wb = loadWorkbook("Shorting at High.xlsx")
sheets = getSheets(wb)
autoSizeColumn(sheets[[1]], colIndex=1:19)
saveWorkbook(wb,"Shorting at High.xlsx")
```

**步骤 4:将指标添加到 excel 表中**

上一节中计算的指标将添加到“在高位做空. xlsx”工作簿中。上一节中显示的代码也为每个股票代码生成一个交易摘要。交易摘要提供了在回顾期内，每当股票超过阈值百分比时，所有历史交易的详细信息。交易摘要自动保存在 R 工作目录下，名称为“symbol past performance.xlsx”(如 BEL past performance.xlsx)。

**第五步:分析汇总表**

下表显示了添加到初始输出中的各种指标。我们设定了 4%的门槛。从表中我们可以看出，在过去 1 年中，BEL 仅 16 次超过 4%,平均下降了卢比。从平均高点 5.66%升至 25.48。此外，在此期间，BEL 的下一个 3 日价格变动为负值。贝尔似乎是做空的好对象。

![Step 5 - Analyzing the summary sheet](img/9c965260b35931a9f00d47b3616164cb.png)

人们可以使用这些指标制定进一步的规则，以确定卖空的最佳股票。在确定最佳股票后，可以通过任何提供算法交易平台的经纪人自动下单和执行。可以根据个人的风险收益目标添加止损和盈利目标。

### **结论**

该策略试图从价格越过高门槛后的下跌中获利。代码可以进一步优化，以提高执行速度。你也可以制定一个类似的策略，当股票下跌超过某个阈值时，你可以做多。我已经在 GitHub 上发布了策略代码([高位做空。R](https://gist.github.com/MilindRCodes/634bab99dc4d0bee7362f8d802c4f7b8) )也欢迎读者提出建议和意见。

### 后续步骤

如果你是一名程序员或技术专业人士，想开始自己的自动交易平台，从日常从业者的实时互动讲座中学习自动交易。算法交易高管课程涵盖统计学&计量经济学、金融计算&技术和算法&量化交易等培训模块。[现在报名](https://www.quantinsti.com/courses/epat/scholarship-test/)！

**更新-** *我们注意到一些用户在从雅虎和谷歌金融平台下载市场数据时面临挑战。如果你正在寻找市场数据的替代来源，你可以使用 [Quandl](https://www.quandl.com/) 来获得同样的信息。*

### **下载中的文件:**

*   股票价格数据文件