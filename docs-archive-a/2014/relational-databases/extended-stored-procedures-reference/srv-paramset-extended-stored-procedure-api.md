---
title: srv_paramset（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paramset
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramset
ms.assetid: 2a509206-a1b8-4b20-b0a2-ef680cef7bd8
author: rothja
ms.author: jroth
ms.openlocfilehash: 9ebe308e5e0c8fc24382582fb71db2f48c77541e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578211"
---
# <a name="srv_paramset-extended-stored-procedure-api"></a>srv_paramset（扩展存储过程 API）
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 设置远程存储过程调用返回参数的值。 此函数已被 srv_paramsetoutput 函数取代****。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_paramset (  
SRV_PROC *  
srvproc  
,  
int  
n  
,   
void *  
data  
,  
int  
len   
);  
  
```  
  
## <a name="arguments"></a>参数  
 srvproc**  
 指向作为特定客户端连接句柄（在这里为接收远程存储过程调用的句柄）的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
 *n*  
 指示要设置的参数的编号。 第一个参数是 1。  
  
 *data*  
 是指向要发送回客户端的数据值的指针，该数据值将作为远程存储过程返回参数。  
  
 *长度*  
 指定要返回的数据的实际长度。 如果参数的数据类型的长度为常量且该数据类型不允许 null 值（例如 srvbit 或 srvint1），则将会忽略 len******。  
  
## <a name="returns"></a>返回  
 如果参数值设置成功，则返回 SUCCEED，否则返回 FAIL。 如果属于以下情况则返回 FAIL：无当前远程存储过程、没有第 n 个远程存储过程参数、参数不是返回参数以及 len 参数是非法的****。  
  
 如果 len 为 0，则返回 NULL**。 将 len 设置为 0 是将 NULL 返回给客户端的唯一方法**。  
  
 如果参数是数据类型之一，则此函数返回以下值 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。  
  
|新数据类型|返回数据长度|  
|--------------------|------------------------|  
|`BITN`|**NULL：** *len* = 0, data = IG, RET = 0<br /><br /> **ZERO：** N/A<br /><br /> **>= 255：** 不适用<br /><br /> **<255：** 不适用|  
|`BIGVARCHAR`|**NULL：** *len* = 0, data = IG, RET = 1<br /><br /> **ZERO：** *len* = IG, data = IG, RET = 0<br /><br /> **>=255：** *len* = max8k, data = valid, RET = 0<br /><br /> **<255：** *len* = <8k, data = valid, RET = 1|  
|`BIGCHAR`|**NULL：** *len* = 0, data = IG, RET = 1<br /><br /> **ZERO：** *len* = IG, data = IG, RET = 0<br /><br /> **>=255：** *len* = max8k, data = valid, RET = 0<br /><br /> **<255：** *len* = <8k, data = valid, RET = 1|  
|`BIGBINARY`|**NULL：** *len* = 0, data = IG, RET = 1<br /><br /> **ZERO：** *len* = IG, data = IG, RET = 0<br /><br /> **>=255：** *len* = max8k, data = valid, RET = 0<br /><br /> **<255：** *len* = <8k, data = valid, RET = 1|  
|`BIGVARBINARY`|**NULL：** *len* = 0, data = IG, RET = 1<br /><br /> **ZERO：** *len* = IG, data = IG, RET = 0<br /><br /> **>=255：** *len* = max8k, data = valid, RET = 0<br /><br /> **<255：** *len* = <8k, data = valid, RET = 1|  
|NCHAR|**NULL：** *len* = 0, data = IG, RET = 1<br /><br /> **ZERO：** *len* = IG, data = IG, RET = 0<br /><br /> **>=255：** *len* = max8k, data = valid, RET = 0<br /><br /> **<255：** *len* = <8k, data = valid, RET = 1|  
|NVARCHAR|**NULL：** *len* = 0, data = IG, RET = 1<br /><br /> **ZERO：** *len* = IG, data = IG, RET = 0<br /><br /> **>=255：** *len* = max8k, data = valid, RET = 0<br /><br /> **<255：** *len* = <8k, data = valid, RET = 1|  
|`NTEXT`|**NULL：** *len* = IG, data = IG, RET = 0<br /><br /> **ZERO：** *len* = IG, data = IG, RET = 0<br /><br /> **>=255：** *len* = IG, data = IG, RET = 0<br /><br /> ** \< 255：** *len* = IG，data = IG，RET = 0|  
|RET = srv_paramset 的返回值||  
|IG = 将忽略值||  
|valid = 任何有效的数据指针||  
  
## <a name="remarks"></a>备注  
 参数包含通过远程存储过程在客户端和应用程序之间传递的数据。 客户端可以指定某些参数作为返回参数。 这些返回参数可包含开放式数据服务服务器应用程序传递回客户端的值。 使用返回参数类似于通过引用传递参数。  
  
 不能设置未作为返回参数调用的参数的返回值。 可以使用 srv_paramstatus 来确定参数的调用方式****。  
  
 此函数会为参数设置返回值，但它不会向客户端实际发送返回值。 在设置了状态标记 SRV_DONE_FINAL 的情况下调用 srv_senddone 时，所有返回参数（无论是否使用 srv_paramset 设置了返回值）都会自动发送到客户端********。  
  
 使用参数调用远程存储过程时，可以按名称或位置（未命名）传递参数。 如果使用部分按名称传递，部分按位置传递的参数调用远程存储过程，则会发生错误。 仍然会调用 SRV_RPC 处理程序，但是它看起来没有参数并且 srv_rpcparams 返回 0****。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另请参阅  
 [srv_paramsetoutput（扩展存储过程 API）](srv-paramsetoutput-extended-stored-procedure-api.md)  
  
  
