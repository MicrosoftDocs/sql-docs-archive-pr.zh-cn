---
title: 创建 SQL Server Native Client OLE DB 提供程序应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, application creation
- applications [SQL Server Native Client]
- OLE DB, creating applications
ms.assetid: f3ae6815-f32d-4913-a1a2-2ba2f20cfd88
author: rothja
ms.author: jroth
ms.openlocfilehash: a661f23cdacc4b581dadbe7625cb6e2ea318857f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688885"
---
# <a name="creating-a-sql-server-native-client-ole-db-provider-application"></a>创建 SQL Server Native Client OLE DB 访问接口应用程序
  创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本机客户端 OLE DB 提供程序应用程序涉及以下步骤：  
  
1.  建立与数据源的连接。  
  
2.  执行命令。  
  
3.  结果处理。  
  
> [!NOTE]  
>  请尽可能使用 Windows 身份验证。 如果 Windows 身份验证不可用，请在运行时提示用户输入其凭据。 不要将凭据存储在一个文件中。 如果必须保存凭据，应当用 [Win32 cryptoAPI](https://go.microsoft.com/fwlink/?LinkId=9504) 对它们加密。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [建立与数据源的连接](establishing-a-connection-to-a-data-source.md)  
  
-   [执行命令](executing-a-command.md)  
  
-   [处理结果](processing-results.md)  
  
-   [关于 OLE DB 属性](about-ole-db-properties.md)  
  
-   [在 SQL Server Native Client 中使用 OUTPUT 子句 (OLE DB)](using-the-output-clause-with-ole-db-in-sql-server-native-client.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client (OLE DB)](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
