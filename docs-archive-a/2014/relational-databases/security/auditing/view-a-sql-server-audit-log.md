---
title: 查看 SQL Server 审核日志 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- audits [SQL Server], viewing logs
- viewing audit logs
- logs [SQL Server], audit
ms.assetid: e8feaca0-7852-422b-895a-319b965d8d9b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 8f9902a4fc92ef0b35bae62eb80170762c52fdec
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578767"
---
# <a name="view-a-sql-server-audit-log"></a>查看 SQL Server 审核日志
  本主题介绍如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中查看 SQL Server 审核日志。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要查看 SQL Server 审核日志，可使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 需要 `CONTROL SERVER` 权限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-a-sql-server-audit-log"></a>查看 SQL Server 审核日志  
  
1.   在对象资源管理器中，展开“安全性”文件夹。  
  
2.  展开“审核”文件夹。  
  
3.  右键单击要查看的审核日志，然后选择“查看审核日志”。 这将打开 "**日志文件查看器-**_server_name_ " 对话框。 有关详细信息，请参阅 [Log File Viewer F1 Help](../../logs/log-file-viewer-f1-help.md)。  
  
4.  完成后，单击“关闭”。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 建议通过使用日志文件查看器查看审核日志。 但是，如果你要创建自动监视系统，则可以使用 [sys.fn_get_audit_file (Transact-SQL)](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql) 函数直接读取审核文件中的信息。 直接读取该文件将以略有不同的（未处理的）格式返回数据。 有关详细信息，请参阅**sys.databases fn_get_audit_file**  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Audit（数据库引擎）](sql-server-audit-database-engine.md)   
 [将 SQL Server 审核事件写入安全日志](write-sql-server-audit-events-to-the-security-log.md)  
  
  
