---
title: MSSQLSERVER_2527 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2527 (Database Engine error)
ms.assetid: 1cef90ef-9c39-44e6-bc7f-316c8f53c10c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 900707634a016ecfd29f9f676e68b4d2f557ccea
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580279"
---
# <a name="mssqlserver_2527"></a>MSSQLSERVER_2527
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|2527|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC_INDEX_FILEGROUP_IS_OFFLINE|  
|消息正文|无法处理表 O_NAME 的索引 I_NAME，因为文件组 F_NAME 离线。|  
  
## <a name="explanation"></a>说明  
 此信息性消息指示由于用来存储索引数据的某个文件组处于脱机状态而无法检查索引。 文件组中文件的状态决定整个文件组的可用性。 文件组中的所有文件都必须联机，文件组才可用。 如果没有其他问题，将检查同一对象的所有其他索引。  
  
## <a name="user-action"></a>用户操作  
 若要查看指定文件组中文件的状态，请查询 **sys.database_files** 或 **sys.master_files** 目录视图。  
  
 从备份还原离线文件。  
  
## <a name="see-also"></a>另请参阅  
 [sys.database_files (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)   
 [sys. master_files &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
