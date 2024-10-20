# 在 Mac 上安装 Prophet 库

> 原文：<https://blog.quantinsti.com/installing-prophet-library-mac/>

马里奥·比萨

Prophet 是由脸书公司开发的一个大型库，用于促进自然语言处理(NLP)任务。在这篇文章中，我们了解了如何在 Mac 机器上安装 Prophet，因为根据我们在机器上的配置，我们可能会面临一些安装问题。

我们涵盖:

*   [从先知开始](#beginning-with-prophet)
*   [安装 Prophet 前检查 Python 环境](#checking-the-python-environment-before-installing-prophet)
*   [安装 Prophet 依赖项](#installing-the-prophet-dependencies)
*   [安装先知库](#installing-the-prophet-library)
*   [测试先知](#testing-prophet)

* * *

## 从先知开始

有时我们会发现自己的机器上的 Python 环境看起来很像一个垃圾抽屉。在安装 Prophet 时，我们已经在使用的 Python 版本和库会让我们有些头疼，更具体地说，是它的主要依赖项 Pystan 库。

为了让 Prophet 在 Mac 上的安装过程不那么痛苦，我根据强烈推荐你阅读的[官方文档](https://facebook.github.io/prophet/)创建了这个帖子。

* * *

## 安装 Prophet 之前检查 Python 环境

在安装 Prophet 之前，让我们检查一下是否正确安装了 Python 环境。

通常，你应该在你的机器上安装 [Anaconda](https://www.anaconda.com/products/individual) 或者 [Miniconda](https://docs.conda.io/en/latest/miniconda.html#macosx-installers) 。如果你还没有安装它，[看看这篇文章](/set-up-python-system/)。

因此，安装了 anaconda 或 Miniconda 后，按 CMD+ <space bar="">在 Mac Spotlight 中搜索，键入 Terminal 并打开 Terminal.app。如果您使用的是 conda 环境，请选择您的首选环境。</space>

让我们检查一下 python 版本:

```py
% python --version
```

如果 Python 版本是 3.6、3.7、3.8 或 3.9 就可以了，如果不是，你可以创建一个 Python 环境，如引用的[帖子](/set-up-python-system/)中所示。

我建议为这个项目创建一个新的 python 环境，因此您可以键入以下命令:

```py
% cd 
% conda create -n prophet39 python=3.9
% conda activate prophet39
```

至此，我们已经有了一个 python 3.9，可以安装新的库了。

如果你想使用 Jupyter 笔记本，你需要安装一些其他的库:

```py
% conda install ipykernel
% python -m ipykernel install --name prophet39 --user
% conda install jupyter
```

* * *

## 安装 Prophet 依赖项

正如官方文件所说，先知的主要依赖是 pystan。PyStan 有自己的[安装说明](https://pystan.readthedocs.io/en/latest/installation.html)。在使用 pip 安装 prophet 之前，使用 pip 安装 pystan。

```py
% pip install pystan==2.19.1.1
```

您可能会得到如下错误:

```py
ERROR: Command errored out with exit status 1
Cython>=0.22 and NumPy are required.
ERROR: Failed building wheel for pystan
```

不要担心这个问题，让安装过程持续到最后，因为它会以正确的方式安装依赖项。过程很慢，耐心点。最后，您将看到以下消息:

```py
Successfully installed Cython-0.29.24 numpy-1.21.1 pystan-2.19.1.1
```

在您的系统上安装了 PyStan 及其依赖项之后，您需要安装 Prophet。

* * *

## 安装先知库

要安装 Prophet 库，您可以照常使用 pip 命令:

```py
% pip install prophet
```

同样，您可能会在安装过程中看到如下一些错误:

*   ***错误:命令出错退出状态 1:***
*   ***ModuleNotFoundError:没有名为“熊猫”的模块***
*   ***错误:未能为先知*** 造轮

不要担心这个问题，让安装过程持续到最后，因为它会以正确的方式安装依赖项。过程很慢，耐心点。最后，您将看到以下消息:

```py
Successfully installed Cython-0.29.24
LunarCalendar-0.0.9
cmdstanpy-0.9.68
convertdate-2.3.2
ephem-4.0.0.2
hijri-converter-2.2.0
holidays-0.11.2
korean-lunar-calendar-0.2.1
pandas-1.1.5
prophet-1.0.1
pymeeus-0.5.11
pystan-2.19.1.1
setuptools-git-1.2
tqdm-4.62.2
ujson-4.1.0

```

* * *

## 测试先知

最后，让我们通过一个简单的测试来检查所有的东西是否都工作正常[。](https://facebook.github.io/prophet/docs/quick_start.html#python-api)

确保您的项目文件夹中有这个 csv 数据文件。您可以通过以下方式查看您的位置:

```py
% pwd
```

这个命令给出了你现在所在机器的绝对路径，用 Finder 把 csv 数据文件复制到那里。

打开一个 Jupyter 笔记本，选择 prophet39 内核，或者您喜欢的编辑器，然后输入下面的例子:(您必须使用几个代码块来检查每个句子)

有关代码，请参见随附的笔记本: