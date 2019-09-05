---
title: 使用 DDD 和 CQRS 模式降低微服务中的业务复杂性
description: 容器化 .NET 应用程序的 .NET 微服务体系结构 | 了解如何应用 DDD 和 CQRS 模式来处理复杂的业务场景
ms.date: 10/08/2018
ms.openlocfilehash: d311641e2ac73205c04c3f1147b54991585ce851
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2019
ms.locfileid: "70295101"
---
# <a name="tackle-business-complexity-in-a-microservice-with-ddd-and-cqrs-patterns"></a><span data-ttu-id="7868e-103">使用 DDD 和 CQRS 模式降低微服务中的业务复杂性</span><span class="sxs-lookup"><span data-stu-id="7868e-103">Tackle Business Complexity in a Microservice with DDD and CQRS Patterns</span></span>

<span data-ttu-id="7868e-104">为每个微服务或反映对业务域理解的绑定上下文设计域模型。 </span><span class="sxs-lookup"><span data-stu-id="7868e-104">*Design a domain model for each microservice or Bounded Context that reflects understanding of the business domain.*</span></span>

<span data-ttu-id="7868e-105">本节重点介绍在需要降低子系统复杂性时实现的更高级的微服务，或按不断变化的业务规则派生自域专家知识的微服务。</span><span class="sxs-lookup"><span data-stu-id="7868e-105">This section focuses on more advanced microservices that you implement when you need to tackle complex subsystems, or microservices derived from the knowledge of domain experts with ever-changing business rules.</span></span> <span data-ttu-id="7868e-106">本节中使用的体系结构模式基于域驱动的设计 (DDD) 以及命令和查询责任分离 (CQRS) 方法，如图 7-1 中所示。</span><span class="sxs-lookup"><span data-stu-id="7868e-106">The architecture patterns used in this section are based on domain-driven design (DDD) and Command and Query Responsibility Segregation (CQRS) approaches, as illustrated in Figure 7-1.</span></span>

![外部体系结构（微服务模式、API 网关、弹性通信、发布/订阅等）和内部体系结构（数据驱动/CRUD、DDD 模式、依赖关系注入、多个库等）之间的区别。](./media/image1.png)

<span data-ttu-id="7868e-108">图 7-1  。</span><span class="sxs-lookup"><span data-stu-id="7868e-108">**Figure 7-1**.</span></span> <span data-ttu-id="7868e-109">外部微服务体系结构与每个微服务的内部体系结构模式</span><span class="sxs-lookup"><span data-stu-id="7868e-109">External microservice architecture versus internal architecture patterns for each microservice</span></span>

<span data-ttu-id="7868e-110">但是，大部分用于数据驱动微服务的技术（例如如何实现 ASP.NET Core Web API 服务或如何公开具有 Swashbuckle 或 NSwag 的 Swagger 元数据）同样适用于使用 DDD 模式在内部实现的更高级的微服务。</span><span class="sxs-lookup"><span data-stu-id="7868e-110">However, most of the techniques for data driven microservices, such as how to implement an ASP.NET Core Web API service or how to expose Swagger metadata with Swashbuckle or NSwag, are also applicable to the more advanced microservices implemented internally with DDD patterns.</span></span> <span data-ttu-id="7868e-111">本节是前几节内容的扩展，因为之前所述的大部分做法也适用于此处或任何类型的微服务。</span><span class="sxs-lookup"><span data-stu-id="7868e-111">This section is an extension of the previous sections, because most of the practices explained earlier also apply here or for any kind of microservice.</span></span>

<span data-ttu-id="7868e-112">本节首先提供有关用于 eShopOnContainers 引用应用程序的简化 CQRS 模式的详细信息。</span><span class="sxs-lookup"><span data-stu-id="7868e-112">This section first provides details on the simplified CQRS patterns used in the eShopOnContainers reference application.</span></span> <span data-ttu-id="7868e-113">之后，将概述 DDD 技术，使你能够找到可在应用程序中重用的常见模式。</span><span class="sxs-lookup"><span data-stu-id="7868e-113">Later, you will get an overview of the DDD techniques that enable you to find common patterns that you can reuse in your applications.</span></span>

<span data-ttu-id="7868e-114">DDD 是一个大主题，具有一套丰富的学习资源。</span><span class="sxs-lookup"><span data-stu-id="7868e-114">DDD is a large topic with a rich set of resources for learning.</span></span> <span data-ttu-id="7868e-115">开始时可以阅读 Eric Evans 撰写的[《域驱动设计》](https://domainlanguage.com/ddd/)等此类书籍，以及 Vaughn Vernon、Jimmy Nilsson、Greg Young、Udi Dahan、Jimmy Bogard 和许多其他 DDD/CQRS 专家撰写的其他资料。</span><span class="sxs-lookup"><span data-stu-id="7868e-115">You can start with books like [Domain-Driven Design](https://domainlanguage.com/ddd/) by Eric Evans and additional materials from Vaughn Vernon, Jimmy Nilsson, Greg Young, Udi Dahan, Jimmy Bogard, and many other DDD/CQRS experts.</span></span> <span data-ttu-id="7868e-116">但最重要的是需要尝试了解如何与具体业务域中的专家配合，从对话、白板和域建模会话应用 DDD 技术。</span><span class="sxs-lookup"><span data-stu-id="7868e-116">But most of all you need to try to learn how to apply DDD techniques from the conversations, whiteboarding, and domain modeling sessions with the experts in your concrete business domain.</span></span>

#### <a name="additional-resources"></a><span data-ttu-id="7868e-117">其他资源</span><span class="sxs-lookup"><span data-stu-id="7868e-117">Additional resources</span></span>

##### <a name="ddd-domain-driven-design"></a><span data-ttu-id="7868e-118">DDD（域驱动设计）</span><span class="sxs-lookup"><span data-stu-id="7868e-118">DDD (Domain-Driven Design)</span></span>

- <span data-ttu-id="7868e-119">**Eric Evans。域语言** </span><span class="sxs-lookup"><span data-stu-id="7868e-119">**Eric Evans. Domain Language** </span></span>\
  <https://domainlanguage.com/>

- <span data-ttu-id="7868e-120">**Martin Fowler。域驱动设计** </span><span class="sxs-lookup"><span data-stu-id="7868e-120">**Martin Fowler. Domain-Driven Design** </span></span>\
  <https://martinfowler.com/tags/domain%20driven%20design.html>

- <span data-ttu-id="7868e-121">**Jimmy Bogard。强化域：入门** </span><span class="sxs-lookup"><span data-stu-id="7868e-121">**Jimmy Bogard. Strengthening your domain: a primer** </span></span>\
  <https://lostechies.com/jimmybogard/2010/02/04/strengthening-your-domain-a-primer/>

##### <a name="ddd-books"></a><span data-ttu-id="7868e-122">DDD 丛书</span><span class="sxs-lookup"><span data-stu-id="7868e-122">DDD books</span></span>

- <span data-ttu-id="7868e-123">**Eric Evans。Domain-Driven Design:软件核心复杂性应对之道** </span><span class="sxs-lookup"><span data-stu-id="7868e-123">**Eric Evans. Domain-Driven Design: Tackling Complexity in the Heart of Software** </span></span>\
  <https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/>

- <span data-ttu-id="7868e-124">**Eric Evans。域驱动设计参考：定义和模式摘要** </span><span class="sxs-lookup"><span data-stu-id="7868e-124">**Eric Evans. Domain-Driven Design Reference: Definitions and Pattern Summaries** </span></span>\
  <https://www.amazon.com/Domain-Driven-Design-Reference-Definitions-2014-09-22/dp/B01N8YB4ZO/>

- <span data-ttu-id="7868e-125">**Vaughn Vernon。实现域驱动设计** </span><span class="sxs-lookup"><span data-stu-id="7868e-125">**Vaughn Vernon. Implementing Domain-Driven Design** </span></span>\
  <https://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577/>

- <span data-ttu-id="7868e-126">**Vaughn Vernon。域驱动设计核心理念** </span><span class="sxs-lookup"><span data-stu-id="7868e-126">**Vaughn Vernon. Domain-Driven Design Distilled** </span></span>\
  <https://www.amazon.com/Domain-Driven-Design-Distilled-Vaughn-Vernon/dp/0134434420/>

- <span data-ttu-id="7868e-127">**Jimmy Nilsson。应用域驱动设计和模式** </span><span class="sxs-lookup"><span data-stu-id="7868e-127">**Jimmy Nilsson. Applying Domain-Driven Design and Patterns** </span></span>\
  <https://www.amazon.com/Applying-Domain-Driven-Design-Patterns-Examples/dp/0321268202/>

- <span data-ttu-id="7868e-128">**Cesar de la Torre。使用 .NET 的 N 层域导向体系结构指南** </span><span class="sxs-lookup"><span data-stu-id="7868e-128">**Cesar de la Torre. N-Layered Domain-Oriented Architecture Guide with .NET** </span></span>\
  <https://www.amazon.com/N-Layered-Domain-Oriented-Architecture-Guide-NET/dp/8493903612/>

- <span data-ttu-id="7868e-129">**Abel Avram 与 Floyd Marinescu。快速完成域驱动设计** </span><span class="sxs-lookup"><span data-stu-id="7868e-129">**Abel Avram and Floyd Marinescu. Domain-Driven Design Quickly** </span></span>\
  <https://www.amazon.com/Domain-Driven-Design-Quickly-Abel-Avram/dp/1411609255/>

- <span data-ttu-id="7868e-130">**Scott Millett，Nick Tune - 域驱动设计的模式、原则和实践** </span><span class="sxs-lookup"><span data-stu-id="7868e-130">**Scott Millett, Nick Tune - Patterns, Principles, and Practices of Domain-Driven Design** </span></span>\
  <http://www.wrox.com/WileyCDA/WroxTitle/Patterns-Principles-and-Practices-of-Domain-Driven-Design.productCd-1118714709.html>

##### <a name="ddd-training"></a><span data-ttu-id="7868e-131">DDD 培训</span><span class="sxs-lookup"><span data-stu-id="7868e-131">DDD training</span></span>

- <span data-ttu-id="7868e-132">**Julie Lerman 与 Steve Smith。域驱动设计基础知识** </span><span class="sxs-lookup"><span data-stu-id="7868e-132">**Julie Lerman and Steve Smith. Domain-Driven Design Fundamentals** </span></span>\
  <https://bit.ly/PS-DDD>

>[!div class="step-by-step"]
><span data-ttu-id="7868e-133">[上一页](../multi-container-microservice-net-applications/implement-api-gateways-with-ocelot.md)
>[下一页](apply-simplified-microservice-cqrs-ddd-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="7868e-133">[Previous](../multi-container-microservice-net-applications/implement-api-gateways-with-ocelot.md)
[Next](apply-simplified-microservice-cqrs-ddd-patterns.md)</span></span>