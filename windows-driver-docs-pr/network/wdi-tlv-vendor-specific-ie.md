---
title: WDI_TLV_VENDOR_SPECIFIC_IE
description: WDI_TLV_VENDOR_SPECIFIC_IE 是一种 TLV，其中包含供应商特定的列表。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_VENDOR_SPECIFIC_IE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4ee16515f568aeb0a2b7cc8c06f343b4f0d10398
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821951"
---
# <a name="wdi_tlv_vendor_specific_ie"></a>WDI \_ TLV \_ 供应商 \_ 特定 \_ IE


WDI \_ tlv \_ 特定于供应商的 \_ \_ IE 是包含供应商特定的列表。

## <a name="tlv-type"></a>TLV 类型


0x5

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                                        |
|-----------|--------------------------------------------------------------------|
| UINT8\[\] | 指定供应商特定的 UINT8 元素的数组。 |

 

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

 

 




