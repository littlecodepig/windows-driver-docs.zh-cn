---
title: IRP_MJ_READ 联合的 FLT_PARAMETERS
description: 当 IRP_MJ_READ 操作的 FLT_IO_PARAMETER_BLOCK 结构的 MajorFunction 字段时，将使用以下联合组件。
keywords:
- IRP_MJ_READ 联合可安装文件系统驱动程序的 FLT_PARAMETERS
- FLT_PARAMETERS 联合可安装文件系统驱动程序
- PFLT_PARAMETERS 联合指针可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FLT_PARAMETERS
api_location:
- fltkernel.h
api_type:
- HeaderDef
ms.date: 02/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: db06549c1f7bf29a2809cb832a379bf426e0de66
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826893"
---
# <a name="flt_parameters-for-irp_mj_read-union"></a>IRP_MJ_READ 联合的 FLT_PARAMETERS

当 [**IRP_MJ_READ**](irp-mj-read.md)操作的 [**FLT_IO_PARAMETER_BLOCK**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的 **MajorFunction** 字段时，将使用以下联合组件。

## <a name="syntax"></a>语法

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG                   Length;
    ULONG POINTER_ALIGNMENT Key;
    LARGE_INTEGER           ByteOffset;
    PVOID                   ReadBuffer;
    PMDL                    MdlAddress;
  } Read;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>成员

**读取**  
包含以下成员的结构。

**长度**  
要读取的数据的长度（以字节为单位）。

**键**  
与目标文件的字节范围锁关联的键值。

**ByteOffset**  
要读取的数据在文件中的起始字节偏移量。

**ReadBuffer**  
指向缓冲区的指针，该缓冲区接收从该文件中读取的数据。 此成员是可选的，如果 **MdlAddress** 中提供 MDL，此成员可以为 NULL。 请参阅 " **备注**"。

**MdlAddress**  
 (MDL 的内存描述符列表的地址) 描述 **ReadBuffer** 成员指向的缓冲区。 此成员是可选的，如果 **ReadBuffer** 中提供了缓冲区，则可以为 **NULL** 。 请参阅 " **备注**"。

## <a name="remarks"></a>备注

IRP_MJ_READ 操作的 [**FLT_PARAMETERS**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters) 结构包含由回调数据表示的读取操作的参数 ([**FLT_CALLBACK_DATA**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 它包含在 FLT_IO_PARAMETER_BLOCK 结构中。

如果同时提供了 **ReadBuffer** 和 **MdlAddress** 缓冲区，则建议 minifilters 使用 MDL。 当 **ReadBuffer** 指向的内存是在调用进程的上下文中访问的用户模式地址时，或者如果它是内核模式地址，则它是有效的。

如果微筛选器更改 **MdlAddress** 的值，则在其后回拨后，筛选器管理器将释放当前存储在 **MDLADDRESS** 中的 MDL，并还原以前的 **MdlAddress** 值。

IRP_MJ_READ 可以是基于 IRP 的操作，也可以是快速的 i/o 操作。

## <a name="requirements"></a>要求

**标头**： Fltkernel (包含 Fltkernel) 


## <a name="see-also"></a>请参阅

[**FLT_CALLBACK_DATA**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT_IO_PARAMETER_BLOCK**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_IS_FASTIO_OPERATION**](/windows-hardware/drivers/ddi/index)

[**FLT_IS_FS_FILTER_OPERATION**](/previous-versions/ff544648(v=vs.85))

[**FLT_IS_IRP_OPERATION**](/previous-versions/ff544654(v=vs.85))

[**FLT_PARAMETERS**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltReadFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreadfile)

[**IRP_MJ_READ**](irp-mj-read.md)

[**ZwReadFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)
