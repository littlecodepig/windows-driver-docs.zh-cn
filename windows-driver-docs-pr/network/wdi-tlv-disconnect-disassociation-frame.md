---
title: WDI_TLV_DISCONNECT_DISASSOCIATION_FRAME
description: WDI_TLV_DISCONNECT_DISASSOCIATION_FRAME 是包含收到的解除
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_DISCONNECT_DISASSOCIATION_FRAME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4d2d636d717dd4fee4270a207a01a8d180f5d0a0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803491"
---
# <a name="wdi_tlv_disconnect_disassociation_frame"></a>WDI \_ TLV \_ 断开解除连接的 \_ \_ 范围


WDI \_ tlv \_ 断开解除连接 \_ \_ 的帧是包含收到的解除连接帧的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x38

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                                                                                              |
|-----------|--------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | UINT8 元素的数组，其中包含所接收到的解除其的解除。 这不包括 802.11 MAC 标头。 |

 

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

 

 




