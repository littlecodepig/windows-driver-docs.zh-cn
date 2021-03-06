---
title: ScannerName 元素
description: 必需的 ScannerName 元素指定扫描程序的管理员分配的用户友好名称。
keywords:
- ScannerName 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScannerName xml lang "..."
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39b91fe81d62c6ff73d00bdccd77c89577958e61
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829585"
---
# <a name="scannername-element"></a>ScannerName 元素


必需的 **ScannerName** 元素指定扫描程序的管理员分配的用户友好名称。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ScannerName xml:lang="..."
  lang = "xs:string">
  text
</wscn:ScannerName xml:lang="...">
```

<a name="attributes"></a>特性
----------

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>类型</th>
<th>必须</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>语言</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p> (可选) 用于标识字符串指定的字符串语言的字符串。<em>字符串</em></p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>文本值
----------

一个字符串，指定扫描程序的用户友好名称。

## <a name="child-elements"></a>子元素


没有任何子元素。

## <a name="parent-elements"></a>父元素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="scannerdescription.md" data-raw-source="[&lt;strong&gt;ScannerDescription&lt;/strong&gt;](scannerdescription.md)"><strong>ScannerDescription</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**ScannerName** 元素的值的配置是特定于实现的;例如，可以通过扫描仪的本地控制台或设备的 web 服务器来配置此值。 如果设备只有一个托管服务，则其易记名称和 **ScannerName** 元素应具有相同的值。 如果设备包含多个托管服务，则 **ScannerName** 应标识扫描仪。

扫描设备可以返回此元素的多个版本，以通过使用 **xml： lang** 特性来支持多种本地化语言。

<a name="examples"></a>示例
--------

下面的代码示例演示如何使用 ScannerName 元素。

```xml
<wscn:ScannerName xml:lang="en-AU, en-CA, en-GB, en-US">
  Accounting Scanner in Copy Room 2
</wscn:ScannerName>
```

## <a name="see-also"></a>请参阅

[**ScannerDescription**](scannerdescription.md)
