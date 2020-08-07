---
title: 设计查询 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptwizard.designquery.f1
ms.assetid: 2dad800f-10a1-453c-8761-2935b9826d84
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9b56d99ec11b50ce53ef223a01eb5fc2766238ab
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691121"
---
# <a name="design-the-query"></a>设计查询
  使用报表向导的此页来创建查询，可以手动键入查询，使用查询生成器来交互生成查询，或从另一个表中导入查询。  
  
 您在“选择数据源”页（报表向导中的上一页）中选择的数据源类型决定了您可以在此页中输入的查询。 例如，如果数据源类型为 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，则可以输入 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句或存储过程名称。 如果数据源类型为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，则 "查询" 窗格将被禁用，并且您不能直接输入查询。 可以使用“查询生成器”来指定查询。  
  
## <a name="options"></a>选项  
 **查询字符串**  
 键入用于检索要在报表中使用的数据的查询。  
  
 **查询生成器**  
 单击“查询生成器”**** 打开数据源的查询设计器，或从另一个表中导入查询。  
  
 有关查询设计器的详细信息，请参阅 [Reporting Services Query Designers](../../2014/reporting-services/reporting-services-query-designers.md)。  
  
## <a name="example"></a>示例  
 对于数据源类型**Microsoft SQL Server**，下面的查询将从数据库表中检索姓氏列表 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] `Person` 。  
  
```  
SELECT LastName FROM Person.Person;  
```  
  
 对于数据源类型**Microsoft SQL Server**，下面的查询将 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 为标识号为1的员工运行存储过程 `uspGetEmployeeManagers` ：  
  
```  
EXEC uspgetEmployeeManagers '1';  
```  
  
## <a name="see-also"></a>另请参阅  
 [报表向导帮助](../../2014/reporting-services/report-wizard-help.md)   
 [报表嵌入数据集和共享数据集 &#40;报表生成器和 SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [将数据添加到报表 &#40;报表生成器和 SSRS&#41;](report-data/report-datasets-ssrs.md)  
  
  
