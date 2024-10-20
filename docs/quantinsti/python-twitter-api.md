# 如何使用 Python 和 Twitter API 获取推文

> 原文：<https://blog.quantinsti.com/python-twitter-api/>

由[乌迪莎·阿洛克](http://www.linkedin.com/in/udisha-alok)

社交媒体是名副其实的信息金矿，也是了解全世界人民集体心理的窗口。无论是政治家、名人、创意艺术家、教授还是学生，每个人似乎都在推特上。

它变得越来越受欢迎，名人的推文影响了数百万粉丝和市场！

因此，Twitter 数据被用于包括交易在内的各种领域的情绪分析。

这篇博客将展示我们如何使用 Twitter API 从 Twitter 获取数据。我们将为此使用 Tweepy 库，并详细探索使用它可以获得的各种类型的数据。这篇博客是由两部分组成的迷你系列的第一部分。

让我们看看我们将在这个博客中涵盖什么。

*   [什么是 Twitter API？](#what-is-twitter-api)
*   [Twitter API v2 访问级别](#twitter-api-v2-access-levels)
*   [访问 Twitter API](#getting-access-to-the-twitter-api)
*   [基本通道与高架通道](#essential-access-vs-elevated-access)
*   [高架通道应用提示](#tips-for-elevated-access-application)
*   [Tweepy 使用 Python 从 Twitter 获取数据](#tweepy-for-fetching-data-from-twitter-using-python)
*   [安装 Tweepy](#installing-tweepy)
*   [API 认证](#api-authentication)
*   [获取用户 id 和屏幕名称](#get-user-id-and-screen-name)
*   [获取用户信息](#get-user-info)
*   [获取追随者数量](#get-follower-count)
*   [从您的时间线获取推文](#get-tweets-from-your-timeline)
*   [获取用户的推文](#get-tweets-by-a-user)
*   [过滤转发和回复](#filtering-retweets-and-replies)
*   [使用分页进行搜索](#search-using-pagination)
*   [获取推文回复](#get-replies-to-a-tweet)
*   [通过标签获取推文](#get-tweets-by-a-hashtag)
*   [通过关键词](#get-tweets-by-a-keyword)获取推文
*   [组合多个查询](#combining-multiple-queries)

* * *

## 什么是 Twitter API？

Twitter API 是 Twitter 提供的官方编程端点。它允许开发者访问 Twitter 上数百万用户每天分享的大量公共数据。

Twitter API 的最新版本是 v2，它是官方的主要 Twitter API。但是 Twitter API v1.1 版还在用。

这两个版本的 API 之间有一些重要的区别。因此，1.1 版中的一些功能可能不适用于 v2。

根据 Twitter 网站的说法，v2 的构建是为了“更好地服务于更广泛的需求，引入了新的功能和端点，并改善了开发人员的体验。”

有关两个版本之间差异的更多信息，请参考此链接。

* * *

## Twitter API v2 访问级别

Twitter API v2 提供了不同的访问级别:基本、高级和学术研究。高架+级也即将到来，根据官方网站。

下图比较了每个访问级别下的一些可用功能。

![Twitter API v2 access levels](img/6cc9f9fd95ae4702d0f43ba759a2076b.png)

Twitter API v2 access levels: Source



对于本文中出现的一些代码，您需要有提升的访问权限。

* * *

## 访问 Twitter API

要使用 Twitter API v2，您需要:

*   经批准的开发人员帐户。
*   来自位于项目中的开发人员应用程序的密钥和令牌，用于身份验证。

阅读官方指南，了解更多关于 Twitter API 的入门知识。

一旦你注册了开发者账户，你就可以立即获得**基本权限**。需要提升访问权限才能向 Twitter v1.1 版发出请求，并获得 v2 的附加功能。基本访问直接可用，而提升访问必须请求。

* * *

## 基本通道与高架通道

简而言之，基本通道和高架通道的区别如下:

| **序列号** | **基本访问** | **高架通道** |
| one | 不需要申请。 | 需要批准的开发者帐户申请。 |
| Two | 立即可用。 | 一般需要 48-72 小时。但是，审查提升访问权限的申请可能需要两周时间 |
| three | 自由的 | 每月免费访问多达 2M 推文和 3 个应用程序环境 |
| four | 1 个应用程序，1 个项目 | 3 个应用程序，1 个项目 |
| five | 有限的功能 | 更多功能 |

您需要从开发者门户申请提升的访问权限，以访问本博客中讨论的所有代码。这个过程非常简单。

### 高架通道应用技巧

以下是一些我认为有助于提升访问权限申请更快获得批准的有用提示:

1.  在你的应用程序中诚实地说明你的应用程序的目标以及你打算如何使用这些数据。
2.  提供关于您的项目/应用程序的详细信息。
3.  如果您的任何回复需要更多信息，Twitter 将向您发送电子邮件。请尽快坦率地详细回答。
4.  如果你的申请因为没有及时提供所需信息而被拒绝，那么你可以通过回复收件箱中的电子邮件来重新打开该申请。
5.  如果您的应用程序因为其用例违反了 Twitter 政策而被拒绝，您就不能重新申请它。

更多详情，请参考[这些](https://developer.twitter.com/en/support/twitter-api/developer-account)常见问题解答。

一旦您的提升访问权限申请获得批准，您将在您注册的电子邮件地址收到一封电子邮件。

让我们从代码开始吧！

* * *

## 使用 Python 从 Twitter 获取数据的 Tweepy

Tweepy 是一个易于使用的 Python 库，用于访问 Twitter API。它的 API 类提供了对 Twitter API 的 RESTful 方法的访问。这使得它易于理解和学习，成为访问 Twitter API 功能的流行选择。

* * *

## 安装 Tweepy

要使用 pip 从 PyPI 安装 Tweepy，可以使用以下命令:

```py
pip install tweepy
```

或者，您可以从 Github 存储库安装它:

```py
pip install git+https://github.com/tweepy/tweepy.git
```

* * *

## API 认证

当你在 Twitter 上注册开发者账户时，你会得到 API 密匙和密码(这些功能类似于你的应用的用户名和密码)，以及访问令牌和密码(这些代表拥有该应用的用户)。在向 Twitter API 发出请求之前，您将需要这些来验证您自己。

除非重新生成，否则这些密钥和令牌不会过期，并且需要安全地保存，以便您可以为您的代码访问它们，而不会将它们透露给其他人。

为此，我们将创建一个配置文件来保存这些凭据。然后，我们将在代码中从配置文件中读取这些值。

### 创建配置文件

1.  打开记事本(或任何基本的文本编辑器)，并创建以下格式的文件:

```py
[twitter]
api_key = XXXXXXXXXXXXXXXXXXXXXXXXX
api_key_secret = XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
access_token = XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
access_token_secret = XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

```

2.现在，用“config.ini”这个名称保存这个文件。

### 从配置文件中读取凭据

我们现在将使用 configparser 库从配置文件中读取凭据的值。