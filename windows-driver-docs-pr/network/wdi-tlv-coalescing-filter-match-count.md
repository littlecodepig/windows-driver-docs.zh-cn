---
title: WDI_TLV_COALESCING_FILTER_MATCH_COUNT
description: WDI_TLV_COALESCING_FILTER_MATCH_COUNT 是一种 TLV，其中包含与网络端口上的接收筛选器匹配的数据包数。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_COALESCING_FILTER_MATCH_COUNT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 58e380fced9ebc16fbb6be957cfc9656b93c9108
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791335"
---
# <a name="wdi_tlv_coalescing_filter_match_count"></a>WDI \_ TLV \_ 合并 \_ 筛选器 \_ 匹配 \_ 计数


WDI \_ tlv \_ 合并 \_ 筛选器 \_ 匹配 \_ 计数是一个 TLV，其中包含与网络端口上的接收筛选器匹配的数据包数。

## <a name="tlv-type"></a>TLV 类型


0x66

## <a name="length"></a>长度


UINT64) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 描述                                                                  |
|--------|------------------------------------------------------------------------------|
| UINT64 | 与网络端口上的接收筛选器匹配的数据包数。 |

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




