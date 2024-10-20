# Zipline 库-在 Windows 10 上安装

> 原文：<https://blog.quantinsti.com/zipline-library-installation-windows/>

马里奥·比萨

在这篇文章中，我们将一步一步地描述 Python Zipline 库在 Windows 机器上的安装过程。

这是我们在这篇文章中将要做的事情的概述:

*   [滑索-简介](#zipline-intro)*   [在 AWS 上设置 Windows 机器](#setup-windows-aws)*   [安装蟒蛇](#install-anaconda)*   [为 Zipline 创建 Conda 环境](#create-conda-zipline)*   [设置 Zipline Conda 环境](#setup-conda-zipline)*   [从 Quandl(摄取过程)中检索数据](#data-from-quandl)*   [执行简单的回溯测试](#perform-backtest)*   [生成绩效报告](#generate-report)

* * *

## **滑索——一个简介**

Zipline 是 Python 中最完整的库之一，它与 Pyfolio 库一起为我们的机器提供了一个完整的回溯测试平台，可以处理多种金融工具和时间框架。

*推荐阅读:[Python 中的 Zipline 介绍](/introduction-zipline-python/)T3】*

回溯测试是我们用历史数据或随机序列测试交易策略的过程，目的是了解它们过去的表现，并对预期的未来行为做出推断。

作为程序员，除了时间，没有什么能阻止从零开始开发一个回溯测试平台，但是根据复杂性，它可以成为一个持续数年的项目。因此，有了正确的工具，我们几乎可以专注于交易策略的实施，并加快回溯测试过程。

*推荐阅读:[在 Zipline 中导入 CSV 数据进行回溯测试](/importing-csv-data-zipline-backtesting/)T3】*

在开始安装过程之前，请记住，您可以直接在 [Blueshift](https://blueshift.quantinsti.com/) 中试验该库，它可以连接到不同市场和时间频率的数据，随时可以使用。

如果你想让你的生活变得复杂一点，那就继续读下去。

* * *

## **在 AWS 上设置 Windows 机器**

我们首先需要一台能够运行 Python 的机器，几乎任何或多或少现代的机器都可以，从简单的 RaspberryPi 到 Linux、Mac 或 Windows PC。

对于这篇文章，我们将使用亚马逊网络服务(AWS)的 Windows 服务器，所以首先要启动这台机器。如果您打算在本地机器上安装 Zipline，可以跳到下一步。

如果这是您第一次使用 AWS，您必须在设置 EC2 机器之前创建一个帐户。

步骤 01 -连接到您的 AWS EC2:[https://console.aws.amazon.com/ec2](https://console.aws.amazon.com/ec2)

步骤 02 -单击正在运行的实例。

![](img/ee8ab41d95bad25ea0d0f4bde61c082d.png)

步骤 03 -单击“启动实例”按钮。

![](img/b9572a1d0e1e2f778bd92a34cb721b77.png)

步骤 04 -选择一个 Windows 实例。即微软 Windows Server 2019 基础:

![](img/610db5c94f04480b791f6cf15f0c281c.png)

AWS 有各种各样的机器配置，从简单和免费的机器到超级计算机，选择一个最适合您的项目和预算。对于这个简单的例子，他们称之为“符合自由层条件”的机器就足够了。

步骤 05 -选择一个实例类型，如带有 8Gb RAM 的 t2.large 或任何其他适合您需要的类型。

![](img/dfbade91811be2276b1201033c12ffc9.png)

步骤 06 -点击查看和启动按钮。

步骤 07 -查看实例的详细信息，然后单击启动按钮。(这里我们接受默认配置)。

![](img/59d52fb1f8b535eda070b6bfca6c0481.png)

步骤 08 -现在，我们已经运行了一个随时可用的 Windows 2019 服务器实例:

![](img/216e59e1447a6787f491cdc54dd3d1e6.png)

步骤 09 -单击 Connect 按钮获取实例的 DNS、用户名和密码。

![](img/0eb35d534165cd6bc1d2f434bcee991b.png)

步骤 10 -启动远程管理员工具，并使用上一步中的凭证连接到远程机器。

![](img/8a45b4fa465ac9c49b46bea99034a1ac.png)

这里我们有一台远程 Windows 机器可以使用。

* * *

## **安装蟒蛇**

在这一步中，我们将安装 Anaconda，这是一个包含多种工具的数据科学套件。真的不需要安装这么多工具，有了 Miniconda 就足够了。

步骤 01 -让我们用 Python 3.7 为 Windows 安装 Anaconda 2019.10

[https://www.anaconda.com/distribution/](https://www.anaconda.com/distribution/)

![](img/e877f9215d843dd723cb0e093a60a7a1.png)

步骤 02 -下载过程完成后，我们就可以开始安装了。

![](img/a24140f5a2af00e2309cc4381d340085.png)

![](img/381f5652f317edc22b79762d55bf8789.png)

![](img/247f64502474e51af5ce52f3b84514ad.png)

![](img/bcbd4eda0777833bf3ba904b59a51548.png)

![](img/2eef7274f7b51fe85ad069eb10250f1f.png)

![](img/af626116e3a2d7354f9e101073745dcb.png)

![](img/13d8dcc22a285f5847359f7cd9647ac5.png)

![](img/c9a44b9a47de7b626b38d053f0cdb68b.png)

现在我们已经在机器上安装了 Anaconda 套装。

步骤 03 -启动 Anaconda 导航器:

![](img/b23be2f129de09dd9e1c549a025240d6.png)

![](img/18233bbab2cf3173e8d0a568219190ea.png)

步骤 04 -点击环境按钮:

![](img/663c6b9bc1c3d9765712fa2ed75a4439.png)

步骤 05 -在 base root 环境中，单击 play 按钮启动 Conda 终端。

![](img/ceb0e4da6f05ddd8e7df8561fc0fbcef.png)

* * *

## **为 Zipline 创造康达环境**

一个 [Conda 环境](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)是一个容器，让我们处理不同版本的 Python 及其库。例如，我们可以在一个环境中使用 Python 3.5 和 Pandas 0.24，在另一个环境中使用 Python 3.7 和 Pandas 1.0.3。这对于隔离项目的特定版本非常有用。

步骤 01 -让我们使用以下命令检查 conda 环境:

*>康达环境列表*

![](img/411a9a4599aab4edf8af3745c4d92e2a.png)

此时，我们只能看到默认安装的基础环境。

步骤 02 -现在让我们用 Python 3.5 安装一个名为“z35”的新环境:

*>康达 create -n z35 python=3.5*

![](img/0e21f534a121162bf5b49b01e5b95488.png)

步骤 03 -让我们再次检查 conda 环境，看看我们的新 z35 环境:

*>康达环境列表*

![](img/3dfbe5e4a5032c9cfa3f089d216f1063.png)

步骤 04 -现在，我们开始激活 z35 环境:

*>康达激活 z35*

![](img/78cd79e4ab209cb59cb94e5ea1b9e319.png)

星号表示活动环境。

步骤 05 -让我们尝试检查 Python 版本:

*> python -版*

![](img/5493c60adb0208ce8b9928a39dcfa6fe.png)

步骤 06 -安装 ipykernel:

*>康达安装 ipykernel*

![](img/f406edf414e3bf7dbb67cf048ffd3da4.png)

*> python -m ipykernel 安装-用户*

![](img/ec967170ba1a366492f726293eeea3fc.png)

步骤 07 -安装 Jupyter:

*>康达安装 jupyter*

![](img/cbaa350fca27249797a20428da94cf60.png)

步骤 08 -启动 Jupyter 笔记本:

*> jupyter notebook*

![](img/2c7c030e737c0fa5a869e4561d188dc9.png)

默认的 web 导航器打开 Jupyter 应用程序。

![](img/4b36727680c32c45d50a8eab1bc38a73.png)

步骤 09 -创建一个新的笔记本并选择 z35 内核。

![](img/2ccf1e59c2b6d90717a8601e42e6cf08.png)

如果笔记本显示消息:**内核错误！**这意味着新环境不存在！

**我们的 z35 环境发生了什么变化？**

我们已经在 Conda 上安装了 ipykernel，但是我们还需要在 Python3 上安装它。

步骤 10 -尝试修复错误:

*> python3 -m pip 安装 ipykernel*

![](img/de8c529de606267367c644781e13fbb8.png)

*> python3 -m ipykernel 安装-名称 z35 -用户*

![](img/0a62e514e3659014b98ecd5e615a0862.png)

步骤 11 -再次启动 Jupyter 笔记本:

![](img/98e21b8bbd565da60cbd204d3963c664.png)

步骤 12 -再次启动 Jupyter 笔记本:

![](img/0d5b4111cf6555927b4653ea3e6c5393.png)

现在我们已经在 z35 环境中的 Python 3.5 上安装了 Jupyter notebook。

* * *

## **设置 Zipline Conda 环境**

到目前为止，我们已经有了一台运行 Python 3.7 的 Anaconda 套件的 Windows 机器，我们已经安装了一个名为 z35 的新 Python 3.5 环境，我们还安装了 Jupyter notebook 的内核，并检查了我们是否可以访问 z35 环境。

现在我们必须安装所需的 [Python 库](/python-trading-library/)来运行 Zipline。虽然我们可以一次安装所有的东西，但是我们将安装通用库，然后专注于以特定的方式安装 Zipline 库。

步骤 01 -让我们安装 Numpy、Pandas 和 matplotlib 库:

*>伯爵安装 numpy 熊猫 matplotlib*

![](img/aad11c8afef3789c3725c20736dfc26f.png)

步骤 02 -和 zipline 库，只获取该库的安装消息:

*>* 康达安装-康达-锻造滑索

![install zipline](img/e4617361475edfa1eae4be8ab9067eae.png)

步骤 03 -现在，我们再次启动笔记本电脑，检查 zipline 库是否安装成功:

*> jupyter notebook*

![](img/7f0fb6b6efe910c25feb053151710c25.png)

**太好了！zipline 库已成功导入。**

* * *

## **从 Quandl(摄取过程)中检索数据**

我们现在已经安装了 zipline 库。为了测试一些代码，我们需要用摄取过程检索数据。为此，我们需要在 Quandl 中注册并获得个人密钥:[https://www.quandl.com](https://www.quandl.com)

之后，需要将 Quandl API key 包含到一个名为 *QUANDL_API_KEY* 的系统变量中，命令如下:

*>设置 QUANDL _ API _ KEY = "<YOUR _ API _ KEY>"*

步骤 01 -设置 QUANDL_API_KEY 环境变量:

![](img/42c49dac08c54f943bd2e14d5a214f7c.png)

如果您想将环境变量配置为永久性的，您可以在系统属性窗口中包含它，单击环境变量按钮。

![](img/e3a0451f5e52d45b60bcea4305e90fac.png)

现在，我们已经安装了 Zipline 库，创建了一个 Quandl 帐户，获得了从 Quandl Wiki DB 检索数据的令牌，并使用该令牌配置了我们的 Windows 机器。是时候检索 Wiki DB 数据集了，以便在 Zipline 回溯测试中使用它们。

步骤 02 -从 Quandl 获取数据:

*> zipline 摄取-b quandl*

![](img/379bcc7dc60256771ae91f49abe81dc9.png)

![](img/ff05723d16f550a7b63f7f8e2a913f5a.png)

现在我们有一些来自 Quandl 的数据来测试一些策略。是时候测试一个基本策略了。

Zipline 实际上存在 2000 年之前的日期问题，因此需要对 zipline 安装文件夹中的 benchmark.py 脚本应用一个解决方法。找到它，并通过对内容进行评论来修改它，然后在上面放上这段文字。

使用命令 *conda env list* 在之前创建的 zipline *z35* 环境中查找 *benchmark.py* 脚本。

步骤 03 -在 benchmark.py 上应用变通方法

![](img/54245d6f379f2a9e6420639904e44e7c.png)

* * *

## **执行简单的回溯测试**

启动 Jupyter 并创建一个新笔记本。

下面的代码改编自 Andreas Clenow 的书“交易进化”，是一个简单的算法，当价格穿过移动平均线时买入股票，当价格穿过移动平均线时平仓。

![](img/1e4b2a5d7f3acb41a8f37ff81d90a77c.png)

* * *

## **生成绩效报告**

如果一切顺利，回溯测试以一个统计表和一些简单的性能图表结束。

在“分析”功能中，我们可以编写任何代码来分析回测，这里我们使用 Pyfolio 库来创建一个简单的退货单。值得研究该图书馆，以发挥其全部力量。

![](img/f59e46fc60ca76936c538d41764acac9.png)

![](img/15f34a3b365824aa3f46704d76d57361.png)

![](img/df58e9c94b2495b8cae9b97a905c5658.png)

* * *

## **结论**

虽然在本文中，我们已经在本地机器上安装了 Zipline 库进行回溯测试，但这场战斗才刚刚开始，因为数据接收过程必须适应每个数据提供商和市场时间表。

另一方面，Zipline 库无疑是一个强大的回测工具，但它不允许我们轻松地切换到实时，所以有一个具有这种能力的库的并行开发 ie。[http://www.zipline-live.io/](http://www.zipline-live.io/)

最后，我们可以利用这个库的功能，而不需要将它安装在我们的机器上，这个平台有几个市场可以实时使用。

*<small>免责声明:本文提供的所有数据和信息仅供参考。QuantInsti 对本文中任何信息的准确性、完整性、现时性、适用性或有效性不做任何陈述，也不对这些信息中的任何错误、遗漏或延迟或因其显示或使用而导致的任何损失、伤害或损害负责。所有信息均按原样提供。</small>*

**参考文献**

*   [量子乌托邦](https://www.quantopian.com/)
*   [蓝移](https://blueshift.quantinsti.com/)
*   [Zipline.io](https://github.com/quantopian/zipline)
*   [文件夹](https://github.com/quantopian/pyfolio)
*   书:交易由安德烈亚斯·克莱诺发展