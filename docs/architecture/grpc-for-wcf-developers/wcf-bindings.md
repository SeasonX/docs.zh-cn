---
title: Wcf 绑定和传输-适用于 WCF 开发人员的 gRPC
description: 了解不同的 WCF 绑定和传输如何与 gRPC 进行比较。
ms.date: 09/02/2019
ms.openlocfilehash: ebe324eace8f5f418b920c59f6d72eaaa686ef02
ms.sourcegitcommit: f38e527623883b92010cf4760246203073e12898
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77503352"
---
# <a name="wcf-bindings-and-transports"></a>WCF 绑定和传输

Windows Communication Foundation （WCF）具有指定不同网络协议、传输格式和其他实现详细信息的内置*绑定*。 gRPC 实际上只有一个网络协议和一种网络格式。 （从技术上讲，你*可以*自定义网络格式，但这超出了本书的范围。）在大多数情况下，你可能会发现 gRPC 提供了最佳解决方案。 

下面是有关最相关的 WCF 绑定的简短讨论，以及它们如何与 gRPC 中的等效项进行比较。

## <a name="nettcp"></a>Wcf-nettcp

WCF 的 Wcf-nettcp 绑定允许永久性连接、小消息和双向消息传递。 但它仅适用于 .NET 客户端和服务器。 gRPC 允许相同的功能，但跨多个编程语言和平台支持。 

gRPC 具有 WCF 的 Wcf-nettcp 绑定的许多功能，但并不总是以相同的方式实现。 例如，在 WCF 中，通过配置控制加密，并在框架中进行处理。 在 gRPC 中，通过 TLS 上的 HTTP/2 在连接级别实现加密。

## <a name="http"></a>HTTP

调用 BasicHttpBinding 的 WCF 绑定通常基于文本，并使用 SOAP 作为网络格式。 与 Wcf-nettcp 绑定相比，此方法更慢。 它通常用于提供跨平台的互操作性或通过 internet 基础结构进行连接。 

GRPC 中的等效项使用 HTTP/2 作为消息的二进制 Protobuf 线路格式的基础传输层。 因此，它可以在 Wcf-nettcp 服务级别提供性能，并通过所有新式编程语言和框架实现跨平台完全互操作性。

## <a name="named-pipes"></a>Named pipes

WCF 提供了一个*命名管道*绑定，用于在同一物理计算机上的进程之间进行通信。 ASP.NET Core gRPC 的第一个版本不支持命名管道。 为命名管道（和 Unix 域套接字）添加客户端和服务器支持是将来版本的目标。

## <a name="msmq"></a>MSMQ

MSMQ 是专有的 Windows 消息队列。 通过 WCF 绑定到 MSMQ，可以在将来随时处理的客户端发出 "火灾" 和 "忘记" 请求。 gRPC 本身不提供任何消息队列功能。 

最佳的替代方法是直接使用消息传递系统，如 Azure 服务总线、RabbitMQ 或 Kafka。 可以通过将消息直接放入队列的客户端实现此，也可以使用 gRPC 客户端流式处理服务（排队消息）来实现。

## <a name="webhttpbinding"></a>WebHttpBinding

WebHttpBinding （也称为 WCF REST），具有 `WebGet` 和 `WebInvoke` 属性，使你能够开发 RESTful Api，在这种情况不太常见的情况下，可能会说出 JSON。 如果有使用 WCF REST 生成的 RESTful API，请考虑将其迁移到常规 ASP.NET Core MVC Web API 应用程序。 此迁移将提供与转换为 gRPC 相同的功能。

>[!div class="step-by-step"]
>[上一页](wcf-endpoints-grpc-methods.md)
>[下一页](rpc-types.md)
