---
date: 2022-04-01
title: "CloudWeGo 助 NextArch 基金会推动标准化建设"
linkTitle: "CloudWeGo 助 NextArch 基金会推动标准化建设"
keywords: ["CloudWeGo", "NextArch", "微服务", "标准化建设"]
description: "CloudWeGo 加入 NextArch 基金会微服务技术小组，推动微服务技术和开源生态的持续发展，针对不同行业和应用场景输出标准化解决方案。"
author: <a href="https://github.com/nextarch" target="_blank">NextArch</a>
---

> 导语：2022 年 3 月，NextArch 基金会正式成立微服务技术小组，致力于推动微服务技术和开源生态的持续发展，根据各个企业在微服务生产实践中遇到的问题，针对不同行业和应用场景输出标准化解决方案，
> 并且联合 PolarisMesh、TARS、go-zero、GoFrame、**[CloudWeGo](https://github.com/cloudwego)** 和 Spring Cloud Tencent 等开源社区提供开箱即用的实现，降低终端用户的使用门槛。
> 来自腾讯、字节跳动、七牛云、快手、BIGO、好未来和蓝色光标等多家企业的技术专家已经加入技术小组，欢迎更多企业和开源社区加入。

2021 年 11 月，Linux 基金会正式成立 NextArch 基金会，共计 40 余家企业或单位联合参与了该基金会的筹建工作，并作为首批共建和支持单位加入，目前已增至 53 家企业。NextArch 基金会致力于在异构基础设施、多元化技术栈和混合云场景下的构建下一代技术架构，始终秉承一个开放中立的治理模式，发展适合企业数字化转型的开源生态。

微服务是下一代架构的关键部分，越来越多企业采用微服务架构。市场调研表明，随着企业数字化转型持续深入，2023 年微服务云市场的规模达到 18.8 亿美元，从 2018 到 2023 年的复合年增长率达到 22.4%。众所周知，微服务相比于传统架构具有诸多优势，但是，我们在微服务实施的各个环节中都可能面临问题。

为了降低微服务架构的落地成本，来自腾讯、快手、字节跳动、好未来、七牛云和蓝色光标等多家企业的技术专家在 NextArch 基金会成立微服务技术小组，共同探讨各自企业在微服务领域中遇到的问题，分享大家在生产过程中的实践经验，并且面向不同的应用场景和终端用户，联合相关开源社区输出标准化的解决方案。

![image](/img/blog/CloudWeGo_helps_NextArch/community.png)

在采用微服务架构之前，我们需要思考为什么采用微服务架构，并不是所有的开发团队和发展阶段都适合采用微服务架构。通常，采用微服务架构可以解决以下问题：首先，开发团队具有一定的规模，所有成员共同开发一个单体应用的内耗太高，如果采用微服务架构，每个服务可以由单个或者少数成员独立负责。第二，业务系统的功能模块很多，耦合在一起会增加测试和部署的成本，任何一个模块故障也会导致整个系统故障。第三，功能模块之间的负载无法隔离，容易互相影响，没有办法针对热点模块的计算层或者存储层进行扩容。

如果我们采用微服务架构，单个服务是⾮常简单的，但是，分布式服务之间的功能调用远⽐单体应用内部更加复杂。在单体应用中，⼀个函数可以调⽤其他任何一个公共函数。在微服务架构中，一个函数只可以调⽤同⼀个微服务的函数。如何实现分布式服务之间的通信是微服务架构的首要问题，构建高性能、高可用的远程调用能力并不容易。值得庆幸的是，已经有 grpc、thrift、tars、go-zero、GoFrame、[cloudwego/kitex](https://github.com/cloudwego/kitex) 和 spring cloud 等大量开源的分布式服务开发框架，这些框架可以帮助终端用户快速地构建微服务。不幸的是，仅仅把服务开发出来并且跑通是不够的，保障大规模服务的稳定运营还需要考虑诸多问题，例如：在分布式架构中如何处理基础设施以及应用层的各种异常、如何实现大规模服务的无损发布和流量调度，如何定位和分析复杂调用链路中出现的问题等。对于中大型企业来说，还存在异构的开发技术栈和运行时环境，存在跨地域和混合云的架构要求，如何在更加复杂的应用场景中解决上述问题，面临更多的挑战。

目前，这个方向还没有开箱即用的解决方案，终端用户必须在不同的基础设施和适当的工具之间做出抉择，才能解决各种问题。近日，NextArch 微服务技术小组向基金会提交了首个提案，根据各自企业在分布式或者微服务生产实践中的经验和痛点，面向多语言、多框架和异构基础设施，针对不同行业和应用场景输出微服务落地的标准化方案，并且依托相关开源社区提供推荐实现，方便终端用户落地。我们也期待更多企业和开源社区加入 NextArch 基金会，共同探讨分布式或者微服务治理的标准化方案。

![image](/img/blog/CloudWeGo_helps_NextArch/framework.png)

### 部分 NextArch Microservice SIG 成员引文：

**PolarisMesh 单家骏**

腾讯云专家工程师，具备 10 年以上中间件研发经验。北极星开源社区（PolarisMesh）联合发起人，负责开源项目的技术规划、代码开发和社区运营等工作。

自分布式架构发展至今，微服务成为了复杂业务系统的首选模式，在企业得到了充分的生产落地，然而各个微服务框架及工具链，对于微服务治理体系的理解存在差异性，使得业务系统在实现微服务治理上存在较大的成本，同时也不利于微服务技术的沉淀及长期发展。北极星是腾讯自研和开源的微服务治理框架，覆盖了腾讯内部 90% 以上的业务，解决了业务系统因多语言、多框架以及业务差异性所带来的服务治理不一致的问题，在腾讯内部完成了服务发现和治理的标准化。我们期望通过加入 NextArch 基金会这样一个中立组织，可以讨论业界微服务治理的相关实践及解决方案，沉淀出标准化的服务治理体系，促进微服务生态的进一步发展，也期望北极星开源社区可以推动并承载微服务治理标准体系的落地。

**go-zero 万俊峰**

万俊峰，七牛云技术副总裁，go-zero 开源社区/go-zero 作者。负责 go-zero 框架的规划、代码编写、代码 review、工具链规划、社区建设、开源推广

微服务在发展了这么多年之后，已经呈现出百花齐放的状态，各种微服务框架和治理能力在很多公司都得到了充分的落地，并带来了巨大的业务价值。但当前的现状也没有形成足够的技术共识和规范，我们需要进一步提炼和抽象微服务的能力，并加以标准化。这样可以更好的沉淀经验，并将各语言的微服务框架提供规划化对接，从而推动微服务技术的进一步发展。同时也期望在 SIG 组织能够更多的讨论微服务落地的各种最佳实践，也期望能够通过 go-zero 开源社区帮助推动共识的微服务治理标准落地。

**GoFrame 郭强**

腾讯高级工程师，GoFrame 开源框架项目发起人及主要贡献者，负责 GoFrame 框架发展规划、社区建设维护、核心代码开发。GoFrame 是一款模块化、高性能、企业级的 Go 基础开发框架。

微服务是一种架构设计思想，目的是为了有效解决业务复杂度提高带来的项目架构问题。微服务需要解决的不仅是技术问题，也是项目协作问题。在"微服务化"过后，项目架构将引入更多的痛点：职责边界界定、服务高效通信、分布事务处理、微服务化治理、服务版本管理、项目迭代协作等等。微服务思想发展至今，这些痛点的解决方案已比较成熟，并且大同小异。NextArch 微服务 SIG 需要做的是在这些方案之上分析共性之处，形成统一化和规范化的解决方案。以帮助企业更快速地实现微服务化，同时，也需要提供一些最佳实践，帮助企业提高在服务化后的项目管理手段。80% 的解决方案抽象，20% 的最佳实践沉淀。

**CloudWeGo 罗广明**

字节跳动微服务架构师，CloudWeGo 开源负责人。CloudWeGo 是一套由字节跳动开源的、可快速构建企业级云原生架构的中间件集合，专注于解决微服务通信与治理的难题，具备高性能、可扩展、高可靠的特点。

微服务技术发展至今，业界涌现出一大批微服务开发框架、技术和最佳实践。这个多样化是不可避免的，没有一个微服务开发框架能够统一所有的语言，但是微服务架构里面所涉及的服务治理体系，却可以做到统一和规范化。NextArch 微服务 SIG 正是在这样的背景下诞生了，旨在提供统一服务治理体系，解决共性问题，将促进微服务框架和技术的进一步演进和发展。
