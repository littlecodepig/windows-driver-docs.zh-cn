---
title: DEVPKEY_DeviceClass_NoDisplayClass
description: DEVPKEY_DeviceClass_NoDisplayClass
ms.assetid: b604c201-c6db-491f-bd7a-ae097249e98a
keywords:
- DEVPKEY_DeviceClass_NoDisplayClass 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_NoDisplayClass
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e4d8155ddb5b80cb869905938217a73007df1c2e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576894"
---
# <a name="devpkeydeviceclassnodisplayclass"></a>DEVPKEY_DeviceClass_NoDisplayClass


DEVPKEY_DeviceClass_NoDisplayClass 设备属性表示一个布尔值标志，用于控制是否在设备[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)显示设备管理器。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_NoDisplayClass</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>相应的注册表值名称</strong></p></td>
<td align="left"><p><strong>NoDisplayClass</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果 DEVPKEY_DeviceClass_NoDisplayClass 的值设置为 DEVPROP_TRUE，设备管理器不显示在设备安装程序类中的设备。 如果此值未设置为 DEVPROP_TRUE，设备管理器中的设备安装程序类会显示设备。

**NoDisplayClass**可以设置注册表值以查找设备安装程序类[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)包含在[ **INFClassInstall32 部分**](https://msdn.microsoft.com/library/windows/hardware/ff546335)的安装类的 INF 文件。

您可以调用[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)或[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090)检索 DEVPKEY_DeviceClass_ 值NoDisplayClass。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_DeviceClass_NoDisplayClass 属性键。 可以通过访问对应访问此属性的值**NoDisplayClass**类注册表项下的注册表值。 有关如何对访问类注册表项下的值项的信息，请参阅[访问注册表项值下类注册表项](https://msdn.microsoft.com/library/windows/hardware/ff537751)。

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
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)

[**INF ClassInstall32 部分**](https://msdn.microsoft.com/library/windows/hardware/ff546335)

[**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

[**SetupDiGetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff551090)

 

 





