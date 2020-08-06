---
title: srv_setcoldata（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_setcoldata
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_setcoldata
ms.assetid: 2e19205a-25ca-4d4a-916b-d591cf2c892b
author: rothja
ms.author: jroth
ms.openlocfilehash: b67aa2f7b5a37057d2ed87846689919d84ec4aaf
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692941"
---
# <a name="srv_setcoldata-extended-stored-procedure-api"></a>srv_setcoldata（扩展存储过程 API）
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 指定列的数据的当前地址。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_setcoldata (  
SRV_PROC *  
srvproc  
,  
int   
column  
,  
void *  
data   
);  
  
```  
  
## <a name="arguments"></a>参数  
 srvproc**  
 指向作为特定客户端连接句柄的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
 *column*  
 指示指定其地址的列的编号。 列的编号从 1 开始。  
  
 *data*  
 指向列的数据的指针。 在将列数据替换为对 srv_setcoldata 的其他调用或调用 srv_senddone 之前，不能释放为 data 分配的内存**********。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>备注  
 必须首先使用 srv_describe 定义行的每个列****。 列数据地址最初使用 srv_describe 进行设置****。 如果列数据的地址发生更改，则必须调用 srv_setcoldata 以便指定该数据的新地址，并且必须针对更改后的每个列单独调用 srv_setcoldata********。  
  
 使用 srv_setcollen 将列的长度设置为 0 可以表示 Null 数据****。 随后将忽略数据地址。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另请参阅  
 [srv_describe（扩展存储过程 API）](srv-describe-extended-stored-procedure-api.md)  
  
  
