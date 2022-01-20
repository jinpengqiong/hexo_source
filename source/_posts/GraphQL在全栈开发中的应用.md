---
title: GraphQL在全栈开发中的应用
date: 2021-09-01 09:12:46
tags: GraphQL Apollo
---

> 长期以来REST API一直作为一种标准用于api的编写，也被大多数公司采用，但它也又自身的很多限制，近年来出现了一个新的标准GraphQL，它成为一种更好的API编写选择，特别是用于多数据源和多端场景。
#### REST API的问题
传统场景下后端提供带有独立URL的api接口给前端进行展示，然而REST API接口有两个典型问题有overfetching和underfetching。Overfetching即返回的数据多于所需要的数据，underfetching即返回的数据少于所需要的数据，甚至有些时候还需要将多个api返回的数据进行组装才能进行前端展示。同时，随着api不断增多，版本升级后也需要维护众多的api和api文档。
### 何为GraphQL
简单的说，Graphql是一种描述请求数据方法的语法，通常用于客户端从服务端加载数据，访问不同来源数据的统一接口。
- 提供单一节点
- 它允许客户端指定具体所需的数据
- 它让从多个数据源(mysql数据库, mongo数据库,redis, API, 第三方数据等)汇总取数据变得更简单
- 它使用了类型系统来描述数据(schema)

下图展示了REST API和Graphql API怎么获取数据的：
#### REST API
![img1](/assets/QaAcN24U8whrNKZNHauw8quMx2dxXTV6QJWk.png)
#### Graphql API
![img2](/assets/HKILGdrpW082ziY6D85tJu0oHDgHuW7p1txZ.png)
Graphql 层处于客户端与一个或多个数据源之间，它接收客户端请求，再根据你的设定取出需要的数据。它仅提供一个节点，让前端去自主选择需要那些字段的数据，返回有效的数据。

REST 模型好比你需要打车、叫外卖和约客户见面等行为，你需要分别打3个电话。
![img3](/assets/2022-01-06_16-25-23.jpg)
GraphQL 就好像你的私人助理，你只要给她一个电话，告诉你要做的这3件事情，它就给你办好了。
![img4](/assets/2022-01-06_16-25-03.jpg)
Graphql建立了一套语言让你畅通的和这个私人助理沟通。它包含了schema（类型），queries（查询） 以及 resolvers（解析器）。

下图展示了在GitHub GraphQL API平台查询react库信息：
![gif1](/assets/1.gif)

- schema 可以理解为一种协议，用来定义描述接口，type 的标量类型有String，Int，Float，Boolean，Enum，ID等.
![img5](/assets/2022-01-08_10-12-28.jpg)

- query 关键字定义了一个新的查询，它将取出如图中repository字段。GraphQL 查询（Queries）最棒之处就是它支持多个字段嵌套查询，同时可传入参数，查询指定字段。

- resolver 会告诉 GraphQL 在哪里以及如何去取到对应字段的数据，这里可以去数据库中查，也可以对接现成的rest api，或微服务提供接口。

### 全栈应用
Graphql可以说是全栈开发的利器，尤其是前端开发者，因为前端最清楚自己想要什么样的数据，这样就可以反推去获取想要的数据。

全栈角度来看，我们需要在前端发起fetch请求或创建Graphql apollo client去请求数据，后端创建一个Graphql server去集中定义数据和对接数据源。Graphql可整合各种数据源，然后根据自身语言，定义为schema来为前端提供有价值的数据。
![img6](/assets/2022-01-07_17-03-17.jpg)

Graphql的开源生态圈也发展迅速，出现了apollo，Relay等优秀的开源库，Apollo基于Graphql提供了更加强大的功能，搭配前端框架React或VUE可完美实现全栈开发。它提供了查询数据的缓存，当后端数据变化时，便根据缓存规则主动返回更新数据到前端，如前端绑定该数据，可实现动态页面变化。Apollo提供了一个统一界面集中式管理不同环境（environment）、不同集群（cluster）、不同命名空间（namespace）的配置。
![img7](/assets/2022-01-10_10-19-14.jpg)

#### 3种Graphql 技术接入架构

1. Graphql 直连数据库，直连的方式可较少性能消耗
![img8](/assets/1.png)

2. 集成现有服务的GraphQL层
![img9](/assets/2.png)

3. 直连数据库和现有服务的混合模式
![img10](/assets/3.png)

由此可见，Graphql 相比于rest api更适用于如下场景：
- 包括移动端在内的多个客户端
- 正在转向或者已经采用了微服务架构
- 遗留 REST API 数量暴增
- 注重良好的 API 文档和开发者体验等场景下更具有优势

同时，Graphql 不论是服务端还是客户端，都提供了大多数编程语言的支持（C# / .NET 、Clojure 、Elixir 、Erlang 、Go 、Groovy、 Java、 JavaScript、 Julia、 Kotlin、 Perl、 PHP、 Python、 R、 Ruby、 Rust、 Scala、 Swift），可以说不止在开源，而是在建立一种标准。

当前Graphql 已运用到本人所在项目中，可依托大数据沉淀的多纬度数据，将所需数据建立schema后统一到Graphql的单一endpoint下，提供更多数据指标展示给客户。

Graphql并不是要取代REST API，只是提供了一个更好的选择，随着微服务和severless的大规模运用，微服务对服务进行拆分，而Graphql对微服务的接口进行组合并完成鉴权，可充分发挥两者的优势，让系统更加灵活和高效。
