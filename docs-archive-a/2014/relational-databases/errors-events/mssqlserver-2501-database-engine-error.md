---
title: MSSQLSERVER_2501 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2501 (Database Engine error)
ms.assetid: 895aafe3-a4e7-4ed8-acc5-93be76ef3664
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 200997dcfe7bf8a5933b9fce492daabd5baffd04
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690623"
---
# <a name="mssqlserver_2501"></a>MSSQLSERVER_2501
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|2501|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC_NO_SUCH_TABLE_NAME|  
|消息正文|找不到名为 'NAME' 的表或对象。 请检查系统目录。|  
  
## <a name="explanation"></a>说明  
 找不到指定的对象。  
  
### <a name="possible-causes"></a>可能的原因  
 此错误可能是由以下问题之一导致的：  
  
-   未正确指定对象。  
  
-   对象不存在，或在语句使用此对象之前就已删除。  
  
-   对象可能存在，但无法向用户显示。 例如，用户可能对此对象没有权限，或者此对象为用户看不到的内部表。  
  
## <a name="user-action"></a>用户操作  
  
-   验证当前数据库上下文是否正确。 有关详细信息，请参阅 [USE (Transact-SQL)](/sql/t-sql/language-elements/use-transact-sql)。  
  
-   验证表或对象名拼写是否正确。  
  
-   验证包含此对象的架构名称。 如果此对象属于默认 (**dbo**) 架构以外的架构，则必须使用两部分构成方式 *schema_name.object_name* 来指定表名或对象名。  
  
-   验证此对象是否存在于系统表中。 若要验证是否存在表或其他架构范围内的对象，请查询 [sys.objects](/sql/relational-databases/system-catalog-views/sys-objects-transact-sql) 目录视图。 如果系统表中没有此对象，则表明此对象已删除或者用户没有查看此对象元数据的权限。 有关如何查看对象元数据的详细信息，请参阅[元数据可见性配置](../security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](/sql/relational-databases/system-catalog-views/catalog-views-transact-sql)  
  
  
