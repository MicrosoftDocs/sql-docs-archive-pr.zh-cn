---
title: IBCPSession::BCPWriteFmt (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IBCPSession::BCPWriteFmt (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPWriteFmt method
ms.assetid: add50425-2ed6-411a-a391-4ce63c364892
author: rothja
ms.author: jroth
ms.openlocfilehash: ee4dcb5809c0f0fbb6d3f7aba6f4af5f6991e0e8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590198"
---
# <a name="ibcpsessionbcpwritefmt-ole-db"></a>IBCPSession::BCPWriteFmt (OLE DB)
  将每一列的格式信息写入格式化文件。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT BCPWriteFmt(   
const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>备注  
 格式化文件指定大容量复制所创建的数据文件的数据格式。 调用 [IBCPSession::BCPColumns](ibcpsession-bcpcolumns-ole-db.md) 和 [IBCPSession::BCPColFmt](ibcpsession-bcpcolfmt-ole-db.md) 方法将定义数据文件的格式。 BCPWriteFmt 方法将此定义保存在 pwszFormatFile 参数引用的文件中****。  
  
 BCPWriteFmt 方法可以通过 xml 或文本格式保存格式化文件****。 这必须通过将 BCP_OPTION_XML 控制选项用于 [IBCPSession::BCPControl](ibcpsession-bcpcontrol-ole-db.md) 方法来指示。  
  
 若要加载已保存的格式化文件，请使用 [IBCPSession::BCPReadFmt](ibcpsession-bcpreadfmt-ole-db.md) 方法。  
  
## <a name="arguments"></a>参数  
 pwszFormatFile**[in]  
 包含数据文件格式值的文件的路径和文件名。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功。  
  
 E_FAIL  
 出现特定于提供程序的错误;有关详细信息，请使用[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)接口。  
  
 E_OUTOFMEMORY  
 内存不足错误。  
  
 E_UNEXPECTED  
 意外调用了该方法。 例如，在调用该方法之前，未调用 [IBCPSession::BCPInit](ibcpsession-bcpinit-ole-db.md) 方法。  
  
## <a name="see-also"></a>另请参阅  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [执行大容量复制操作](../native-client/features/performing-bulk-copy-operations.md)  
  
  
