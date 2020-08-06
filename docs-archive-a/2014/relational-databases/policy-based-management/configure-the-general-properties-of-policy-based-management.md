---
title: 配置基于策略的管理的常规属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.dmf.PolicyManagement.f1
helpviewer_keywords:
- Policy-Based Management, configure properties
ms.assetid: 6d1e0e37-29ea-408a-a055-384984d884be
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a2efb37fafa29bcb043dedbcfa8719d0092b1c77
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689335"
---
# <a name="configure-the-general-properties-of-policy-based-management"></a>配置基于策略的管理的常规属性
  本主题说明如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中配置基于策略的管理的属性。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **配置基于策略的管理，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 要求具有 PolicyAdministratorRole 固定数据库角色的成员身份。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-policy-based-management"></a>配置基于策略的管理  
  
1.  在“对象资源管理器”**** 中，单击加号以展开你要在其中配置基于策略的管理属性的服务器。  
  
2.  单击加号以便展开 **“管理”** 文件夹。  
  
3.  右键单击“策略管理”****，然后选择“属性”****。  
  
     在 **“策略管理属性”** 对话框中提供以下选项。  
  
     **已启用**  
     指定是否启用基于策略的管理。  
  
     **HistoryRetentionInDays**  
     指定策略评估历史纪录应保留的天数。 如果该值为 0（默认值），则不会自动删除历史纪录。  
  
     **LogOnSuccess**  
     指定基于策略的管理是否记录成功的策略评估。  
  
    -   如果该值为 false（默认值），则仅记录失败的策略评估。  
  
    -   如果该值为 true，则成功和失败的策略评估都会记录。  
  
4.  完成后，单击 **“确定”** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-policy-based-management"></a>配置基于策略的管理  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    -- enables Policy-Based Management   
    USE msdb;  
    GO  
    EXEC dbo.sp_syspolicy_configure   
         @name = N'Enabled',   
         @value = 1;  
    GO  
    ```  
  
 有关详细信息，请参阅 [sp_syspolicy_configure (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-syspolicy-configure-transact-sql)。  
  
  
