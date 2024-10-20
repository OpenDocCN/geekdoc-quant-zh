# 通过 FIX 连接 FXCM–详细教程

> 原文：<https://blog.quantinsti.com/connecting-fxcm-fix-detailed-tutorial/>

![Connecting FXCM with Fix engine - A tutorial](img/d8327321ac08b865cb4d018b04ad47c2.png "Connecting FXCM over Fix")

由 [Sunith Reddy](https://www.linkedin.com/in/sunith-reddy-62a8046)

我们在上一篇关于 [FIX 协议](https://blog.quantinsti.com/fix-trading-protocol/)的文章中讨论了消息通信的事实标准。

> *“金融信息交换(* *[FIX](http://www.fixprotocol.org/) )协议是为了促进与证券交易相关的信息的电子交换而开发的消息标准。它旨在用于希望实现通信自动化的贸易伙伴之间。<sup>[1](http://www.quickfixengine.org/quickfix/doc/html/)</sup>*

在本文中，我们将更进一步，讨论在 fix 上连接 FXCM】所涉及的一些操作。我们将使用 QuickFix 引擎对示例进行编码。Quickfix 是一个开源的修复引擎。

> ***“quick FIX*****是一个开源的修复引擎。它与金融应用程序相集成，为他们提供了与全球数百个支持 FIX 的系统进行通信所需的连接。 **QuickFIX** 让您的应用程序能够使用简单的界面与所有这些系统进行电子交互。”**

 *你可以从[这里](http://www.quickfixengine.org/)了解更多关于 QuickFIX 的信息。

### 资格证书

就像我们拥有使用 IBridgePY 连接到[交互式代理的凭证一样，我们在这里也拥有凭证。通过 fix 连接 FCMX 将需要一些凭据来标识 FXCM 的连接实体。全权证书由以下内容组成:](https://blog.quantinsti.com/implement-python-in-interactive-brokers-api/)

*   **插座连接主机，端口**–您要连接的地方
*   **发送者公司 Id**–识别信息的发送者。
*   **目标公司 id**–确定消息的预期接收人
*   **目标子 id**–完成接收方标识的子标识符。

对于 quickFix，这些凭证需要在配置文件中进行配置。配置文件将如下所示:

```py
# Default settings. These settings are inherited by each
# individual session found below

[DEFAULT]

BeginString=FIX.4.4

ConnectionType=initiator

HeartBtInt=30

FileStorePath=.\Store

FileLogPath=.\Logs

# Start and End times for the FIX session (in UTC)

StartDay=Sunday

StartTime=21:15:00

EndDay=Friday

EndTime=20:00:00

UseDataDictionary=Y

DataDictionary=FIXFXCM10.xml

ValidateUserDefinedFields=N

ValidateFieldsHaveValues=N

ValidateFieldsOutOfOrder=N

ReconnectInterval=20

ResetOnDisconnect=Y

ResetSeqNumFlag=Y

SendResetSeqNumFlag=Y

ContinueInitializationOnError=Y

# Session specific settings along with FIX credentials 
# supplied by FXCM

[SESSION]

SenderCompID=someID

TargetCompID=FXCM

SocketConnectHost=someHost

SocketConnectPort=somePort

TargetSubID=someTargetID

Username=someUsername

Password=somePassword

```

### 登录

都准备好了吗？很好，如果您的配置是正确的，那么 quickfix 引擎将启动连接。这包括连接到主机和端口，并发送登录请求。登录请求是任何会话的第一条消息。如果不是第一条消息，则在登录请求之前发送的所有消息**都将被忽略**。

"所有在登录请求之前发送的消息都被忽略."

示例登录消息如下所示:

```py
#Send Username/Password on Logon (35=A)8=FIX.4.49=114 35=A 34=1 49=sendercompId 52=20120927-13:15:34.754 56=FXCM 57=someTargetSubId 553=someUsername 554=somePassword 98=0 108=30 141=Y 10=146
```

标签 553 和 554 意在传递用户名和密码。请注意，34=1 假定这是一天中的第一次尝试。在其他情况下，它只是消息的序列号。如果所有凭证都正确，那么来自 FXCM 的登录响应将如下所示

```py
#FXCM Logon response 8=FIX.4.49=92 35=A 34=1 49=FXCM 50=someTargetSubId 52=20120927-13:15:34.810 56=somesenderCompId 98=0 108=30 141=Y 10=187
```

请注意，因为响应是由 fxcm 发送的，而预期接收方是我们的系统，所以 49 标签是 **FXCM(发送方)**和标签 56 = **somesenderCompId(预期接收方)**。

一旦验证了凭证并收到成功的响应，就可能需要一些初始化参数。例如，市场状态如何(开盘/收盘)、符号信息(批量大小、报价大小)等。为了做到这一点，我们使用了**交易会话状态请求** (35=g)

下面的代码片段显示了如何发送交易会话状态请求

```py
FIX44::TradingSessionStatusRequest request;request.setField(FIX::TradSesReqID(NextId())); request.setField(FIX::SubscriptionRequestType(FIX::SubscriptionRequestType_SNAPSHOT_PLUS_UPDATES)); FIX::Session::sendToTarget(request,session_id);
```

这将发送请求，对请求的响应是交易会话状态消息。会话状态消息如下所示

```py
-- Core TradingSessionStatus Message -- 8=FIX.4.49=12384 35=h34=3 49=FXCM 50=U100D1 52=20120828-13:24:52.38756=fx1294946_client158=Market is closed. Any trading functionality is not available.60=20120828-13:24:52325=N 335=2336=FXCM339=2340=2625=U100D19019=09030=Coordinated Universal Time 
#-- Embedded SecurityList -- 
#NoRelatedSym (This field shows the total number of securities. Below we only show the first 5 to save space)146=69 55=CAD/JPY15=CAD228=1231=1460=4561=19000=189001=39002=0.019003=0.159004=-0.339005=18009076=D9080=19090=09091=09092=09093=09094=500000009095=19096=O55=GBP/CHF15=GBP228=1231=1460=4561=19000=139001=59002=0.00019003=0.159004=-0.379005=13009076=D9080=19090=09091=09092=09093=09094=500000009095=19096=O55=JPN22515=JPY228=100231=1460=7561=19000=10079001=09002=19003=0.079004=-0.099005=1007009076=T9080=29090=259091=19092=259093=19094=10009095=19096=O55=EUR/SEK15=EUR228=1231=1460=4561=19000=329001=59002=0.00019003=-0.829004=0.269005=32009076=D9080=19090=09091=09092=09093=09094=500000009095=19096=O55=AUD/USD15=AUD228=1231=1460=4561=19000=69001=59002=0.00019003=0.639004=-1.319005=6009076=V9080=19090=09091=09092=09093=09094=500000009095=19096=O 

-- FXCM System Parameters --  

NoFXCMParam (This field shows the total number of system parameters)9016=17 

9017=TP_949018=Y9017=BASE_CRNCY9018=USD9017=TRAILING_STOP_USED9018=Y9017=SERVER_TIME_UTC9018=UTC9017=BASE_TIME_ZONE9018=America/New_York9017=EXT_PRICE_TERMINAL9018=PDEMO1_PRICES9017=COND_DIST9018=0.19017=COND_DIST_ENTRY9018=0.19017=TP_1729018=Y9017=BASE_CRNCY_SYMBOL9018=$9017=REPORTS_URL9018=https://fxpa.fxcorporate.com/fxpa/getreport.app/9017=BASE_UNIT_SIZE9018=100009017=END_TRADING_DAY9018=21:00:009017=BASE_CRNCY_PRECISION9018=29017=FixSupport9018=FIXONLY9017=TRAILING_STOP_DYNAMIC9018=Y

9017=FORCE_PASSWORD_CHANGE9018=N10=058
```

然而，我们有兴趣从代码中读取这个消息。读取这些系统参数的方法如下:

```py
int param_count = FIX::IntConvertor::convert(status.getField(9016));

cout << "TSS - FXCM System Parameters" << endl;
 for(int i = 1; i =< param_count; i++)
 {
 FIX::FieldMap map = status.getGroupRef(1,9016);
 string param_name = map.getField(9017);
 string param_value = map.getField(9018);

cout << param_name << " - " << param_value << endl;
 }

```

FXCM 在 **tradingSessionStatus** 消息中发送附加标签。这些可以在**安全列表**和**系统**参数中找到。该信息将在发送订单时使用。

**安全列表**中的自定义字段

*   9001-**精度**-安全的精度。前述，美元/日元值为 3 = >此符号的值字段引用到小数点后 3 位。
*   9002-**点大小**-这代表我们所说的证券的点。例如，欧元/美元将为该字段显示值 0.0001。
*   9003-**syminterest buy**–您的服务器默认批量的价格，以您的账户货币表示。例如，如果你的账户是美元，服务器默认的手数是 10000。那么 9003=0.64 = >你将得到 0.64 美元的 10K 大小。
*   9004—**symInterestSell**—同上。9004=-1.48 = >你要为每个 10K 尺码付 1.48 美元。您可以从标签 9017=BASE_UNIT_SIZE 9018=10000 中读取默认批量。
*   9080-**product id**–每种证券都属于一种产品类型。1 =外汇，2 =指数，3 =商品，4 =国库，5 =金条。例如，欧元/美元将为 1。
*   9090-**条件止损单停止**-止损单与当前市场价格的最小距离。如果你有买入头寸，那么你的止损单必须至少与当前出价有这个距离。
*   9091-**conditionalDistanceLimit**-限价单与当前市价的最小距离。如果您有买入头寸，那么您的限价订单必须至少与当前买价相差这个距离。
*   9092—**conditionalDistanceEntryStop**—新止损单(挂单)的最小距离。如果你想下止损单买入，那么这个订单的价格必须至少与当前的要价相差这个距离。
*   9093—**conditionalDistanceEntryLimit**—新限价挂单(挂单)的最小距离。如果你想下一个新的限价挂单买入，那么订单的价格必须至少与当前的要价相差这个距离。
*   9094-**最大数量**-单笔订单的最大数量。
*   9095-**最小数量**-单笔订单的最小数量。
*   9096—**trading status**—这表示目的地是开放(‘O’)还是关闭(‘C’)。

除了上述自定义字段，系统参数也在此消息中返回(9017，9018 标签的组合)

*   **BASE _ CRNCY—**您账户的货币
*   **SERVER _ TIME _ UTC–**如果此字段设置为 UTC，则服务器将以 UTC 表示所有时间字段。如果不是，那么它会用本地时区来表示
*   **BASE _ TIME _ ZONE–s**如何显示服务器的本地时区，例如“亚洲/加尔各答”
*   **COND _ DIST**–新止损单或限价单的价格与当前市场价格之间的最小距离。该值以点数表示，通常默认为 0.10
*   **COND _ DIST _ 进场**–新止损进场单或限价进场单的价格与当前市场价格之间的最小距离。该值以点数表示，通常默认为 0.10
*   **BASE _ UNIT _ SIZE**–外汇证券的最小订单量。对于 CFD 证券，我们需要检查 9095 标签
*   **END _ TRADING _ DAY**–交易日收盘时间。它以 hh:mm:ss 格式表示。这个时间总是采用 UTC

### 请求市场数据

在与服务器建立连接后，我们准备请求市场数据。**市场数据**由快照消息和增量更新消息组成。**marketdatasnapshotfullresh(W)**消息包含市场数据的更新。它是作为对 marketdatarequest (v)消息的响应而获得的。

以下代码片段显示了如何发送 **marketdatarequest** 消息:

```py
FIX44::MarketDataRequest mdr; mdr.set(FIX::MDReqID(NextId()));mdr.set(FIX::SubscriptionRequestType(FIX::SubscriptionRequestType_SNAPSHOT_PLUS_UPDATES));mdr.set(FIX::MarketDepth(0));mdr.set(FIX::NoMDEntryTypes(2)); FIX44::MarketDataRequest::NoMDEntryTypes types_group;types_group.set(FIX::MDEntryType(FIX::MDEntryType_BID));mdr.addGroup(types_group);types_group.set(FIX::MDEntryType(FIX::MDEntryType_OFFER));mdr.addGroup(types_group); int no_sym = FIX::IntConvertor::convert(security_list.getField(FIX::FIELD::NoRelatedSym));for(int i = 1; i <= no_sym; i++){   FIX44::SecurityList::NoRelatedSym sym_group;   mdr.addGroup(security_list.getGroup(i,sym_group));} FIX::Session::sendToTarget(mdr,session_id);
```

示例**marketDataSnapshotFullRefresh**消息如下所示:

```py
8=FIX.4.49=53335=W34=3649=FXCM50=U100D152=2012091313:07:51.38756=fx157369001_client155=AUD/USD228=1231=1262=4460=4 # Number of MDEntries268=4# High 269=7270=1.03902272=20120913273=13:07:49# Low269=8270=1.03843272=20120913273=13:07:49# Bid269=0270=1.04437271=0272=20120913273=13:07:49336=FXCM625=U100D1276=A299=FXCM-AUDUSD-12638558537=1 # Offer269=1270=1.04459271=0272=20120913273=13:07:49336=FXCM625=U100D1276=A299=FXCM-AUDUSD-12638558537=1# Custom FXCM Fields9000=69001=59002=0.00019005=6009011=09020=19080=19090=09091=09092=09093=09094=500000009095=19096=O10=030
```

#### MDEntryTypes

您可以接收的数据类型在 FIX 中称为 MDEntryTypes。FXCM 支持:

*   **出价(0)**
*   **问(1)**
*   **高价(7)**
*   **低价(8)**

其他 MDEntryTypes，如 **MDEntryDate** 、 **MDEntryTime** 等。在邮件的第一个重复组中只出现一次。

### 位置信息

在开始策略之前，总是检索位置信息是很重要的。这是使用位置报告(35=AP)消息来完成的。人们不仅可以请求位置报告，还可以订阅更新。发送订阅请求类型(263)设置为 1 的 RequestForPositions (AN)消息将订阅更新。

PosReqType(标签 724)用于确定接收的报告是开放(由 0 指示)还是关闭(由 1 指示)位置。

当收到开仓报告时，它还包含开仓的价格(标签 730)。在平仓报告的情况下，平仓时的价格，以及一些附加标签:

*   9052–头寸的总 P&L。
*   9040–适用于头寸的展期利息
*   9053–已申请佣金
*   9043–头寸的收盘价

职位报告示例

| *5* | *货币* | *美元* | *美元* |
| *37* | *订单 ID* | *134757321* | *134757321* |
| *55* | *符号* | *美元/日元* | *美元/日元* |
| *58* | *正文* | *我* | *我* |
| *325* | *未冻结指示器* | *Y* | *Y* |
| *336* | 翻译 ID | *福汇* | *福汇* |
| *第 447 章* | *甲方来源* | *D* | *D* |
| *第 448 章* | *甲方* | *FXCM ID* | *FXCMID* |
| *第 452 章* | *甲方角色* | *3* | *3* |
| *第 453 章* | *NoPartyIDs* | *1* | *1* |
| *523* | *PartySubID* | *32* | *32* |
| *第 581 章* | *账户类型* | *6* | *6* |
| *625* | *TradingSessionSubID* | *U100D1* | *U100D1* |
| *702* | *no position* | *1* | *1* |
| *703* | *PosType* | *TQ* | *TQ* |
| *704* | *长脚* | *1000* | *1000* |
| *707* | *PosAmtType* | *现金* | *现金* |
| *708* | *PosAmt* | *0* | *0* |
| *第 715 章* | *清算业务日期* | *20121220* | *20121220* |
| *721* | *后期处理* | *2610968257* | *2610968446* |
| *724* | *PosReqType* | *0* | *1* |
| *727* | *总报告数* | *0* | *0* |
| *第 728 章* | *PosReqResult* | *0* | *0* |
| *730* | *设置价格* | 84.242 | 84.242 |
| *731* | *设置价格类型* | *1* | *1* |
| *第 734 章* | *优先价格* | *0* | *0* |
| *753* | *NoPosAmt* | *1* | *1* |
| *802* | *NoPartySubIDs* | *4* | *4* |
| *803* | *批量子类型* | *26* | *26* |
| *9000* | *FXCMSymID* | *2* | *2* |
| *9038* | *FXCMUsedMargin* | *5* |  |
| *9040* | *fxcmpostinterest* | *0* | *0* |
| *9041* | *FXCMPosID* | *46961794* | *46961794* |
| *9042* | *fxcmpospentime* | *20121220-03:46:25* | *20121220-03:46:25* |
| *9043* | *fxcmclossettlprice* |  | *84.231* |
| *9044* | *FXCMCloseTime* |  | *20121220-03:46:37* |
| *9048* | *FXCMCloseClOrdID* |  | *1_157* |
| *9052* | *FXCMPosClosePNL* |  | *-0.13* |
| *9053* | *FXCMPosCommission* | *0* | *0* |
| *9054* | *FXCMCloseOrderID* |  | *134757323* |

### 基本订单类型概览

#### 生效时间

生效时间表示订单在未执行的情况下保留在订单簿中的持续时间。可能的不同值有:

*   **GTC** (取消前有效)——这意味着订单在明确执行或取消前一直有效。通常在您不希望订单被立即执行时使用。您希望订单保持活动状态，直到完成为止。
*   **Day** -这意味着订单在执行前或当天到期前一直有效。通常，当您的订单意图随着时间的推移而过时时，会使用这种方法。
*   **IOC** (立即或取消)–订单在进入订单簿时尽可能得到满足。剩下的被取消了。你想以特定的价格买进。
*   **FOK** (填充或删除)——订单要么在进入订单簿时被完全填充，要么被立即取消。你有兴趣以特定价格购买全部产品。

#### 订单类型

##### 市场

不管价格如何，这个订单都会打到对方头上。只要订单簿不是空的，它将接受下一个可用价格的填充。通常用在填充订单比填充的价格更重要的时候。对于一个市场秩序来说，TIF 可以是 GTC、天、奥委会、霍英东。

```py
FIX44::NewOrderSingle order;order.setField(FIX::ClOrdID(NextClOrdID())); order.setField(FIX::Account(account));order.setField(FIX::Symbol("EUR/USD")); order.setField(FIX::Side(FIX::Side_BUY)); order.setField(FIX::TransactTime(FIX::TransactTime())); order.setField(FIX::OrderQty(10000));order.setField(FIX::OrdType(FIX::OrdType_MARKET)); FIX::Session::sendToTarget(order,session_id);
```

##### 停止极限

该订单是一个市价订单，有一个成交价格范围。这提供了防止填充价格滑动的保护。标签 40=4 表示这是一个停车限制命令，停车价格设置在标签 99 中。这代表了你愿意接受的最差价格。TIF 可以是国际奥委会或 FOK

```py
FIX44::NewOrderSingle order;order.setField(FIX::ClOrdID(NextClOrdID())); order.setField(FIX::Account(account));order.setField(FIX::Symbol("EUR/USD")); order.setField(FIX::Side(FIX::Side_BUY)); order.setField(FIX::TransactTime(FIX::TransactTime())); order.setField(FIX::OrderQty(10000));order.setField(FIX::OrdType(FIX::OrdType_STOPLIMIT));order.setField(FIX::StopPx(stop)); FIX::Session::sendToTarget(order,session_id);
```

##### 限制

订单将以等于或优于订单信息(标签 44)中提到的价格成交。当填料的价格比填料本身更重要时，使用这种订单类型。支持的 TIF 有 GTC、戴、国际奥委会、福克。

```py
FIX44::NewOrderSingle order;order.setField(FIX::ClOrdID(NextClOrdID())); order.setField(FIX::Account(account));order.setField(FIX::Symbol("EUR/USD")); order.setField(FIX::Side(FIX::Side_BUY)); order.setField(FIX::TransactTime(FIX::TransactTime())); order.setField(FIX::OrderQty(10000));order.setField(FIX::OrdType(FIX::OrdType_LIMIT)); order.setField(FIX::Price(price)); FIX::Session::sendToTarget(order,session_id);
```

##### 停止

这是一个市价单，当当前市价低于止损单消息中提到的止损价时，就会发出该市价单。填料的价格没有保证，因为这是市场订单。支持的 TIF 是 GTC 和戴。

```py
FIX44::NewOrderSingle order;order.setField(FIX::ClOrdID(NextClOrdID())); order.setField(FIX::Account(account));order.setField(FIX::Symbol("EUR/USD")); order.setField(FIX::Side(FIX::Side_BUY)); order.setField(FIX::TransactTime(FIX::TransactTime())); order.setField(FIX::OrderQty(10000));order.setField(FIX::OrdType(FIX::OrdType_STOP)); order.setField(FIX::StopPx(price)); FIX::Session::sendToTarget(order,session_id);
```

#### 密码

**例子**

这段代码假设安装了 quickfix 库。需要相应地编辑包含路径。这将使您对如何建立 FXCM 会话、订阅市场数据和发送订单有一个基本的了解。

```py
Main.cpp
#include "fix_application.h"

// -- FIX Example --

//

// Upon starting this application, a FIX session will be created and the connection sequence will commence. This includes sending a Logon message, a request for TradingSessionStatus. After the responses to these requests are received, you can use the command prompt to test out the functionality seen below in the switch block.

int main()

{

            FixApplication app;

            // Start session and Logon

            app.StartSession();

            while(true){

                        int command = 0;

                        bool exit = false;

                        cin >> command;

                        switch(command){

                        case 0: // Exit example application

                                    exit = true;

                                    break;

                        case 1: // Get positions 

                                    app.GetPositions();

                                    break;

                        case 2: // Subscribe to market data

                                    app.SubscribeMarketData();

                                    break;

                        case 3: // Unsubscribe to market data

                                    app.UnsubscribeMarketData();

                                    break;

                        case 4: // Send market order

                                    app.MarketOrder();

                                    break;

                        }

                        if(exit)

                                    break;

            }

            // End session and logout

            app.EndSession();

            while(true){

            } // Wait

            return 0;

}

fix_application.h 
#ifndef FIXAPPLICATION_H
#define FIXAPPLICATION_H

#include <iostream>
#include <vector>
#include "quickfix\Application.h"
#include "quickfix\FileLog.h"
#include "quickfix\FileStore.h"
#include "quickfix\fix44\CollateralInquiry.h"
#include "quickfix\fix44\CollateralInquiryAck.h"
#include "quickfix\fix44\CollateralReport.h"
#include "quickfix\fix44\ExecutionReport.h"
#include "quickfix\fix44\MarketDataRequest.h"
#include "quickfix\fix44\MarketDataRequestReject.h"
#include "quickfix\fix44\MarketDataSnapshotFullRefresh.h"
#include "quickfix\fix44\NewOrderList.h"
#include "quickfix\fix44\NewOrderSingle.h"
#include "quickfix\fix44\PositionReport.h"
#include "quickfix\fix44\RequestForPositions.h"
#include "quickfix\fix44\RequestForPositionsAck.h"
#include "quickfix\fix44\SecurityList.h"
#include "quickfix\fix44\TradingSessionStatus.h"
#include "quickfix\fix44\TradingSessionStatusRequest.h"
#include "quickfix\MessageCracker.h"
#include "quickfix\Session.h"
#include "quickfix\SessionID.h"
#include "quickfix\SessionSettings.h"
#include "quickfix\SocketInitiator.h"

using namespace std;

using namespace FIX;

class FixApplication : public MessageCracker, public Application

{

private:

            SessionSettings  *settings;

            FileStoreFactory *store_factory;

            FileLogFactory   *log_factory;

            SocketInitiator  *initiator;

            // Used as a counter for producing unique request identifiers

            unsigned int requestID;

            SessionID sessionID;

            vector<string> list_accountID;

            // Custom FXCM FIX fields

            enum FXCM_FIX_FIELDS

            {

                        FXCM_FIELD_PRODUCT_ID      = 9080,

                        FXCM_POS_ID                = 9041,

                        FXCM_POS_OPEN_TIME         = 9042,

                        FXCM_ERROR_DETAILS         = 9029,

                        FXCM_REQUEST_REJECT_REASON = 9025,

                        FXCM_USED_MARGIN           = 9038,

                        FXCM_POS_CLOSE_TIME        = 9044,

                        FXCM_MARGIN_CALL           = 9045,

                        FXCM_ORD_TYPE              = 9050,

                        FXCM_ORD_STATUS            = 9051,

                        FXCM_CLOSE_PNL             = 9052,

                        FXCM_SYM_POINT_SIZE        = 9002,

                        FXCM_SYM_PRECISION         = 9001,

                        FXCM_TRADING_STATUS        = 9096,

                        FXCM_PEG_FLUCTUATE_PTS     = 9061,

                        FXCM_NO_PARAMS             = 9016,

                        FXCM_PARAM_NAME            = 9017,

                        FXCM_PARAM_VALUE           = 9018

            };

public:

            FixApplication();

            // FIX Namespace. These are callbacks which indicate when the session is created,

            // when we logon and logout, and when messages are exchanged 

            void onCreate(const SessionID& session_ID);

            void onLogon(const SessionID& session_ID);

            void onLogout(const SessionID& session_ID);

            void toAdmin(Message& message, const SessionID& session_ID);

            void toApp(Message& message, const SessionID& session_ID);

            void fromAdmin(const Message& message, const SessionID& session_ID);

            void fromApp(const Message& message, const SessionID& session_ID);

            // Overloaded onMessage methods used in conjuction with MessageCracker class. FIX::MessageCracker

            // receives a generic Message in the FIX fromApp and fromAdmin callbacks, constructs the

            // message sub type and invokes the appropriate onMessage method below.

            void onMessage(const FIX44::TradingSessionStatus& tss, const SessionID& session_ID);

            void onMessage(const FIX44::CollateralInquiryAck& ack, const SessionID& session_ID);

            void onMessage(const FIX44::CollateralReport& cr, const SessionID& session_ID);

            void onMessage(const FIX44::RequestForPositionsAck& ack, const SessionID& session_ID);

            void onMessage(const FIX44::PositionReport& pr, const SessionID& session_ID);

            void onMessage(const FIX44::MarketDataRequestReject& mdr, const SessionID& session_ID);

            void onMessage(const FIX44::MarketDataSnapshotFullRefresh& mds, const SessionID& session_ID);

            void onMessage(const FIX44::ExecutionReport& er, const SessionID& session_ID);

            // Starts the FIX session. Throws FIX::ConfigError exception if our configuration settings

            // do not pass validation required to construct SessionSettings 

            void StartSession();

            // Logout and end session 

            void EndSession();

            // Sends TradingSessionStatusRequest message in order to receive as a response the

            // TradingSessionStatus message

            void GetTradingStatus();

            // Sends the CollateralInquiry message in order to receive as a response the

            // CollateralReport message.

            void GetAccounts();

            // Sends RequestForPositions which will return PositionReport messages if positions

            // matching the requested criteria exist; otherwise, a RequestForPositionsAck will be

            // sent with the acknowledgement that no positions exist. In our example, we request

            // positions for all accounts under our login

            void GetPositions();

            // Subscribes to the EUR/USD trading security

            void SubscribeMarketData();

            // Unsubscribes from the EUR/USD trading security 

            void UnsubscribeMarketData();

            // Sends a basic NewOrderSingle message to buy EUR/USD at the 

            // current market price

            void MarketOrder();

            // Generate string value used to populate the fields in each message

            // which are used as a custom identifier

            string NextRequestID();

            // Adds string accountIDs to our vector<string> being used to

            // account for the accountIDs under our login

            void RecordAccount(string accountID);

};

#endif // FIXAPPLICATION_H

fix_application.cpp
#include "fix_application.h"

FixApplication::FixApplication()

{

            // Initialize unsigned int requestID to 1\. We will use this as a 

            // counter for making request IDs

            requestID = 1;

}

// Gets called when quickfix creates a new session. A session comes into and remains in existence

// for the life of the application.

void FixApplication::onCreate(const SessionID& session_ID)

{

            // FIX Session created. We must now logon. QuickFIX will automatically send

            // the Logon(A) message

            cout << "Session -> created" << endl;

            sessionID = session_ID;

}

// Notifies you when a valid logon has been established with FXCM.

void FixApplication::onLogon(const SessionID& session_ID)

{

            // Session logon successful. Now we request TradingSessionStatus which is

            // used to determine market status (open or closed), to get a list of securities,

            // and to obtain important FXCM system parameters 

            cout << "Session -> logon" << endl;

            GetTradingStatus();

}

// Notifies you when an FIX session is no longer online. This could happen during a normal logout

// exchange or because of a forced termination or a loss of network connection. 

void FixApplication::onLogout(const SessionID& session_ID)

{

            // Session logout 

            cout << "Session -> logout" << endl;

}

// Provides you with a peak at the administrative messages that are being sent from your FIX engine 

// to FXCM.

void FixApplication::toAdmin(Message& message, const SessionID& session_ID)

{

            // If the Admin message being sent to FXCM is of typle Logon (A), we want

            // to set the Username and Password fields. We want to catch this message as it

            // is going out.

            string msg_type = message.getHeader().getField(FIELD::MsgType);

            if(msg_type == "A"){

                        // Get both username and password from our settings file. Then set these

                        // respective fields

                        string user = settings->get().getString("Username");

                        string pass = settings->get().getString("Password");

                        message.setField(Username(user));

                        message.setField(Password(pass));

            }

            // All messages sent to FXCM must contain the TargetSubID field (both Administrative and

            // Application messages). Here we set this.

            string sub_ID = settings->get().getString("TargetSubID");

            message.getHeader().setField(TargetSubID(sub_ID));

}

// A callback for application messages that you are being sent to a counterparty. 

void FixApplication::toApp(Message& message, const SessionID& session_ID)

{

            // All messages sent to FXCM must contain the TargetSubID field (both Administrative and

            // Application messages). Here we set this.

            string sub_ID = settings->get().getString("TargetSubID");

            message.getHeader().setField(TargetSubID(sub_ID));

}

// Notifies you when an administrative message is sent from FXCM to your FIX engine. 

void FixApplication::fromAdmin(const Message& message, const SessionID& session_ID)

{

            // Call MessageCracker.crack method to handle the message by one of our 

            // overloaded onMessage methods below

            crack(message, session_ID);

}

// One of the core entry points for your FIX application. Every application level request will come through here. 

void FixApplication::fromApp(const Message& message, const SessionID& session_ID)

{

            // Call MessageCracker.crack method to handle the message by one of our 

            // overloaded onMessage methods below

            crack(message, session_ID);

}

// The TradingSessionStatus message is used to provide an update on the status of the market. Furthermore, 

// this message contains useful system parameters as well as information about each trading security (embedded SecurityList).

// TradingSessionStatus should be requested upon successful Logon and subscribed to. The contents of the

// TradingSessionStatus message, specifically the SecurityList and system parameters, should dictate how fields

// are set when sending messages to FXCM.

void FixApplication::onMessage(const FIX44::TradingSessionStatus& tss, const SessionID& session_ID)

{

            // Check TradSesStatus field to see if the trading desk is open or closed

            // 2 = Open; 3 = Closed

            string trad_status = tss.getField(FIELD::TradSesStatus);

            cout << "TradingSessionStatus -> TradSesStatus -" << trad_status << endl;

            // Within the TradingSessionStatus message is an embeded SecurityList. From SecurityList we can see

            // the list of available trading securities and information relevant to each; e.g., point sizes,

            // minimum and maximum order quantities by security, etc. 

            cout << "  SecurityList via TradingSessionStatus -> " << endl;

            int symbols_count = IntConvertor::convert(tss.getField(FIELD::NoRelatedSym));

            for(int i = 1; i <= symbols_count; i++){

                        // Get the NoRelatedSym group and for each, print out the Symbol value

                        FIX44::SecurityList::NoRelatedSym symbols_group;

                        tss.getGroup(i,symbols_group);

                        string symbol = symbols_group.getField(FIELD::Symbol);

                        cout << "    Symbol -> " << symbol << endl;

            }

            // Also within TradingSessionStatus are FXCM system parameters. This includes important information

            // such as account base currency, server time zone, the time at which the trading day ends, and more.

            cout << "  System Parameters via TradingSessionStatus -> " << endl;

            // Read field FXCMNoParam (9016) which shows us how many system parameters are 

            // in the message

            int params_count = IntConvertor::convert(tss.getField(FXCM_NO_PARAMS)); // FXCMNoParam (9016)

            for(int i = 1; i < params_count; i++){

                        // For each paramater, print out both the name of the paramater and the value of the 

                        // paramater. FXCMParamName (9017) is the name of the paramater and FXCMParamValue(9018)

                        // is of course the paramater value

                        FIX::FieldMap field_map = tss.getGroupRef(i,FXCM_NO_PARAMS);

                        cout << "    Param Name -> " << field_map.getField(FXCM_PARAM_NAME) 

                                    << " - Param Value -> " << field_map.getField(FXCM_PARAM_VALUE) << endl;

            }

            // Request accounts under our login

            GetAccounts();

            // ** Note on Text(58) ** 

            // You will notice that Text(58) field is always set to "Market is closed. Any trading

            // functionality is not available." This field is always set to this value; therefore, do not 

            // use this field value to determine if the trading desk is open. As stated above, use TradSesStatus for this purpose

}

void FixApplication::onMessage(const FIX44::CollateralInquiryAck& ack, const SessionID& session_ID)

{

}

// CollateralReport is a message containing important information for each account under the login. It is returned

// as a response to CollateralInquiry. You will receive a CollateralReport for each account under your login.

// Notable fields include Account(1) which is the AccountID and CashOutstanding(901) which is the account balance

void FixApplication::onMessage(const FIX44::CollateralReport& cr, const SessionID& session_ID)

{

            cout << "CollateralReport -> " << endl;

            string accountID = cr.getField(FIELD::Account);

            // Get account balance, which is the cash balance in the account, not including any profit

            // or losses on open trades

            string balance = cr.getField(FIELD::CashOutstanding);

            cout << "  AccountID -> " << accountID << endl;

            cout << "  Balance -> " << balance << endl;

            // The CollateralReport NoPartyIDs group can be inspected for additional account information

            // such as AccountName or HedgingStatus

            FIX44::CollateralReport::NoPartyIDs group;

            cr.getGroup(1,group); // CollateralReport will only have 1 NoPartyIDs group

            cout << "  Parties -> "<< endl;

            // Get the number of NoPartySubIDs repeating groups

            int number_subID = IntConvertor::convert(group.getField(FIELD::NoPartySubIDs));

            // For each group, print out both the PartySubIDType and the PartySubID (the value)

            for(int u = 1; u <= number_subID; u++){

                        FIX44::CollateralReport::NoPartyIDs::NoPartySubIDs sub_group;

                        group.getGroup(u,sub_group);

                        string sub_type = sub_group.getField(FIELD::PartySubIDType);

                        string sub_value = sub_group.getField(FIELD::PartySubID);

                        cout << "    " << sub_type << " -> " << sub_value << endl;

            }

            // Add the accountID to our vector<string> being used to track all

            // accounts under our login

            RecordAccount(accountID);

}

void FixApplication::onMessage(const FIX44::RequestForPositionsAck& ack, const SessionID& session_ID)

{

            string pos_reqID = ack.getField(FIELD::PosReqID);

            cout << "RequestForPositionsAck -> PosReqID - " << pos_reqID << endl;

            // If a PositionReport is requested and no positions exist for that request, the Text field will

            // indicate that no positions mathced the requested criteria 

            if(ack.isSetField(FIELD::Text))

                        cout << "RequestForPositionsAck -> Text - " << ack.getField(FIELD::Text) << endl;

}

void FixApplication::onMessage(const FIX44::PositionReport& pr, const SessionID& session_ID)

{

            // Print out important position related information such as accountID and symbol 

            string accountID = pr.getField(FIELD::Account);

            string symbol = pr.getField(FIELD::Symbol);

            string positionID = pr.getField(FXCM_POS_ID);

            string pos_open_time = pr.getField(FXCM_POS_OPEN_TIME);

            cout << "PositionReport -> " << endl;

            cout << "   Account -> " << accountID << endl;

            cout << "   Symbol -> " << symbol << endl;

            cout << "   PositionID -> " << positionID << endl;

            cout << "   Open Time -> " << pos_open_time << endl;

}

void FixApplication::onMessage(const FIX44::MarketDataRequestReject& mdr, const SessionID& session_ID)

{

            // If MarketDataRequestReject is returned as the result of a MarketDataRequest message,

            // print out the contents of the Text field but first check that it is set

            cout << "MarketDataRequestReject -> " << endl;

            if(mdr.isSetField(FIELD::Text)){

                        cout << " Text -> " << mdr.getField(FIELD::Text) << endl;

            }

}

void FixApplication::onMessage(const FIX44::MarketDataSnapshotFullRefresh& mds, const SessionID& session_ID)

{

            // Get symbol name of the snapshot; e.g., EUR/USD. Our example only subscribes to EUR/USD so 

            // this is the only possible value

            string symbol = mds.getField(FIELD::Symbol);

            // Declare variables for both the bid and ask prices. We will read the MarketDataSnapshotFullRefresh

            // message for tthese values

            double bid_price = 0;

            double ask_price = 0;

            // For each MDEntry in the message, inspect the NoMDEntries group for

            // the presence of either the Bid or Ask (Offer) type 

            int entry_count = IntConvertor::convert(mds.getField(FIELD::NoMDEntries));

            for(int i = 1; i < entry_count; i++){

                        FIX44::MarketDataSnapshotFullRefresh::NoMDEntries group;

                        mds.getGroup(i,group);

                        string entry_type = group.getField(FIELD::MDEntryType);

                        if(entry_type == "0"){ // Bid

                                    bid_price = DoubleConvertor::convert(group.getField(FIELD::MDEntryPx));

                        }else if(entry_type == "1"){ // Ask (Offer)

                                    ask_price = DoubleConvertor::convert(group.getField(FIELD::MDEntryPx));

                        }

            }

            cout << "MarketDataSnapshotFullRefresh -> Symbol - " << symbol 

                        << " Bid - " << bid_price << " Ask - " << ask_price << endl; 

}

void FixApplication::onMessage(const FIX44::ExecutionReport& er, const SessionID& session_ID)

{

            cout << "ExecutionReport -> " << endl;

            cout << "  ClOrdID -> " << er.getField(FIELD::ClOrdID) << endl; 

            cout << "  Account -> " << er.getField(FIELD::Account) << endl;

            cout << "  OrderID -> " << er.getField(FIELD::OrderID) << endl;

            cout << "  LastQty -> " << er.getField(FIELD::LastQty) << endl;

            cout << "  CumQty -> " << er.getField(FIELD::CumQty) << endl;

            cout << "  ExecType -> " << er.getField(FIELD::ExecType) << endl;

            cout << "  OrdStatus -> " << er.getField(FIELD::OrdStatus) << endl;

            // ** Note on order status. ** 

            // In order to determine the status of an order, and also how much an order is filled, we must

            // use the OrdStatus and CumQty fields. There are 3 possible final values for OrdStatus: Filled (2),

            // Rejected (8), and Cancelled (4). When the OrdStatus field is set to one of these values, you know

            // the execution is completed. At this time the CumQty (14) can be inspected to determine if and how

            // much of an order was filled.

}

// Starts the FIX session. Throws FIX::ConfigError exception if our configuration settings

// do not pass validation required to construct SessionSettings 

void FixApplication::StartSession()

{

            try{

                        settings      = new SessionSettings("settings.cfg");

                        store_factory = new FileStoreFactory(* settings);

                        log_factory   = new FileLogFactory(* settings);

                        initiator     = new SocketInitiator(* this, * store_factory, * settings, * log_factory/*Optional*/);

                        initiator->start();

            }catch(ConfigError error){

                        cout << error.what() << endl;

            }

}

// Logout and end session 

void FixApplication::EndSession()

{

            initiator->stop();

            delete initiator;

            delete settings;

            delete store_factory;

            delete log_factory;

}

// Sends TradingSessionStatusRequest message in order to receive as a response the

// TradingSessionStatus message

void FixApplication::GetTradingStatus()

{

            // Request TradingSessionStatus message 

            FIX44::TradingSessionStatusRequest request;

            request.setField(TradSesReqID(NextRequestID()));

            request.setField(TradingSessionID("FXCM"));

            request.setField(SubscriptionRequestType(SubscriptionRequestType_SNAPSHOT));

            Session::sendToTarget(request, sessionID);

}

// Sends the CollateralInquiry message in order to receive as a response the

// CollateralReport message.

void FixApplication::GetAccounts()

{

            // Request CollateralReport message. We will receive a CollateralReport for each

            // account under our login

            FIX44::CollateralInquiry request;

            request.setField(CollInquiryID(NextRequestID()));

            request.setField(TradingSessionID("FXCM"));

            request.setField(SubscriptionRequestType(SubscriptionRequestType_SNAPSHOT));

            Session::sendToTarget(request, sessionID);

}

// Sends RequestForPositions which will return PositionReport messages if positions

// matching the requested criteria exist; otherwise, a RequestForPositionsAck will be

// sent with the acknowledgement that no positions exist. In our example, we request

// positions for all accounts under our login

void FixApplication::GetPositions()

{

            // Here we will get positions for each account under our login. To do this,

            // we will send a RequestForPositions message that contains the accountID 

            // associated with our request. For each account in our list, we send

            // RequestForPositions. 

            int total_accounts = (int)list_accountID.size();

            for(int i = 0; i < total_accounts; i++){

                        string accountID = list_accountID.at(i);

                        // Set default fields

                        FIX44::RequestForPositions request;

                        request.setField(PosReqID(NextRequestID()));

                        request.setField(PosReqType(PosReqType_POSITIONS));

                        // AccountID for the request. This must be set for routing purposes. We must

                        // also set the Parties AccountID field in the NoPartySubIDs group

                        request.setField(Account(accountID)); 

                        request.setField(SubscriptionRequestType(SubscriptionRequestType_SNAPSHOT));

                        request.setField(AccountType(

                                    AccountType_ACCOUNT_IS_CARRIED_ON_NON_CUSTOMER_SIDE_OF_BOOKS_AND_IS_CROSS_MARGINED));

                        request.setField(TransactTime());

                        request.setField(ClearingBusinessDate());

                        request.setField(TradingSessionID("FXCM"));

                        // Set NoPartyIDs group. These values are always as seen below

                        request.setField(NoPartyIDs(1));

                        FIX44::RequestForPositions::NoPartyIDs parties_group;

                        parties_group.setField(PartyID("FXCM ID"));

                        parties_group.setField(PartyIDSource('D'));

                        parties_group.setField(PartyRole(3));

                        parties_group.setField(NoPartySubIDs(1));

                        // Set NoPartySubIDs group

                        FIX44::RequestForPositions::NoPartyIDs::NoPartySubIDs sub_parties;

                        sub_parties.setField(PartySubIDType(PartySubIDType_SECURITIES_ACCOUNT_NUMBER));

                        // Set Parties AccountID

                        sub_parties.setField(PartySubID(accountID));

                        // Add NoPartySubIds group

                        parties_group.addGroup(sub_parties);

                        // Add NoPartyIDs group

                        request.addGroup(parties_group);

                        // Send request

                        Session::sendToTarget(request, sessionID);

            }

}

// Subscribes to the EUR/USD trading security

void FixApplication::SubscribeMarketData()

{

            // Subscribe to market data for EUR/USD

            string request_ID = "EUR_USD_Request_";

            FIX44::MarketDataRequest request;

            request.setField(MDReqID(request_ID));

            request.setField(SubscriptionRequestType(

                        SubscriptionRequestType_SNAPSHOT_PLUS_UPDATES));

            request.setField(MarketDepth(0));

            request.setField(NoRelatedSym(1));

            // Add the NoRelatedSym group to the request with Symbol

            // field set to EUR/USD

            FIX44::MarketDataRequest::NoRelatedSym symbols_group;

            symbols_group.setField(Symbol("EUR/USD"));

            request.addGroup(symbols_group);

            // Add the NoMDEntryTypes group to the request for each MDEntryType

            // that we are subscribing to. This includes Bid, Offer, High, and Low

            FIX44::MarketDataRequest::NoMDEntryTypes entry_types;

            entry_types.setField(MDEntryType(MDEntryType_BID));

            request.addGroup(entry_types);

            entry_types.setField(MDEntryType(MDEntryType_OFFER));

            request.addGroup(entry_types);

            entry_types.setField(MDEntryType(MDEntryType_TRADING_SESSION_HIGH_PRICE));

            request.addGroup(entry_types);

            entry_types.setField(MDEntryType(MDEntryType_TRADING_SESSION_LOW_PRICE));

            request.addGroup(entry_types);

            Session::sendToTarget(request, sessionID);

}

// Unsubscribes from the EUR/USD trading security 

void FixApplication::UnsubscribeMarketData()

{

            // Unsubscribe from EUR/USD. Note that our request_ID is the exact same

            // that was sent for our request to subscribe. This is necessary to 

            // unsubscribe. This request below is identical to our request to subscribe

            // with the exception that SubscriptionRequestType is set to

            // "SubscriptionRequestType_DISABLE_PREVIOUS_SNAPSHOT_PLUS_UPDATE_REQUEST"

            string request_ID = "EUR_USD_Request_";

            FIX44::MarketDataRequest request;

            request.setField(MDReqID(request_ID));

            request.setField(SubscriptionRequestType(

                        SubscriptionRequestType_DISABLE_PREVIOUS_SNAPSHOT_PLUS_UPDATE_REQUEST));

            request.setField(MarketDepth(0));

            request.setField(NoRelatedSym(1));

            // Add the NoRelatedSym group to the request with Symbol

            // field set to EUR/USD

            FIX44::MarketDataRequest::NoRelatedSym symbols_group;

            symbols_group.setField(Symbol("EUR/USD"));

            request.addGroup(symbols_group);

            // Add the NoMDEntryTypes group to the request for each MDEntryType

            // that we are subscribing to. This includes Bid, Offer, High, and Low

            FIX44::MarketDataRequest::NoMDEntryTypes entry_types;

            entry_types.setField(MDEntryType(MDEntryType_BID));

            request.addGroup(entry_types);

            entry_types.setField(MDEntryType(MDEntryType_OFFER));

            request.addGroup(entry_types);

            entry_types.setField(MDEntryType(MDEntryType_TRADING_SESSION_HIGH_PRICE));

            request.addGroup(entry_types);

            entry_types.setField(MDEntryType(MDEntryType_TRADING_SESSION_LOW_PRICE));

            request.addGroup(entry_types);

            Session::sendToTarget(request, sessionID);

}

// Sends a basic NewOrderSingle message to buy EUR/USD at the 

// current market price

void FixApplication::MarketOrder()

{

            // For each account in our list, send a NewOrderSingle message

            // to buy EUR/USD. What differentiates this message is the

            // accountID

            int total_accounts = (int)list_accountID.size();

            for(int i = 0; i < total_accounts; i++){

                        string accountID = list_accountID.at(i);

                        FIX44::NewOrderSingle request;

                        request.setField(ClOrdID(NextRequestID()));            

                        request.setField(Account(accountID));

                        request.setField(Symbol("EUR/USD"));

                        request.setField(TradingSessionID("FXCM"));

                        request.setField(TransactTime());

                        request.setField(OrderQty(10000));

                        request.setField(Side(FIX::Side_BUY));

                        request.setField(OrdType(OrdType_MARKET));

                        request.setField(TimeInForce(TimeInForce_GOODTILLCANCEL));

                        Session::sendToTarget(request, sessionID);

            }

}

// Generate string value used to populate the fields in each message

// which are used as a custom identifier

string FixApplication::NextRequestID()

{

            if(requestID == 65535)

                        requestID = 1;

            requestID++;

            string next_ID = IntConvertor::convert(requestID);

            return next_ID;

}

// Adds string accountIDs to our vector<string> being used to

// account for the accountIDs under our login

void FixApplication::RecordAccount(string accountID)

{

            int size = (int)list_accountID.size();

            if(size == 0){

                        list_accountID.push_back(accountID);

            }else{

                        for(int i = 0; i < size; i++){

                                    if(list_accountID.at(i) == accountID)

                                                break;

                                    if(i == size - 1){

                                                list_accountID.push_back(accountID);

                                    }

                        }

            }

}
```

### **下一步**

福汇无疑是允许散户投资者进行外汇投机的领先在线交易平台之一。如果你是一名散户交易者或技术专业人士，希望开始自己的自动化交易平台，或者想了解更多关于外汇和算法交易的知识，那么从基本概念开始，如[自动化交易架构](https://blog.quantinsti.com/algorithmic-trading-system-architecture/)、[市场微观结构](https://blog.quantinsti.com/market-microstructure/)、[策略回溯测试系统](https://blog.quantinsti.com/backtesting/)和[订单管理系统](https://blog.quantinsti.com/automated-trading-order-management-system/)。今天就开始[学习 algo 交易](https://www.quantinsti.com/courses/epat/)！

*免责声明:股票市场的所有投资和交易都有风险。在金融市场进行交易的任何决定，包括股票或期权或其他金融工具的交易，都是个人决定，只能在彻底研究后做出，包括个人风险和财务评估以及在您认为必要的范围内寻求专业帮助。本文提到的交易策略或相关信息仅供参考。*

### **下载代码**

*   FXCM over FIX 教程- C++代码*