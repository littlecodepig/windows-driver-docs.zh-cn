---
title: WIA \_ IPA \_ 最小 \_ 缓冲区 \_ 大小
description: WIA \_ IPA \_ MIN \_ buffer \_ size 属性指定数据传输中使用的最小缓冲区大小。
keywords:
- WIA_IPA_MIN_BUFFER_SIZE 图像设备
topic_type:
- apiref
api_name:
- WIA_IPA_MIN_BUFFER_SIZE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56329f30bf4b697193403267199b073e4f87b698
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817263"
---
# <a name="wia_ipa_min_buffer_size"></a>WIA \_ IPA \_ 最小 \_ 缓冲区 \_ 大小


WIA \_ IPA \_ MIN \_ buffer \_ size 属性指定数据传输中使用的最小缓冲区大小。

## <span id="ddk_wia_ipa_min_buffer_size_si"></span><span id="DDK_WIA_IPA_MIN_BUFFER_SIZE_SI"></span>


属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

如果通过回调机制执行数据传输，则 WIA \_ IPA \_ MIN \_ BUFFER \_ SIZE 属性值最小可为 64 KB。 但是，如果传输到文件，则属性值是一次传输一页数据所需的字节数。 WIA 微型驱动程序创建并维护此 WIA 属性。

WIA \_ IPA \_ 最小 \_ 缓冲区 \_ 大小与 [**WIA \_ IPA \_ 缓冲区 \_ 大小**](wia-ipa-buffer-size.md) 属性相同。

应用程序可以读取 WIA \_ IPA \_ 最小 \_ 缓冲区 \_ 大小，以确定用于数据传输的驱动程序指定的缓冲区大小。 WIA 服务还会读取此属性，以便在数据传输过程中为微型驱动程序分配内存。

**注意**   WIA \_ IPA \_ MIN \_ BUFFER \_ SIZE 属性包含的值是应用程序可以在任何给定时间请求的最小数据量。 缓冲区的大小越大，对设备的请求就越多。 这种较大的缓冲区大小会使设备显示速度缓慢和无响应，从而降低计算机的整体性能，并可能会消耗过多的资源。 如果缓冲区太小，则可能需要很多较小的请求，从而降低数据传输的性能。 通过考虑对设备的数据请求的典型大小、请求数量以及这些请求的大小，选择合理的缓冲区大小。

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>对于所有启用了传输的项，Windows Vista 驱动程序都可选。 如果实现此属性，则为 Windows Server 2003、Windows XP 和早期版本 Windows 版本编写的应用程序可以估计传输缓冲区大小，因此，传输速率将是最佳的。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ IPA \_ 缓冲区 \_ 大小**](wia-ipa-buffer-size.md)

 

 






