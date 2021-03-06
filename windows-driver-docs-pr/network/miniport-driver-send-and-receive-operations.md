---
title: 微型端口驱动程序发送和接收操作
description: 微型端口驱动程序发送和接收操作
keywords:
- 微型端口驱动程序 WDK 网络，发送数据
- NDIS 微型端口驱动程序 WDK，发送数据
- 微型端口驱动程序 WDK 网络，接收数据
- NDIS 微型端口驱动程序 WDK，接收数据
- 发送数据 WDK 网络
- 接收数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e33f682184025834fb50c6e68b5e03627514178
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802323"
---
# <a name="miniport-driver-send-and-receive-operations"></a>微型端口驱动程序发送和接收操作





微型端口驱动程序处理来自过量驱动程序的发送请求，并产生接收指示。 在单个函数调用中，NDIS 微型端口驱动程序可以指示链接列表，其中包含多个接收的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构。 微型端口驱动程序可以处理多个网络缓冲区列表结构的列表的发送请求 \_ \_ ，其中每个网络缓冲区列表结构上具有多个 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构 \_ \_ 。

微型端口驱动程序必须管理接收缓冲池。 大多数微型端口驱动程序创建 \_ 使用每个网络 \_ 缓冲区列表结构预分配单个网络缓冲区结构的池 \_ 。

以下主题提供了有关微型端口驱动程序缓冲区管理、发送操作和接收操作的详细信息：

[微型端口驱动程序缓冲区管理](miniport-driver-buffer-management.md)

[从微型端口驱动程序发送数据](sending-data-from-a-miniport-driver.md)

[在微型端口驱动程序中取消发送请求](canceling-a-send-request-in-a-miniport-driver.md)

[指示已从微型端口驱动程序收到数据](indicating-received-data-from-a-miniport-driver.md)

 

