---
title: srv_willconvert（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_willconvert
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_willconvert
ms.assetid: 6f4db5fd-215a-461c-95e4-17697852733e
author: rothja
ms.author: jroth
ms.openlocfilehash: 0b9adfbd2a73b30cbfc0229b7942f79d3ddc1a82
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693894"
---
# <a name="srv_willconvert-extended-stored-procedure-api"></a>srv_willconvert（扩展存储过程 API）
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 确定特定数据类型转换在 ODS 库中是否可用。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL srv_willconvert (  
int  
srctype  
,  
int  
desttype   
);  
  
```  
  
## <a name="arguments"></a>参数  
 srctype**  
 指示要转换的数据的数据类型。 该参数可以为任意一种扩展存储过程 API 数据类型。  
  
 desttype**  
 指示源数据要转换成的目标数据类型。 该参数可以为任意一种扩展存储过程 API 数据类型。  
  
## <a name="returns"></a>返回  
 如果支持数据类型转换，则为 TRUE；否则为 FALSE。  
  
## <a name="remarks"></a>备注  
 有关每种数据类型的说明，请参阅[数据类型（扩展存储过程 API）](data-types-extended-stored-procedure-api.md)。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另请参阅  
 [srv_convert（扩展存储过程 API）](srv-convert-extended-stored-procedure-api.md)  
  
  
