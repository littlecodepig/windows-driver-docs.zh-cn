---
title: '\_DXGKARG \_ MOVEPAGEDIRECTORY 结构'
description: DXGKARG \_ MOVEPAGEDIRECTORY 结构保留供系统使用。 不要在您的驱动程序中使用它。
keywords:
- _DXGKARG_MOVEPAGEDIRECTORY 结构显示设备
- DXGKARG_MOVEPAGEDIRECTORY 结构显示设备
topic_type:
- apiref
api_name:
- DXGKARG_MOVEPAGEDIRECTORY
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: d37111c82a69b59cb0d32f13d48e4c90818625c3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808971"
---
# <a name="_dxgkarg_movepagedirectory-structure"></a>\_DXGKARG \_ MOVEPAGEDIRECTORY 结构


DXGKARG \_ MOVEPAGEDIRECTORY 结构保留供系统使用。 不要在您的驱动程序中使用它。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGKARG_MOVEPAGEDIRECTORY {
  PVOID            pPageDirectory;
  PHYSICAL_ADDRESS PhysicalAddress;
  UINT             Segment;
  UINT             SizeInPages;
} DXGKARG_MOVEPAGEDIRECTORY;
```

<a name="members"></a>成员
-------

**pPageDirectory** 保留供系统使用。

**PhysicalAddress** 保留供系统使用。

**段** 保留供系统使用。

**SizeInPages** 保留供系统使用。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 windows 7 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">D3dkmddi (包含 D3dkmddi) </td>
</tr>
</tbody>
</table>

 

 





