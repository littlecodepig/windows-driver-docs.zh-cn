---
title: 用于 head 装载和专用监视器的 EDID 扩展
description: 用于 head 装载和专用监视器的 EDID 扩展
keywords:
- 显示设备 WDK
- 监视驱动程序 WDK
- 显示驱动程序 WDK，监视驱动程序
- monitors
- HMD
- 虚拟现实
ms.date: 11/30/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: 9f4abfd4477a41bdb80375a369430350a5ad3ed0
ms.sourcegitcommit: abe7fe9f3fbee8d12641433eeab623a4148ffed3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92185168"
---
# <a name="edid-extension-for-head-mounted-and-specialized-monitors"></a>用于 head 装载和专用监视器的 EDID 扩展

本页为显示制造商提供了有关如何在 HMD (Head 装入显示) 或专用显示固件中实现 [EDID](https://en.wikipedia.org/wiki/Extended_Display_Identification_Data) CTA (使用者技术) 关联的指南，使 windows 可以将显示器识别为特别显示，从而使 windows OS 中的每一层都可以正确地处理它们。 术语 "显示" 和 "监视器" 是同义词。

如果没有此 EDID 扩展，HMDs 和专用显示器会出现以下问题：

* Windows 桌面将扩展到显示屏上，应用可以启动，而鼠标光标可以漫游到显示器上。 如果用户不希望这样做，则从该状态恢复可能会令人感到困惑。
* 第三方排序器必须使用基于 HWND 或基于 CoreWindow 的演示 Api，这不允许独占访问显示。 Windows 桌面组合器负责将有窗口的演示 Api 路由到显示，在某些情况下可能会产生额外的非确定性延迟。

本文档中的规范需要两部分来解决上述问题：

1. 显示中包含 [EDID](https://en.wikipedia.org/wiki/Extended_Display_Identification_Data) 的固件将被修改为包含 [特定于供应商的数据块](https://en.wikipedia.org/wiki/Extended_Display_Identification_Data#EIA.2FCEA-861_extension_block) ，以标识显示的特定于 Windows 的用例。
2. Windows 显示子系统将正确识别此文档中所述的特定于供应商的数据块，并适当地处理显示。 请注意，不同版本的 Windows 操作系统可能具有不同的行为，如下所示。

1的组合。 和第 2 步 以上将从显示器第一次插入的那一刻起，产生正确的 Windows 行为。 特别是，HMDs 和某些专用显示器不会包含在常规的 Windows 桌面环境中，并可使用 [Windows. display. Core](/uwp/api/windows.devices.display.core) api 访问显示。

视频电子标准关联 (VESA) 已在 DisplayId v2.0 中定义标准化字段，该字段提供了与本文档中定义的 VSDB 相同的信息的访问权限。  DisplayID v2.0 或更高版本是为 HMDs 传递此数据的首选机制，但是，如果设备由于其他原因必须使用 EDID，则应使用此 VSDB。

## <a name="vendor-specific-data-block-vsdb"></a>特定于供应商的数据块 (VSDB) 

负责写入包含 EDID 的固件代码的参与方必须包含 CTA extension 块，并将 Microsoft 定义的供应商特定数据块 (VSDB) 中。  ([E-EDID](https://vesa.org/standards-specifications/)) 中介绍了 "EDID 的 VESA 增强的扩展显示识别数据标准" 中所述的结构，请参阅版本1.4，版本 A，修订版本2，其中第2.2 节描述了扩展块。  CTA 扩展块在 CTA 的861系列文档中定义，这是一个用于未压缩 High-Speed 数字接口的 DTV 配置文件。  VSDBs 在 [ANSI/CTA-861-G](https://webstore.ansi.org/Standards/ANSI/CTA8612016ANSI) 中进行了介绍，其中包括 VSDB 相对于其他数据块的顺序。

VSDB 结构必须包含下表中所述的格式和值。

![VSDB 规范](images/specialized-displays-vsdb.png)

### <a name="vendor-specific-tag-code-3-bits"></a>供应商特定标记代码 [3 位]

此字段必须设置为 `0x3` 。

### <a name="length-5-bits"></a>长度 [5 位]

数据块的总长度，不包括此字节。  此字段必须设置为 `0x15` 。

### <a name="ieee-oui-3-bytes"></a>IEEE OUI [3 个字节]

用于标识显示的 IEEE 组织唯一标识符 (OUI) 分配给 Microsoft，用于标识显示：按 `0x5C` `0x12` `0xCA` 顺序字节顺序。

### <a name="version-1-byte"></a>版本 [1 字节]

与 Microsoft 显示供应商特定数据块的内容关联的版本号。

| 建议 Use-Case | 版本 | 支持的 Windows 版本 |
|----------------------|---------|---------------------------|
| HMD (VR/AR) 显示将由 Windows Mixed Reality 体验使用的设备 | `0x1` | 在 Windows 10 创建者的更新和更高版本中受支持 |
| HMD (VR/AR) 显示第三方排序器 (的设备，而不是 Windows Mixed Reality 体验)  | `0x2` | Windows 10 十月2018更新及更高版本中受支持 |
| 不 HMDs 的专用显示设备 | `0x3` | 在下一 Windows vNext 和更高版本中受支持 |

### <a name="desktop-usage-flag-1-bit"></a>桌面使用标志 [1 位]

在 `0x3` 此 VSDB 的版本和更高版本中，此位指示显示是否应为桌面的一部分。

* 如果显示应为桌面的一部分，则应将其设置为 `0x1` 。
* 如果显示不应是桌面的一部分，则应将其设置为 `0x0` 。

在 `0x1` `0x2` 此 VSDB 的版本和中，此值应始终设置为 `0x0` 。

### <a name="third-party-usage-flag-1-bit"></a>第三方使用标志 [1 位]

在 `0x3` 此 VSDB 的版本和更高版本中，此位指示显示应可由第三方排序器使用，还是仅供 Microsoft 提供的 Windows 合成器使用。

* 如果显示应由非 Windows software 排序器使用，则应将其设置为 `0x1` 。
* 如果显示应仅由 Windows 合成器使用，则应将其设置为 `0x0` 。

在 `0x1` `0x2` 此 VSDB 的版本和中，此值应始终设置为 `0x0` 。

### <a name="display-product-primary-use-case-5-bits"></a>显示产品的主要用例 [5 位]

显示设备的主要用例：

* 测试设备- `0x1`
* 一般显示- `0x2`
* 电视显示器- `0x3`
* 桌面生产力显示- `0x4`
* 桌面游戏显示器- `0x5`
* 演示显示- `0x6`
* 虚拟现实耳机- `0x7`
* 扩充的现实- `0x8`
* 视频墙壁显示- `0x10`
* 医疗图像显示- `0x11`
* 专用游戏显示器- `0x12`
* 专用视频监视器显示器- `0x13`
* 附件显示- `0x14`

### <a name="container-id-16-bytes"></a>容器 ID [16 字节]

每个设备独有的16字节全局唯一标识符。 这是在工厂地面上烧录的标识符。

## <a name="remarks"></a>备注

请注意，为了保持与早期操作系统的最大兼容性，建议 HMDs 继续使用版本 `0x1` 和 `0x2` 此 EDID 扩展。 有关要用于 HMDs 的值，请参阅上一节。
