---
title: 移动计划 Web 门户
description: 本主题介绍 Mobile plan 计划的实现步骤。
keywords:
- Windows Mobile 计划 Web 门户，移动计划实现移动运营商
ms.date: 03/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 43035c0ca0d3b7fce550ef3f7b136118af924aee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832929"
---
# <a name="mobile-operator-web-portal"></a>移动运营商 Web 门户

## <a name="overview"></a>概述

本主题介绍了 web 门户，该门户使移动运营商可以通过移动计划应用中托管的特选 web 体验直接向 Windows 用户提供连接解决方案。 移动运营商必须遵循这些设计原则来创建其 web 体验，以确保用户在导航门户时具有优质的体验。 移动运营商 web 门户用于移动计划解决方案中支持的所有方案，因此，它是程序中最重要的组件之一。

有关 web 门户流和引用设计的详细信息，请参阅 [web 门户流和引用设计](mobile-plans-appendix.md#web-portal-flow-and-reference-design)。

## <a name="web-portal-interface-for-esim-enabled-devices"></a>启用了 eSIM 的设备的 Web 门户接口

移动计划应用使用 [Web 视图](/uwp/api/Windows.UI.Xaml.Controls.WebView) 控件来承载和提供移动运营商 web 门户体验。 门户由直接调用移动运营商托管的服务终结点的应用程序调用，返回的内容直接呈现在控件中

当启动时 `WebView` ，会将多个参数作为调用的一部分传递到门户。 如果至少有一个 eSIM 配置文件与移动运营商关联，还会将 *iccid* 传递到门户。

下面的示例显示了在对的调用中嵌入的已启用 eSIM 功能的设备的启动参数 `MyWebView.Navigate()` 。

```C#
MyWebView.ScriptNotify += MyWebView_ScriptNotify;

List<Uri> allowedUris = new List<Uri>();

allowedUris.AddRange(AllowedNotifyUris);

MyWebView.AllowedScriptNotifyUris = allowedUris;

MyWebView.Navigate(“https://moportal.com?market=US&location=US&transactionId=%2F7RBTuSJt02OZbX8.4&eid=89033023422130000000000199055797&imei=001102000315468&iccids=8988247000101867183,8988247000103824828”);
```

为了提供与应用程序更新的向后兼容性，门户必须忽略还可能在请求中传递的任何其他参数。 这可确保在应用中引入新功能的灵活性和能力，而不会中断移动运营商的集成。

下表介绍了适用于 eSIM 的启动参数。

| 参数名称 | 说明 | 示例  |
| --- | --- | --- |
| eid            | ESIM 标识符。 仅当存在 eSIM 时才发送此。                                                                                                                            | `eid= 89033024010400000100000000009136`          |
| iccid         | 可选参数。 指定仅来自 eSIM 的可用配置文件的 Iccid 列表。 如果没有匹配 eSIM 上可用的 MO 的 Iccid，则不会发送此参数。 | `iccids=8988247000100003319, 988247000100003555` |
| imei           | 设备的 IMEI 号码。                                                                                                                                                                | `imei=001201234567890`                           |
| location       | 具有国家/地区级别粒度的用户的当前物理位置。                                                                                                                    | `location=us`                                    |
| transactionId  | 用于调试会话的事务 ID。 提供程序应记录此项并将其发送到通知负载。 最大大小为64个字符。                                     | `transactionId=waoigFfX00yGH3Vb.1`               |
| market         | PC 中区域设置的双字母 ISO 代码。                                                                                                                                | `market=us`                                      |

用户的语言首选项使用下表中所述的 Accept-Language 标头进行发送。

| 标头名称     | 描述  | 示例 |
| --- | --- | --- |
| Accept-Language | 用户的当前语言设置。 如果可能，MO 门户应以指定的语言呈现内容。 有关详细信息，请参阅 [RFC 7231 5.3.5： Accept-Language 部分](https://tools.ietf.org/html/rfc7231#section-5.3.5)。 | `Accept-Language: en-us` |

## <a name="web-portal-interface-for-physical-sims"></a>适用于物理 Sim 的 Web 门户接口

使用旧的物理 UICC 调用移动运营商门户的接口与 eSIM 的接口相同。 但是，传递到门户的参数是不同的。

```C#
MyWebView.Navigate(“https://moportal.com?iccid=8988247000100003319&imei=001102000311608&market=us&transactionId=waoigFfX00yGH3Vb.1&location=us”);
```
下表介绍了可用于物理 SIM 的启动参数。

| 参数名称 | 说明                                                                                                                                                                              | 示例                                          |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| iccid          | 物理 SIM 的必需参数。 指定物理 sim 上的 ICCID。                                                                                                          | `iccid=8988247000100003319`                      |
| imei           | 设备的 IMEI 号码。                                                                                                                                                                | `imei=001201234567890`                           |
| location       | 具有国家/地区级别粒度的用户的当前物理位置。                                                                                                                    | `location=us`                                    |
| transactionId  | 用于调试会话的事务 ID。 提供程序应记录此项并将其发送到通知负载。 最大大小为64个字符。                                     | `transactionId=waoigFfX00yGH3Vb.1`               |
| market         | PC 中区域设置的双字母 ISO 代码。                                                                                                                                | `market=us`                                      |

用户的语言首选项使用下表中所述的 Accept-Language 标头进行发送。

| 标头名称     | 描述                                                                                                                                                                                                                                     | 示例                  |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------ |
| Accept-Language | 用户的当前语言设置。 如果可能，MO 门户应以指定的语言呈现内容。 有关详细信息，请参阅 [RFC 7231 5.3.5： Accept-Language 部分](https://tools.ietf.org/html/rfc7231#section-5.3.5)。 | `Accept-Language: en-us` |

## <a name="web-portal-design-policies"></a>Web 门户设计策略

若要确保在 Windows 上获得最佳用户体验，建议移动运营商在开发其 web 门户时遵循本部分中的策略和指导原则。

### <a name="business-functions"></a>业务功能

| 策略                                                                                                                                                                                                                                                                           | 必需还是建议 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------- |
| Web 门户体验必须满足所提供国家/地区中所有适用的法律和法规要求。 Web 门户中显示的任何内容都必须遵守所有适用的法律。 | 必须 |
| 通过 web 门户体验提供的产品必须是网络连接的产品/服务。 | 必须 |
| 通过 web 门户体验提供的网络连接产品必须包括对产品/服务和条款的清楚说明。 要使用户能够从 web 门户体验中查看任何特定的服务条款。 | 必须 |
| 用户必须可以从 web 门户体验中访问客户支持联系人信息。 | 必须 |
| 移动运营商的隐私策略必须可供用户在 web 门户体验中查看。 | 必须 |
| 移动运营商提供的帐户管理体验必须使用户能够对其当前数据计划执行操作，如取消订阅。 | 必须 |
| 成功完成从 web 门户中购买或激活计划后，用户必须收到订单确认。 | 建议 |

### <a name="security"></a>安全性

| 策略                                                                                                                                                                                                                                                                           | 必需还是建议 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------- |
| Web 门户体验不得交付或安装任何第三方拥有或品牌的应用或模块。 | 必须 |
| 用户在退出移动运营商的 web 门户体验之前，必须从 web 门户安全地注销用户。  | 必须 |
| 门户 URI 以及从 web 门户发送到和的所有请求或通知都必须使用安全的 HTTPS 协议。 | 必须 |
| 所有 web 门户资源和引用必须使用安全的 HTTPS 协议。 | 必须 |

### <a name="advertising"></a>广告

| 策略                                                                                                                                                                                                                                                                           | 必需还是建议 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------- |
| Web 门户不能显示，也不能用于下载、广告、赞助内容、视频、声音文件、动画或其他大媒体文件或图像。 | 必须 |

### <a name="capabilities"></a>功能

| 策略                                                                                                                                                                                                                                                                           | 必需还是建议 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------- |
| Web 门户体验所需的最小功能是使用户能够使用注册了移动运营商的帐户购买数据计划。 | 必须 |
| 在用户退出 web 门户体验之前，web 门户必须立即启动并保持对用户输入的响应。 | 必须 |
| 调用后，web 门户必须具有和保留用户焦点，直到： <ul><li>激活流已完成，并且 web 门户已将焦点返回到移动计划应用程序。</li></ul><p>OR</p><ul><li>用户已取消流并返回到移动计划应用。</li></ul> | 必须 |
| Web 门户不能显示任何弹出窗口、打开任何其他窗口，或者将用户重定向到任何其他网站或应用程序，除非需要完成激活流。 | 必须 |
| Web 门户必须处理所有合法的错误和异常，例如拒绝支付方法、后端失败，等等。处理错误或异常后，web 门户必须保持响应状态，以便用户退出并返回到移动计划应用。 | 必须 |
| 如果用户遇到可通过用户操作解决的错误，建议使用错误消息显示移动运营商的客户支持信息。 | 建议 |

### <a name="usability"></a>可用性

| 策略                                                                                                                                                                                                                                                                           | 必需还是建议 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------- |
| Web 门户的默认帧大小为800x600。 移动运营商应采用响应式 web 设计，以便在用户调整移动计划应用的大屏幕和较小屏幕时，可以自动调整 web 门户上的内容，使其适应 web 控件框架。 | 必须 |
| 加载 web 门户体验的加载时间和数据消耗应进行优化。 | 必须 |
| Web 门户体验应该简单轻松地导航到所需的屏幕指导原则。 | 必须 |
| Web 门户上的用户界面元素应该提供与移动计划应用集成的统一体验，而无需混淆用户或提醒用户这是一个嵌入的 web 控件。 例如，web 门户中不应有 "关闭/最大/最小值" 按钮。 | 必须 |
| Web 门户中的页面布局应清晰且易于导航。 用户可以在门户中通过 UI 元素向后导航到 web 门户中的页面。 有关详细信息，请参阅 [Web 门户流和引用设计](mobile-plans-appendix.md#web-portal-flow-and-reference-design)。 |必须 |
| Web 门户必须在 web 视图控制框架内正常运行，一旦调用后，就不能干扰用户与移动计划应用的交互。 | 必须 |
| Web 门户不一定混乱，图像过多、横幅、冗长文本、外部链接等。 | 必须 |
| Web 体验中的屏幕 "取消" 按钮应该可供用户在适用时退出流。 | 建议 |
| 移动运营商可以选择最能代表品牌的配色方案和字体。 应注意确保所有视觉对象都能顺利合作并强化品牌。 | 建议 |

### <a name="localization"></a>本地化

| 策略                                                                                                                                                                                                                                                                           | 必需还是建议 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------- |
| Web 门户应该能够接收并了解移动计划应用传递的用户区域设置，以用户的首选语言显示内容。 | 必须 |
| 移动运营商可以采用他们希望支持的语言本地化其 web 门户。 | 建议 |
| Web 门户提供的体验应该相当类似于它支持的所有语言，但数据计划可用性可能因区域而异。 | 建议 |

### <a name="accessibility"></a>可访问性

| 策略                                                                                                                                                                                                                                                                           | 必需还是建议 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------- |
| Web 门户应提供已禁用用户的可访问性，并遵循移动运营商提供服务的管辖区中适用的辅助功能准则。 | 建议 |
