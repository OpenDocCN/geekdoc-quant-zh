# 反向交易者:它是什么，如何安装，策略，交易和更多

> 原文：<https://blog.quantinsti.com/backtrader/>

苏莱曼·埃姆雷·耶希尔

Python 使交易者和投资者能够对他们的策略进行回溯测试，以便他们可以通过观察策略的过去表现来评估策略是否良好。然而，并不是每个人都有高水平的编码技能，能够以最准确和有效的方式实现他们的回溯测试。多亏了 Backtrader 库，每个人都可以高效准确地回溯测试他们的策略。

在本博客中了解如何使用 Backtrader 库进行回溯测试，包括:

*   [什么是反向交易者？](#what-is-backtrader)
*   [如何安装 Backtrader 库？](#how-to-install-the-backtrader-library)
*   [用 Backtrader 创建你的第一个代码](#create-your-first-code-with-backtrader)
*   如何用 Backtrader 对策略进行回溯测试？
*   [如何用 Backtrader 做现场交易？](#how-to-do-live-trading-with-backtrader)
*   [反向交易者的优势](#advantages-of-backtrader)
*   [反向交易者的限制](#limitations-of-backtrader)

* * *

## 什么是反向交易者？

Backtrader 是一个开源的 Python 库，可以用于回溯测试、策略可视化和实时交易。

虽然不使用任何特殊的库，用 Python 回测你的算法交易策略是完全可能的，但是 Backtrader 提供了许多特性来促进这个过程。一般来说，普通回溯测试的每个复杂组件都可以通过调用特殊函数用一行代码创建。

* * *

## 如何安装 Backtrader 库？

安装 Backtrader 库没有特殊要求。它也没有任何依赖关系。您可以使用软件包管理器“pip”来安装这个库。

要使用“pip”软件包管理器安装 Backtrader 库，请打开命令提示符(或 Mac 用户的终端),然后键入以下代码:

`pip install backtrader`

您可以通过尝试以下代码来检查它是否安装成功: