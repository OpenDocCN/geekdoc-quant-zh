# k-最近邻算法:用 Python 实现的步骤

> 原文：<https://blog.quantinsti.com/machine-learning-k-nearest-neighbors-knn-algorithm-python/>

由[维布·辛格](https://www.linkedin.com/in/vibhu-singh-1b76b6105/)

在这篇博客中，我们将向您概述 K-最近邻(KNN)算法，并了解使用 Python 中的 K-最近邻一步步实现[交易策略](/algorithmic-trading-strategies/)。

本博客涵盖以下内容:

*   [机器学习的使用越来越多](#the-growing-use-of-machine-learning)
*   [关于 K-最近邻(KNN)](#about-k-nearest-neighbors-knn)
*   [用 Python 实现 K 近邻(KNN)的步骤](#steps-to-implement-k-nearest-neighbors-knn-in-python)
*   [KNN 算法的实现](#implementation-of-the-knn-algorithm)

* * *

## **机器学习的使用越来越多**

机器学习是人工智能中最流行的方法之一。在过去的十年里，[机器学习](/trading-using-machine-learning-python/)已经成为我们生活中不可或缺的一部分。

它是在像识别人类笔迹这样简单的任务或像自动驾驶汽车这样复杂的任务中实现的。预计在几十年后，更加机械的重复性工作将会结束。

随着越来越多的数据变得可用，有很好的理由相信[机器学习](/machine-learning-basics/)作为技术进步的必要元素将变得更加普遍。

ML 在许多关键行业产生了巨大的影响:金融服务、送货、市场营销和销售、医疗保健等等。不过这里我们就讨论一下[机器学习在交易](https://quantra.quantinsti.com/course/introduction-to-machine-learning-for-trading)中的实现和用法。

* * *

## **关于 K-最近邻(KNN)**

k-最近邻(KNN)是用于回归和分类问题的[机器学习中最简单的算法之一。KNN 算法使用数据，并基于相似性度量(例如距离函数)对新数据点进行分类。](https://quantra.quantinsti.com/course/trading-with-machine-learning-regression)

分类是通过对其邻居的多数投票来完成的。数据被分配给具有最近邻居的类。随着最近邻数量的增加，k 值的精确度可能会增加。

现在，让我们来了解一下在 [Python](/python-trading/) 中创建交易策略时 K 近邻(KNN)的实现。

如果你不熟悉 Python 并且希望学习 Python，这本[免费课程](https://quantra.quantinsti.com/course/python-trading-basic)和[免费书籍](https://www.quantinsti.com/python-basics-handbook)将对你有极大的帮助。

* * *

## **用 Python 实现 K 近邻(KNN)的步骤**

### **步骤 1 - **导入库****

我们将从导入在 Python 中实现 KNN 算法所需的必要的[库](/python-trading-library/)开始。我们将导入 numpy 库进行科学计算。(你可以在这里了解 numpy [，在这里](/python-numpy-tutorial-installation-arrays-random-sampling/)了解 matplotlib [)。](/python-matplotlib-tutorial/)

接下来，我们将导入用于绘制图形的 **matplotlib.pyplot** 库。

<u>我们将导入两个机器学习库</u>:

*   **KNeighborsClassifier** 来自 *sklearn.neighbors* 实现 k 近邻投票和
*   **accuracyscore** 来自 *sklearn.metrics* 的准确度分类分数。

我们还将导入 *fixyahoo_finance* 包来从雅虎获取数据。