---
title: GraphQL在全栈开发中的应用
date: 2021-09-01 09:12:46
tags:
---

> 长期以来REST API一直作为一种标准用于api的编写，也被大多数公司采用，但它也又自身的很多限制，近期出现了一个新的标准GraphQL，它成为一种更好的API编写选择，特别是用于多数据源场景。
#### REST API的问题
传统的情况是后端会提供带有独立URL的api接口给前端来进行展示，然而REST API接口有两个典型问题有overfetching和underfetching。Overfetching即返回的数据多于所需要的数据，underfetching即返回的数据少于所需要的数据，甚至有些时候还需要将多个api返回的数据进行组装才能进行前端展示。同时，随着api不断增多，版本升级后也需要维护众多的api和api文档。


### 何为GraphQL
简单的说，GraphQL是一种描述请求数据方法的语法，通常用于客户端从服务端加载数据，它是用于访问不同来源数据的统一接口。
- 提供单一节点
- 它允许客户端指定具体所需的数据。
- 它让从多个数据源(mysql数据库, mongo数据库,redis, API, 第三方数据等)汇总取数据变得更简单。
- 它使用了类型系统来描述数据(schema)。

GraphQL 层处于客户端与一个或多个数据源之间，它接收客户端的请求然后根据你的设定取出需要的数据，它仅提供一个节点，让前端去自主选择需要那些字段的数据，返回有效的数据。

REST 模型好比你需要打车、叫外卖和约客户见面，你需要分别打3个电话。

GraphQL 就好像你的私人助理，你只要给她一个电话，告诉你要做的这3件事情，它就给你办好了。

GraphQL建立了一套语言让你畅通的和这个私人助理沟通。它包含了schema（类型），queries（查询） 以及 resolvers（解析器）。
下图展示了在GitHub GraphQL API平台查询react库信息：

- schema 可以理解为一种协议，用来定义描述接口，type 的标量类型有String，Int，Float，Boolean，Enum，ID等
- query 关键字定义了一个新的查询，它将取出名叫 repository的字段。GraphQL 查询（Queries）最棒之处就是它支持多个字段嵌套查询，同时可传入参数，查询指定字段
- resolver 会告诉 GraphQL 在哪里以及如何去取到对应字段的数据，这里可以去数据库中查，也可以对接现成的rest api，也可以是三方api

### 全栈应用
Graphql可以说是全栈开发的利器，尤其是前端开发者，因为前端最清楚自己想要什么样的数据，这样就可以反推去获取想要的数据。
全栈角度来看，我们需要在前端发起fetch请求或创建Graphql apollo client去请求数据，后端创建一个Graphql server去集中定义数据。Graphql可整合各种数据源，然后根据自身语言，定义为schema来为前端提供数据，这样的数据才是有价值的数据。

Graphql的开源生态圈也发展迅速，出现了apollo，Relay等优秀的开源库，apollo可实现查询数据的缓存，当后端数据变化时，便根据缓存规则主动返回更新数据到前端，如前端绑定该数据，可实现动态页面变化。

#### 3种Graphql 技术接入架构

1. Graphql 直连数据库，直连的方式可较少性能消耗

2. 集成现有服务的GraphQL层

3. 直连数据库和现有服务的混合模式

由此可见，Graphql 相比于rest api更适用于如下场景：
- 包括移动端在内的多个客户端、
- 正在转向或者已经采用了微服务架构、
- 遗留 REST API 数量暴增、
- 注重良好的 API 文档和开发者体验等场景下更具有优势。


同时，Graphql 不论是服务端还是客户端，都提供了大多数编程语言的支持（C# / .NET 、Clojure 、Elixir 、Erlang 、Go 、Groovy、 Java、 JavaScript、 Julia、 Kotlin、 Perl、 PHP、 Python、 R、 Ruby、 Rust、 Scala、 Swift），可以说不止在开源，而是在建立一种标准。
当前Graphql 已运用到本人所在项目中，可依托大数据沉淀的多纬度数据，将所需数据建立schema后统一到Graphql的单一endpoint下，提供更多数据指标展示给客户。
相信随着微服务和severless的大规模运用，Graphql 的运用将越来越广泛。
